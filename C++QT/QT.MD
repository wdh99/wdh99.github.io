问题1

>  WCHAR无法转换为char *

发生错误的代码

`strcmp(currentProcess.szExeFile, appname)`

下面时更详细的代码

```C++
const char *appname;
...
PROCESSENTRY32 currentProcess;
...
if(strcmp(currentProcess.szExeFile, appname)==0){...
```

上面这段代码, 用Visual Studio下的编译工具编译是不会报错的, 但是QtCreator里会报错(QtCreator使用的编译器是mingw), msvc编译器编译命令如下:

```
cl xxx.cpp #成功
```

解决方法:

```c++
char *szExeFile =QString::fromStdWString(currentProcess.szExeFile).toLocal8Bit().data();
if(strcmp(szExeFile, appname)==0){...
```

