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

- **Do not reveal upstream channel vendors.** Never name, link, or imply internal providers or reseller gateways in customer-facing docs (e.g. DYU, KYY, MT, ZZ, JMLT, VIRALTOKAI as routing codes, Apifox vendor portals, private upstream hostnames). Describe only ViraltokAI OpenAPI models, request fields, billing, and behavior.
- Do not document internal admin features, channel weights, provider mounts, or YAML vendor credentials.
- Do not paste upstream vendor API path shapes or slug aliases unless they are identical to our public OpenAPI contract.
- When models differ by quality/speed tier (e.g. Fast vs Lite), document them as product variants — not as different upstream suppliers.
