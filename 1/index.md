# 内存映射文件


使用内存映射的方法读取大数据文件
<!--more-->

## 相关代码

```cpp
// 创建或打开文件内核对象;
HANDLE fileH = CreateFile("data.txt",
    GENERIC_READ|GENERIC_WRITE,
    FILE_SHARE_READ,
    NULL,
    OPEN_EXISTING,
    FILE_ATTRIBUTE_NORMAL,
    NULL);
if(fileH == INVALID_HANDLE_VALUE)
{
    cout<<"error in CreateFile"<<endl;
    return -1;
}

// 创建一个文件映射内核对象;
HANDLE mapFileH = CreateFileMapping(fileH,
    NULL,
    PAGE_READWRITE,
    0,
    0,
    "Resource");
if(mapFileH == NULL)
{
    cout<<"error in CreateFileMapping"<<endl;
    return -1;
}

// 将文件数据映射到进程的地址空间;
char * mapH = (char *)MapViewOfFile( mapFileH,
    FILE_MAP_ALL_ACCESS,
    0,
    0,
    0);
if(mapH == NULL)
{
    cout<<"error in MapViewOfFile"<<endl;
    return -1;
}

// 读取数据;
char *buf = mapH;
double k;
int i = 1;
while(1)
{
    k = atof(buf);
    cout << i << ": " << k << endl;
    if (i % 3 == 0)
    {
        buf = strstr(buf, "\n");  
    }
    else
    {
        buf = strstr(buf, " ");
    }
    if (strstr(buf, " ") == NULL)
    {
        cout << i << endl;
        break;
    }
    i++;
}

// 关闭句柄;
UnmapViewOfFile(mapH);
CloseHandle(mapFileH);
CloseHandle(fileH);
```

---

其中 data.txt 数据如下所示（这里只是一个例子，实际处理的都是几十万几百万行数据）

```dada
-0.7211251 0.0245522 123.9979
-0.3867341 0.01316716 132.9994
0 0 128
0.3809185 -0.01296916 130.9995
0.7676494 -0.02613621 131.9978
1.072957 -0.03653103 122.9953
1.477118 -0.05029155 126.9914
1.919066 -0.06533858 131.986
2.302844 -0.07840508 131.9799
2.625543 -0.08939204 128.9733
```

---

{{< admonition >}}
LPWSTR类型在MinGw下可以直接这样写，但在MSVC下会有所不同。修改如下"data.txt" 改为 L"data.txt"，"Resource" 改为 L"Resource"而LPWSTR类型的赋值应为LPWSTR file_name = TEXT("data.txt");
{{< /admonition >}}

