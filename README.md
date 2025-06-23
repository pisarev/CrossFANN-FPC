# CrossFANN-FPC

> **FANN** (Fast Artificial Neural Network Library) *runtime* wrapper for **Delphi** and **FreePascal**  
> – Windows x64 & Linux x64/arm64 – with fully **dynamic** loading at run-time.

This fork stems from *Hatsunearu FANN for Delphi* (originally in **Laex/Delphi-Artificial-Neural-Network-Library**) and has been re-engineered for modern tool-chains **and** multiple operating systems.

---

## Repository layout (since 2025-06-23)

```text
.
├── src/
│   └── delphi_hatsunearu_fann.pas   ←  the wrapper unit
├── README.md                       ←  you are here
└── tree.txt                        ←  generated file-list for reference
```

All legacy folders with pre-built DLLs/SOs, datasets, and Delphi demos have been removed.  
Grab the latest FANN binaries that match your target platform and place them next to your own executable as described below.

---

## Why this fork?

| # | Feature | Original wrapper | **CrossFANN-FPC** |
|---|---------|------------------|-------------------|
| 1 | **Compiler support** | Delphi Win32 only | Delphi ≥ XE **and** FPC 3.2+ on Windows x64 & Linux x64/arm64 |
| 2 | **Library binding** | Static `{$L fann.lib}` / implicit `fann.dll` | Pure runtime `LoadLibrary` / `dlopen` – swap **any** *libfann* build without recompiling |
| 3 | **Graceful fallback** | Missing DLL ⇒ crash | Missing DLL/SO ⇒ all function pointers = `nil` |

---

## Deploying the native FANN library

### Windows x64

```text
MyApp.exe
└── fann\
    fanndouble.dll
    fannfloat.dll
    fannfixed.dll
```

Download **`fann-2.2.0-win64.zip`** and unzip so that the `fann\` directory sits next to your application’s executable.  
No `PATH` editing required—the wrapper automatically prepends the executable directory when loading the DLLs.

### Linux x64 / arm64

```text
/path/to/myapp              (ELF)
/path/to/myapp/bin/
└── fann/
    libfloatfann.so  -> ./libfloatfann.so.2.2.0
    libdoublefann.so -> …
    libfixedfann.so  -> …
```

Extract **`fann-2.2.0-linux-<arch>.tar.xz`** beside the executable.  
Symbolic links are preserved by `tar.xz`; the wrapper calls  
`dlopen(<exe_dir>/bin/fann/...)` – no need to touch `LD_LIBRARY_PATH`.

### Windows x86

Not provided in this fork (contributions welcome).

---

## License

* Original Hatsunearu code – **LGPL 2.1**  
* All modifications in this fork – **MPL 1.1**

---

*Last updated: 2025-06-23*
