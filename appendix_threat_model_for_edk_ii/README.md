<!--- @file
  README.md for appendix_threat_model_for_edk_ii for EDK II Secure Coding Guide

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

# Appendix:Threat Model for EDK II {#appendix-threat-model-for-edk-ii}
This chapter provides the basic assumptions for the threat model of EDK II firmware. The threat model discussed here is a general guide and serves as the baseline of the EDK II firmware. For each specific feature in EDK II firmware, there might be additional feature-based threat models in addition to the general threat model.

In [UEFI Threat Model](https://uefi.org/sites/default/files/resources/Intel-UEFI-ThreatModel.pdf), we discussed the asset, threat and mitigation. Here we will revisit these items and based upon [STRIDE](https://en.wikipedia.org/wiki/STRIDE_(security)).

| Threat | Desired Property |
| --- | --- |
| Spoofing | Authentication |
| Tampering | Integrity |
| Repudiation | Non-Repudiation |
| Information Disclosure | Confidentiality |
| Denial of Service | Availability |
| Elevation of Privilege | Authorization |

In EDK II firmware, the denial of service can be temporary in the current boot, or permanent in which case the system never boot again. The latter is more serious and it is named as permanent denial of service (PDoS).

We will consider the below adversary for the EDK II firmware:

| Adversary | Capability |
| --- | --- |
| Network Attacker | The attacker may connect to the system by network in order to eavesdrop, intercept, masquerade, or modify the network packet. |
| Unprivileged Software Attacker | The attacker may run ring-3 software in an OS application layer. The attacker may perform a software based side channel attack (such as using cache timing). |
| System Software Attacker | The attacker may run ring-0 software in the OS kernel or hypervisor, or run 3rd party firmware code in firmware boot phase. The attacker may perform the software based side channel attack (such as using cache timing, performance counters, branch information, or power status). |
| Simple Hardware Attacker | The attacker may touch the platform hardware (such as power button or jumper) and attach/remove a simple malicious device (such as hardware debugger, PCI Leach to the external port, PCIE card to the PCIE slot, memory DIMM, NIC cable, hard drive, keyboard, USB device, Bluetooth device). The attacker may hijack the simple system bus (such as the SPI bus or I2C bus). |
| Skilled Hardware Attacker | The attacker may hijack the complex system bus (such as memory bus, or PCI express bus). The attacker may perform the hardware based side channel attack, such as power analysis, thermal analysis, or electromagnetic analysis. The attacker may perform a glitch attack. |

We will consider the below mitigations for the EDKII firmware:

| Mitigation | Objective |
| --- | --- |
| Protection | The mitigation is to prevent such an attack for damaging the system. |
| Detection | The mitigation is to detect if the system is under attack. |
| Recovery | The mitigation is to recover the system if it is under attack. |

* Asset: Flash Content
* Asset: Boot Flow
* Asset: S3 Resume
* Asset: Management Mode
* Asset: Build Tool
