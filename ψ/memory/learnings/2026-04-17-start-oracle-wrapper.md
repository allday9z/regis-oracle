---
name: start-oracle wrapper scripts + maw-ui fixes
description: 3 CLI wrappers for fleet bootstrap, DashboardPro bug fixes, federation config requirement
type: project
---

# start-oracle Wrapper + maw-ui Fixes — 2026-04-17

## Wrapper Scripts Created

3 scripts ใน `~/.local/bin/` (อยู่ใน PATH):

| Script | หน้าที่ |
|--------|---------|
| `start-oracle` | บูตทุก service + idempotent check |
| `stop-oracle` | หยุด services (ไม่แตะ tmux) |
| `status-oracle` | ports, PIDs, HTTP, fleet, tmux |

Services ที่ manage:
- maw server :3456 (via `maw serve`)
- maw-ui vite :5173 (via `bun run dev` ใน maw-ui dir)
- qmd MCP :7789 (via `qmd mcp --http --port 7789 --daemon`)

## maw-ui Bugs Found (upstream)

### Bug 1: JSX Syntax Error in DashboardPro.tsx:200

```tsx
// ❌ broken — { inside map((x) => ( ... )) = object literal
s.windows.map((w) => (
  {READONLY ? <A/> : <B/>}
))

// ✓ fix — remove wrapping parentheses
s.windows.map((w) =>
  READONLY ? <A/> : <B/>
)
```

### Bug 2: Runtime Crash — plugins.plugins.reduce()

maw `/api/plugins` คืน array ตรงๆ ไม่ใช่ `{plugins: [...]}`

**Fix:** defensive parsing:
```tsx
const list = Array.isArray(plugins) ? plugins : (plugins.plugins ?? []);
```

### Bug 3: Federation Page "No Backend Connected"

`useFederationList` hook ต้องการ `config.node` แต่ default `maw.config.json` ไม่มี field นี้

**Fix:** เพิ่มใน `~/.config/maw/maw.config.json`:
```json
{
  "node": "local"
}
```

## Key Insight: config hot-reload

maw ไม่ hot-reload `~/.config/maw/maw.config.json` — ต้อง:
```bash
kill $(ss -tlnp | grep :3456 | grep -oP 'pid=\K[0-9]+')
nohup maw serve > /tmp/maw-serve.log 2>&1 &
```

## Upstream Debt

แก้ไข 2 bugs ใน maw-ui แบบ local — `git pull` จะ overwrite
**TODO:** Fork → PR ไป `Soul-Brews-Studio/maw-ui`
