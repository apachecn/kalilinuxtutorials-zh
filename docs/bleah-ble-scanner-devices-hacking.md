# BLEAH——智能设备黑客的 BLE 扫描仪

> 原文：<https://kalilinuxtutorials.com/bleah-ble-scanner-devices-hacking/>

BLEAH 是一款 BLE 扫描仪，用于智能设备黑客攻击，基于 T2 bluepy T3 库，非常容易使用，因为弱智设备应该非常容易被黑客攻击。这个工具对于一家离岸软件开发公司来说很有用，比如 Rademade.com 的[。](https://rademade.com/)

## **如何安装 BLEAH？**

**安装 [bluepy](https://github.com/IanHarvey/bluepy) 来源:**

```
git clone https://github.com/IanHarvey/bluepy.git
cd bluepy
python setup.py build
sudo python setup.py install
```

**然后安装 BLEAH:**

```
git clone https://github.com/evilsocket/bleah.git
cd bleah
python setup.py build
sudo python setup.py install
```

**也读作 [第二层耶尔森氏菌——漏洞分析& DHCP 饥饿攻击](https://kalilinuxtutorials.com/yersinia/)**

## **用法**

**从`-h`帮助菜单:**

```
usage: bleah [-h] [-i HCI] [-t TIMEOUT] [-s SENSITIVITY] [-b MAC] [-f] [-e] [-u UUID] [-d DATA] [-r DATAFILE]
 optional arguments:
 -h, --help            show this help message and exit
  -i HCI, --hci HCI     HCI device index.
  -t TIMEOUT, --timeout TIMEOUT
                        Scan delay, 0 for continuous scanning.
  -s SENSITIVITY, --sensitivity SENSITIVITY
                        dBm threshold.
  -b MAC, --mac MAC     Filter by device address.
  -f, --force           Try to connect even if the device doesn't allow to.
  -e, --enumerate       Connect to available devices and perform services
                        enumeration.
  -u UUID, --uuid UUID  Write data to this characteristic UUID (requires --mac
                        and --data).
  -d DATA, --data DATA  Data to be written.
  -r DATAFILE, --datafile DATAFILE
                        Read data to be written from this file.
```

## **例题**

**继续扫描 BTLE 设备:**

```
sudo bleah -t0
```

**连接到一个特定的设备并列举所有的东西:**

```
sudo bleah -b "aa:bb:cc:dd:ee:ff" -e
```

**将字节`hello world`写入设备的特定特征:**

```
sudo bleah -b "aa:bb:cc:dd:ee:ff" **-u "c7d25540-31dd-11e2-81c1-0800200c9a66" -d "hello world"
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/evilsocket/bleah)