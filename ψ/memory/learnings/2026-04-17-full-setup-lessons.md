---
name: Oracle Full Setup — Key Lessons
description: Critical lessons from Step 0-10 setup session for regis-oracle
type: project
---

# Oracle Full Setup Lessons — 2026-04-17

## maw Naming Convention (CRITICAL)

Oracle repo ต้องชื่อ `<name>-oracle` เสมอ — maw wake, maw bud, fleet registry ทุกอย่างใช้ convention นี้
ถ้าชื่อไม่มี suffix `-oracle` → `maw wake` จะ fail และต้อง rename ทีหลัง

**Why:** maw ใช้ `-oracle` suffix เป็น canonical marker ในทุก detection logic

## ghq Root Structure

```
ghq.root = /home/<user>
repos อยู่ที่: /home/<user>/github.com/<org>/<repo>
```

maw oracle scan walk `<ghqRoot>/<org>/<repo>/` — ถ้า repo อยู่ผิดที่จะไม่ถูก detect

## qmd บน Node 18

qmd ต้องการ Node 22+ หรือ Bun 1.0+ แต่ถ้า install ผ่าน `bun add -g` จะใช้ node runtime โดย default
**Fix:** `touch ~/.bun/install/global/node_modules/@tobilu/qmd/bun.lock` → force bun runtime

## Fleet Config Minimum Requirements

```json
{
  "name": "<oracle-name>",
  "project_repos": ["<org>/<repo>-oracle"],
  "windows": [{"name": "<repo>-oracle", "repo": "<org>/<repo>-oracle"}]
}
```

ไฟล์ต้องอยู่ที่ `~/.config/maw/fleet/<name>.json`

## tmux ใน Claude Code Sandbox

ใช้ custom socket เพื่อความเสถียร:
```bash
TMUX_TMPDIR=/tmp tmux -L <fleet-name> new-session ...
TMUX_TMPDIR=/tmp tmux -L <fleet-name> send-keys ...
```

default socket `/tmp/tmux-1000/default` อาจ conflict กับ sandbox process
