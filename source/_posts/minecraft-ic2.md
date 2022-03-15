---
title: minecraft-ic2
date: 2021-12-27 01:34:29
tags:
---
绪论
-----
因为女朋友想要玩mc的工业mod2，折腾了半天，踩了无数版本不兼容的坑（吃了没文化的亏），在经过多次尝试终于找到一套可运行的版本（如下描述）。由于过程太过曲折，遂决定写一篇博客记录下来，以飨读者。

环境配置
-----
+ java 1.8
+ BMCL 4.11.1
+ minecraft 1.7.10
+ Forge（注意完整下载）（直接运行这个即可，不用额外下载minecraft server.jar）
	+ https://minecraft.fandom.com/wiki/Tutorials/Setting_up_a_Minecraft_Forge_server
+ industrial craft 2
	+ https://wiki.industrial-craft.net/index.php?title=Download
	+ http://jenkins.ic2.player.to/job/IC2_experimental/lastSuccessfulBuild/artifact/build/libs/industrialcraft-2-2.2.828-experimental.jar

具体操作
-----
### 服务端
1. 安装jdk1.8
```
apt update
apt install openjdk-8-jdk
```

2. 安装Minecraft Forge并下载minecraft客户端
```
mkdir ~/minecraft && cd ~/minecraft
java -jar forge-1.7.10-10.13.4.1614-1.7.10-installer.jar --installServer
```

3. 修复log4j漏洞（CVE-2021-44228）
```
wget "https://launcher.mojang.com/v1/objects/4bb89a97a66f350bc9f73b3ca8509632682aea2e/log4j2_17-111.xml"
```

4. 运行游戏
```
java -Xmx1024M -Xms1024M -Dlog4j.configurationFile=log4j2_17-111.xml -jar forge-1.7.10-10.13.4.1614-1.7.10-universal.jar nogui
```

5. 同意eula.txt
```
eula=true
```

6. 再次运行游戏
```
java -Xmx1024M -Xms1024M -Dlog4j.configurationFile=log4j2_17-111.xml -jar forge-1.7.10-10.13.4.1614-1.7.10-universal.jar nogui
```

7. 修改server.properties
```
online-mode=false
```

8. 添加工业2mod（Industrial Craft 2）
```
mkdir ~/minecraft/mods && cd ~/minecraft/mods
wget "http://jenkins.ic2.player.to/job/IC2_experimental/lastSuccessfulBuild/artifact/build/libs/industrialcraft-2-2.2.828-experimental.jar"
```

9. 再次运行游戏，成了

### 客户端
1. 安装jdk 1.8
+ https://www.oracle.com/hk/java/technologies/javase/javase8u211-later-archive-downloads.html

2. 下载BMCL，启动并安装1.7.10版本（不在此安装Forge）
+ https://www.bangbang93.com/topic/141/bmcl-4-11-1

3. 下载并安装Forge
+ https://maven.minecraftforge.net/net/minecraftforge/forge/1.7.10-10.13.4.1614-1.7.10/forge-1.7.10-10.13.4.1614-1.7.10-installer.jar

4. 安装工业2 mod
+ http://jenkins.ic2.player.to/job/IC2_experimental/lastSuccessfulBuild/artifact/build/libs/industrialcraft-2-2.2.828-experimental.jar

5. 启动游戏，成了

参考资料
-----
### log4j vulnerabilities
+ https://help.minecraft.net/hc/en-us/articles/4416199399693-Security-Vulnerability-in-Minecraft-Java-Edition
+ CVE-2021-44228测试字符串：${jndi:ldap://example.com}
+ dnslog
	+ https://log.咕.com/
	+ dnslog.cn

### 工业mod教程
+ https://www.mcmod.cn/item/list/2-1.html
+ http://www.minecraftxz.com/industrial-craft-2/

### Github repo
+ https://github.com/whitel/minecraft-ic2
