---
title: "启动多个服务"
linkTitle: "启动多个服务"
weight: 7
description: >
  如何在启动器中，启动多个 GoFrame 服务？
---

## 概述
通过启动器，用户可以在一个进程里面，启动多个 GfEntry。

用户还可以同时启动 GoFrame 服务和 GRPC 服务。

## 快速开始
- 安装

```shell script
$ go get github.com/rookie-ninja/rk-boot
$ go get github.com/rookie-ninja/rk-gf
```

```yaml
gf:
  - name: alice
    port: 8080
    enabled: true
    commonService:
      enabled: true
  - name: bob
    port: 8081
    enabled: true
    commonService:
      enabled: true
```

### 1.访问 Entry
```go
package main

import (
	"context"
	"github.com/rookie-ninja/rk-boot"
	"github.com/rookie-ninja/rk-gf/boot"
)

// Application entrance.
func main() {
	// Create a new boot instance.
	boot := rkboot.NewBoot()

    // Get alice
	boot.GetEntry("alice").(*rkgf.GfEntry)
    // Get bob
    boot.GetEntry("bob").(*rkgf.GfEntry)

	// Bootstrap
	boot.Bootstrap(context.Background())

	// Wait for shutdown sig
	boot.WaitForShutdownSig(context.Background())
}
```

### _**Cheers**_
![](/bootstrapper/user-guide/cheers.png)