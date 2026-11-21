# Scripting and Terminal Updates

This reference records scripting-related changes called out in the developer archive. It supplements the older [CodeDocs pages](README.md#source-pages); it does not provide full API signatures. Check the in-game Manual or CodeEditor help for exact parameters and return values.

## Core model

- Since v0.7.2590a (October 2019), players can write GreyScript tools and exploits, and many built-in programs expose source code that can be studied or modified.
- Commands migrated into the scripting system over subsequent releases. By v0.9.6087 (August 2025), Bash itself loads as `/bin/bash`, including on a remote computer when a terminal is started there. This allows a replacement Bash script to integrate with terminal history, completion, and visual programs.
- v0.9.6087 also corrected inconsistent `program_path` and `launch_path` behavior. Recheck scripts that relied on earlier path results.

## Notable API changes

| Release | Change recorded in the notes |
| --- | --- |
| v0.7.3351a (2020) | Renamed `computer_ports` to `device_ports` and `computers_lan_ip` to `devices_lan_ip`. Added network/device methods including `connect_ethernet`, `network_gateway`, `active_net_card`, `ping`, `connect_wifi`, and `clear_screen`; `wait` was re-enabled. |
| v0.7.4120a (2021) | Added `import_code` for compile-time inclusion of source from a path. The notes warn that its argument must be a complete path, not a variable. Added email scripting and player-repository APIs. |
| v0.7.4120a (2021) | Added a `Service` object obtained by importing service libraries with `include_lib`, including `libssh.so`, `libftp.so`, `libchat.so`, `libhttp.so`, `librshell.so`, and `librepository.so`. Service installers and start/stop binaries moved to scripts. |
| v0.8.4490a (2022) | Updated the underlying MiniScript version to 1.5.1 and added `get_custom_object` for sharing a map with programs launched through `shell.launch`. Older scripts may need compatibility adjustments. |
| v0.8.4981a (2023) | Multiplayer introduced server-enforced CPU and RAM limits for player scripts. The notes recommend yielding in tight loops (for example, `wait(0.1)`) when work need not run continuously; they describe an approximate 512 MB RAM limit at that time. |
| v0.9.5603 (2025) | Added scripting objects `debugLibrary`, `smartAppliance`, and `TrafficNet`; methods `metalib.payload`, `metalib.debug_tools`, `file.symlink`, and `file.is_symlink`; and libraries including `libsmartappliance.so` and `libtrafficnet.so`. |
| v0.9.6087 (2025) | Added `get_abs_path` to resolve relative paths. Script methods that accept paths now consistently require absolute paths; terminal commands can use `.` and `./` for the current directory. |
| v0.9.6087 (2025) | Added `crypto.encrypt`, `crypto.decrypt`, and `crypto.is_encrypted` for password-protected files. Encrypted files/programs cannot be read, modified, or executed until handled appropriately. |
| v0.9.6087 (2025) | Added `net_session.flood_connection` for the in-game DDoS mechanic. Its impact depends on multiple networks/terminals and can reboot a target for 10 in-game minutes. |
| v0.9.6724 (2026) | Added non-blocking `poll_input`, and extended `get_abs_path` to recognize `~` as the active user's home directory. |
| v0.9.6974 nightly (2026) | `MetaMail.read` and `MetaMail.delete` were changed to accept lists of mail IDs for batch operations; later public notes also mention batch email support. Confirm exact current signatures in the Manual. |

## Compatibility and resource notes

- File-path behavior changed substantially with the Bash migration. Convert relative paths with `get_abs_path` before passing them to path-taking GreyScript methods; do not assume an API accepts the terminal's current-directory shorthand.
- The Bash script is loaded from the machine where the terminal starts. A remote terminal may therefore run that remote machine's `/bin/bash`, not the local one.
- Multiplayer script resource limits are enforced server-side. Add waits to polling loops and avoid unnecessary allocations; limits and scheduling details may change between versions.
- Release announcements sometimes say that additional GreyScript functions or batch operations were added without naming every method. Do not infer unspecified API names from these summaries.
