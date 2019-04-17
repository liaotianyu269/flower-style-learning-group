//sqlite使用的是UTF-8编码，而vs里面使用的是ascii编码，需要进行转换，不然就会出现乱码，需要在存库时ascii转UTF-8，读库时UTF-8转ascii。  

//以下函数为转换函数。（Change为我创建的转换类）  

//主要使用：  
//utf-8 转 ascii   
//string Change::UTF_82ASCII(string& strUtf8Code)  
//ascii 转 Utf8   
//string Change::ASCII2UTF_8(string& strAsciiCode)  

```C++
//UTF-8转Unicode   
std::wstring Change::Utf82Unicode(const std::string& utf8string)  
{  
	int widesize = ::MultiByteToWideChar(CP_UTF8, 0, utf8string.c_str(), -1, NULL, 0);  
	if (widesize == ERROR_NO_UNICODE_TRANSLATION)  
	{  
		throw std::exception("Invalid UTF-8 sequence.");  
	}  
	if (widesize == 0)  
	{  
		throw std::exception("Error in conversion.");  
	}  
	std::vector<wchar_t> resultstring(widesize);  
	int convresult = ::MultiByteToWideChar(CP_UTF8, 0, utf8string.c_str(), -1, &resultstring[0], widesize);  
	if (convresult != widesize)  
	{  
		throw std::exception("La falla!");  
	}  
	return std::wstring(&resultstring[0]);  
}  
//unicode 转为 ascii   
string Change::WideByte2Acsi(wstring& wstrcode)  
{  
	int asciisize = ::WideCharToMultiByte(CP_OEMCP, 0, wstrcode.c_str(), -1, NULL, 0, NULL, NULL);  
	if (asciisize == ERROR_NO_UNICODE_TRANSLATION)  
	{  
		throw std::exception("Invalid UTF-8 sequence.");  
	}  
	if (asciisize == 0)  
	{  
		throw std::exception("Error in conversion.");  
	}  
	std::vector<char> resultstring(asciisize);  
	int convresult = ::WideCharToMultiByte(CP_OEMCP, 0, wstrcode.c_str(), -1, &resultstring[0], asciisize, NULL, NULL);  
	if (convresult != asciisize)  
	{  
		throw std::exception("La falla!");  
	}  
	return std::string(&resultstring[0]);  
}  

//utf-8 转 ascii   
string Change::UTF_82ASCII(string& strUtf8Code)  
{  
	string strRet("");  
	//先把 utf8 转为 unicode   
	wstring wstr = Utf82Unicode(strUtf8Code);  
	//最后把 unicode 转为 ascii   
	strRet = WideByte2Acsi(wstr);  
	return strRet;  
}  
//ascii 转 Unicode   
wstring Change::Acsi2WideByte(string& strascii)  
{  
	int widesize = MultiByteToWideChar(CP_ACP, 0, (char*)strascii.c_str(), -1, NULL, 0);   
	if (widesize == ERROR_NO_UNICODE_TRANSLATION)  
	{  
		throw std::exception("Invalid UTF-8 sequence.");  
	}  
	if (widesize == 0)  
	{  
		throw std::exception("Error in conversion.");  
	}  
	std::vector<wchar_t> resultstring(widesize);  
	int convresult = MultiByteToWideChar(CP_ACP, 0, (char*)strascii.c_str(), -1, &resultstring[0], widesize);  
	if (convresult != widesize)  
	{  
		throw std::exception("La falla!");  
	}  
	return std::wstring(&resultstring[0]);  
}  

//Unicode 转 Utf8   
std::string Change::Unicode2Utf8(const std::wstring& widestring)  
{  
	int utf8size = ::WideCharToMultiByte(CP_UTF8, 0, widestring.c_str(), -1, NULL, 0, NULL, NULL);  
	if (utf8size == 0)  
	{  
		throw std::exception("Error in conversion.");  
	}  
	std::vector<char> resultstring(utf8size);  
	int convresult = ::WideCharToMultiByte(CP_UTF8, 0, widestring.c_str(), -1, &resultstring[0], utf8size, NULL, NULL);  
	if (convresult != utf8size)  
	{  
		throw std::exception("La falla!");  
	}  
	return std::string(&resultstring[0]);  
}  
  
//ascii 转 Utf8   
string Change::ASCII2UTF_8(string& strAsciiCode)  
{  
	string strRet("");  
	//先把 ascii 转为 unicode   
	wstring wstr = Acsi2WideByte(strAsciiCode);  
	//最后把 unicode 转为 utf8   
	strRet = Unicode2Utf8(wstr);  
	return strRet;  
}  
```
