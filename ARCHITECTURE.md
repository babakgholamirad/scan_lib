# scan_lib source layout

`scan_lib.txt` is the entry point. Grey Hack's `import_code` compiles the
separate source files into that program, so the modules must be installed at
the absolute paths used by the imports:

```text
/bin/scan_lib_modules/scan_parsing.src
/bin/scan_lib_modules/menu_input.src
/bin/scan_lib_modules/computer_result.src
/bin/scan_lib_modules/shell_result.src
```

Copy the entry source to `/bin/scan_lib` (or edit the four import paths if you
install the module folder elsewhere). Keep the module sources in the separate
`/bin/scan_lib_modules` folder so it does not conflict with the executable name,
and keep them as importable source files in CodeEditor. The modules only define
functions; the entry point owns
argument validation, the network scan, address/exploit navigation, and result
dispatch. `import_code` is compile-time inclusion, so these files do not need
to be launched separately.

## Module responsibilities

- `scan_parsing.src`: scan-output cleanup, parsing, and overflow precomputation.
- `menu_input.src`: shared selection validation and back/quit behavior.
- `computer_result.src`: handling computer objects and local passwd-file flow.
- `shell_result.src`: shell menu, remote mail/decipher workflow, uploads, and log tools.
- `scan_lib.txt`: app startup, scanning, memory-address and exploit menus, and result dispatch.

Grey Hack runtime behavior cannot be checked from the host checkout. Review the
modules' absolute paths and compile/run the entry point in CodeEditor after
installing the files.

┌───────────────────────────────┐
│ scan_lib.txt (entry)          │
│ args, scan, menus, dispatch   │
│                               ├─────┐
│                               ├─────╪─┐
│                               ├─────╪─╪─┐
│                               ├─────╪─╪─╪─┐
└───────────────────────────────┘     │ │ │ │
                                      │ │ │ │
                                      │ │ │ │
┌───────────────────────────────┐     │ │ │ │
│ scan_parsing.src              │     │ │ │ │
│ clean + parse + precompute    │     │ │ │ │
│                               ├◄────┘ │ │ │
└───────────────────────────────┘       │ │ │
                                        │ │ │
                                        │ │ │
┌───────────────────────────────┐       │ │ │
│ menu_input.src                │       │ │ │
│ select_index                  │       │ │ │
│                               ├◄──────┘ │ │
│                               ├◄────────╪─╪─┐
│                               ├◄────────╪─╪─╪─┐
└───────────────────────────────┘         │ │ │ │
                                          │ │ │ │
                                          │ │ │ │
┌───────────────────────────────┐         │ │ │ │
│ computer_result.src           │         │ │ │ │
│ handle_computer_result        │         │ │ │ │
│                               ├◄────────┘ │ │ │
│                               ├───────────╪─┘ │
└───────────────────────────────┘           │   │
                                            │   │
                                            │   │
┌───────────────────────────────┐           │   │
│ shell_result.src              │           │   │
│ handle_shell_result + helpers │           │   │
│                               ├◄──────────┘   │
│                               ├───────────────┘
└───────────────────────────────┘
