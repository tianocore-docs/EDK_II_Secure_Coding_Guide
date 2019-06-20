<!--- @file
  secure-coding-guidelines-boot-firmware.md for EDK II Secure Coding Guide

  Copyright (c) 2019, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

-->

# Secure Coding Guidelines: Boot Firmware {#secure-coding-guidelines-boot-firmware}

### Flash {#flash}

**#FLASH.1**: The platform MUST lock flash part no later than EndOfDxe.

**#FLASH.2**: The flash lock MUST happen in all boot mode (normal, S3, S4, capsule update, recovery, etc).

### Flash Update {#flash-update}

**#FLASH.UPDATE.1**: Firmware Flash Update MUST check the integrity of a new Firmware image. ([CapsuleRecovery](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Capsule_Update_and_Recovery_in_EDK_II.pdf))

**#FLASH.UPDATE.2**: Firmware Flash Update MUST check the version of a new Firmware image.

**#FLASH.UPDATE.3**: The verification process MUST happen in the trusted execution environment.

**#FLASH.UPDATE.4**: The new Firmware MUST exist in a trusted region when the verification performs.

**#FLASH.UPDATE.5**: The verification and update MUST happen in the same trusted execution environment and with no interruption.

**#FLASH.UPDATE.6**: System Firmware Update requests MUST be handled before EndOfDxe.

**#FLASH.UPDATE.7**: Device Firmware Update requests MAY be handled after EndOfDxe.

### Recovery {#recovery}

**#FLASH.RECOVERY.1**: Firmware recovery MUST check the integrity of a Firmware recovery image if it is from an external source. ([CapsuleRecovery](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Capsule_Update_and_Recovery_in_EDK_II.pdf))

**#FLASH.RECOVERY.2**: Firmware recovery MUST check the version of a Firmware recovery image if it is from an external source.

### Variable {#variable}

**#VARIABLE.1**: A platform MUST lock the variable before EndOfDxe if it is critical, such as memory configuration, TPM Physical Presence (PP) flag. NOTE: This locked variable can still be updated in SMM. ([Variable](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_UEFI_Authenticated_Variables_in_SMM_with_EDKII_V2.pdf))

**#VARIABLE.2**: A platform MUST use the same lock policy in a normal boot and S4.

**#VARIABLE.3**: A platform MAY define the variable property (attribute, max size, min size). This variable property can be a list defined by the platform.

**#VARIABLE.4**: The return status for variable access MUST be verified.

**#VARIABLE.SET.1**: A platform MUST use error handling on variable set if the variable NOT locked, such as OUT_OF_RESOURCE, or attribute mismatch.

**#VARIABLE.SET.2**: A platform MUST provide a way to handle variable out of resource. Such as clean unknown variable.

**#VARIABLE.GET.1**: A platform MUST use error handling variable get if the variable is NOT locked. Such as NOT_FOUND, or unexpected value.

**#VARIABLE.GET.2**: A platform MUST not assume to get the correct variable content/size if the variable is NOT locked.

**#VARIABLE.ATTRIB.1**: A platform MUST NOT set variable RT attribute unless it is needed.

**#VARIABLE.ATTRIB.2**: A platform MUST NOT set variable NV attribute unless it is needed.

**#VARIABLE.CHECK.1**: A platform MUST enable Human Interface Infrastructure (HII) variable check.

**#VARIABLE.CHECK.2**: A platform MUST enable Platform Configuration Database (PCD) variable check.

**#VARIABLE.CHECK.3**: A platform MUST enable UEFI variable check.

**#VARIABLE.QUOTA.1**: A platform MUST define a reasonable variable quota.

**#VARIABLE.CONFIDENTIALITY.1**: Current variable driver does not provide confidentiality support. If the variable confidentiality is needed, the caller MUST encrypt it and decrypt it.

**#VARIABLE.CONFIDENTIALITY.2**: The encryption and decryption MUST be in a secure execution environment, such as SMM.

### S3 {#s3}

**#S3.1**: S3 BootScript MUST be saved in a secure place (lockbox) ([S3Resume](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_S3_resume_with_EDKII_V2.pdf))

**#S3.2**: S3 BootScript image dispatch and parameter MUST be saved in a secure place (lockbox).

**#S3.3**: S3 CPU data MUST be saved in a secure place (SMM).

**#S3.4**: S3 configuration data (memory, chipset) MUST be saved in a secure place (ReadOnly variable, SMM).

### Secure Boot {#secure-boot}

**#SECUREBOOT.1**: Platform MUST NOT provide a way to disable secure boot without authentication.

**#SECUREBOOT.2**: Platform MUST verify all images in the secure boot path. The bypass of any image verification is NOT ALLOWED.

**#SECUREBOOT.3**: If a firmware update is supported, the new firmware image must be signed.

**#SECUREBOOT.4**: If a firmware recovery is supported, the recovery firmware image must be signed. The recovery firmware image is from an external source.

**#SECUREBOOT.5**: The verification MUST happen in all boot path (normal, S3, S4, capsule update, recovery, etc).

**#SECUREBOOT.UEFI.1**: UEFI secure boot MUST be used to verify the 3<sup>rd</sup> part image, such as PCI Option ROM, or OS loader.

**#SECUREBOOT.UEFI.2**: If UEFI secure boot is used, any 3<sup>rd</sup> part image MUST be verified.

