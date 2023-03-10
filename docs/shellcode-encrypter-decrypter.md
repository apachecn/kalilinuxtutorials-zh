# 外壳代码-加密器-解密器:外壳代码加密器和解密器使用异或密码

> 原文：<https://kalilinuxtutorials.com/shellcode-encrypter-decrypter/>

这是一个外壳代码加密器和解密器，使用异或密码加密和解密外壳代码。

## **外壳代码-加密器-解密器安装**

```
git clone https://github.com/blacknbunny/Shellcode-Encrypter-Decrypter.git && cd Shellcode-Encrypter-Decrypter/

python enc.py --help
```

**也读作[Munin——病毒总量在线哈希检查器&其他服务](https://kalilinuxtutorials.com/munin-online-hash-checker/)**

## **使用示例**

```
Encryption:
    python encdecshellcode.py --shellcode \x41\x41\x42\x42 --key SECRETKEY --option encrypt
Decryption:
    python encdecshellcode.py --shellcode \x41\x41\x42\x42 --key SECRETKEY --option decrypt
```

## **帮助**

```
usage: enc.py [-h]  [-s SHELLCODE]  [-k KEY]  [-o OPTION]
Encrypting & Decrypting Shellcode
optional arguments:` `-h,  --help			show this help message and exit
        -s  SHELLCODE,	--shelcode SHELCODE
				Shellcode To Encrypt & Decrypt
       -k  KEY,  --key KEY		Key Of The Shellcode To Encrypt & Decrypt
        -o  OPTION,   --option  OPTION
				Argument For Encrypting & Decrypting Shellcode
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/blacknbunny/Shellcode-Encrypter-Decrypter)