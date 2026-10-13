# 📡 JioRouter AX6000 (JIDU6x01) — Custom Firmware

Ye repo aapke **JioRouter AX6000** (JIDU6101 aur JIDU6201/6401/6601/6701) ke liye roz automatically **OpenWrt** aur **ImmortalWrt** firmware banata hai.

> ⚠️ **Apni zimmedari par use karein.** Galat tarike se flash karne par router kharab (brick) ho sakta hai.

---

## 📱 Aapka router konsa hai?

| Router Model | Config |
|---|---|
| JIDU6101 | `jidu6101` |
| JIDU6201 / 6401 / 6601 / 6701 | `jidu6j01` |

---

## 🔄 Kitni baar naya firmware milega?

Har roz automatically build hoti hai:
- **OpenWrt** — raat ~5:30 AM (IST)
- **ImmortalWrt** — subah ~7:30 AM (IST)

---

## ✨ Firmware mein kya milega?

- WiFi khud-b-khud ON (2.4GHz + 5GHz, no password)
- **Smart LED indicator:**
  - 🟢 Solid Green — internet OK
  - 🟡 Blinking Yellow — internet OK, lekin koi port sirf 100Mbps pe hai (gigabit ki jagah)
  - 🔴 Blinking Red — internet down
- **Model naam runtime pe automatically detect** hota hai (MFG partition se, accurate)
- **Aurora theme** pre-installed aur default set
- Extra apps: WireGuard, SQM, nlbwmon, CPU/temp status, mwan3, zram, SCTP support
- Custom banner (SSH login pe dikhega)

---

## 📥 Firmware kaha se download karein?

**Releases** section mein jao — dono devices ke liye alag entries milengi, purani release automatically replace ho jaati hai.

---

## ⚠️ Zaroori baat

Flash karne se pehle apni original firmware ka backup zaroor rakhein.
