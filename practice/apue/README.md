# UNIX 环境高级编程

从 http://www.apuebook.com/code3e.html 获取 APUE 一书的源码。

解压，重命名为 `apue3e`

```bash
tar -zxvf src.tar.gz
mv apue.3e apue3e
```

创建 `lib`：

```bash
cd lib
make
```

将 `lib` 目录下的 `libapue.a` 复制到 `/usr/lib`：

```bash
sudo cp libapue.a /usr/lib
sudo cp libapue.a /usr/lib64
```

将 `include` 目录下的 `apue.h` 复制到 `/usr/include`：

```bash
cd ../include
sudo cp apue.h /usr/include
```

验证头文件可用，编译 `intro` 下的 `ls1.c` 为 `myls` 程序，然后运行 `myls`：

```bash
cd ../intro
gcc -o myls ls1.c -lapue

./myls .
```

`-lapue` 选项去掉 `err` 部分。
