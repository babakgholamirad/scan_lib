# Grey Hack GreyScript Field Guide

This is an original, condensed study guide to the Grey Hack CodeDocs site, supplemented with developer release-note summaries from the local archive. The CodeDocs site documents GreyScript as a customized MiniScript language integrated with Grey Hack's in-game commands; its own release notes stop in 2019, so the local guides below capture later changes.

## Local update guides

- [Release history, 2019–2026](release-history.md): dated milestones and coverage notes from the supplied developer announcements.
- [Scripting and terminal changes](scripting-updates.md): API additions, compatibility notes, path rules, and the Bash migration.
- [Networks and security systems](network-security-updates.md): LANs, rented networks, exploits, traces, and defensive systems.
- [Missions, guilds, and economy](gameplay-updates.md): mission systems, NPC behavior, companies, multiplayer progression, and guilds.

These are summaries, not replacements for current in-game documentation. The archive includes nightly and preview announcements as well as public releases; check the branch and version before relying on a feature.

## Source pages

- [Welcome and getting started](https://codedocs.ghtools.xyz/)
- [Data handling](https://codedocs.ghtools.xyz/data/)
- [Language conventions](https://codedocs.ghtools.xyz/conventions/)
- [Grey Hack API](https://codedocs.ghtools.xyz/api/)
- [About CodeDocs](https://codedocs.ghtools.xyz/about/)
- [Release notes](https://codedocs.ghtools.xyz/about/release-notes/)
- [MiniScript quick reference PDF](https://codedocs.ghtools.xyz/files/MiniScript-QuickRef.pdf)

## GreyScript essentials

- Assign functions to variables, for example `greet = function(name) ... end function`.
- Use `if ... then ... end if`, `for ... end for`, and `while ... end while` blocks. Curly braces are not used for blocks.
- Use double quotes for strings. The conventions page says single-quoted strings and the `++` increment operator are unsupported.
- Parentheses are used for function calls and grouping, but generally are not wrapped around `if` or `while` conditions.
- Prefer one statement per line. Semicolons can separate statements, but the guide discourages that style.
- GreyScript has strings, numbers, lists, and maps, with built-in operations and methods. Indexing and slices are used with collections and strings; check the data page for type-specific behavior and examples.
- The conventions guide covers case sensitivity, comments, whitespace, variable scope (`globals` and `locals`), classes/objects, truth values, and control flow including `break` and `continue`.

## API map

The API page documents the global `params` list, system functions, and game objects. System functions include output, timing, type inspection, hashing, network lookups, path and user information, input, library inclusion, bitwise operations, and program exit. The object reference includes Router, Computer, File, Port, Shell, FtpShell, Crypto, MetaLib, Metaxploit, and NetSession.

Use the API page for exact signatures, return values, and in-game restrictions; object methods often depend on game state and permissions.

## Data handling map

- **Strings:** concatenation, repetition, indexing and slicing; methods include searching, splitting, replacing, trimming, case conversion, and length/value conversion.
- **Numbers:** arithmetic and comparisons, with helpers for rounding, ranges, random values, signs, roots, trigonometry, and conversion.
- **Lists:** ordered collections with indexing, slicing, searching, insertion/removal, joining, sorting, reversing, and aggregation helpers.
- **Maps:** keyed collections with key/value lookup, insertion, removal, and collection inspection methods.

## Version context

The CodeDocs site's latest listed release is CodeDocs v1.5, dated October 20, 2019. The supplied developer-announcement archive extends beyond that; its latest card is Update 0.9.7392, posted November 16 (the year is omitted in that card). Treat both the old site and these summaries as references rather than guarantees: verify signatures, permissions, and branch-specific behavior in the current in-game Manual or a test script.
