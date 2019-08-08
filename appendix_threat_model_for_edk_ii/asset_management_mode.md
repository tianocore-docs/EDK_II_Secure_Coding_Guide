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

## Asset: Management Mode {#asset-management-mode}

Management mode is a special system execution environment. X86 systems have system management mode (SMM), and ARM has ARM TrustZone. The firmware code in management mode is considered as a secure world and having high privilege.

| Threat | Example |
| --- | --- |
| Spoofing | N/A |
| Tampering | The attacker may update the management mode memory to inject code or data. |
| Repudiation | N/A |
| Information Disclosure | The management mode may contain a secret (such as password, TPM MOR2 entropy), or its own information (code and data structure location). This information may be exposed to normal world. |
| Denial of Service | The management mode only has limited resource (such as memory). The attacker may send command to management mode code to make it run out of resource. |
| Elevation of Privilege | The attacker may gain unauthorized execution rights in management mode. For example, if the management code calls the normal world code, the attacker may replace the original code with malicious code to gain the privilege.<BR>The attacker may construct a confused-deputy attack for management mode. For example, the OS kernel may send a command to management mode to let it modify the hypervisor memory or management mode memory. |

| Adversary | Example |
| --- | --- |
| Network Attacker | N/A |
| Unprivileged Software Attacker | N/A |
| System Software Attacker | The attacker may take advantage of an implementation flaw in the management mode code to read or modify the management mode content, or content of a higher privilege environment, such as a hypervisor.<BR>The attacker may use a side channel to steal a secret in the management mode memory. |
| Simple Hardware Attacker | N/A |
| Skilled Hardware Attacker | N/A |

| Mitigation | Example |
| --- | --- |
| Protection | The management mode code must lock the management mode after it is constructed, no later than 3rd part code running.<BR>The management mode code must not call out to the normal world code.<BR>The system must remove unnecessary management mode handlers.<BR>The required management mode handler must check the untrusted external input, including the communication buffer, the pointer inside of the communication buffer, the general purpose register served as communication buffer pointer, the hardware base address register. The checked content must be copied into management mode memory to prevent TOC/TOU.<BR>The management mode handler must prevent unauthorized access to itself and high privileged content such as hypervisor or OS kernel memory.<BR>The management mode handler must prevent side channel attacks for the secret.<BR>The management mode handler must not allocate more resources to serve the request. If additional sources are allocated, they must be freed before the handler return to the normal world. |
| Detection | N/A |
| Recovery | N/A |
