# 蝎狮:符号执行工具

> 原文：<https://kalilinuxtutorials.com/manticore-symbolic-execution-tool/>

蝎狮是一个用于分析二进制文件和智能合约的符号执行工具。从版本 0.2.0 开始，需要 Python 3.6+版本。

## **蝎狮特色**

*   **输入生成**:蝎狮自动生成触发唯一代码路径的输入
*   **崩溃发现**:蝎狮通过违反内存安全发现使程序崩溃的输入
*   **执行跟踪**:蝎狮记录每个生成输入的指令级执行跟踪
*   **编程接口**:蝎狮通过 Python API 公开了对其分析引擎的编程访问

蝎狮可以分析以下类型的程序:

*   以太坊智能合约(EVM 字节码)
*   Linux ELF 二进制文件(x86、x86_64 和 ARMv7)

**也读 [Invisi-Shell:将你的 Powershell 脚本隐藏在众目睽睽之下(绕过所有 Powershell 安全特性)](https://kalilinuxtutorials.com/invisi-shell-hide-powershell-script/)**

## **用途**

### CLI

蝎狮有一个命令行界面，可以用来轻松地象征性地执行支持的程序或智能合同。分析结果将被放入以`mcore_`开始的新目录中。

使用 CLI 探索以太坊智能合约中可能的状态。蝎狮包括*检测器*，用于标记已发现状态中的潜在易受攻击代码。Solidity smart 合约必须有一个`.sol`扩展，以便蝎狮进行分析。

```
$ manticore ./path/to/contract.sol  # runs, and creates a mcore_* directory with analysis results
$ manticore --detect-reentrancy ./path/to/contract.sol  # Above, but with reentrancy detection enabled
$ manticore --detect-all ./path/to/contract.sol  # Above, but with all detectors enabled
```

命令行也可以用来简单地研究 Linux 二进制文件:

```
$ manticore ./path/to/binary        # runs, and creates a mcore_* directory with analysis results
$ manticore ./path/to/binary ab cd  # use concrete strings "ab", "cd" as program arguments
$ manticore ./path/to/binary ++ ++  # use two symbolic strings of length two as program arguments
```

### **API**

蝎狮有一个 Python 编程接口，可用于实现定制分析。

对于以太坊智能合约，可以用于任意合约属性的详细验证。设置开始条件，执行符号事务，然后检查发现的状态，以确保合同保持不变。

```
from manticore.ethereum import ManticoreEVM
contract_src="""
contract Adder {
 function incremented(uint value) public returns (uint){
 if (value == 1)
 revert();
 return value + 1;
 }
}
"""
m = ManticoreEVM()

user_account = m.create_account(balance=1000)
contract_account = m.solidity_create_contract(contract_src,
                                              owner=user_account,
                                              balance=0)
value = m.make_symbolic_value()

contract_account.incremented(value)

for state in m.running_states:
    print("can value be 1? {}".format(state.can_be_true(value == 1)))
    print("can value be 200? {}".format(state.can_be_true(value == 200)))
```

**也可以使用 API 为 Linux 二进制文件创建定制的分析工具。**

```
# example Manticore script
from manticore import Manticore

hook_pc = 0x400ca0

m = Manticore('./path/to/binary')

@m.hook(hook_pc)
def hook(state):
  cpu = state.cpu
  print('eax', cpu.EAX)
  print(cpu.read_int(cpu.ESP))

  m.terminate()  # tell Manticore to stop

m.run()
```

## **快速入门**

在几个 shell 命令中安装并尝试蝎狮:

```
# Install system dependencies
sudo apt-get update && sudo apt-get install python3 python3-pip -y

# Install Manticore and its dependencies
sudo pip3 install manticore

# Download the examples
git clone https://github.com/trailofbits/manticore.git && cd manticore/examples/linux

# Build the examples
make

# Use the Manticore CLI
manticore basic
cat mcore_*/*0.stdin | ./basic
cat mcore_*/*1.stdin | ./basic

# Use the Manticore API
cd ../script
python3 count_instructions.py ../linux/helloworld
```

你也可以使用 Docker 快速安装并试用蝎狮:

```
# Run container with a shared examples/ directory
# Note that `--rm` will make the container be deleted if you exit it
# (if you want to persist data from the container, use docker volumes)
$ docker run --rm -it trailofbits/manticore bash

# Change to examples directory
manticore@8d456f662d0f:~$ cd manticore/examples/linux/

# Build the examples
manticore@8d456f662d0f:~/manticore/examples/linux$ make

# Use the Manticore CLI
manticore@8d456f662d0f:~/manticore/examples/linux$ manticore basic

manticore@8d456f662d0f:~/manticore/examples/linux$ cat mcore_*/*0.stdin | ./basic
manticore@8d456f662d0f:~/manticore/examples/linux$ cat mcore_*/*1.stdin | ./basic

# Use the Manticore API
manticore@8d456f662d0f:~/manticore/examples/linux$ cd ../script
manticore@8d456f662d0f:~/manticore/examples/script$ python3 count_instructions.py ../linux/helloworld
```

## **安装**

注意:如果您使用 Mac OS X，您需要手动安装依赖项(最好是在 manticore 的 python 虚拟环境中):

```
brew install capstone
export MACOS_UNIVERSAL=no && pip install capstone

brew install unicorn
UNICORN_QEMU_FLAGS="--python=`whereis python`" pip install unicorn
```

选项 1:执行用户安装(需要`PATH`中的`~/.local/bin`)。

```
echo "PATH=\$PATH:~/.local/bin" >> ~/.profile
source ~/.profile
pip3 install --user manticore
```

选项 2:使用虚拟环境。

```
sudo pip3 install virtualenvwrapper
echo "source /usr/local/bin/virtualenvwrapper.sh" >> ~/.profile
source ~/.profile
mkvirtualenv manticore
sudo ./manticore/bin/pip3 install manticore
```

选项 3:执行系统安装。

```
sudo pip3 install manticore
```

选项 4:通过 Docker 安装。

```
docker pull trailofbits/manticore
```

安装后，manticore CLI 工具和 Python API 将可用。

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/trailofbits/manticore) ** *您可以在 [Linkedin](https://www.linkedin.com/company/gbhackers/) 、 [Twitter](https://twitter.com/GbhackerOn) 、[脸书](https://www.facebook.com/gbhackersadmin)上关注我们的日常网络安全更新，您还可以在线参加[最佳网络安全课程](https://ethicalhackersacademy.com/)以保持自我更新。***