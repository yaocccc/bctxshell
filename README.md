# BC TX SHELL —— blockchain transcation shell —— 区块交易执行器

基于golang，http协议

feature:
  1. 权限管理
  2. 指定时间执行交易的能力
  3. 指定条件执行交易的能力

## API 设计

```plaintext
标准headers, 所有请求均需带上headers
{
  auth: string    // 签名
  ns: string      // 所属服务 namespace
  address: string // 钱包地址
}

APIS
  1 鉴权，按钱包签名鉴权
    body: {
      auth: string          // 签名后的消息
      msg: string           // 签名的消息
    }
  2 指定时间执行签完名交易的接口
    body: {
      uuid: string          // 交易唯一标识
      address: string       // 交易对应的地址 和 headers里的地址不同 headers里的地址仅做鉴权
      signedTx: string      // 签名后的消息
      excuteTime: string    // 执行时间
    }
  3 指定watch条件 执行签完名交易的接口
    body: {
      uuid: string          // 交易唯一标识
      address: string       // 交易对应的地址 和 headers里的地址不同 headers里的地址仅做鉴权
      signedTx: string      // 签名后的消息
      conditions: WatchConditon[] // 关注的watch条件 TODO 待定义
      endTime: string       // 超过这个时间就不再执行了
    }
  4 查询接口
    body: {
      uuids?: string[]
      types?: (TIME | WATCH)[] // 类型 定时执行 或 WATCH执行
      addresses?: string[]     // 交易对应的地址
    }
```
