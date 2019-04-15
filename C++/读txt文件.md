**UTF8读取txt中文出现乱码，使用该函数转换**
inline string UTF8ToGB(const char* str)
{
	string result;
	WCHAR *strSrc;
	LPSTR szRes;

	//获得临时变量的大小
	int i = MultiByteToWideChar(CP_UTF8, 0, str, -1, NULL, 0);
	strSrc = new WCHAR[i + 1];
	MultiByteToWideChar(CP_UTF8, 0, str, -1, strSrc, i);

	//获得临时变量的大小
	i = WideCharToMultiByte(CP_ACP, 0, strSrc, -1, NULL, 0, NULL, NULL);
	szRes = new CHAR[i + 1];
	WideCharToMultiByte(CP_ACP, 0, strSrc, -1, szRes, i, NULL, NULL);

	result = szRes;
	delete[]strSrc;
	delete[]szRes;

	return result;
}


**读取txt数字，读为int型（注意int范围，身份证号不可以）**
bool JudgeNum(string str, int& iTmp)
{
	bool bNum = true;
	string::size_type szSize = str.size();
	for (int i = 0; i<szSize; ++i)
	{
		char ch = str.at(i);
		if ((ch < '0') || (ch > '9'))
		{
			bNum = false;
			break;
		}
	}
	if (bNum)
	{
		istringstream iss(str);
		iss >> iTmp;
	}
	return bNum;
}
int ReadIntFromTxt(const char* filename, std::vector<int>& outfile)
{
	ifstream infile(filename);
	string strTmp;
	int iTmp = 0;
	if (!infile)
	{
		printf("error!");
		return -1;
	}
	while (getline(infile, strTmp, '\n'))    // 以回车为分隔符，读取每一个词
	{
		if (JudgeNum(strTmp, iTmp))
		{
			outfile.push_back(iTmp);
		}
	}
	return 0;
}



**读txt，读为string**
inline int ReadTxt(const char* filename, std::vector<std::string>& outfile){
	FILE *fp;
	char StrLine[1024];             //每行最大读取的字符数
	if ((fp = fopen(filename, "r")) == NULL) //判断文件是否存在及可读
	{
		printf("error!");
		return -1;
	}

	while (!feof(fp))
	{
		fgets(StrLine, 1024, fp);  //读取一行
		outfile.push_back(StrLine);
	}
	fclose(fp);
	return 0;
}
