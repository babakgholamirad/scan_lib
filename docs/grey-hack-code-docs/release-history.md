# Developer Release Notes: 2019–2026

This timeline summarizes the developer announcements in [`docs/releasse notes.html`](../releasse%20notes.html). The export contains 382 announcement cards dated August 6, 2019 through November 16 (year omitted on the newest card); it includes public releases, nightly/experimental updates, previews, and general news. It is a thematic guide, not a transcript of every bug fix.

## Milestones

- **2019 — scripting foundation (37 cards):** Update v0.7.2590a introduced player-written GreyScript programs and a rebuilt library-based exploit system. Programs and commands progressively moved from hard-coded behavior to scripts that players could inspect and modify.
- **2020 — world and LAN redesign (85 cards):** World generation expanded across the usable IPv4 range. Local networks gained multiple routers, switches, and hubs; network devices became exploitable targets, and scripting gained device/network methods. Firewalls and player-rented network development followed in the nightly cycle.
- **2021 — multiplayer networks and exploration (57 cards):** v0.7.3590a brought configurable rented networks, firewalls, sniffers, reverse shells, CCTV, and router scanning. v0.7.4120a added hidden missions and lore, clue-bearing file types, richer email, player repositories, and further scripting support.
- **2022 — economy and language updates (57 cards):** v0.8.4458a replaced the game network layer and introduced an economy iteration. Cryptocurrency is simulated in-game; it is not real cryptocurrency. MiniScript 1.5.1 and `get_custom_object` later changed the scripting environment and program-to-program data sharing.
- **2023 — server-side script controls and player missions (40 cards):** v0.8.4981a reworked world/database/script management, added multiplayer CPU and RAM limits, and introduced player-created Capture the Flag missions.
- **2024 — major-feature previews (28 cards):** nightly previews developed zero-day exploit research, richer NPC routines, and player influence on companies. Treat preview announcements as development history, not proof a feature was already in the public branch.
- **2025 — Beta and deeper simulation (44 cards):** v0.9.5603 moved the game to Beta and expanded NPC schedules, banking traces, company ownership, smart devices, and zero-day research. v0.9.6087 migrated Bash and terminal behavior into GreyScript, revised path rules and traces, and added file encryption, DDoS, and rentable Superadmins.
- **2026 — procedural missions and guild/company systems (34 cards):** v0.9.6724 expanded the tutorial and procedural missions and added `poll_input`. Later updates improved permissions and mission puzzles. v0.9.7374 overhauled guild progression, company management, investigations, and desktop window management; the notes describe it as effectively version 1.0 pending a stabilization period.

## Reading the newest entries

The newest card is Update 0.9.7392, posted Monday, November 16, with no year printed in the exported card. The preceding public-branch major update is v0.9.7374, posted November 12. The developer describes the latter as a stabilization step before officially moving to version 1.0; do not treat the notes as confirmation that 1.0 has already been released.

For current scripting signatures and mechanics, use the in-game Manual and the linked CodeDocs source pages. Release notes often announce an API or behavior without specifying its complete signature, and nightly changes may be revised before merging.
