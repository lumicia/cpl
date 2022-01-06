# UNIX 网络编程源码配置

下载 UNP 一书的源码：http://unpbook.com/unpv13e.tar.gz。

把压缩包解压：

```bash
tar -zxvf unpv13e.tar.gz
```

在解压得到的 `unpv13e` 目录下根据 `README` 来配置，首先执行

```bash
./configure
```

创建 `lib`：

```bash
cd lib
make
```

创建 `libfree`：

```bash
cd ../libfree
make
```

报错：

```bash
gcc -I../lib -g -O2 -D_REENTRANT -Wall   -c -o get_rtaddrs.o get_rtaddrs.c
In file included from get_rtaddrs.c:1:
unproute.h:3:17: fatal error: net/if_dl.h: No such file or directory
    3 | #include        <net/if_dl.h>           /* sockaddr_sdl{} */
      |                 ^~~~~~~~~~~~~
compilation terminated.
make: *** [<builtin>: get_rtaddrs.o] Error 1
```

解决方法：修改 `inet_ntop.c` 第 60 行的 `size_ t size` 为 `socklen_t size`。

我使用 Ubuntu，因此跳过接下来的两步。直接构建和测试一个简单的客户端程序：

```bash
cd ../intro
make daytimetcpsrv
make daytimetcpcli
sudo ./daytimetcpsrv

# open the same directory in another terminal
./daytimetcpcli 127.0.0.1
```

如果一切正常，终端应该会输出当前的时间。

将根目录下的 `libunp.a` 复制到 `/usr/lib` 和 `/usr/lib64`，`config.h` 复制到 `/usr/include`：

```bash
cd ..
sudo cp libunp.a /usr/lib
sudo cp libunp.a /usr/lib64
sudo cp config.h /usr/include
```

在 `lib` 目录下的 `unp.h` 添加一行：

```c
#define MAX_LINE 2048
```

复制到 `/usr/include`：

```bash
cd lib
sudo cp unp.h /usr/include
```

然后将 `/usr/include/unp.h` 第 7 行修改为：

```c
#include <config.h>
```

编写 `Hello World` 程序验证头文件可用：

```c
#include <stdio.h>
#include <unp.h>

int main() {
    printf("Hello World!\n");
    return 0;
}
```
