# Network and Security System Updates

This is a version-aware overview of network and defensive mechanics introduced or revised in the supplied developer announcements. For exact command syntax, exploit behavior, and current restrictions, use the in-game Manual.

## Network topology

- v0.7.2864a (January 2020) reworked world generation and made the usable IPv4 space explorable, excluding reserved addresses.
- v0.7.3351a (July 2020) replaced the simple router-and-computers LAN with networks that can contain multiple routers, switches, and hubs. Some machines can sit behind additional devices, so fewer externally visible ports do not necessarily mean there are no internal services.
- Routers and switches became exploit targets as well as network infrastructure. Router access can expose connection logs and provide ways to update router libraries. `ScanLan` is intended to run from a device on the LAN to inspect its topology; `scanrouter` inspects router/kernel and firewall information from outside.
- Rented networks expanded beyond a single server. `ConfigLan.exe` manages devices and firewalls and can restore or back up a rented network, helping recover from configuration mistakes or compromise.

## Attacks and defenses

- v0.7.3590a (January 2021) introduced player-relevant sniffers, reverse shells, CCTV, and configurable router firewalls. Sniffers can capture credentials; SSH/FTP encryption changes what is captured, and the notes advise understanding the in-game encryption scripts rather than assuming the default scheme is strong.
- The exploit system depends on libraries and versions installed on a target. Updates can reveal vulnerabilities in older library versions, so exploit availability is version-specific. Later releases added a collaborative zero-day research path, described as especially relevant to multiplayer PvP.
- Superadmins can intercept overflow attacks and force guest-level permissions. Rented-network Superadmins also defend against DDoS; the 2025 notes distinguish them from NPC-network admins, including how tracing behavior differs.
- v0.9.6087 rewrote active/passive trace behavior and added bank-trace reporting. The notes recommend checking `AdminMonitor.exe` for active traces and reviewing strike details for active, passive, or banking traces. Earlier releases also revised trace aggressiveness and strike warnings, so use the current Manual rather than relying on old trace assumptions.
- The same 2025 release added password-based file encryption and `net_session.flood_connection`. These mechanics are game systems; exact availability and effects may depend on version, network, and multiplayer context.

## Permissions and connectivity

- The 2026 permission overhaul aims to behave more like Unix. Folder listing and access to files within a folder are distinct; file and folder operations may skip entries the current user cannot access and report that result.
- A later network simulation checks whether each computer in a connection chain still has internet access before network commands run. A broken intermediate network can prevent commands from continuing through a remote machine.
- Current releases add more context-sensitive recovery and social-engineering behaviors. For example, a DDoS-suspicion message can cause an administrator restoration under the conditions specified by the game, potentially undoing network changes. It can also affect a guild company's leaderboard score for a limited in-game duration.

## Version caution

Several features first appeared in nightly or experimental notes and may have changed before public release. Refer to the release-history timeline and verify the current branch/version before treating a listed behavior as current.
