
## 2026-11-23 - Task: 更新 Seedance 2.0 Fast 公开文档

### What was done

- 中英文 API 文档和 LLM 索引同步说明在线制作入口 `sd2-sp-fast`，并注明直接调用 API 时按有无参考视频选择请求模型。

### Testing

- 对照工作室源码检查两个语言版本的公开名和请求模型。确认 MDX 的 OpenAPI 绑定及所有请求示例未改动，索引条目和页面内相对链接有效，新增文案没有包含路由内部信息。
- `git diff --check` 通过。本机没有 Mint CLI，本轮未运行 Mintlify 构建或预览。

### Notes

- `en/api-reference/seedance/fast/create-sp.mdx`：更新英文模型选择说明。
- `zh/api-reference/seedance/fast/create-sp.mdx`：更新中文模型选择说明。
- `llms.txt`：同步中英文入口和 API 请求模型。
- `progress.md`：追加本轮修改与验证记录。
- 回滚点为 `21d1e05`。确认没有后续编辑后，执行 `git restore --source=21d1e05 -- en/api-reference/seedance/fast/create-sp.mdx zh/api-reference/seedance/fast/create-sp.mdx llms.txt`。

## 2026-11-23 - Task: 更新 Seedance 2.0 SP Fast 视频 API 请求与计费文档

### What was done

- 中英文文档和接口示例均使用 `sd2-sp-fast`。说明有无参考视频的计费档、实际响应模型名和旧配置兼容行为。

### Testing

- 解析中英文 OpenAPI JSON 和 MDX 中的 curl 请求体，确认有无参考视频的实例都使用同一模型。检查文档内相对链接与新增内容。
- `git diff --check` 通过。未运行 Mintlify 构建或发布。

### Notes

- `en/api-reference/seedance/fast/create-sp.mdx`：英文统一请求示例与计费说明。
- `zh/api-reference/seedance/fast/create-sp.mdx`：中文统一请求示例与计费说明。
- `en/api-reference/openapi.json`：英文视频 API 补充两个请求示例。
- `zh/api-reference/openapi.json`：中文视频 API 补充两个请求示例。
- `llms.txt`：索引中的中英文摘要同步统一模型名。
- `progress.md`：追加本轮记录。
- 本机回滚可执行 `git apply --reverse /tmp/jimiai-sp-fast-api-docs-20261123.patch`，保留上一轮的在线入口说明。

## 2026-11-23 - Task: 将 SP Fast 对外文档统一为 720p

### What was done

- 中英文 SP Fast 文档和索引明确写明固定输出 720p，移除对外页面中的旧计费名说明。

### Testing

- 检查两页均无 780p 字样，计费表使用两条 720p 计费名，curl 示例继续使用 `sd2-sp-fast`。 `git diff --check` 通过。

### Notes

- `en/api-reference/seedance/fast/create-sp.mdx`：明确英文页面输出为 720p。
- `zh/api-reference/seedance/fast/create-sp.mdx`：明确中文页面输出为 720p。
- `llms.txt`：两条对应索引同步分辨率。
- `progress.md`：追加本轮记录。
- 回滚方式：在两个 MDX 文件恢复本轮替换的旧计费兼容段落，并从索引的两条 SP Fast 摘要移除本轮追加的 720p 说明。

## 2026-11-23 - Task: 下线创建满血版 Fast 视频文档页

### What was done

- 下线中英文满血版 Fast 独立文档页，清理导航、站内引用和 LLM 索引。旧网址跳转至对应语言的 Seedance 满血版文档，SP Fast 和官转 Fast 仍可访问。

### Testing

- 解析 `docs.json`，确认两条旧路由只保留重定向、目标页存在、导航无旧条目。检查中英文 MDX 和 LLM 索引无旧页链接，SP Fast 与官转 Fast 页面仍在。
- `git diff --check` 通过。未运行 Mintlify 构建或发布。

### Notes

- `docs.json`：移除中英文导航入口，配置旧地址跳转。
- `en/api-reference/seedance/fast/create.mdx`：删除英文独立文档页。
- `zh/api-reference/seedance/fast/create.mdx`：删除中文独立文档页。
- `en/api-reference/seedance/create.mdx`：清理标准版英文文档的旧页链接。
- `zh/api-reference/seedance/create.mdx`：清理标准版中文文档的旧页链接。
- `en/api-reference/seedance/fast/create-sp.mdx`：清理 SP Fast 英文文档的旧页链接。
- `zh/api-reference/seedance/fast/create-sp.mdx`：清理 SP Fast 中文文档的旧页链接。
- `llms.txt`：移除旧页的两个索引条目。
- `progress.md`：追加本轮修改和验证记录。
- 本机回滚可执行 `git apply --reverse /tmp/jimiai-retire-full-fast-docs-20261123.patch`，保留本轮之前的 SP Fast 文档改动。

## 2026-11-23 - Task: 下线 Seedance 2.0 满血版文档

### What was done

- 移除满血版独立中英文文档，清理导航和相关文档的旧链接。满血版、满血版 Fast 和 MD 的旧网址直接跳转到对应语言的统一视频创建文档。

### Testing

