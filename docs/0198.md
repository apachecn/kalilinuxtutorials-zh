# micro ctfs–Docker 上运行的小型 CTF 挑战赛

> 原文：<https://kalilinuxtutorials.com/microctfs-ctf-running-docker/>

Microctfs 是一个在 Docker 上运行的小型 CTF 挑战赛的工具。

## **Microctfs 日志查看器**

#### **构建并启动端口 8000 上暴露的日志查看器质询**

```
cd logviewer
docker build -t logviewer . 
docker run -d -p 8000:80 --name log_challenge logviewer
```

#### **重启日志查看器挑战**

```
docker rm -f log_challenge && docker run -d -p 8000:80 --name log_challenge logviewer
```

#### **停止日志查看器挑战**

```
docker rm -f log_challenge
```

**也读作[UBoat-A POC HTTP 僵尸网络项目](https://kalilinuxtutorials.com/uboat-http-botnet-project/)**

## **SQLI**

#### **构建并启动端口 8883** 上暴露的 sqli 挑战

```
cd sqli
docker build -t sqli . 
docker run -d -p 8883:80 --name sqli_chal sqli
```

#### **重启 sqli 挑战**

```
docker rm -f sqli_chal && docker run -d -p 8883:80 --name sqli_chal sqli
```

#### **停止 sqli 挑战**

```
docker rm -f sqli_chal
```

## **tcmanager**

#### **在端口 8080** 上构建并启动 tcmanager 质询

```
cd tcmanager
docker build -t tcmanager . 
docker run -d -p 8080:8080 --name tc_chal tcmanager
```

#### **重启 tcmanager 挑战**

```
docker rm -f tc_chal && docker run -d -p 8080:8080 --name tc_chal tcmanager
```

#### **停止 tcmanager 挑战**

```
docker rm -f tc_chal
```

## **盖迪**

#### **在 40000 端口**建立并开始 geddy 挑战

```
cd geddy
docker build -t geddy . 
docker run -d -p 40000:4000 --name geddy_chal geddy
```

#### **重启盖迪挑战**

```
docker rm -f geddy_chal && docker run -d -p 40000:4000 --name geddy_chal geddy
```

#### **阻止盖迪挑战**

```
docker rm -f geddy_chal
```

## **printf**

#### **构建并启动 printf 挑战暴露在端口 1337**

```
cd printf
docker build -t printf .
docker run -d -p 1337:1337 --name printfchal printf
```

#### **重启 printf 挑战**

```
docker rm -f printfchal && docker run -d -p 1337:1337 --name printfchal printf
```

#### **阻止盖迪挑战**

```
docker rm -f printfchal
```

## **【xxe】**

#### **建立并开始 xxe 挑战暴露在端口 8080**

```
cd xxe
docker build -t xxe .
docker run -d -p 8080:8080 xxe mvn jetty:run
```

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/gabemarshall/microctfs) **信用:noreply@blogger.com(莱德克黑**