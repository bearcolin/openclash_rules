# OpenClash 本地订阅存档

此目录属于现有的 `openclash_rules` 项目，专门保存**本地私有**的订阅入口及生成后的 Clash/Mihomo 配置快照。与仓库根目录的公开分流规则（`.ini`）分开存放。

## 文件说明

| 文件 | 用途 | Git |
| --- | --- | --- |
| `README.md` | 本说明，无凭证信息 | 可以跟踪 |
| `机场订阅源.md` | **机场信息的唯一维护入口**：官网、注册邮箱、完整订阅 URL、到期时间及是否启用；**敏感** | 忽略 |
| `20261116-fusion-url.txt` | 完整的 SubConverter 融合订阅 URL，包含认证信息和多个订阅源；**敏感** | 忽略 |
| `20261116-merged-clash.yaml` | 从上述 URL 转换得到的完整 OpenClash/Mihomo 配置快照，含节点密钥；**敏感** | 忽略 |
| `archive/20261116-query-draft.txt` | 更早生成、未经最终端到端验证的参数草稿，仅作历史参考，**不要作为正式订阅使用**；**敏感** | 忽略 |

根目录的 `.gitignore` 忽略 `subscriptions/` 下所有文件，唯一例外是 `README.md`。未来更换机场时，仍将带凭证的订阅链接和生成文件放在这里，**不要**放到仓库根目录或提交到 GitHub。

## 当前融合配置（2026-11-16）

- 入口：现有 `edge.151510.xyz:8443/sub`，经 Cloudflare、HTTPS 和 Basic Auth 访问；本文件不记录用户名、密码、令牌或完整 URL。
- 来源：DMIT 自建 IPv4 Reality、IPv6 Reality、Hy2（OpenClash 通过本机 SOCKS 接入）、Cloudflare WS+TLS 备用，共 4 条；机场来源为 ikuuu、赔钱、好猫，共 3 个订阅。
- 公开分流规则：仓库根目录 `20261116-airport-merge.ini`。
- 验证：SubConverter 返回了 109 条节点（含 4 条 DMIT）；在家中 OpenClash 已安装的 Mihomo Meta 内核上完成了配置加载语法检查。
- **注意：这里的 YAML 是快照，不会自动随机场更新；完整 URL 才是用于日后重新转换的订阅入口。**

## 更新和恢复

1. 机场订阅失效、更换官网或新增机场时，**优先只编辑私有的 `机场订阅源.md`**。按固定字段填写官网、注册邮箱、完整订阅 URL、到期时间及「是否加入融合」，可以追加自定义字段；不要手工同步修改多个文件。
2. 让 AI 读取 `机场订阅源.md` 与现有 `20261116-fusion-url.txt`，保留原有四条 DMIT 入口、SubConverter 域名及认证信息，使用启用的机场订阅链接重建参数并进行 URL 编码；验证成功后覆盖 `20261116-fusion-url.txt`。
3. 使用新完整 URL 重新下载转换结果，确认包含 `proxies`、`proxy-groups`、`rules`，并先以 Mihomo 的配置测试命令验证；成功后更新 `20261116-merged-clash.yaml` 快照。失败时保留旧版。
4. 如果要切换家中 OpenClash，请先备份当前运行中的配置并确认新订阅的连通性；不要仅因配置检查通过就直接替换活动配置。
5. DMIT 不能访问时，已缓存的 YAML 可以作为本地恢复材料；但如果里面的机场节点失效，仍需另外获取有效的原始机场订阅。也可以把 URL 参数迁移到可信的新 SubConverter 实例。

## 安全和同步

- `.gitignore` 仅阻止**未被 Git 跟踪**的文件进入提交；不要用 `git add -f` 强制添加此目录下的私有文件。
- 订阅 URL、生成的 YAML 和历史版本都可能包含凭证。不要复制到 Issue、PR、聊天公开记录或 GitHub 仓库。
- 建议本地权限：目录 `700`，私有文件 `600`。
- 此项目位于 iCloud Drive；**Git 忽略不影响 iCloud 同步**。如果不希望这些私有文件进入 iCloud，需要另外迁到本机非同步目录或加密存储。