- 解析 `docs.json` 并扫描中英文 MDX 和 LLM 索引。确认下线页不在导航中，旧路由没有多级跳转，跳转目标及 SP、SP Fast、官转 Fast、Mini 页面都存在。
- `git diff --check` 通过。未运行 Mintlify 构建或发布。

### Notes

- `docs.json`：清理满血版导航，设置直接跳转。
- `en/api-reference/seedance/create.mdx`、`zh/api-reference/seedance/create.mdx`：删除中英文满血版页面。
- `en/api-reference/seedance/assets-audit.mdx`、`zh/api-reference/seedance/assets-audit.mdx`：素材引用说明改链统一视频接口。
- `en/api-reference/seedance/gz720/create.mdx`、`zh/api-reference/seedance/gz720/create.mdx`：官转说明改链统一视频接口。
- `en/api-reference/seedance/mini/create.mdx`、`zh/api-reference/seedance/mini/create.mdx`：清理 Mini 文档的满血版引用。
- `en/api-reference/seedance/sp/create.mdx`、`zh/api-reference/seedance/sp/create.mdx`：清理 SP 文档的满血版引用。
- `llms.txt`：移除两个满血版页面条目。
- `progress.md`：追加本轮修改与验证。
- 本机回滚可执行 `git apply --reverse /tmp/jimiai-retire-seedance-full-docs-20261123.patch`，保留上一轮满血版 Fast 的下线改动。

## 2026-11-23 - Task: 下线满血版素材审核文档分组

### What was done

- 移除中英文满血版导航分组及其两项素材审核文档，同时清理 OpenAPI 文档入口、LLM 索引和站内引用。SP 素材库及统一视频文档仍可使用。

### Testing

- 解析中英文 OpenAPI 和导航配置，确认旧审核路径、模型结构及站内链接均已移除，SP 上传素材和视频创建入口仍存在。
- `git diff --check` 通过。没有发布文档。

### Notes

- `docs.json`：删除两个满血版导航分组。
- `en/api-reference/seedance/assets-audit.mdx`、`zh/api-reference/seedance/assets-audit.mdx`：移除提交素材审核页面。
- `en/api-reference/seedance/assets-status.mdx`、`zh/api-reference/seedance/assets-status.mdx`：移除审核状态页面。
- `en/api-reference/openapi.json`、`zh/api-reference/openapi.json`：删除审核相关的文档操作和专用结构。
- `en/api-reference/seedance/sp/assets-upload.mdx`、`zh/api-reference/seedance/sp/assets-upload.mdx`：清理已删除的满血版审核页链接。
- `llms.txt`：移除四条中英文索引。
- `progress.md`：追加本轮记录。
- 本机回滚可执行 `git apply --reverse /tmp/jimiai-retire-full-audit-docs-20261123.patch`。

## 2026-11-23 - Task: 同步 Seedance 2.5 标准版预扣和 token 结算文档

### What was done

- 更新中英文标准版用法与 LLM 索引，解释按秒预扣、成功后按实际 token 调整差额、创建与查询响应中的金额。

### Testing

- 检查两份文档中的预扣模型、结算模型、`completion_tokens` 和 `data.cost` 与实现匹配，清除原参考视频时长计费描述。`git diff --check` 通过。未发布。

### Notes

- `en/api-reference/seedance/25/create.mdx`：英文预扣、结算和响应说明。
- `zh/api-reference/seedance/25/create.mdx`：中文预扣、结算和响应说明。
- `llms.txt`：同步两条标准版摘要。
- `progress.md`：追加本轮记录。
- 回滚点为 `6cbbad1`。确认无后续编辑后，执行 `git restore --source=6cbbad1 -- en/api-reference/seedance/25/create.mdx zh/api-reference/seedance/25/create.mdx llms.txt`。

## 2026-11-23 - Task: 补充 Seedance 2.5 标准版两档 token 价格说明

### What was done

- 中英文 API 文档说明 480p 和 720p 共用普通档，1080p 使用独立 token 单价。

### Testing

- 核对两种语言的分辨率、计费模型名和费用字段。`git diff --check` 通过。未发布。

### Notes

- `en/api-reference/seedance/25/create.mdx`：说明英文 API 的两档结算价。
- `zh/api-reference/seedance/25/create.mdx`：同步中文两档说明。
- `progress.md`：追加本轮记录。
- 回滚点为 `30339b6`。确认无后续修改后，对上述两个 MDX 文件执行 `git restore --source=30339b6 --` 加对应路径。

## 2026-11-23 - Task: 补充 Seedance 2.5 标准版参考视频结算档位

### What was done

- 中英文 API 文档同步四档结算模型，说明参考视频参与选档，按实际 token 结算。

### Testing

- 校验两种语言的档位顺序、四个计费模型名及相关 API 字段。`git diff --check` 通过。未发布。

### Notes

- `en/api-reference/seedance/25/create.mdx`：更新英文四档结算说明。
- `zh/api-reference/seedance/25/create.mdx`：更新中文四档结算说明。
- `progress.md`：追加本轮记录。
- 回滚点为 `64cb957`。确认无后续编辑后，执行 `git restore --source=64cb957 -- en/api-reference/seedance/25/create.mdx zh/api-reference/seedance/25/create.mdx`。
