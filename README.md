# StageSync

**Make fans’ fever visible.**  
StageSync turns fan gestures into on‑chain reactions that drive live lights/FX, enable fair tips, and generate second‑by‑second insight for artists and venues.

> This repository documents the **concept** and product design for StageSync. Implementation details and code samples will be added as the project evolves.

---

## TL;DR

- **Problem:** In physical concerts, fans can’t interact at the exact moment they feel something. Artists don’t get time‑stamped feedback, and venues lack creator‑economy rails that work in‑room. Existing wristbands/penlights are closed systems with no open data or value transfer.
- **Solution:** A lightweight participation rail: fans tap or wave → **on‑chain reactions** → stage cues (DMX/Art‑Net), **event NFTs & rewards**, **tips with auto‑splits**, and a **time‑stamped heatmap** for artists.
- **Presence:** We verify “in‑venue” via **cell‑base ID check** (serving base‑station ID compared to the venue area using public cell‑tower datasets). Privacy‑preserving; no PII stored on‑chain.
- **Demo beat:** Scan QR/blink → mint **Compressed NFT** Event Pass + Reaction Credits → verify presence → send reactions → watch lights react → redeem collectibles.

---

## Problem

*We’re all big fans of bands and live houses. But we noticed…*

- Fans feel peak moments but **can’t interact at the exact second** it hits.
- Artists **don’t see time‑stamped feedback** (which verse/solo truly landed).
- Venues **lack creator‑economy rails** (Twitch‑style tips/perks) that work **in‑room, in real time**.
- Existing wristbands/penlights are **closed‑loop**: great visuals, but **no open data or value transfer**.

---

## Concept Overview

StageSync is a **real‑time participation layer for concerts**:

1. **Join**: Fans scan a QR/blink at the venue to mint an **Event Pass (Compressed NFT)** and receive **Reaction Credits**.
2. **Verify (optional gating)**: A **cell‑base ID check** confirms the fan is inside the venue area.
3. **React**: Fans tap a button or wave a paired penlight/wristband to **send reactions** (spending credits).
4. **Show Control**: Aggregated on‑chain reactions drive **DMX/Art‑Net** cues in real time (browser simulator for demos).
5. **Rewards**: Thresholds (e.g., 1/3/5/10 reactions) mint **event‑specific NFTs**; collections can be **redeemed for special goods**.
6. **Insights**: Artists see **second‑by‑second heatmaps** and section breakdowns; top fans receive badges automatically.

---

## Key Product Elements

- **Event Pass (Compressed NFT)**: Proof of attendance/tier; cheap to mint at venue scale.
- **Reaction Credits (fungible tokens)**: Lightweight spending unit for reactions; seeded for demos; supports fee sponsorship.
- **Reaction Logging (on‑chain)**: Minimal memo schema (`eventId`, `sectionId`, `cueId`) for verifiable, sharded logs.
- **Show Control Bridge**: A small cue server consumes logs and drives **DMX/Art‑Net**. A **browser‑based DMX simulator** is used in demos.
- **Cell‑Base Presence (optional add‑on)**: Check the **current serving base‑station ID** against the **venue area** using public tower datasets; mark the pass **Verified** if matched. (No GPS references in UX.)
- **Rewards & Collectibles**: Hitting reaction thresholds mints **event‑specific NFTs**. Fans **collect across shows** and **redeem** for limited merch or perks.
- **Tips & Auto‑Splits**: Optional tipping with automatic split routes to collaborators. (No new token required.)
- **Fee Sponsorship**: Organizers can sponsor transaction fees to keep the fan UX frictionless.

---

## Conceptual Architecture

```
[ Fan Device ] --scan QR/blink--> [ Web/App ]
      |                                 |
      |  mint Pass + Credits            |    (Compressed NFT + credits)
      |-------------------------------> [ Program / Mint ]
      |                                 |
      |  Verify Presence (cell-base)    |
      |---- Serving Cell ID ----------> [ Venue Area Match ] --(verdict only)--> [ Pass: Verified ]
      |                                 |
      |  Send Reaction (spend credit)   |
      |-------------------------------> [ On-chain Log (memo: event/section/cue) ]
                                        |
                                        v
                              [ Cue Server / Mapper ]
                                        |
                                        v
                                 [ DMX / Art-Net ]
                                        |
                                   [ Lights ]
```

> **Privacy:** We do **not** store IMSI/IMEI or raw radio data on‑chain. Only a verification result (e.g., “Verified in‑venue”) and reaction logs are written. Optional **2‑of‑3** presence (Cell | BLE | Staff QR) can be used for higher assurance.

---

## User Journeys

- **Fan (before show):** Scan → Pass + Credits → (optional) verify → ready to react.
- **Fan (during show):** Tap/wave to react → device light animates by tier → see lights respond.
- **Fan (after show):** Claim **event NFTs**, **redeem** for goods, keep a collection across events.
- **Artist/Organizer:** Watch live heatmap → trigger cues → review top fans → export moment highlights.

---

## Design Goals

- **Audience‑first**: Zero‑to‑joy in < 30 seconds for first‑time fans.
- **Portable demo**: Runs in a browser with a built‑in DMX simulator.
- **Open & composable**: On‑chain logs with a simple memo schema; small helper libraries.
- **Safe by design**: Minimal data, clear consent, and rate limiting.

### Non‑Goals (Hackathon scope)

- Network‑side carrier attestations (future exploration).  
- Full hardware distribution for penlights/wristbands (we demo with a browser sim).  
- Complex tokenomics (we use credits + existing currencies for tips).

---

## Roadmap (Concept)

- **Short‑term:** Judge Mode demo; rewards tiers; tip auto‑splits; presence gating; analytics heatmap.
- **Mid‑term:** iOS beacon kit; organizer SDK; discovery/partner integrations.
- **Long‑term:** Network‑assisted attestations; venue network roll‑outs; deeper creator‑economy features.

---

## Glossary

- **Compressed NFT (cNFT):** Low‑cost NFT suitable for large audiences.
- **Reaction Credits:** Fungible tokens used to submit reactions.
- **DMX/Art‑Net:** Lighting control protocols used by venues.
- **Cell‑Base Presence:** In‑venue verification using current **serving cell‑tower ID** vs **venue area** from public datasets.

---

## Contributing

Issues and feedback are welcome. For larger changes, please open a discussion first to align on design goals and privacy constraints.

## License

TBD

