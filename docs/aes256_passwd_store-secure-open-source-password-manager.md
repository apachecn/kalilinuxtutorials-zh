# AES256_Passwd_Store:安全的开源密码管理器

> 原文：<https://kalilinuxtutorials.com/aes256_passwd_store-secure-open-source-password-manager/>

[![](img/a7ce21330d93d1e2655ee823d63d3d1f.png)](https://1.bp.blogspot.com/-cizB3jCDfPM/YU1rbJ001dI/AAAAAAAAK8I/HOdea6JA4tESzAQaBtWdwOuZDq7RVySEACLcBGAsYHQ/s728/download%2B%25281%2529.png)

**AES256_Passwd_Store** 脚本在自定义数据库文件中安全地加密或解密磁盘上的密码。它还具有从先前生成的数据库文件中检索密码的功能。

该脚本从 stdin/内存中获取一个主密码，然后使用传递给算法参数/-a (scrypt，sha256)的指定哈希算法对密码进行哈希处理，最后 AES-256 使用该算法的哈希作为 AES-256 密钥对文件数据进行加密/解密。

当向算法参数提供“scrypt”参数时，脚本将为每个数据库文件编辑或创建生成一个自定义的 scrypt salt。唯一生成的 salt 是 base64 编码的，并作为元数据添加到每个数据库文件的加密字节前，加密字节由回车符换行字节(用于解析)分隔。

使用更改密码参数/-cp 时，脚本会将数据库文件的数据解密到内存中，将随机字节*WIPE_PASSES 写入数据库文件，截断文件，最后将使用新的哈希主密码加密的新数据 AES-256 写入数据库文件。实际上使得数据恢复/取证变得困难。

**使用脚本作为哈希算法的用法示例**

创建数据库文件

**python 3 AES passwd _ store . py-a scrypt-c**

更改数据库文件的主口令

**python 3 AES passwd _ store . py-a scrypt-CP**

编辑数据库文件

**python 3 AES passwd _ store . py-a scrypt-e**

从数据库文件中查询数据

**python 3 AES passwd _ store . py-a scrypt-q**

例子

**#向数据库添加条目/修改现有数据:
pass _ id1 =密码
pass _ id2 =密码
pass _ ID3 =密码
#删除现有数据:
pass _ id1 =删除
pass _ id2 =删除
# -q 参数:查询数据(不输入任何内容转储所有数据):
pass_id1
pass_id3
#按 ctrl+D (linux)或 ctrl+Z (windows)保存来自**

[**Download**](https://github.com/c0dy-c0des/aes256_passwd_store)