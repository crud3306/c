


c++文件操作
===========





c 与 c++ 文件操作比较
============
c++ 的是 fstream, ifstream,ofstream
c 的是 fopen、fread、fwrite、fget

另外注意：CreateFile、ReadFile、WriteFile等等，是只能在windows环境中用的c++方法。


测试写文件速度
-------------
程序设计思路： 将TEST_SIZE个字符用两种方式写入文件，记录两种方式的耗时。 
```
void test_write()  
{     
    const int TEST_SIZE = 10000000 ;  
    const char* c_plus_write_file = "H://c_plus_write_file.txt";  
    const char* c_write_file = "H://c_write_file.txt";  
      
    cout<<"Test size :" << TEST_SIZE <<endl;  
    //c++ style writing file  
    ofstream of(c_plus_write_file);  
    assert(of);  
    time_t start, end;  
    start =  clock();  
    for(int i=0; i < TEST_SIZE; ++i)  
    {  
        char tmp[1];  
        tmp[0] = char(i);  
        of << tmp[0];  
    }  
    end = clock();  
    of.close();  
    cout<<"C++ style: "<<end - start <<" ms"<<endl;  


    //c style writing file  
    FILE* fp = fopen(c_write_file, "w");  
    start =  clock();  
    for(int i=0; i < TEST_SIZE; ++i)  
    {  
        char tmp[1];  
        tmp[0] = char(i);  
        fwrite( tmp, 1, 1, fp);  
    }  
    end = clock();  
    fclose(fp);  
    cout<<"C style: "<<end - start <<" ms"<<endl;  
    cin.get();  
}  
```

把 把of<<的代码改成了: of.write(tmp,1); 后结果：
```
void test_write()  
{     
    const int TEST_SIZE = 1000000 ;  
    const char* c_plus_write_file = "H://c_plus_write_file.txt";  
    const char* c_write_file = "H://c_write_file.txt";  
      
    cout<<"Test size :" << TEST_SIZE <<endl;  
    //c++ style writing file  
    ofstream of(c_plus_write_file);  
    assert(of);  
    time_t start, end;  
    start =  clock();  
    for(int i=0; i < TEST_SIZE; ++i)  
    {  
        char tmp[1];  
        tmp[0] = char(i);  
        of.write(tmp,1);  
    }  
    end = clock();  
    of.close();  
    cout<<"C++ style: "<<end - start <<" ms"<<endl;  


    //c style writing file  
    FILE* fp = fopen(c_write_file, "w");  
    start =  clock();  
    for(int i=0; i < TEST_SIZE; ++i)  
    {  
        char tmp[1];  
        tmp[0] = char(i);  
        fwrite( tmp, 1, 1, fp);  
    }  
    end = clock();  
    fclose(fp);  
    cout<<"C style: "<<end - start <<" ms"<<endl;  
    cin.get();  
} 
```

下面做读文件的比较：
程序设计思路： 用两种方法去读一个近100M的文本，记录时间。
```
void test_read()  
{     
    const char* read_file = "H://read4.txt";  
    const int BUF_SIZE = 1024 ;  
    char buf[BUF_SIZE];  
    //c++ style writing file  
    ifstream ifs(read_file,ios::binary);  
    assert(ifs);  
    time_t start, end;  
    start =  clock();  
    while(!ifs.eof())  
    {  
      ifs.read(buf,BUF_SIZE);  
    }  
    end = clock();  
    ifs.close();  
    cout<<"C++ style: "<<end - start <<" ms"<<endl;  


    //c style writing file  
    FILE* fp = fopen(read_file, "rb");  
    start =  clock();  
    int len = 0;  
    do  
    {  
        len = fread(buf,1,BUF_SIZE,fp);  
        //cout<<len<<endl;  
    }while(len != 0);  
    end = clock();  
    fclose(fp);  
    cout<<"C style: "<<end - start <<" ms"<<endl;  
    cin.get();  
}  
```


