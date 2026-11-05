# OpenViking / VikingBot

OpenViking is a memory engine; VikingBot is its optional chat-gateway that connects the engine to chat platforms.

## Language

**飞书 (Feishu)**:
字节跳动的国内协作平台，开放平台域名为 `open.feishu.cn`。
_Avoid_: 飞书国际版

**Lark**:
飞书的国际版，开放平台域名为 `open.larksuite.com`。与飞书共用同一套开放 API 和 SDK，仅域名不同；由同一条 feishu 通道承载，靠 `domain` 配置区分。
_Avoid_: 飞书海外版, Lark Suite

**通道 (Channel)**:
机器人接入一个聊天平台的连接单元，如 telegram、feishu、slack。飞书和 Lark 同属 feishu 通道。

## Credentials

**普通用户 key (user key)**:
OpenViking 发给普通用户的 API key，角色为 `user`。机器人用它连接时，身份由 key 在服务端解析。

**管理员 key (admin key)**:
OpenViking 发给管理员的 API key，角色为 `admin`。与普通用户 key 同属 api_key 模式，行为差异沿用现有规则（如 HTTP 网关中普通用户连接禁用 `exec`）。

**root key**:
OpenViking 的根 API key，配账号和用户身份头部使用（trusted 模式），不是给 bot 常规连接用的身份。
_Avoid_: 管理员 key（两者角色不同）

**接入已有应用 (Connect existing app)**:
用户先在开放平台自己创建应用，再把凭证填给 studio 的接入方式。
_Avoid_: 手动接入

**自动创建应用 (Auto-create app)**:
studio 通过浏览器自动化替用户在开放平台创建应用并抄回凭证的接入方式。Lark 不支持这种方式。
