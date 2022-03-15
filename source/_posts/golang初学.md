---
title: golang初学
date: 2020-09-05 20:41:45
tags:
---

# tips
+ import path prefix（Where to find module）、module（go.mod）、package（directories）
+ 目录名与文件名不重要，真正重要的是package名和module名（但一般目录名和包名相同）
+ 一个目录下只能有一个package，但在这个目录下的子目录可以包含另一个package
+ 同一个包的源码文件不能放在多个目录下
+ 两个不同的包不能放在同一目录下
+ import使用全路径，package定义时仅使用包名
+ 使用 import 语句导入包时，使用的是包所属文件夹的名称

# GO111MODULE
+ GO111MODULE=off使用旧版包管理方式，需要手动指定包的位置，需要自己管理版本
+ GO111MODULE=on使用新版module包管理模式，可以自动处理import的第三方包，使用go mod init初始化module，使用go mod tidy来自动进行包管理

# GOPATH
+ 在$GOPATH/src/package_name之内使用go mod init，会自动把当前目录名作为module名
+ 在$GOPATH/src/package_name之外使用go mod init，需要手动加上module名，如：go mod init package_name

+ solve import and not used error
```
import (
    _ "github.com/hyperledger/fabric"
)
```

+ go module
```
go env -w 'GO111MODULE=auto'    // auto switch between on and off
go env -w 'GO111MODULE=on'      // enable go module management
go env -w 'GO111MODULE=off'     // disable go module management and use traditional methods

go mod init     // initialize new module in current directory
go mod tidy     // add missing and remove unused modules
go get          // add dependencies to current module and install them
```

+ go compile and programs
```
go build        // compile packages and dependencies
go run          // compile and run Go program
go install      // compile and install packages and dependencies
go clean        // remove object files and cached files
```

+ go proxy
```
go env -w 'GOPROXY=https://goproxy.io, direct'      // set go proxy for China
```
