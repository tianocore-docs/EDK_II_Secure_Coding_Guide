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

## Asset: Boot Flow {#asset-boot-flow}

The main system firmware work is to initialize the silicon and then transfer control to an operating system. Because the firmware is almost the first component running on the system, another responsibility of the system firmware is to maintain the secure boot chain (defined in UEFI specification) and the trusted boot chain (defined by TCG).

Here the secure boot chain means that the first entity needs to verify if the second entity is good before running it, not run the second entity if the verification fails. The trusted boot chain means that the first entity needs to measure the second entity before running it and then always run the second entity. The attestation may happen later. The system firmware needs to maintain both boot flows carefully. The verification and measurement must not be bypassed.

In addition, the system firmware may need to authenticate the end user, to determine if the user is authorized to perform some action. For example, the user may be asked to input a hard driver password to continue the boot. Or the user may be asked to input an administrator password to enter a setup page. Those actions must not be bypassed as well.

| Threat | Example |
| --- | --- |
| Spoofing | If the firmware needs to authenticate the user, the attacker may spoof the identity, or bypass the authentication check. |
| Tampering | The attacker may want to modify the secure boot logic or trusted boot logic (either code or configuration data) to bypass the verification or measurement. |
| Repudiation | N/A |
| Information Disclosure | The user identity and device password are secret information. The attacker may want to steal them. |
| Denial of Service | The attacker may modify the secure boot configuration data to cause a system crash during verification. |
| Elevation of Privilege | If the attacker bypasses the user authentication, he or she may enter firmware setup page to modify the configuration.If the attacker bypasses the secure boot verification, he or she may run the unauthorized 3rd part code in the ring-0 environment. |



| Adversary | Example |
| --- | --- |
| Network Attacker | The attacker may send malformed network packets to inject code into the system.<BR>The attacker may send a bad UEFI image to bypass or break the secure boot logic. |
| Unprivileged Software Attacker | The attacker may write a malformed UEFI authenticated variable to break the secure boot configuration. |
| System Software Attacker | The attacker may send a command to the isolated execution environment in order to modify the secure boot configuration.<BR>The attacker may enable a side channel to get secrets from memory. |
| Simple Hardware Attacker | The attacker may attach PCI Leach to perform DMA attack to read the secret from memory, or write the code region to bypass the verification. |
| Skilled Hardware Attacker | The attacker may hijack the memory bus to read secrets from memory, or write the code region to bypass the verification. |

| Mitigation | Example |
| --- | --- |
| Protection | Do check for untrusted external input before use (such as network packet, option ROM, OS loader, and UEFI authenticated variable). Do not run any untrusted 3rd part code before verification.<BR>If the secret is generated, it must be cleared after use (such as temporary input from HII). If the secret needs to be stored, the choice includes: to save secret to hardware directly (such as OPAL password), to save hash plus salt to a UEFI variable (such as user password), to save the secret in an isolated environment (such as TPM MOR2). Side channel prevention must be applied in this case.<BR>DMA protection must be enabled. Memory encryption must be used if the memory bus attack is in scope. |
| Detection | N/A |
| Recovery | N/A |
