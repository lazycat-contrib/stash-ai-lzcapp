# Stash AI - LazyCat App

[Stash](https://github.com/savewithstash/stash)（自托管 AI 笔记收藏，"Hoard everything. Find Anything."）的懒猫微服（LazyCat）打包。

> 因 `stash` 包名已被占用（stashapp/stash 的懒猫包），本包使用 `stash-ai` 标识。

## 模式

- **镜像模式（mirror）**：`docker.io/savewithstash/stash` 镜像经 `docker.1ms.run` 加速器拉取，`require_digest_match: true` 校验镜像内容与上游一致。
- **自动跟随上游**：每日检查上游 semver tag（`channel: stable`），发现新版本自动更新版本号与镜像、构建 LPK、发布商店。
- **喵喵商店发布**：仅私有商店（MiaoMiao private store），不发布官方商店。

## 说明

- **全本地 AI**：通过 QVAC 在设备上运行语言/嵌入/视觉模型，推理不经任何外部服务
- **双数据卷**：`/lzcapp/var/stash-ai/data:/app/data`（笔记/上传）+ `/lzcapp/var/stash-ai/models:/app/models`（模型权重，首启后台下载约 1.3GB，UI 有进度条）
- 健康检查用 `/api/status`（node fetch 探测，无 curl/wget 依赖）
- 建议内存 ≥ 4GB（本地推理）

## 所需 Secrets

| Secret | 说明 |
| --- | --- |
| `APPSTORE_URL` / `APPSTORE_TOKEN` | 喵喵商店 API 地址与发布令牌 |
| `APP_ID` | 可选 |
| `PRIVATE_STORE_GROUP_CODES` | 可选，私有分组码 |

## 许可

AGPL-3.0（上游）
