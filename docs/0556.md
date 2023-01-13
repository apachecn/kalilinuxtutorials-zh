# DrAFL:模糊 Linux 上没有源代码的二进制文件

> 原文：<https://kalilinuxtutorials.com/drafl-fuzzing-binaries-linux/>

原始 AFL 支持使用 QEMU 模式的黑盒覆盖引导模糊。我强烈建议先试一下，如果不行，你可以试试 drAFL 工具。

**用途**

你需要指定 **DRRUN_PATH** 指向 drrun launcher，指定 **LIBCOV_PATH** 指向 libbinafl.so 覆盖率库。你还需要关闭 AFL 的 fork 服务器( **AFL_NO_FORKSRV=1** )可能还有一个 **FL_SKIP_BIN_CHECK=1** 。有关更多详细信息，请参见下面构建部分中的步骤 5。

> **注意**:别忘了 64 位二进制要用 64 位 DynamoRIO，32 位二进制要用 32 位 DynamoRIO，否则不行。为了确保您的目标在 DynamoRIO 下运行，您可以使用以下命令运行它:

```
drrun --<path>
```

**检测 DLL**

Instrumentation library 是由 Ivan Fratric 创建的 winAFL 覆盖库的修改版本。

**也可阅读-[Easysploit:Metasploit 自动化更容易&比以往更快](https://kalilinuxtutorials.com/easysploit-metasploit-automation/)**

**建造**

**第一步。克隆 drAFL 回购**

git 克隆 https://github.com/mxmssh/drAFL.git/home/max/drAFL
CD/home/max/drAFL

**第二步。克隆和构建 DynamoRIO**

git 克隆 https://github.com/DynamoRIO/dynamorio
mkdir build _ dr
CD build _ dr/
cmake../dynamorio/
make -j
cd..

如果你有任何关于 DynamoRIO 编译的问题，请查看这个页面

**第三步。构建覆盖工具**

mkdir 构建
cd 构建
cmake../bin_cov/ -DDynamoRIO_DIR=../build _ dr/cmake
make-j
CD..

**第四步。构建补丁 AFL**

cd afl/
制作
cd..

**第五步。配置环境变量并运行目标**

CD build
mkdir in
mkdir out
echo“AAAA”>in/seed
export DRRUN _ PATH =/home/max/drAFL/build _ dr/BIN 64/dr run
export lib cov _ PATH =/home/max/drAFL/build/libbinafl . so
export AFL _ NO _ forks RV = 1
export AFL _ SKIP _ BIN _ CHECK = 1
../AFL/AFL-fuzz-m none-I in-o out-。/afl_test @

在 afl_test 的情况下，你应该预期 25-30 exec/sec 和 2-3 分钟内的一个独特的崩溃。

[Download](https://github.com/mxmssh/drAFL)