**#SECUREBOOT.UEFI.3**: If UEFI secure boot is used, a platform MUST implement the PlatformSecureLib to provide a secure platform-specific method to detect a physically present user.

**#SECUREBOOT.Key.1**: If signing verification is required, the public key or hash MUST be stored in hardware, or boot block or UEFI authenticated variable.

### TCG {#tcg}

**#TCG.1**: If TCG trusted boot is enabled, a platform MUST do measurement following the TCG specification. ([TPM2 EDK II](https://firmware.intel.com/sites/default/files/resources/A_Tour_Beyond_BIOS_Implementing_TPM2_Support_in_EDKII.pdf))

**#TCG.2**: All parent Firmware Volumes (FV) MUST be reported and measured. The child FV MAY NOT be measured.

**#TCG.3**: If an image is not in a FV, it MUST be measured. The image inside of a FV MAY NOT be measured.

**#TCG.4**: Any FV MUST be measured, including external FV from firmware update capsule, or recovery.

**#TCG.5**: The platform MUST link Tcg2MeasurementLib to be the last NULL instance for SecurityStub.

**#TCG.SMBIOS.1**: The platform MUST make sure the measured SMBIOS record is the same cross boot. (If the record might be different, it MUST NOT be measured)

**#TCG.MOR.1**: Memory Override (MOR) request MUST be handled by the platform/Memory Reference Code (MRC).

**#TCG.MOR.2**: Storage MOR request MUST be handled by platform BDS before EndOfDxe.

**#TCG.MOR.3**: If the MOR variable is not got, the platform MUST treat it as MOR requested.

**#TCG.MOR.4**: Secure MOR MUST be used for the platform. ([SecureMOR](https://docs.microsoft.com/en-us/windows-hardware/drivers/bringup/device-guard-requirements))

**#TCG.PP.1**: TCG TPM Physical Presence (PP) request MUST be handled before EndOfDxe.

**#TCG.PP.2**: TCG storage PP request MUST be handled before EndOfDxe.

**#TCG.PP.3**: TCG TPM PP flag MUST be locked in normal boot and S4.

**#TCG.PP.4**: TCG storage PP flag MUST be locked in normal boot and S4.

**#TCG.TPM.1.** A Platform MUST generate random TPM2 PlatformAuth and discard it in normal boot.

**#TCG.TPM.2**: A Platform MUST generate random TPM2 PlatformAuth and discard it in S3 if device error in S3.

**#TCG.TPM.3**: A platform MAY disable TPM if the TPM device returns an error.

**#TCG.TPM.4**: A platform MUST handle TPM device error in both normal boot and S3.

**#TCG.TPM.5**: If S3 Startup(STATE) fails, the platform MUST send Startup(Clear) and extend error code to PCRs.

### Option ROM {#option-rom}

**#OROM.1**: Any 3<sup>rd</sup> party option ROM MUST NOT be dispatched before EndOfDxe. The 3<sup>rd</sup> party option ROM means a PCI option ROM on the 3<sup>rd</sup> party PCI card. If a PCI option ROM is integrated inside of the firmware, it is NOT considered as a 3<sup>rd</sup> party option ROM and it MAY be dispatched before EndOfDxe.

**#OROM.2**: Platform BDS MUST handle the deferred PCI option ROM after EndOfDxe.

### Console {#console}

**#CONSOLE.1**: A trusted console SHOULD be available before EndOfDxe, based upon the need. A trusted console means: 1) Integrated device such as a PS2/USB keyboard/mouse without any option ROM, 2) A chipset-integrated video card which is welded to the board and whose driver is inside of the boot firmware instead of in a PCI option ROM, 3) A 3<sup>rd</sup> party video card which is welded to the board and whose driver is inside of the boot firmware instead of in a PCI Option ROM.

**#CONSOLE.2**: The trusted console MAY support features, such as TCG Physical Presence, hard drive Password or TCG OPAL password.

**#CONSOLE.3**: If a remote console is used, additional authentication MAY be used, such as user password.

### Storage {#storage}

**#STORAGE.1**: A platform MUST connect trusted storage device before EndOfDxe, based upon the need. A trusted storage means:

1.  Integrated device, such as a Universal Serial Bus (USB), Advanced Technology Attachment (ATA), AT Attachment Packet Interface (ATAPI), Non-Volatile Memory express (NVMe), Universal Flash Storage  (UFS), Embedded MultiMedia Card (eMMC), Secure Digital (SD) Card, without any option ROM,
2.  A chipset-integrated storage card, such as Redundant Arrays of Independent Drives (RAID), which is welded to the board and whose driver is inside of the boot firmware instead of in a PCI Option ROM,
3.  A 3rd party storage card, such as Small Computer System Interface (SCSI), Fiber Channel (FC), which is welded to the board and whose driver is inside of the boot firmware instead of in a PCI Option ROM.

**#STORAGE.2**: A platform MUST send TPer Reset to storage device if there is a MOR request.

**#STORAGE.3**: A platform MUST let user input hard drive password or TCG OPAL password to unlock the hard drive if the hard drive is locked.

**#STORAGE.4**: A platform MUST disable the DMA on the storage if it is not a boot device. (Disconnect Device)

### Silicon {#silicon}

**#SILICON.1**: The lockable silicon register MUST be locked before EndOfDxe, include SMRAM, Flash, Top Swap, Remap Bar, etc

**#SILICON.2**: The lockable silicon register MUST be locked in all booth path including S3, S4, Capsule, Recovery, etc.