c 与 c++ 的文件读写比较(含文本文件 与 二进制文件)
```
#include <iostream>
#include <fstream>
#include <windows.h>
#include <string.h>
#include <stdio.h>
 
using namespace std;
 
void WriteTXTFile_C()
{
	FILE* fp = fopen("c.txt","wt");
	for(int i = 0; i < 1000; i++)
	{
		for(int j = 0; j < 1000; j++)
		{
			fputc('C', fp);
			fputs("Hello, world!\n", fp);
		}
	}
	fclose(fp);
}
 
void ReadTXTFile_C()
{
	FILE* fp = fopen("c.txt","rt");
	char str[15];
	for(int i = 0; i < 1000; i++)
	{
		for(int j = 0; j < 1000; j++)
		{
			fgetc(fp);
			fgets(str, 15, fp);
		}
	}
	fclose(fp);
}
 
void WriteBINFile_C()
{
	FILE* fp = fopen("c.bin","wb");
	char* str = "CHello, world!\n";
	int len = strlen(str);
	
	for(int i = 0; i < 1000; i++)
	{
		for(int j = 0; j < 1000; j++)
		{
			fwrite(str, 1, len, fp);
		}
	}
	fclose(fp);
}
 
void ReadBINFile_C()
{
	FILE* fp = fopen("c.bin","rb");
	char str[16];
	
	for(int i = 0; i < 1000; i++)
	{
		for(int j = 0; j < 1000; j++)
		{
			fread(str, 1, 16, fp);
		}
	}
	fclose(fp);
}
 


void WriteTXTFile_CPlus()
{
	fstream file;
	file.open("cp.txt", ios::in | ios::out | ios::trunc);//注意ios::in，或者ios::in | ios::out两种方式在文件不存在时会执行写操作但不会建立文件。
 
	for(int i = 0; i < 1000; i++)
	{
		for(int j = 0; j < 1000; j++)
		{
			file.put('C');
			file<<"Hello, world!\n";
		}
	}
	file.close();
}
 
void ReadTXTFile_CPlus()
{
	fstream file;
	file.open("cp.txt", ios::in | ios::out);
	char str[15];
 
	for(int i = 0; i < 1000; i++)
	{
		for(int j = 0; j < 1000; j++)
		{
			file.get(str, 15);
		}
	}
	file.close();
}
 
void WriteBINFile_CPlus()
{
	fstream file;
	file.open("cp.bin", ios::in | ios::out | ios::trunc | ios::binary);
	char* str = "CHello, world!\n";
	int len = strlen(str);
 
	for(int i = 0; i < 1000; i++)
	{
		for(int j = 0; j < 1000; j++)
		{
			file.write(str, len);
		}
	}
	file.close();
}
 
void ReadBINFile_CPlus()
{
	fstream file;
	file.open("cp.bin", ios::in | ios::out | ios::binary);
	char str[16];
 
	for(int i = 0; i < 1000; i++)
	{
		for(int j = 0; j < 1000; j++)
		{
			file.read(str, 16);
		}
	}
	file.close();
}
 
int main()
{
	DWORD start, end;
	start = GetTickCount();
	WriteTXTFile_C();
	end = GetTickCount();
	printf("C语言写文本文件操作运行时间为：%d ms\n", end - start);
	start = GetTickCount();
	WriteTXTFile_CPlus();
	end = GetTickCount();
	cout<<"C++写文本文件操作运行时间为："<<end - start<<" ms"<<endl;
 
	cout<<endl;
 
	start = GetTickCount();
	ReadTXTFile_C();
	end = GetTickCount();
	printf("C语言读文本文件操作运行时间为：%d ms\n", end - start);
	start = GetTickCount();
	ReadTXTFile_CPlus();
	end = GetTickCount();
	cout<<"C++读文本文件操作运行时间为："<<end - start<<" ms"<<endl;
 
	cout<<endl;
 
	start = GetTickCount();
	WriteBINFile_C();
	end = GetTickCount();
	printf("C语言写二进制文件操作运行时间为：%d ms\n", end - start);
	start = GetTickCount();
	WriteBINFile_CPlus();
	end = GetTickCount();
	cout<<"C++写二进制文件操作运行时间为："<<end - start<<" ms"<<endl;
 
	cout<<endl;
 
	start = GetTickCount();
	ReadBINFile_C();
	end = GetTickCount();
	printf("C语言读二进制文件操作运行时间为：%d ms\n", end - start);
	start = GetTickCount();
	ReadBINFile_CPlus();
	end = GetTickCount();
	cout<<"C++读二进制文件操作运行时间为："<<end - start<<" ms"<<endl;
}
```



