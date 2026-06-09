# Ultimate Gaming Windows 11 Setup

A no-nonsense guide to squeezing every frame and millisecond out of Windows 11 for gaming. No fluff — just what to do, why it matters, and in what order.

> **Not very tech savvy?** Chris Titus Tech's Windows Utility automates a large portion of this guide — debloat, tweaks, and app installs in one place. Run it in PowerShell as Administrator:
> ```powershell
> irm christitus.com/win | iex
> ```
> If you're comfortable doing things manually, follow this guide for full control.

---

## Table of Contents

1. [Before You Start](#before-you-start)
2. [Windows Updates](#windows-updates)
3. [Uninstall Bloatware](#uninstall-bloatware)
4. [Required Apps](#required-apps)
5. [Power Plan](#power-plan)
6. [GPU Drivers](#gpu-drivers)
7. [Display Settings](#display-settings)
8. [Network Optimizations](#network-optimizations)
9. [Audio](#audio)
10. [Storage](#storage)
11. [Mouse Settings](#mouse-settings)
12. [Registry Tweaks](#registry-tweaks)
13. [Advanced Tweaks](#advanced-tweaks)
14. [Summary: Order of Operations](#summary-order-of-operations)

---

## Before You Start

- **Back up your data.**
- **Create a restore point:** Start → search "Create a restore point" → Create.
- **Run everything as Administrator** unless stated otherwise.
- Do these steps in order. Some depend on others.

---

## Windows Updates

Do this first. Running tweaks on an outdated OS is a waste of time.

1. `Settings > Windows Update > Check for updates`
2. Install everything, including optional driver updates
3. Reboot

**Why:** Driver updates, security patches, and DirectStorage/DirectX improvements ship through Windows Update. You want the latest foundation before touching anything else.

---

## Uninstall Bloatware

### Microsoft Preinstalled Apps

`Settings > Apps > Installed apps` — uninstall every app listed below that you find:

| App | Reason |
|-----|--------|
| Clipchamp | Useless video editor |
| Copilot | Background resource usage, not useful for gaming |
| Cortana | Dead product, still runs in background |
| Family Safety | Parental controls you don't need |
| Feedback Hub | Telemetry front-end |
| Get Help | Useless support app |
| Get Started | One-time setup app that never dies |
| Media Player | Replaced by VLC |
| Microsoft 365 (Office) | Subscription nag — install proper Office if needed |
| Microsoft News | Background data fetching |
| Microsoft Teams (personal) | Preinstalled — safe to remove, not the work version |
| Microsoft To Do | Unnecessary |
| Movies & TV | Replaced by VLC |
| MSN Weather / News / Sports | All fetch data in background |
| OneDrive | Disable or uninstall if you don't use cloud sync |
| Outlook (new) | Preinstalled mail client |
| Solitaire & Casual Games | Ad-supported games on a paid OS |
| Sticky Notes | Minor, but unnecessary |
| Xbox App | Keep only if you use Xbox Game Pass |
| Xbox Game Bar | Disable if not using it for clips (see Display section) |

> **OneDrive:** To fully uninstall: `Settings > Apps > Installed apps > Microsoft OneDrive > Uninstall`. To just disable startup: Task Manager → Startup apps → OneDrive → Disable.

### Manufacturer Bloatware

Remove anything from this list that matches your hardware manufacturer.

**Dell:**
- Dell SupportAssist (resource hog — replace with manual driver checks)
- Dell Update
- Dell Digital Delivery
- Dell Core Services
- McAfee / Norton (preinstalled antivirus trials — use Windows Defender instead)

**HP:**
- HP Support Assistant
- HP Sure Connect
- HP Audio Switch
- HP JumpStart
- McAfee / Norton trials

**ASUS:**
- McAfee Security
- ASUS Live Update (use MyASUS or manual updates instead)
- ASUS Splendid (optional to keep)
- ExpressVPN trial

**Lenovo:**
- Lenovo Vantage (keep only if you need driver updates — less bloated than others)
- Lenovo Now
- Lenovo Smart Appearance
- McAfee / Norton trials

**MSI:**
- MSI App Player (Android emulator — remove unless you use it)
- Nahimic (audio software — known to cause frame stutters, uninstall)
- McAfee trials

**Acer:**
- Acer Care Center
- Acer Collection
- McAfee / Norton trials

> **Note on antivirus:** Windows Defender is genuinely good now. You don't need a third-party AV running full-time. Malwarebytes (installed later) covers on-demand scanning.

### GPU Software Bloat

**NVIDIA:**
- Uninstall GeForce Experience if you don't use ShadowPlay or automatic driver notifications. NVIDIA App is the lighter replacement — still optional.

**AMD:**
- Adrenalin is required for driver management. Keep it.
- Uninstall AMD link/streaming components if you don't use them.

---

## Required Apps

Two options — use the script or install manually.

### Option A: Automated (Recommended)

An `install-apps.ps1` script is included in this repo. It installs all required apps via winget with a single command. It does **not** touch your registry or system settings — apps only.

1. Right-click `install-apps.ps1` → **Run with PowerShell**
   Or open PowerShell as Administrator and run:
   ```powershell
   Set-ExecutionPolicy Bypass -Scope Process -Force
   .\install-apps.ps1
   ```
2. Follow the on-screen prompts (browser choice, confirmation)
3. Done — install WinToys from the Microsoft Store manually after (not available on winget)

> **winget not working?** Open the Microsoft Store, search **App Installer**, and update it. Then retry.

### Option B: Manual (winget)

Open PowerShell as Administrator and run the commands below.

```powershell
# Browser (pick one)
winget install Mozilla.Firefox
# winget install Hibbiki.Chromium      # Ungoogled Chromium

# Uninstall Edge (if no option in Settings)
winget uninstall Microsoft.Edge

# Utilities
winget install 7zip.7zip
winget install Microsoft.PowerToys
winget install VideoLAN.VLC
winget install Notepad++.Notepad++
winget install GeekUninstaller.GeekUninstaller
winget install voidtools.Everything

# Gaming
winget install Valve.Steam
winget install Discord.Discord
winget install MSI.Afterburner
winget install Guru3D.RTSS

# Monitoring
winget install CPUID.CPU-Z
winget install TechPowerUp.GPU-Z
winget install REALiX.HWiNFO
winget install CrystalDewWorld.CrystalDiskInfo

# Security
winget install Malwarebytes.Malwarebytes
```

Then install **WinToys** from the Microsoft Store manually.

### App Notes

**RivaTuner + MSI Afterburner:** These work together. Afterburner handles GPU clocks, voltage, and fan curves. RTSS handles the overlay and frame rate limiting. Cap frames 2-3 below your refresh rate (e.g. 141fps on 144Hz) with FreeSync/G-Sync enabled for smooth, tear-free gameplay with low latency.

**Geek Uninstaller:** Use this instead of `Settings > Apps` for anything you want fully removed. It catches registry leftovers and AppData junk that the built-in uninstaller misses.

**Everything (voidtools):** Indexes your entire drive in seconds. Replaces Windows Search. After install, disable Windows Search indexing (covered in the Storage section).

**WinToys:** A clean GUI for Windows settings and tweaks otherwise buried in menus or PowerShell. Install from the Microsoft Store — not on winget.

**Malwarebytes:** Run a full scan after setup. You can leave real-time protection off if you're using Windows Defender — no need for two real-time scanners competing.

---

## Power Plan

### Enable Ultimate Performance Plan

Open PowerShell as Administrator:

```powershell
powercfg -duplicatescheme e9a42b02-d5df-448d-aa00-03f14749eb61
```

Then: `Control Panel > Power Options` → select **Ultimate Performance**

**Why:** The Balanced plan throttles your CPU to save power. Ultimate Performance keeps clocks consistently high, reducing frame time variance.

### Additional Power Settings

`Control Panel > Power Options > Change plan settings > Change advanced power settings`

| Setting | Value |
|---------|-------|
| Hard disk > Turn off hard disk after | Never |
| Sleep > Sleep after | Never |
| USB settings > USB selective suspend | Disabled |
| PCI Express > Link State Power Management | Off |
| Processor power management > Minimum processor state | 100% |
| Processor power management > Maximum processor state | 100% |

---

## GPU Drivers

### Clean Driver Install

Always do a clean install. Leftover driver files cause stutters and crashes.

1. Download **DDU (Display Driver Uninstaller)** from [guru3d.com](https://www.guru3d.com/files-details/display-driver-uninstaller-download.html)
2. Boot into Safe Mode: `Settings > System > Recovery > Advanced startup > Restart now > Troubleshoot > Advanced options > Startup Settings > Restart > press 4`
3. Run DDU → **Clean and restart**

### NVIDIA

1. Download the latest **Game Ready Driver** from [nvidia.com/drivers](https://www.nvidia.com/drivers)
2. Run installer → **Custom** → check **Clean installation**

**NVIDIA Control Panel settings:**

| Setting | Value |
|---------|-------|
| Power management mode | Prefer maximum performance |
| Texture filtering - Quality | High performance |
| Vertical sync | Off |
| Low Latency Mode | Ultra (disable if using DLSS Frame Generation) |
| Shader Cache Size | Unlimited |
| Threaded Optimization | On |
| Maximum Pre-Rendered Frames | 1 |

### AMD

1. Download latest **Adrenalin driver** from [amd.com/support](https://www.amd.com/support)
2. Run installer → check **Factory Reset**

**AMD Adrenalin settings:**

| Setting | Value |
|---------|-------|
| Radeon Anti-Lag | Enabled |
| Radeon Chill | Disabled |
| Enhanced Sync | Disabled |
| FreeSync | Enabled (if monitor supports it) |
| Texture Filtering Quality | Performance |

---

## Display Settings

### Resolution & Refresh Rate

`Settings > System > Display > Advanced display`
- Native resolution, maximum refresh rate

If your monitor supports 144Hz+ but shows 60Hz: check your cable. Use DisplayPort for high refresh rates — HDMI 2.0 caps at 144Hz at 1080p, HDMI 2.1 handles higher.

### Enable FreeSync / G-Sync

- **NVIDIA G-Sync:** NVIDIA Control Panel → Display → Set up G-Sync → enable
- **AMD FreeSync:** AMD Adrenalin → Display tab → FreeSync → enable

### Hardware-Accelerated GPU Scheduling (HAGS)

`Settings > System > Display > Graphics > Change default graphics settings`
- Hardware-Accelerated GPU Scheduling: **On**

> Only for RTX 30 series / RX 6000 series or newer. Older GPUs may regress.

### Xbox Game Bar

`Settings > Gaming > Xbox Game Bar` → **Off** (unless you use it for clips)

### Game Mode

`Settings > Gaming > Game Mode` → **On**

**Why:** Prioritizes CPU and GPU resources toward the active game process.

### Disable Full-Screen Optimizations (Per-game)

Right-click your game `.exe` → Properties → Compatibility → check **Disable fullscreen optimizations**

Forces true exclusive fullscreen, reducing input lag vs. borderless window.

### Variable Refresh Rate

`Settings > System > Display > Graphics > Change default graphics settings`
- Variable refresh rate: **On**

---

## Network Optimizations

### Use a Wired Connection

Ethernet over Wi-Fi, always. If you're on Wi-Fi and experiencing packet loss or high ping variance, no software tweak will fix it.

### DNS

`Settings > Network & Internet > [your connection] > DNS server assignment > Manual`

| Provider | Primary | Secondary |
|----------|---------|-----------|
| Cloudflare (recommended) | `1.1.1.1` | `1.0.0.1` |
| Google | `8.8.8.8` | `8.8.4.4` |

### Disable Nagle's Algorithm

Open `regedit` (`Win + R` → `regedit`):

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces
```

Find the subkey matching your active network adapter (look for your IP address). Create two new **DWORD (32-bit)** values:

| Name | Value |
|------|-------|
| `TcpAckFrequency` | `1` |
| `TCPNoDelay` | `1` |

Reboot after.

### Network Adapter Advanced Settings

`Device Manager > Network Adapters > [your adapter] > Properties > Advanced`

| Setting | Value |
|---------|-------|
| Interrupt Moderation | Disabled |
| Energy Efficient Ethernet | Disabled |
| Green Ethernet / Power Saving Mode | Disabled |
| Receive Buffers | Maximum available |
| Transmit Buffers | Maximum available |
| Flow Control | Disabled |
| Large Send Offload v2 (IPv4/IPv6) | Disabled |

---

## Audio

### Disable Audio Enhancements

`Control Panel > Sound > [your output device] > Properties > Enhancements`
- Check **Disable all enhancements**

`Control Panel > Sound > [your output device] > Properties > Advanced`
- Check **Allow applications to take exclusive control of this device**
- Check **Give exclusive mode applications priority**

### Uninstall Nahimic / Sonic Studio / DTS (if present)

These manufacturer audio suites run background services with real overhead. Nahimic in particular (common on MSI/ASUS) is known to cause frame stutters. Uninstall it.

---

## Storage

### Enable TRIM (SSDs)

```cmd
fsutil behavior query DisableDeleteNotify
```

If result is `1`, TRIM is disabled. Fix it:

```cmd
fsutil behavior set DisableDeleteNotify 0
```

### Disable Search Indexing on Game Drives

1. File Explorer → right-click drive → Properties
2. Uncheck **Allow files on this drive to have contents indexed**
3. Apply to all subfolders

### Disable Hibernate

```cmd
powercfg -h off
```

### Check Drive Health

Open **CrystalDiskInfo** after install. Any drive showing **Caution** or **Bad** needs replacing before anything else.

---

## Mouse Settings

### Disable Mouse Acceleration

`Settings > Bluetooth & devices > Mouse > Additional mouse settings > Pointer Options`
- **Uncheck Enhance pointer precision**

**Why:** Mouse acceleration makes cursor movement inconsistent — distance traveled depends on speed, not physical movement. In FPS games this destroys muscle memory. Turn it off.

### Enable Raw Input In-Game

In every FPS or competitive game, find the mouse/input settings and enable **Raw Input** if available. This bypasses Windows input processing entirely.

### Polling Rate

If your mouse supports 1000Hz+ polling rate, enable it in the mouse software. Higher polling rate = more frequent position updates = lower input latency.

---

## Registry Tweaks

> **Before touching the registry:** Create a restore point. Back up the specific key you're editing via File → Export before changing anything.

Open Registry Editor: `Win + R` → `regedit`

### GPU Priority

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games
```

| Name | Type | Value |
|------|------|-------|
| `GPU Priority` | DWORD | `8` |
| `Priority` | DWORD | `6` |
| `Scheduling Category` | String | `High` |
| `SFIO Priority` | String | `High` |

### Disable GameDVR / Fullscreen Optimizations

```
HKEY_CURRENT_USER\System\GameConfigStore
```

| Name | Type | Value |
|------|------|-------|
| `GameDVR_Enabled` | DWORD | `0` |
| `GameDVR_FSEBehaviorMode` | DWORD | `2` |
| `GameDVR_HonorUserFSEBehaviorMode` | DWORD | `1` |
| `GameDVR_DXGIHonorFSEWindowsCompatible` | DWORD | `1` |

```
HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\GameDVR
```

Create this key if it doesn't exist, then add:

| Name | Type | Value |
|------|------|-------|
| `AllowGameDVR` | DWORD | `0` |

### Multimedia Class Scheduler (System Responsiveness)

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile
```

| Name | Type | Value |
|------|------|-------|
| `NetworkThrottlingIndex` | DWORD | `ffffffff` (hex) |
| `SystemResponsiveness` | DWORD | `0` |

### Disable Auto-Tuning (Network)

Open Command Prompt as Administrator:

```cmd
netsh int tcp set global autotuninglevel=disabled
```

To revert: `netsh int tcp set global autotuninglevel=normal`

### Disable Spectre/Meltdown Mitigations (Advanced)

> **Warning:** These are CPU security patches. Disabling them is a real security risk. Only do this on a dedicated gaming machine that doesn't handle sensitive data or work. You have been warned.

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management
```

| Name | Type | Value |
|------|------|-------|
| `FeatureSettingsOverride` | DWORD | `3` |
| `FeatureSettingsOverrideMask` | DWORD | `3` |

To revert, delete both values.

---

## Advanced Tweaks

### MSI Mode for GPU

Message Signaled Interrupts reduce GPU interrupt latency.

1. Download **MSI Utility v3**
2. Find your GPU in the list
3. Enable MSI mode
4. Reboot

### Timer Resolution

Windows defaults to a 15.6ms system timer. Reducing it improves frame time consistency.

Download **TimerResolution** from lucashale.com → set to `0.5ms`.

> Windows 11 22H2+ manages timer resolution per-process automatically for some games. Test before relying on this.

### Process Priority

Task Manager → Details tab → right-click game process → Set Priority → **High**

Do **not** set Realtime. It starves system processes and causes instability.

### Disable Core Parking

Download **ParkControl** (free, Bitsum) → disable CPU Core Parking for AC power.

### Disable HPET

On some systems this improves frame time consistency. On others it regresses. Test it.

```cmd
bcdedit /deletevalue useplatformclock
bcdedit /set disabledynamictick yes
```

To revert:
```cmd
bcdedit /set useplatformclock true
bcdedit /set disabledynamictick no
```

### Intel Hybrid CPU (12th gen+)

On P-core + E-core CPUs, Windows sometimes schedules game threads on E-cores. If your game process isn't staying on P-cores (check Task Manager), use **Process Lasso** to pin it.

### Strip Windows Visual Effects

`Settings > System > About > Advanced system settings > Performance > Settings`
→ **Adjust for best performance**

Or manually uncheck everything except:
- Smooth edges of screen fonts
- Show thumbnails instead of icons

---

## Summary: Order of Operations

| Priority | Step |
|----------|------|
| 1 | Windows Update |
| 2 | Uninstall bloatware (Microsoft + manufacturer) |
| 3 | Install required apps (script or manual) |
| 4 | Power Plan → Ultimate Performance |
| 5 | GPU Driver (DDU clean install) |
| 6 | Display → refresh rate, G-Sync/FreeSync, HAGS, Game Mode |
| 7 | Network → DNS, Nagle's off, adapter settings |
| 8 | Mouse → disable acceleration, enable raw input |
| 9 | Audio → enhancements off, exclusive mode on |
| 10 | Storage → TRIM, indexing off, drive health check |
| 11 | Registry tweaks |
| 12 | Advanced tweaks (optional, test individually) |

---

## Contributing

PRs welcome. Keep entries accurate, manually reproducible, and sourced. No black-box script dependencies in the main guide.

---

## License

MIT
