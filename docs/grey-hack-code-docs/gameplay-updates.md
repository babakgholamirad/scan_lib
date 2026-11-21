# Missions, Guilds, and Economy Updates

This guide summarizes persistent gameplay systems described in the developer-announcement archive. Exact rewards, eligibility, and balancing can change; check the current in-game Manual and program interfaces.

## Missions and investigation

- Direct Hackshop missions remain the shorter, structured option. Police-station jobs, karma/reputation missions, and hidden missions broaden the ways to progress and affect outcomes.
- Hidden missions use clues that may appear in emails, logs, web pages, images, chat logs, PDFs, and other files. Some require visiting several networks. Depending on the situation, outcomes can include reporting a crime or choosing an illicit resolution; those choices can affect karma and rewards.
- Procedural missions require gathering clues across networks and devices. The 2026 notes list fraud, sabotage, corporate espionage, and ransomware at Hackshops, plus police investigations such as extortion, identity theft, evidence fabrication, and access sales. Mission puzzles may involve permissions, encryption, timestamps, or scripting.
- v0.8.4981a (October 2023) added player-created Capture the Flag missions. A creator rents a server whose network becomes the mission template; creators and players who solve missions can earn money.

## NPCs and companies

- The 2025 Beta update expanded NPC schedules and interactions. Work/leisure patterns, CCTV, traffic cameras, employee records, smartphones, and NPC-to-NPC email can provide situational clues. NPC employment and performance can affect company results.
- NPCs may report suspicious bank activity, triggering bank traces. Unusual deposits as well as theft can draw attention; financial actions should not be assumed to be untraceable.
- In the stock/company system, players can buy shares in eligible companies. The release notes state that ownership above 50% gives control and access to management and employee-performance information. Dividends and company outcomes depend on in-game business performance; this is a simulation, not real-world investment advice.
- Player-run software/hardware shops were added alongside NPC companies. The notes describe configuring software sales through `/server/conf/httpd.conf` and hardware sales through a warehouse.
- Company tools include `ConfigCompany.exe` for inspecting/managing company networks and `HiringManager.exe` for reviewing and hiring staff. Available actions depend on ownership and permissions.

## Guild progression (2026)

- Guilds now have private channels, membership applications, role management, and a treasury. Members can keep their mission reward while the guild earns additional experience based on the member's mission XP; the v0.9.7374 notes specify a 15% guild XP share.
- Guild levels unlock purchasable perks, including expanded membership/roles, more company investments, hardware discounts, and mission XP boosts. Leaving or losing members can impose progression penalties.
- The leaderboard ranks guilds based on company ownership and performance. DDoS incidents and company-admin loss can cause temporary or conditional score penalties.
- Holding first place for 15 in-game days grants the crown. While held, the guild can purchase CrownShield for an eligible company network or the guild leader's rented server; the notes describe protection against exploits, DDoS, and social engineering while the guild retains the crown.

## Economy and version context

The 2022 economy update introduced an in-game blockchain/cryptocurrency simulation and related programs; coins have no real-world value. Later company-share mechanics connect player purchases, employee performance, company rankings, and dividends. These rules were actively redesigned in later updates, so treat old guides and Nightly notes as historical unless confirmed in the current build.
