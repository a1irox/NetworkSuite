# Network Priority Manager

A small, lightweight Windows tool that lets you decide which network adapter (Wi‑Fi, Ethernet, USB modem, mobile hotspot, etc.) the operating system uses as the default internet route — through a simple drag-and-drop GUI, with no need to manually edit network settings in Control Panel or PowerShell.

## What problem does this solve?

When multiple network adapters are active at the same time (e.g. Wi‑Fi and Ethernet together, or a VPN), Windows decides which one takes priority based on a value called the **Interface Metric**. Windows calculates this value automatically, and it's often not what you actually want (for example, you want Ethernet to be the priority, but Windows keeps favoring Wi‑Fi). There's also no built-in GUI way to change this value manually — it normally requires PowerShell/netsh commands.

This app does that job with a few clicks and a drag-and-drop.

## Features

- **Live adapter list**: every physical network adapter is shown with its current status (connected / disconnected / disabled) and its current Metric. Status refreshes automatically every few seconds.
- **Drag and drop reordering**: drag rows to reorder them; the higher a row sits, the higher its priority.
- **One-click Apply**: clicking Apply sets Interface Metric values in stepped order (10, 20, 30, …) based on the order you arranged, and also disables Windows' Automatic Metric — otherwise Windows recalculates and silently overwrites the metric after a while, undoing the priority you just set.
- **Restore previous settings**: before any change, the original values are backed up automatically; you can revert everything back to how it was before you ever used the app, with one click.
- **New adapter notifications**: when a new network adapter is connected (e.g. a USB dongle), the app notifies you so you can place it in the priority order if you want.
- **Minimize to tray**: the app can keep running in the background from the System Tray without taking up taskbar space.
- **Bilingual (English / Persian)**: the whole UI switches between English and Persian with one button, including full right-to-left (RTL) support for Persian.
- **Built-in Help and About**: a Help section and an About dialog are included in the app itself.

## How it works (technical)

- The app is written in **PowerShell + WPF**; the GUI is defined in XAML and loaded directly inside the script itself (no separate file).
- Reading and changing adapter state is done through native Windows cmdlets like `Get-NetAdapter` and `Set-NetIPInterface` — no drivers or third-party tools are installed.
- Since changing the Interface Metric requires administrator rights, the app self-elevates via a UAC prompt as soon as it starts.
- Settings (adapter order and the backup of original values) are stored as JSON files under `%APPDATA%\NetworkSuite\`, not in the registry.
- To run without a console window, a separate exe launcher (`NetworkSuite.exe`) starts PowerShell in the background, hidden.

## Installation & Usage

1. Put all release files (`NetworkSuite.exe`, `NetworkSuite.ps1`, `icon.ico`) in the same folder — these three files must always stay together.
2. Double-click `NetworkSuite.exe`.
3. Accept the UAC (administrator) prompt — without this permission the app can't change network priority.
4. If Windows Defender/SmartScreen shows an "unrecognized app" warning (since the file isn't code-signed), click **More info → Run anyway**.

If the app doesn't open or you run into an issue, run `NetworkSuite_Debug.bat`; it keeps a console window open so you can see the exact error text. A full error log is always saved here as well:
`%TEMP%\NetworkSuite_error.log`

## Requirements

- Windows 8 / Server 2012 or newer (due to the dependency on the `NetAdapter` module)
- Administrator access

## File structure

| File | Role |
|---|---|
| `NetworkSuite.exe` | Main launcher — run this |
| `NetworkSuite.ps1` | The app's full logic and GUI |
| `icon.ico` | App icon (window, taskbar, tray) |
| `NetworkSuite_Debug.bat` | Troubleshooting run with a visible console |

## Credits

Made by A1iRoX with the help of AI.
