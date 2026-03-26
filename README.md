# EFI_Hackintosh

A complete OpenCore EFI configuration for running macOS on AMD Ryzen-based systems, specifically optimized for the Ryzen 5 2600 platform.

## 📋 System Configuration

| Component | Specification |
|-----------|---------------|
| **Processor** | AMD Ryzen 5 2600 |
| **Motherboard** | Gigabyte B450M S2H |
| **Graphics Card** | AMD RX 570 (Sapphire Pulse) |
| **RAM** | 8GB DDR4 2666MHz |

## 🍎 macOS Compatibility

### ✅ Supported Versions
- macOS Ventura (13.x)
- macOS Sonoma (14.x)
- macOS Sequoia (15.x)
- macOS Tahoe (23.4)

### ⚠️ Known Issues
The following features are **not working**:
- AirDrop
- Sidecar

## 📁 EFI Structure Overview

#### ACPI Patches (`/OC/ACPI/`)
System Definition Table modifications for proper hardware recognition:
- `SSDT-EC.aml` - Embedded Controller (EC) definition for Gigabyte board
- `SSDT-PLUG.aml` - CPU power management plugin initialization
- `SSDT-USB-Reset.aml` - USB controller reset handling
- `SSDT-USBX.aml` - Extended USB power support

#### Kexts (`/OC/Kexts/`)
Kernel extensions providing hardware support and system patches:

**Core System**
- `Lilu.kext` - Base library and patching engine (required for others)
- `VirtualSMC.kext` - Emulates Apple's System Management Controller (SMC)

**Graphics/GPU**
- `WhateverGreen.kext` - GPU support, VRAM patching, and fixes for AMD (Radeon), Nvidia, and Intel GPUs
- `SMCRadeonSensors.kext` - Temperature and sensor monitoring for AMD Radeon GPUs

**Audio**
- `AppleALC.kext` - Audio codec emulation and support for Realtek/other chipsets

**Networking**
- `RealtekRTL8111.kext` - Support for Realtek RTL8111 family Ethernet controllers

**Storage**
- `CtlnaAHCIPort.kext` - SATA/AHCI controller enumeration (SATA SSD support)
- `NVMeFix.kext` - NVMe SSD support and compatibility fixes
- `HibernationFixup.kext` - Hibernate/sleep mode support

**USB**
- `USBToolBox.kext` - Advanced USB port mapping and power management
- `UTBMap.kext` - USB port map configuration for USBToolBox

**Security/System**
- `AMFIPass.kext` - Bypasses Apple Firmware Interface (AFI) for SMBIOS compatibility
- `RestrictEvents.kext` - Event restriction and bridging patches
- `AppleMCEReporterDisabler.kext` - Disables MCE (Machine Check Exception) error reporting

## 🚀 Usage Instructions

### Before Installation

> **⚠️ IMPORTANT**: If you intend to use this EFI configuration, you **MUST** update the SMBIOS values in `config.plist` to avoid conflicts and ensure proper macOS system identification. The current SMBIOS will not work on your system.

1. Backup your current EFI partition
2. Update SMBIOS information specific to your hardware:
   - SystemProductName
   - SystemSerialNumber
   - MLB (Main Logic Board)
   - ROM

3. Adjust BIOS settings for AMD Ryzen compatibility (disable CSM, disable secure boot, disable 4G Above decoding)

### Installation Steps

1. Copy the entire `/efi/` folder to your EFI partition
2. Update SMBIOS in `config.plist`
3. Configure boot order to prioritize the EFI partition
4. Restart and select OpenCore from the boot menu


## 📝 License

This EFI configuration is provided as-is for personal use and educational purposes.
