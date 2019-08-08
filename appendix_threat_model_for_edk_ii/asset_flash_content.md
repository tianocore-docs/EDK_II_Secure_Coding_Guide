<!--- @file
  asset_flash_content.md for appendix_threat_model_for_edk_ii for EDK II Secure Coding Guide

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

## Asset: Flash Content {#asset-flash-content}

NIST [SP 800-147](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-147.pdf) and [SP 800-147B](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-147B.pdf) provide system firmware protection guidelines, including the detailed information on system firmware protection and update. NIST [SP 800-193](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-193.pdf) provides platform firmware resiliency guidelines. It extends protection to 3 principles: protection, detection, and recovery. It also enlarges the scope from system firmware (BIOS) to all the firmware on the platform.

The flash content here includes both firmware code (such as PEI, DXE, SMM etc) and firmware data (such as UEFI variables, Microcode, etc).

| Threat | Example |
| --- | --- |
| Spoofing | N/A |
| Tampering | If the firmware is not protected or locked, the attacker might modify the firmware directly.<BR>If the firmware update process is not authenticated, the attacker might send a malicious firmware update image for update. |
| Repudiation | N/A |
| Information Disclosure | If the system software stores the secret in the firmware, the attacker may read the firmware content and get the secret. |
| Denial of Service | If the attacker can modify the firmware content (code or data) and cause the firmware crash, the system might no longer boot. It becomes a permanent denial of service. |
| Elevation of Privilege | If the attacker can modify the firmware content (code or data) and store a Trojan in firmware, the Trojan may hide itself and gain the higher privilege. |

| Adversary | Example |
| --- | --- |
| Network Attacker | If the network is enabled before SMM lock and flash lock, the attacker may send mal-formed network packets. |
| Unprivileged Software Attacker | The attacker may trigger a firmware update, or write the UEFI variable. |
| System Software Attacker | The attacker may access a silicon register to unlock the flash access register.<BR>The attacker may create a race condition to break the flash write protection or flash update authentication. |
| Simple Hardware Attacker | The attacker may press the power button during flash update or recovery, or set a jumper to modify the system boot mode from normal boot to recovery or even manufacturing mode.<BR>The attacker may attach PCI Leach to perform DMA attack during flash update or recovery.<BR>The attacker may hijack the SPI bus to read or write to the chip data. |
| Skilled Hardware Attacker | N/A |

| Mitigation | Example |
| --- | --- |
| Protection | For the code region, the flash write protection must always be applied. During the flash update, the new firmware image must be authenticated and the version must be checked to prevent a rollback attack. In order to mitigate Time-of-check/Time-of-use (TOC/TOU) attacks, the new image must be copied to a secure environment before the check. The DMA protection must be enabled during flash update.<BR>For the data region, the UEFI authenticated variable write must happen in an isolated execution environment. The authenticated variable data must be authenticated and the rollback protection must be applied. Just as in code region protection, in order to mitigate TOC/TOU attack, new variable content must be copied to a secure environment before the check and DMA protection must be applied to this environment. In addition, the secret must not be saved to the firmware code or data region. |
| Detection | The detection happens in the next boot.<BR>For the code region, the industry may have different solutions to make sure the initial boot code is unmodified, such as Project Cerberus, Intel® Boot Guard, etc.<BR>For the data region, the UEFI variable driver needs to detect if the variable region is modified without using UEFI variable services. |
| Recovery | If something wrong is detected, the entity which detects the failure needs to start the recovery process, and the recovery data must be in a known good and secure configuration and be delivered from a trusted and always available source. |
