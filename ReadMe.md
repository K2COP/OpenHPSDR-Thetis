# Thetis HL2 NNR

**mi0bot's Thetis for the Hermes Lite 2, with WDSP Neural Noise Reduction (NNR) added.**

Latest release: **v2.10.3.15-nnr1** — based on mi0bot's Thetis HL2 **v2.10.3.15** (final release, 4 September 2026).

➡️ **[Download from the Releases page](../../releases/latest)**

- **Installer (recommended):** `Thetis-NNR-HL2-v2.10.3.15-x64.msi`
- **Portable zip (try it without installing):** `Thetis-NNR-HL2-v2.10.3.15-x64.zip`. See [Try it without installing](#try-it-without-installing-portable-zip).

---

## Why this exists

NNR is the neural-network noise reduction that Warren Pratt (NR0V) added to WDSP, the DSP library at the heart of Thetis. If you have heard it, you know: it pulls voices and CW out of the noise in a way the older noise reductions can't, and the band goes *quiet*.

The Hermes Lite 2 version of Thetis is maintained by Reid (MI0BOT), and he is taking a well-earned break. The official Thetis by Richie (MW0LGE) doesn't support the HL2 properly. NNR was too good to wait for, so I (K2COP) added it to Reid's Thetis myself and am sharing it here for any HL2 owner who wants it now.

This is **not** an official release by Reid or Richie. It is Reid's v2.10.3.15 with NNR added and nothing else changed. When Reid is back and releases his own version, that should take priority over this one.

## What's added

- **NNR (Neural Noise Reduction)** from official TAPR WDSP 2.11, built from source into `wdsp.dll`, with all four of Warren's models:

  | Model | For | Notes |
  |---|---|---|
  | **Voice – Standard** | SSB, AM, FM, digital | Lighter on the CPU |
  | **Voice – Premium** | SSB, AM, FM, digital | Larger network, best results, more CPU |
  | **CW – Standard** | CWL / CWU | Lighter on the CPU |
  | **CW – Premium** | CWL / CWU | Larger network, more CPU |

- **The model follows the mode automatically:** the CW model in CWL/CWU, and the Voice model in every other mode. You only choose Standard or Premium for each.
- An **NNR** entry in the DSP menu, on the front-panel **NR** button, and a **Setup → DSP → NNR** tab.
- **CAT:** NNR can be turned on with the existing `ZZNE` (RX1) / `ZZNF` (RX2) commands. CAT only uses numbers, so NNR's code is `ZZNE5;` / `ZZNF5;` (`0` = off, `1`–`4` = NR1–NR4).
- **CAT, Standard/Premium:** `ZZNI` (RX1) / `ZZNJ` (RX2). `ZZNI1;` = Premium, `ZZNI0;` = Standard, `ZZNI;` reads it back. It changes the model for the current mode (the CW model in CWL/CWU, the Voice model in other modes), the same as picking it on the Setup NNR tab.
- **MIDI (Midi2Cat):** "Noise Reduction NNR On Off" and "Rx2 Noise Reduction NNR On Off", plus "NNR Standard/Premium" and "Rx2 NNR Standard/Premium" toggles.
- **TCI:** TCI clients are told when NNR is on. TCI has no name for NNR, so it is sent as the next noise-reduction number after NR4.
- The title bar reads **"HL2 NNR (MI0BOT + K2COP)"**, so you can always tell which Thetis is running.

Everything else (HL2 support, PureSignal, the Database Manager, TCI, skins and the rest) is exactly as in Reid's v2.10.3.15.

## ⚠️ Back up your database first — and keep doing it

Thetis keeps all your settings in a database. Before installing, and regularly after that:

1. In Thetis, open **Database Manager** from the menu bar.
2. Click **Take backup now**.
3. While you're there, turn on **Backup On Start-Up** and/or **Backup On Shut-Down** for your database, so a backup is taken automatically every time.

Backups live in `%APPDATA%\OpenHPSDR\Thetis-x64\DB\` and can be restored from the same Database Manager window. **Always** take a backup before installing a new Thetis build, this one or anyone else's.

## Installing

1. Download `Thetis-NNR-HL2-v2.10.3.15-x64.msi` from the [Releases page](../../releases/latest).
2. Double-click it. Windows SmartScreen will warn you because the installer isn't code-signed: click **More info → Run anyway**.
3. Follow the installer. It needs Windows 10/11 64-bit with .NET Framework 4.8, which Windows already includes. The Visual C++ runtime is **included** in the installer, so there's nothing else to install.

**It installs alongside your other Thetis installs, and won't replace them.** It goes into `C:\Program Files\OpenHPSDR\Thetis-HL2-NNR`, separate from Reid's Thetis-HL2 and the official Thetis. You can keep all of them and switch between them.

The installer makes two shortcuts (on the desktop and in Start → OpenHPSDR → Thetis-NNR), just like Reid's installer:

| Shortcut | Use it for | Database |
|---|---|---|
| **Thetis-NNR-HL2** | Your Hermes Lite 2 — **this is the one you want** | `-dbid:NNR` |
| **Thetis-NNR** | ANAN radios | `-dbid:NNR-ANAN` |

Both open the same program with separate databases, so the HL2 and ANAN settings never mix. Both use databases separate from Reid's and the official Thetis, so neither of those ever sees NNR settings.

To uninstall, go to **Settings → Apps → Thetis HL2 NNR**. Your databases are kept.

## Try it without installing (portable zip)

If you'd rather not run an installer, download `Thetis-NNR-HL2-v2.10.3.15-x64.zip` instead. It's the same program as the MSI, just not installed. Full steps are in `README-FIRST.txt` inside the zip. In short:

1. **Back up your database** in your current Thetis (see above).
2. **Unblock the zip before extracting it:** right-click the zip → **Properties** → tick **Unblock** (if shown) → OK. Otherwise Windows may block the DLLs.
3. **Extract it to a new folder**, e.g. `C:\Thetis-NNR-HL2`. Don't extract over an existing Thetis.
4. **Install the Microsoft VC++ x64 runtime** from [aka.ms/vs/17/release/vc_redist.x64.exe](https://aka.ms/vs/17/release/vc_redist.x64.exe), unless mi0bot's or the official Thetis installer has been run on this PC before. Without it, Thetis stops at startup with a `channelmaster.dll` error.
5. **Make a shortcut:** right-click `Thetis.exe` → **Send to → Desktop (create shortcut)**. In the shortcut's **Properties → Target**, add ` -dbid:NNR` after the closing quote:
   ```
   "C:\Thetis-NNR-HL2\Thetis-NNR-HL2-v2.10.3.15\Thetis.exe" -dbid:NNR
   ```
   This is the same database the installer's **Thetis-NNR-HL2** shortcut uses, so your settings carry over if you install the MSI later. For an ANAN radio, use `-dbid:NNR-ANAN`.
6. **Allow the Windows Firewall prompt** on first run (at least Private networks). Thetis needs it to find the HL2. The installer adds these rules itself; the zip can't.

To remove it, delete the folder and the shortcut.

## Bringing over your existing settings

On first run, Thetis-NNR-HL2 starts with a blank database. To copy your existing HL2 setup instead of setting everything up again:

1. **In your normal HL2 Thetis:** open **Database Manager**, highlight your active database, and click **Duplicate the database**. Then close that Thetis.
2. **In Thetis-NNR-HL2:** open **Database Manager**. The copy now appears under **Available Databases**. Highlight it, click **Make the database active**, and restart Thetis if it asks.

Your original database is left untouched and stays with your normal Thetis. Keep one database for each Thetis build, and don't point your old Thetis at the NNR copy.

(Alternative: **Export the selected database** in your normal Thetis, then **Import into the active database** in Thetis-NNR-HL2.)

## Turning NNR on

Any of these work:

- **NR button:** press it repeatedly. It steps NR → NR2 → NR3 → NR4 → **NNR** → off. Stop when it reads **NNR**.
- **DSP menu:** choose **NNR** (for RX1 or RX2).
- **CAT:** send `ZZNE5;` (RX1) or `ZZNF5;` (RX2). This is NNR's CAT code.

That's it. The Voice or CW model is picked for you from the mode.

### Standard or Premium, and the mask floor

Open the settings by **right-clicking the NR button while it shows NNR**, or go to **Setup → DSP → NNR** (the last tab). Each receiver has:

- **Voice model:** Standard or Premium.
- **CW model:** Standard or Premium.
- **Mask floor** (−50 to −10 dB, default −25): how far NNR is allowed to push the noise down. Lower (e.g. −40) means deeper suppression but can sound more processed. Higher (e.g. −15) means a more natural sound with a little more noise left in.

Start with **Premium**. If the audio crackles or the CPU is struggling, switch to **Standard**.

## Good to know

- **CPU:** NNR is a neural network and uses much more CPU than NR1–NR4. Premium uses the most. Using NNR on both RX1 and RX2 doubles the load.
- **One noise reduction at a time:** NNR replaces NR1–NR4, the same way they replace each other.
- **In SSB, CW and digital modes,** NNR takes over the front of the receive chain (Warren's design in WDSP 2.11). While it's on, the **RX EQ** and **SNB** are bypassed. They come back as soon as you turn NNR off. In AM and FM, NNR runs after the demodulator instead.
- **TCI clients** don't know about NNR yet. Some apps may show it as a plain NR on/off, or not at all.
- **ANAN radios:** the ANAN code from Reid's build is unchanged and the Thetis-NNR shortcut is there for it, but NNR has only been tested on air with a **Hermes Lite 2**.
- **Support:** please **don't** contact Reid or Richie about NNR in this build. They didn't make it. Open an [issue here](../../issues) instead.

## Building from source

The NNR work is on the [`nnr-hl2`](../../tree/nnr-hl2) branch. Every push is built by GitHub Actions (`.github/workflows/build-nnr.yml`) with Visual Studio's MSBuild and WiX v3, producing both the MSI and a plain zip of the program folder.

To build it yourself, open `Project Files/Source/Thetis_VS2026.sln` in Visual Studio 2026 and build **Release | x64**. The installer project is `Project Files/Source/Thetis-Installer` (WiX Toolset v3).

NNR code changes:

- `Project Files/Source/wdsp/` — Warren's NNR files from TAPR WDSP 2.11 (`nnr.*`, `nnet.*`, `nnio.*`, `nnrbypass.*`, `nnr_model_0..3.c`), merged into Reid's WDSP alongside his NR3/NR4.
- `Project Files/Source/Console/` — `radio.cs`, `dsp.cs`, `console.cs`, `setup.cs`, CAT, TCI and Midi2Cat wiring.

## Credits

- **Warren Pratt, NR0V** — WDSP, and the NNR algorithm and models ([TAPR/OpenHPSDR-wdsp](https://github.com/TAPR/OpenHPSDR-wdsp)).
- **Reid, MI0BOT** — Thetis for the Hermes Lite 2 ([mi0bot/OpenHPSDR-Thetis](https://github.com/mi0bot/OpenHPSDR-Thetis)), on which this is built.
- **Richie Samphire, MW0LGE**, and the Thetis/PowerSDR developers before him (Doug Wigley W5WC, FlexRadio Systems and others) — Thetis ([ramdor/Thetis](https://github.com/ramdor/Thetis)).
- The deskHPSDR (DL1BZ) and piHPSDR NNR integrations were used as references.
- NNR integration into Thetis HL2: **K2COP**.

## License

Thetis and WDSP are free software under the **GNU General Public License v2** (see [LICENSE](LICENSE)). This build is a modified version of mi0bot's Thetis, distributed under the same license, and its full source is in this repository. The dual-licensing statement in [LICENSE-DUAL-LICENSING](LICENSE-DUAL-LICENSING) applies only to Richie Samphire's own code.

**No warranty.** Use at your own risk. Back up your database, and check your power output after installing any new Thetis build.

---

*Reid's original release notes for v2.10.3.15 follow.*

# 2.10.3.15 (2026-09-04)

- Upgraded to release 2.10.3.15 of official Thetis
- Corrected timeout of auto tune routine
- Updated alternate RX selection form
