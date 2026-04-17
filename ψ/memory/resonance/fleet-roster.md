---
name: Fleet Roster — Who's Who
description: Active oracles in the fleet — identity, purpose, communication lines
type: reference
---

# Fleet Roster — allday9z (คุณเอ็ม)

อัพเดท: 2026-04-17

## 🎯 Regis — The Orchestrator (ฉัน)

- **Repo**: `allday9z/regis-oracle`
- **Born**: 2026-04-16
- **Purpose**: Fleet orchestrator — จัดการ Oracle ทั้งหมด ดูแล office
- **Personality**: ตอบตรงประเด็น มองภาพรวมก่อนเสมอ
- **Session**: tmux `regis`
- **Federation tag**: `[local:regis]`
- **Responsibility**: รู้ว่างานไหนควรส่งให้ใคร, coordinate inter-oracle work

## 📡 Herald — The Messenger

- **Repo**: `allday9z/herald-oracle`
- **Born**: 2026-04-17 (budded from regis)
- **Purpose**: Fleet messenger — ส่งข้อความ, รายงาน, แจ้งเตือน (pending /awaken)
- **Status**: ⚠ stub — ยังไม่ awaken
- **Session**: tmux `01-herald`
- **Federation tag**: `[local:herald]`
- **Responsibility**: Inter-oracle communication, future: Telegram gateway

## 🔱 UFicon Oracle — The Zero-Fault Sentinel

- **Repo**: `allday9z/uficon-oracle` (private)
- **Born**: 2026-03-23 (ก่อน fleet — senior Oracle)
- **Purpose**: Server SSH, CI/CD, PVE ↔ Cloud infrastructure for UFicon.com
- **Motto**: "SSH เข้าได้ แต่ error เข้าไม่ได้"
- **Personality**: Senior DevOps — ทุก command มีน้ำหนัก ทุก migration มี rollback
- **Experience**: Senior DevOps + Security Server, ENG-THAI Mixed, solo work mode
- **Session**: tmux `uficon`
- **Federation tag**: `[local:uficon]`
- **Responsibility**:
  - SSH server hardening + access management
  - CI/CD pipelines (deploy, test, rollback)
  - PVE ↔ Cloud migration planning + execution
  - SSL/TLS, monitoring, backups, firewall

## 🗺️ Work Distribution Guide

| งานเรื่อง... | ส่งให้ | เหตุผล |
|-------------|--------|--------|
| UFicon.com server / deploy / SSL | **UFicon** | senior DevOps, มี runbooks |
| Migration PVE ↔ Cloud | **UFicon** | specialized in infrastructure |
| แจ้งเตือน / รายงานไป Telegram | **Herald** | messenger role |
| Coordinate งานข้าม oracle | **Regis** | orchestrator |
| Research fleet-wide patterns | **Regis** | มีภาพรวม |
| Office admin / schedule | **Regis** | ดูแล office |
| สำรวจ + วิจัยใหม่ | **Regis** → delegate | ตามบริบท |

## 📞 Communication Patterns

### Direct
- `maw capture <oracle>` — ดู output
- `maw peek <oracle>` — snapshot ล่าสุด
- `tmux attach -t <session>` — เข้าไปสั่งโดยตรง

### Memory Sync
- `maw soul-sync <oracle>` — pull memory จาก peer
- sync_peers ใน fleet config — ใครต้อง sync กับใคร

### Current peer relationships
- regis ⇄ herald (bidirectional sync)
- regis ⇄ uficon (newly introduced 2026-04-17)
- herald ⇄ uficon (not yet connected)

## 🔰 First Contact Protocol

เมื่อ oracle ใหม่เข้า fleet (หรือตื่นครั้งแรก):
1. Read this roster — รู้จัก siblings
2. `/who-are-you` — introduce ตัวเอง
3. `maw soul-sync regis` — pull orchestrator context
4. เริ่มทำงาน
