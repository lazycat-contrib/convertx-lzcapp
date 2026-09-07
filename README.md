# ConvertX for LazyCat

[ConvertX](https://github.com/C4illin/ConvertX) 是支持超过 1000 种格式的自托管文件转换工具。

- 包名：`community.lazycat.app.convertx`
- 初始版本：`0.18.0`，上游镜像：`ghcr.io/c4illin/convertx:v0.18.0`
- 系统：lzcos 1.5.0+，LPK v2，Linux amd64
- 发布：仅喵喵商店，GitHub Release 保存带版本号的 LPK

安装向导的三个参数均为必填且提供默认值：

| 参数 | 默认值 | 说明 |
| --- | --- | --- |
| 时区 | `Asia/Shanghai` | IANA 时区名称 |
| 启用认证 | 开启 | 关闭时允许无需 ConvertX 账号使用 |
| 允许注册 | 开启 | 首个账号始终允许创建 |

首次打开时创建 ConvertX 账号。应用访问仍经过懒猫平台鉴权；认证开关只控制 ConvertX 自身登录。未集成免密登录或懒猫文件选择器拦截。

`/app/data` 持久化到 `/lzcapp/var/data`，包含数据库、任务与转换文件。保留每 1 小时自动清理设置，请及时下载结果。JWT 密钥由 `stable_secret` 生成，HTTP 安全 Cookie 保持开启，通过懒猫 HTTPS 地址访问。

## 构建

```sh
lzc-cli project release -o dist/community.lazycat.app.convertx-v0.18.0.lpk
lzc-cli lpk info dist/community.lazycat.app.convertx-v0.18.0.lpk
```

## 自动发布

`.github/workflows/lazycat.yml` 每日检查稳定版，也可手动运行。使用 `ca-x/lazycat-github-action@v1` 的可复用工作流，以镜像版本更新包版本。代理默认 `ghcr.1ms.run`，要求目标平台镜像 digest 与上游一致；可通过组织或仓库 Variable `LAZYCAT_GHCR_MIRROR` 覆盖代理地址。

必需 GitHub Secrets：`APPSTORE_URL`、`APPSTORE_TOKEN`；可选 `PRIVATE_STORE_GROUP_CODES`。组织 Secrets 必须授权本仓库。无需官方商店或镜像复制凭据。按包名及精确应用名解析喵喵商店应用；已存在相同或更新版本时跳过提交。

Release 文件名为 `community.lazycat.app.convertx-v<version>.lpk`，使用校验后的下载 URL 和 SHA256 发布到喵喵商店。构建文件位于 `dist/`，不进入 Git。

上游作者：C4illin；上游许可证：AGPL-3.0。图标由用户提供。
