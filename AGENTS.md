# Project guide for coding agents

## What this project is

This repository contains GreyScript programs for Grey Hack, a hacking simulation. The main program, `scan_lib.txt`, connects to a target network service, inspects its remote library, discovers exploit options, lets the player choose an option, and handles the returned object. `community_exploiter.txt` is a separate, simpler example that runs an exploit specified directly as command-line arguments. `scan_lib_backup.txt` is an older snapshot of the scanner and can help explain how the current version evolved; treat `scan_lib.txt` as the active implementation.

GreyScript is the game's customized MiniScript language. Its control blocks use `if ... then ... end if`, `for ... end for`, and `while ... end while`; functions are assigned with `name = function(...) ... end function`. The project files use the `.txt` extension because they are intended to run in the game, not as ordinary Python or shell scripts.

## Main scanner flow

`scan_lib.txt` runs in this order:

1. Validate command-line `params`: IP address, port, and an optional new password. `-h` and `--help` print usage.
2. Load `metaxploit.so`, preferring `/lib/metaxploit.so` and then `current_path + "/tools/metaxploit.so"`.
3. Open a `net_session` with `metaxploit.net_use`, print target/network details, and fetch the target library with `net_session.dump_lib`.
4. Scan the library with `metaxploit.scan`. For each returned memory address, call `metaxploit.scan_address`, clean and parse its text output, and keep addresses that have parsed exploit entries.
5. While building `exploit_array`, parse each memory address and call `meta_lib.overflow` for every parsed exploit. Store the returned object and its type on the exploit map.
6. Display the discovered memory-address menu. Selecting an address displays its exploit keywords, result types, and conditions. `b` at the exploit prompt returns to the address menu; `q` exits.
7. Selecting an exploit uses its stored overflow result; it does not call `overflow` again. A `shell` opens the in-script shell menu, a `computer` is passed to `handle_computer_result`, a `file` is displayed safely, numbers are reported (`1` success, `0` failure), and unsupported types are reported. Shell-menu `b` returns to that address's exploit list.

## Important functions and data

- `clean_result(text)` removes known scan-output noise and HTML bold tags, compresses repeated blank lines, and returns an empty string for null input. If scan output changes, review this cleanup list alongside the parser.
- `parse_scan_result(text, memory, meta_lib, new_password)` turns cleaned scan output into exploit maps and precomputes each exploit's result. Each map has `keyword`, `conditions`, `result`, and `result_type`. A normal nonempty line starts an exploit; lines beginning with `* ` are attached as conditions to the current exploit. It is called once for each scanned memory address.
- `select_index(prompt, item_count, allow_back)` validates a user-entered zero-based index. It returns `-1` for `q` or null input and `-2` for `b` when `allow_back` is true. The menu loop handles `-2` by continuing to its top, which redraws the memory-address list.
- `handle_computer_result(computer)` checks for a readable, nonempty `/etc/passwd` on the returned target computer, asks before overwriting a local copy, writes it as `/home/<active_user>/receivedPaswd.txt`, and offers to launch `/bin/decipher`, remove the file, or return.
- `get_shell_home_users(shell)` lists folders under the returned shell's `/home` through its `host_computer`.
- `handle_shell_result(shell)` offers to list `/home` users, print a selected user's `/home/<user>/Config/Mail.txt` via `shell.launch("/bin/cat", mail_path)`, upload and run decipher, or remove the session's uploaded files and open the remote log tools for trace cleanup. If `/bin/LogViewer.exe` or `/bin/FileExplorer.exe` is missing remotely, it checks local `/bin` and `current_path + "/tools/"`, uploads a readable copy to `/home/guest/scan_lib_tools/`, launches it, then removes the uploaded copy. Wait two seconds between launching the two GUI apps.
- `exploit_array` is a list of maps shaped like `{"memory": address, "exploits": [...]}`. Each exploit map contains `keyword`, `conditions`, `result`, and `result_type`. `selected_memory` and `selected_exploit` are the entries chosen in the menus.

## Grey Hack runtime notes from in-game runs

