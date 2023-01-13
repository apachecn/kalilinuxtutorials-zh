# Hash pump——在各种哈希算法中利用哈希长度扩展攻击的工具

> 原文：<https://kalilinuxtutorials.com/hashpump-tool-exploit-hash-length/>

HashPump 是一个利用各种哈希算法中的哈希长度扩展攻击的工具。目前支持的算法:MD5，SHA1，SHA256，SHA512。

## 菜单

```
$ hashpump -h
HashPump [-h help] [-t test] [-s signature] [-d data] [-a additional] [-k keylength]
    HashPump generates strings to exploit signatures vulnerable to the Hash Length Extension Attack.
    -h --help          Display this message.
    -t --test          Run tests to verify each algorithm is operating properly.
    -s --signature     The signature from known message.
    -d --data          The data from the known message.
    -a --additional    The information you would like to add to the known message.
    -k --keylength     The length in bytes of the key being used to sign the original message with.
    Version 1.2.0 with CRC32, MD5, SHA1, SHA256 and SHA512 support.
    <Developed by bwall(@botnet_hunter)>
```

**也可理解为[MobSF——移动安全框架是一个自动化的一体化移动应用](https://kalilinuxtutorials.com/mobsf-mobile-security-framework/)**

## **样本输出**

```
$ hashpump -s '6d5f807e23db210bc254a28be2d6759a0f5f5d99' --data 'count=10&lat=37.351&user_id=1&long=-119.827&waffle=eggo' -a '&waffle=liege' -k 14
0e41270260895979317fff3898ab85668953aaa2
count=10&lat=37.351&user_id=1&long=-119.827&waffle=eggo\x80\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00
```

## **水泵安装**

```
$ git clone https://github.com/bwall/HashPump.git
$ apt-get install g++ libssl-dev
$ cd HashPump
$ make
$ make install
```

`apt-get`和`make install`需要 root 权限才能正确运行。实际需求是针对`-lcrypto`，因此根据您的操作系统，您的依赖关系可能会有所不同。

在 OS X HashPump 也可以使用[自制软件](http://brew.sh/)安装:

```
$ brew install hashpump
```

## **Python 绑定**

Python 爱好者会对这一新增功能感到满意。Python 绑定以 hashpumpy 的形式添加，省去了我用 Python 编写所有这些哈希算法的实现和修改状态的能力。

### **安装**

PyPI 上有这些 Python 绑定，可以通过 pip 安装。pip 安装哈希

### **用途**

```
>>> import hashpumpy
>>> help(hashpumpy.hashpump)
Help on built-in function hashpump in module hashpumpy:

hashpump(...)
    hashpump(hexdigest, original_data, data_to_add, key_length) -> (digest, message)

    Arguments:
        hexdigest(str):      Hex-encoded result of hashing key + original_data.
        original_data(str):  Known data used to get the hash result hexdigest.
        data_to_add(str):    Data to append
        key_length(int):     Length of unknown data prepended to the hash

    Returns:
        A tuple containing the new hex digest and the new message.
>>> hashpumpy.hashpump('ffffffff', 'original_data', 'data_to_add', len('KEYKEYKEY'))
('e3c4a05f', 'original_datadata_to_add')
```

### **Python 3 注**

hashpumpy 支持 Python 3。与 Python 2 版本不同的是，从`hashpumpy.hashpump`返回的元组中的第二个值(新消息)是一个类似字节的对象，而不是一个字符串。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/bwall/HashPump#sample-output)