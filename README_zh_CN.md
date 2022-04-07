# webpush-go

[![Go Report Card](https://goreportcard.com/badge/github.com/SherClockHolmes/webpush-go)](https://goreportcard.com/report/github.com/SherClockHolmes/webpush-go)
[![GoDoc](https://godoc.org/github.com/SherClockHolmes/webpush-go?status.svg)](https://godoc.org/github.com/SherClockHolmes/webpush-go)

网络推送 API 加密，支持 VAPID。

```bash
go get -u github.com/SherClockHolmes/webpush-go
```

## 例子

所有的例子在 [example](example/) 文件夹内。

```go
package main

import (
	"encoding/json"

	webpush "github.com/SherClockHolmes/webpush-go"
)

func main() {
	// 订阅解码
	s := &webpush.Subscription{}
	json.Unmarshal([]byte("<YOUR_SUBSCRIPTION>"), s)

	// 发送通知
	resp, err := webpush.SendNotification([]byte("Test"), s, &webpush.Options{
		Subscriber:      "example@example.com",
		VAPIDPublicKey:  "<YOUR_VAPID_PUBLIC_KEY>",
		VAPIDPrivateKey: "<YOUR_VAPID_PRIVATE_KEY>",
		TTL:             30,
	})
	if err != nil {
		// TODO: 处理错误
	}
	defer resp.Body.Close()
}
```

### 生成 VAPID 密钥

使用辅助方法 `GenerateVAPIDKeys` 来生成 VAPID 密钥对。

```golang
privateKey, publicKey, err := webpush.GenerateVAPIDKeys()
if err != nil {
	// TODO: 处理错误
}
```

## 开发

1. 安装 [Go 1.11+](https://golang.org/)
2. `go mod vendor`
3. `go test`

#### 其他编程语言实现参考这里：

[WebPush Libs](https://github.com/web-push-libs)
