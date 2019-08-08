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

## Asset: S3 Resume {#asset-s3-resume}

S3 resume is a special boot flow. It is defined by ACPI specification. During S3 resume, the system restores the configuration from a normal boot and jumps to OS waking vector.

All protection applied to the normal boot must also be applied in S3 resume.

| Threat | Example |
| --- | --- |
| Spoofing | N/A |
| Tampering | The attacker may try to modify the S3 configuration, also known as S3 boot script. |
| Repudiation | N/A |
| Information Disclosure | If the s3 configuration includes a secret (such as HDD password), the attacker may want to steal the secret. |
| Denial of Service | The attacker may destroy the S3 configuration to prevent the system from booting. |
| Elevation of Privilege | The attacker may disable the protections stored in the S3 configuration such as register lock. |



| Adversary | Example |
| --- | --- |
| Network Attacker | N/A |
| Unprivileged Software Attacker | The attacker may write a malformed UEFI variable to break the S3 configuration. |
| System Software Attacker | The attacker may send a command to the isolated execution environment to modify the S3 configuration. If there is a secret saved in the isolated environment, the attacker may send a commend to get the secret, or use a side channel to steal the secret. |
| Simple Hardware Attacker | N/A |
| Skilled Hardware Attacker | N/A |

| Mitigation | Example |
| --- | --- |
| Protection | The S3 configuration data must be saved to a secure place. For example, embedded into read only code region, a read only variable, an isolated execution environment, or a lock box.<BR>If the S3 configuration data is secret, then it must be saved in an isolated execution environment or a lock box to prevent unauthorized reads. |
| Detection | N/A |
| Recovery | N/A |