- Overflow results are calculated for all parsed options while the scan menu is being prepared. This can execute exploit payloads before a player selects them. It also means the stored result is reused when selected; changing this behavior requires revisiting the precompute and menu flow together.
- A returned object with `typeof(result) == "file"` may represent a directory. Check `result.is_folder` before accessing `result.content`; directory maps can lack the `content` key and raise a runtime error.
- For the current target setup, mail is under `/home/<user>/Config/Mail.txt`. Keep the `Config` segment in menu labels and paths. Remote `shell.host_computer.File(mail_path)` often failed even when the path was usable by a command, so the working read path is `shell.launch("/bin/cat", mail_path)`.
- The decipher executable and its `crypto.so` dependency are expected at `current_path + "/tools/decipher"` and `current_path + "/tools/crypto.so"` in the game runtime. Those assets may not exist in the host repository checkout, so verify them in-game rather than assuming the checkout contains a `tools/` directory. Option 3 transfers both to a staging directory under `/home/guest/scan_lib_<user>/` and then launches the copied decipher with the target Mail.txt path. The decipher app must search for `crypto.so` both in `/lib` and in its current directory; checking only `/lib/crypto.so` produced `Error: Missing crypto library` after both files had transferred successfully.
- Follow [`docs/Manual/Shell/scp.md`](docs/Manual/Shell/scp.md) for transfer arguments: `scp(path_orig, path_dest, remoteShell, is_upload=false)`. In the documented example, `path_dest` is a destination **directory**, not a full destination filename. Passing the local file and the remote staging directory lets the source basename be retained. The manual says the result is `true` on success, an error string on transfer failure, or `null` if a shell/computer is unavailable; partial files may remain after an error. Compare success with `true` and check each transfer result independently.
- For a local-to-remote copy with `get_shell.scp`, use `is_upload=false`, matching the manual's current-shell-to-remoteShell direction. Pass the returned exploit shell as `remoteShell`.
- Follow [`docs/Manual/Shell/launch.md`](docs/Manual/Shell/launch.md) for `launch(program_path, program_parameters)`. Use the returned remote shell's `launch` method for target commands; `get_shell.launch` runs commands on the local shell.
- Grey Hack's `/bin/mkdir` in the tested environment accepts one path and does not support `-p`. The staging-directory setup uses `mkdir <path>`; if it reports that the directory already exists, uploads can continue into it.
- In-game output showed that password-change payloads require alphanumeric passwords. Treat exact payload messages as runtime behavior and preserve them in logs when diagnosing failures.

## Related files

- `community_exploiter.txt` is a separate argument-driven exploit runner. It is useful as a reference for `metaxploit.net_use`, `dump_lib`, `MetaLib.overflow`, and handling a returned shell/computer, but its behavior and assumptions differ from the scanner.
- `scan_lib_backup.txt` is a historical copy. Do not copy old behavior into the active script without checking the current implementation and the desired behavior.
- `docs/releasse notes.html` is the raw, large developer-announcement export. Read the focused summaries below first; search the HTML only when a specific release detail is needed.

## Documentation

The local field guide starts at [`docs/grey-hack-code-docs/README.md`](docs/grey-hack-code-docs/README.md). It links to official CodeDocs pages and explains their coverage and version limitations.

- [`network-security-updates.md`](docs/grey-hack-code-docs/network-security-updates.md): network topology, library-based exploits, traces, permissions, and version caveats.
- [`scripting-updates.md`](docs/grey-hack-code-docs/scripting-updates.md): GreyScript and terminal changes, API additions, path behavior, and compatibility notes.
- [`release-history.md`](docs/grey-hack-code-docs/release-history.md): condensed 2019–2026 release timeline and guidance for reading the archive.
- [`gameplay-updates.md`](docs/grey-hack-code-docs/gameplay-updates.md): missions, NPCs, companies, guilds, and related game systems.
- [`releasse notes.html`](docs/releasse%20notes.html): source announcement archive summarized by the local guides.

The README links to the official [CodeDocs home](https://codedocs.ghtools.xyz/), [data handling](https://codedocs.ghtools.xyz/data/), [language conventions](https://codedocs.ghtools.xyz/conventions/), [Grey Hack API](https://codedocs.ghtools.xyz/api/), [CodeDocs about page](https://codedocs.ghtools.xyz/about/), [CodeDocs release notes](https://codedocs.ghtools.xyz/about/release-notes/), and [MiniScript quick reference](https://codedocs.ghtools.xyz/files/MiniScript-QuickRef.pdf).

Use CodeDocs for language concepts and API reference, but verify exact signatures and current game behavior in Grey Hack's in-game Manual. CodeDocs' published release notes are old, and the local announcement summaries include nightly or preview changes that may not match the current public game version. The summaries are guides, not authoritative API specifications.

## Working in this repository

- Keep edits in GreyScript syntax and preserve the existing indentation and one-statement-per-line style.
- When changing scan parsing, menu behavior, or exploit result handling, trace the whole path from scan output through `parse_scan_result` and `exploit_array` to the menu and `overflow` result branches.
- Preserve the current distinction between quitting (`-1`) and returning to the address menu (`-2`) in `select_index` and its callers.
- Check `docs/Manual/` for the relevant in-game API page before changing `Shell.launch`, `Shell.scp`, file access, or command parameters. The in-game manual takes precedence over remembered API behavior.
- For runtime bug reports, read the current end of `logs.txt` and compare the exact failing operation with the active `scan_lib.txt`; logs may reflect a script version newer than an earlier code read.
- These scripts depend on the Grey Hack runtime and game objects. There is no local automated test harness in this repository; use a syntax/runtime check in-game when available and state clearly when behavior has only been reviewed from source.
