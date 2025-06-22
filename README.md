# CrossFANN-FPC

> Cross-platform **FANN** (Fast Artificial Neural Network Library) wrapper for **Delphi** and **FreePascal**  
> – Windows x64 & Linux x64/arm64 – with fully **dynamic** runtime loading.

This fork is based on *Hatsunearu FANN for Delphi* (originally in Laex/Delphi-Artificial-Neural-Network-Library) and has been re-engineered for modern tool-chains and multiple OSes.

---

## Key differences from the original

| # | Feature | Original wrapper | **CrossFANN-FPC** |
|---|---------|------------------|-------------------|
| 1 | **Compiler support** | Delphi Win32 only | Delphi ≥ XE **and** FPC 3.2+ on Windows x64 & Linux x64/arm64 |
| 2 | **Library binding** | Static `{$L fann.lib}` / implicit `fann.dll` | Pure runtime `LoadLibrary` / `dlopen` – swap any libfann build without recompiling |
| 3 | **Graceful fallback** | Missing DLL ⇒ crash | Missing DLL/SO ⇒ function pointers = `nil` |

---

## Library placement & packaging

| Platform | Archive asset | Where files must end up |
|----------|---------------|-------------------------|
| **Windows x64** | `fann-2.2.0-win64.zip` | Unzip so your tree becomes<br>```
MyApp.exe
└── fann\
    fanndouble.dll
    fannfloat.dll
    fannfixed.dll
``` |
| **Linux x64** | `fann-2.2.0-linux-x86_64.tar.xz` | Extract next to the executable:<br>```
/path/to/myapp              (ELF)
└── bin/
    └── fann/
        libfloatfann.so -> ./libfloatfann.so.2.2.0
        libdoublefann.so -> …
        libfixedfann.so  -> …
```<br>Symbolic links are preserved by `tar.xz`; the wrapper calls `dlopen(<exe_dir>/bin/fann/...)`. |
| *Windows x86* | — | not provided in this fork |

No environment variables (`PATH` / `LD_LIBRARY_PATH`) are required: the wrapper prepends the executable directory automatically.

## License

* Original Hatsunearu code – **LGPL 2.1**.  
* All modifications in this fork – **MPL 1.1**.

---

_Last updated: 2025-06-22_
