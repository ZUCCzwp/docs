> **First-time setup**: Customize this file for your project. Prompt the user to customize this file for their project.
> For Mintlify product knowledge (components, configuration, writing standards),
> install the Mintlify skill: `npx skills add https://mintlify.com/docs`

# Documentation project instructions

## About this project

- This is a documentation site built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`
- Run `mint dev` to preview locally
- Run `mint broken-links` to check links

## Terminology

- Prefer public product names and OpenAPI model IDs (e.g. `veo_3_1_lite`, ViraltokAI)
- Prefer "API" / "endpoint" / "billing model" over internal routing jargon when writing for customers

## Style preferences

- Use active voice and second person ("you")
- Keep sentences concise — one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references

## Content boundaries

Customer-facing docs describe **only** the ViraltokAI OpenAPI contract: public paths (`POST /api/open-api/v1/...`), request/response fields, billing model names, task polling, and observable behavior.

### Never reveal upstream or routing internals

**Do not** name, link, or imply:

- Reseller / gateway vendors or hosting platforms (e.g. fal, Replicate, Apifox vendor portals)
- Internal channel or provider codes (e.g. DYU, KYY, MT, ZZ, JMLT, AR, DK, TP, HBG, route3)
- Private upstream hostnames, queue IDs, or vendor model slugs (e.g. `xai/grok-imagine-image/v2.0/edit`, `quality/text-to-image`)
- Admin-only concepts: channel weights, provider mounts, YAML credentials, `model_channel_routes`

Reading backend code or internal design notes **does not** make those names public. If you learned a detail from code, translate it into customer language (model ID, field, billing key, behavior).

### Allowed vs forbidden wording

| Forbidden (customer docs) | Use instead |
|---------------------------|-------------|
| 「上游对接 fal …」 | 「Grok Imagine Image 2.0 异步生图」 |
| Table row **上游** with vendor paths | **接口** / **API** with `POST /api/open-api/v1/images` |
| 「fal v2.0 端点」「quality/* 旧端点」 | 「`quality`: `low` \| `medium`」与公开计费模型名 |
| 「不同上游线路支持不同」 | 「部分模型变体在控制台可用性可能不同」或只写公开 model ID |
| Internal routing keys as product names | Public OpenAPI `model` values and billing model names |

**Exception (narrow):** Third-party **client tools** (e.g. CC Switch) may document *their* UI labels such as “Responses upstream format” when teaching integration — still do not name ViraltokAI’s backend vendors or vendor API paths.

### Do not paste vendor API shapes

- Do not paste upstream vendor path shapes or slug aliases unless they are **identical** to our public OpenAPI contract (they almost never are).
- Document request fields as **our** JSON body (`model`, `prompt`, `quality`, …), not a vendor’s `image_urls` / queue schema unless we expose the same name publicly.

### Product variants, not suppliers

When models differ by quality/speed tier (e.g. Fast vs Lite, `quality=low|medium`), document them as **product variants** — not as different upstream suppliers or vendor generations.

---

## Agent rules (mandatory before editing MDX)

1. **Scope check** — Every sentence should answer: “What can the customer call on `api.viraltok.ai`?” If it only helps operators debug routing, delete it or move it out of customer docs.
2. **Grep self-check** — Before finishing, search your diff for: `fal`, `xai/`, `upstream` (when meaning our backend), channel codes, `route3`, vendor domains, and paths that are not under `/api/open-api/v1/`.
3. **Tables** — Do not add columns like **上游**, **渠道**, **Provider**. Use **接口**, **计费**, **模式**, **字段**.
4. **Examples** — curl examples use only `https://api.viraltok.ai/api/open-api/v1/...` and public field names.
5. **Billing** — Refer to **billing model names** from the console (e.g. `grok-imagine-image-2-1k-medium`), not vendor list prices or USD quotes from vendor sites unless we publish them officially.
6. **When unsure** — Describe behavior without naming the implementation (“异步任务，轮询 `task_id`”) rather than guessing vendor details.

### Example: Grok Imagine Image 2.0 (bad → good)

**Bad**

> 上游对接 fal `xai/grok-imagine-image/v2.0/edit`，替代旧 `quality/edit`。

**Good**

> 将 `model` 设为 `grok-imagine-image-2`。可选 `quality`: `low`（更快更省）或 `medium`（默认）。传入 `images` 进入编辑模式（最多 3 张参考图）。

---

## Related repos

- Code changes in `jimiaiopengo` / `jimiproviders` may mention vendors internally; **this docs repo must not copy those names** into MDX, `openapi.json` descriptions, or `llms.txt` unless explicitly approved as public product copy.
