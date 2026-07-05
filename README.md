# TG Airdrop Bot — Reusable Telegram Airdrop Automation

> Framework untuk automate SEMUA Telegram airdrop bot yang pakai inline buttons + tasks.

## Info

| | |
|---|---|
| **Type** | H2 (Telegram Inline Button Bot) |
| **Language** | Python 3.10+ |
| **Auth** | MTProto userbot (Telethon) |
| **Modal** | GRATIS |
| **Reusable** | ✅ Works with ANY Telegram airdrop bot |

## Features

- ✅ Auto-detect task types (join, follow, submit address, captcha, done)
- ✅ Auto-click inline buttons (OK, Done, Next, Start, Claim)
- ✅ Auto-submit wallet address (EVM/BSC/SOL)
- ✅ Multi-account support (multiple Telegram sessions)
- ✅ Multi-campaign tracking (campaigns.json)
- ✅ Wallet address management per campaign (wallets.json)
- ✅ Batch mode (process multiple bots from bots.txt)
- ✅ Daily mode (run all pending campaigns)
- ✅ Referral code support (/start_REF_CODE)
- ✅ New wallet generation per campaign (eth-account)
- ✅ Campaign status tracking (pending/completed/failed)

## How It Works

```
1. Add Telegram account (phone number + verification code)
2. Set wallet address (or auto-generate per campaign)
3. Add campaign (bot username + referral code)
4. Run → bot auto-detects tasks → auto-completes → stores address
5. Check campaigns → see which completed → wait for distribution
```

## Installation

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Get Telegram API credentials
#    Go to https://my.telegram.org
#    Create application → get api_id + api_hash

# 3. Configure
cp config.json.example config.json
# Edit config.json with your api_id, api_hash, phone number

# 4. Add account (first run)
python main.py
# Select option 4 → enter phone → verify code

# 5. Run
python main.py
```

## Menu Options

```
1) Run Bot              — Run tasks on single Telegram bot
2) Run Batch            — Process multiple bots from bots.txt
3) Add Campaign         — Register new bot to track
4) Add Account          — Add new Telegram session
5) Set Wallet Address   — Store address for campaign
6) Generate New Wallet  — Create new EVM wallet for campaign
7) View Campaigns       — See pending/completed campaigns
8) View Wallets         — See all stored addresses
9) Check Sessions       — Verify Telegram sessions
0) Exit
```

## Batch Mode (bots.txt)

```
# Format: @bot_username|referral_code|campaign_name
ZeroEDEXAirdropBot|518128455|ZeroE DEX Airdrop
AnotherBot|ABC123|Another Airdrop
SimpleBot||Simple Campaign
```

## CLI Usage

```bash
# Single bot
python main.py --bot @ZeroEDEXAirdropBot --ref 518128455

# Batch mode
python main.py --batch bots.txt

# Daily mode (all pending campaigns)
python main.py --daily
```

## Address Management

Bot stores wallet addresses per campaign in `data/wallets.json`:
```json
{
  "ZeroE_DEX": {
    "bot": "ZeroEDEXAirdropBot",
    "evm": "0x...",
    "private_key": "0x...",
    "created_at": "2026-07-05T16:00:00"
  }
}
```

When campaign distributes rewards, check your stored addresses.

## Campaign Tracking

Bot tracks campaigns in `data/campaigns.json`:
- Bot username
- Campaign name
- Source (where you found it)
- Expected reward
- Distribution date
- Referral code
- Status (pending/completed/failed)
- Accounts used
- Address submitted

## Supported Task Patterns

| Task Type | Auto-Detection | Auto-Action |
|-----------|---------------|-------------|
| Join Channel | Button text: "join", "subscribe" | Click URL button |
| Follow Twitter | Button text: "follow", "twitter", "x.com" | Click URL button |
| Submit Address | Bot asks for "wallet", "address", "0x" | Auto-send stored address |
| Captcha | Button text: "captcha", "verify" | Log for manual |
| OK/Done | Button text: "ok", "done", "complete" | Auto-click |
| Next/Start | Button text: "next", "start", "begin" | Auto-click |
| Claim | Button text: "claim", "collect" | Auto-click |

## File Structure

```
tg-airdrop-bot/
├── main.py                  # Entry point + CLI menu
├── utils/
│   ├── client.py            # MTProto multi-account manager
│   ├── tasks.py             # Task auto-detection + completion
│   ├── wallets.py           # Address management per campaign
│   └── campaigns.py         # Campaign tracking
├── sessions/                # Telegram session files (.gitignored)
├── data/
│   ├── campaigns.json       # Tracked campaigns
│   └── wallets.json         # Stored addresses
├── config.json              # Configuration (.gitignored)
├── config.json.example      # Config template
├── bots.txt.example         # Batch file template
├── requirements.txt         # Python dependencies
├── .gitignore
└── README.md
```

## Requirements

| Item | Required? | Cost |
|------|-----------|------|
| Python 3.10+ | ✅ | Free |
| Telegram API (api_id + api_hash) | ✅ | Free (my.telegram.org) |
| Telegram account(s) | ✅ | Free |
| EVM wallet address | ✅ | Free (auto-generated) |
| Proxy | ❌ | Optional |

## Contact

| | |
|---|---|
| **Telegram** | [@rmndkyl](https://t.me/rmndkyl) |
| **Channel** | [@layerairdrop](https://t.me/layerairdrop) |
| **Discussion** | [@layerairdropdiskusi](https://t.me/layerairdropdiskusi) |
| **GitHub** | [github.com/layerairdrop](https://github.com/layerairdrop) |

---

*Built by [Layer Airdrop ID](https://t.me/layerairdrop)*
