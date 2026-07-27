# Unattended-Win11-Debloat

## Introduction

Unattended-Win11-Debloat leverages Microsoft's [Answer Files](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/update-windows-settings-and-scripts-create-your-own-answer-file-sxs?view=windows-11) (or Unattend files) to automate and customize Windows installations. It allows uninstallation of Windows Apps and Features and changes to Windows Settings during the Windows setup process.

### Why Use an Answer File?

- Provides transparency by allowing inspection of all changes in the answer file.
- Runs directly on official Windows ISOs from Microsoft, eliminating the need for unofficial sources.
- Utilizes a Microsoft-supported feature designed for streamlined mass deployment of Windows installations.
- Enables automated configuration across multiple devices, saving time and effort by eliminating repetitive manual setups. 

</br>

> [!NOTE]
> Unattended-Win11-Debloat has been tested and optimized for personal use. For those unsatisfied or interested in customizing further, consider creating your own answer file using: </br> - [Winhance Unattend Generator](https://github.com/memstechtips/Winhance) following [this video guide](https://youtu.be/lrq3ph3xi50). </br> - [Schneegans Unattend Generator](https://schneegans.de/windows/unattend-generator/) following [this video guide](https://youtu.be/WyLiJl-NQU8).

## Requirements

- Windows 10 or Windows 11  
  - *(Tested on Windows 10 22H2 & Windows 11 23H2, 24H2 and 25H2)*
  - *(32-bit, 64-bit and arm64 is supported)*

## What Does Unattended-Win11-Debloat Do?

The Unattended-Win11-Debloat answer file comes with detailed descriptions for nearly all configurations and registry tweaks, which are available for inspection here on GitHub. For customization, download the answer file and open it in editors like [Cursor](https://www.cursor.com/) or [VSCode](https://code.visualstudio.com/).

### Key Features

- Ability to choose Windows Edition (Unless Windows setup detects key in UEFI BIOS)
- Bypasses Windows 11 system requirements
- Skips forced Microsoft account creation during Windows setup
- Removes all preinstalled bloatware apps except Calculator, Camera, Clock, Media Player, Notepad, Paint, Photos, Sticky Notes and Snipping Tool.
  - Copilot, OneDrive and Edge are removed along with all other UWP apps (Downloading a browser is recommended).
  - Recall is disabled.
- Applies the following Optimizations:
  - Privacy & Security (Disables telemetry and ads)
  - Power Settings (Imports and applies the Winhance Power Plan for better performance)
  - Gaming & Performance (Applies settings and visual effects to improve performance, sets unneeded services to manual, disables unneeded scheduled tasks)
  - Windows Updates (Disables auto updates and configures Windows Update to notify of available security updates only)
  - Notifications (Disables all notifications except if related to privacy and security)
  - Sound (Disables startup sound during boot)
- Applies the following Customizations:
  - Windows Theme (Sets Dark Mode by default, enables transparency effects)
  - Taskbar (Hides task view and widget icons, aligns to the left on Windows 11)
  - Start Menu (Enables list view, Disables Bing search results)
  - Explorer (Applies Classic Context Menu, shows file extensions, hides Home and Gallery folders in Navigation Pane and much more)

> [!TIP]
> Use [Winhance](https://winhance.net/) once Windows is installed to install software, re-apply or revert settings and manage your Windows apps and settings.

## Usage Instructions

To use an answer file, include `autounattend.xml` at the root of your Windows Installation Media to be executed during Windows setup.

> [!IMPORTANT]  
> Ensure the answer file is named `autounattend.xml`; otherwise, it won’t be recognized by the installer.

---

### Using Memory's WIMUtil in Winhance (Recommended)

To use **WIMUtil**, follow these steps:

1. Download and install Winhance from [Winhance.net](https://winhance.net/) or [GitHub](https://github.com/memstechtips/Winhance/releases/latest).

2. Launch Winhance, click on the "Advanced Tools" navigation button (bottom left) and select WIMUtil.

Once launched, **WIMUtil** guides you through a wizard:

1. **Select or Download Windows ISO**
2. **Add `autounattend.xml` or create your own with Winhance**
3. **Extract and Add Current Device Drivers to Installation Media (Optional)**
4. **Create New ISO with Customizations Included**

Once the ISO file is created:

1. **Create a Bootable USB Flash Drive with [Ventoy](https://github.com/ventoy/Ventoy)**
2. **Copy the New ISO File to the Ventoy Flash Drive**
3. **Boot from the USB flash drive, choose your ISO & Install Windows**

For more info, check out the full [video guide](https://youtu.be/lrq3ph3xi50?t=3477).

---

## FAQ

### Can this answer file be used for an in-place upgrade?

- No, in-place upgrades do not support answer files.

### Why is Windows still updating automatically?

- Feature updates are delayed for a year; however, security and driver updates continue as usual.

### Why don't I have internet after installing Windows?

<details>
  <summary>Click to Show Instructions</summary>
  </br>
  If you’re unable to connect to the internet after installation, it’s likely because your Wi-Fi or LAN (Ethernet) drivers are missing. Windows sometimes doesn’t include all necessary drivers for network adapters, especially if they’re specific to your device.

  To resolve this, follow these steps:

  1. **Download your network driver** from the manufacturer’s website on another computer with internet access. Look for Wi-Fi or LAN drivers specific to your device model.
  2. **Transfer the driver** to your Windows installation via USB drive.
  3. **Install the driver** on your Windows system and restart if necessary.

  After installation, you should be able to connect to the internet.

  > [!TIP] </br>
  > You can use WIMUtil in [Winhance](https://winhance.net/) to extract and add the drivers from your current operating system to the Windows installation media. These drivers should then be installed automatically during the Windows installation process, preventing any internet connection issues.

</details>
