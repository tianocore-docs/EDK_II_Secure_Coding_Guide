<!--- @file
  secure-coding-guidelines-general.md for EDK II Secure Coding Guide

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

# Secure Coding Guidelines: General {#secure-coding-guidelines-general}

Guidelines general

### General {#general}

**#GENERAL.1**: The code in trusted region MUST check any date from an untrusted region, such as a Portable and Executable (PE) image, capsule image, System Management Mode (SMM) communication buffer, Memory Mapped Input/Output (MMIO) Base Address Register (BAR), etc.

**#GENERAL.2**: When a code processes the untrusted data, it MUST avoid buffer overflows. Please do not access (write or read) the buffer beyond the size field.

**#GENERAL.3**: When code processes the untrusted data, it MUST avoid integer overflow. Please use addition instead of subtraction, use division instead of multiplication.

**#GENERAL.4**: When code processes the untrusted data, it MUST avoid untrusted data overlap with the trusted region.

**#GENERAL.5**: When code processes the untrusted data, it MUST check the untrusted data in all possible paths.

**#GENERAL.INPUT.1**: The code MUST check for valid input and reject everything else

**#GENERAL.INPUT.2**: The code MUST perform sanity checks and bounds checks, such as check type, length, range, format.

**#GENERAL.INPUT.3**: The code MUST use canonical representation. Always use fully qualified pathnames for files that get opened

**#GENERAL.INPUT.4**: The code MUST beware of character encoding and watch out for escape characters if using a shell script

**#GENERAL.INPUT.5**: The code MUST validate as much and as deep as possible to prevent unintentional errors if the code is changed; balance against coding time/performance.

**#GENERAL.INPUT.6**: The code MUST be careful of boundary conditions (e.g., off by one error, array indices) and conditionals (e.g., reverse logic)

**#GENERAL.BUFFER.1**: The code MUST check buffer sizes, copies, and indices (esp. sizeof)

**#GENERAL.BUFFER.2**: The code MUST check for appropriate buffer size. Maximums should be defined globally where possible to avoid assumptions in lower code layers.

**#GENERAL.BUFFER.3**: The code MUST check for NULL Pointers dereferenced in the code.

**#GENERAL.BUFFER.4**: The code MUST check NULL for NIL-terminate strings.

**#GENERAL.ARITH.1**: The code MUST check based on data type limitations (e.g., integer underflows and overflows).

**#GENERAL.ARITH.2**: The code MUST properly cast numeric variables involved in string manipulation.

**#GENERAL.ARITH.3**: The code SHOULD use SafeInt library to handle integer of external input.

**#GENERAL.FAIL.1:** Once the check fails, the code MUST fail secure – fail closed.

**#GENERAL.FAIL.2:** Once the check fails, the code MUST not provide hints to hackers (e.g., by disclosing information on failure). Don’t help an attacker with ‘guiding’ error messages.

### ASSERT {#assert}

**#ASSERT.1**: ASSERT MUST be used for something that NEVER occurs. If something MIGHT occur, use ERROR HANDLING, please. Check function return values in a consumed API. (from Code Complete)

**#ASSERT.Variable.1**: GetVariable with Non-Volatile (NV)+Runtime (RT) without Authentication (AU)/ReadOnly(RO) attribute MUST NOT ASSERT(), or at least have error handling code followed by.

**#ASSERT.Variable.2**: SetVariable with NV attribute MUST NOT ASSERT(), or at least have error handling code followed by.

**#ASSERT.Variable.3**: GetVariable with AU/RO attribute MAY ASSERT(), if driver assumes variable must exist.

**#ASSERT.Variable.4**: SetVariable without NV attribute MAY ASSERT(), before EndOfDxe.

**#ASSERT.Resource.1**: Memory Allocation MUST NOT ASSERT() after EndOfDxe.

**#ASSERT.Resource.2**: Memory Allocation MAY ASSERT() before EndOfDxe, if the allocation failure prevents the system from booting. E.g. SEC/PEI phase, the error means configuration error or hardware error. If we need return, we might return to the CPU reset vector, which is meaningless.

**#ASSERT.Resource.3**: MMIO/IO Allocation for external devices MUST NOT use ASSERT().

**#ASSERT.Resource.4**: MMIO/IO Allocation for onboard devices MAY use ASSERT() before EndOfDxe.

**#ASSERT.SMM.1**: SMI handler MUST NOT use ASSERT for external input, after EndOfDxe.

**#ASSERT.SMM.2**: SMM driver MAY use ASSERT in the entrypoint to construct the environment.

**#ASSERT.NETWORK.1**: Network driver MUST NOT use ASSERT for the packet from the remote.

**#ASSERT.SHELL.1**: Shell MUST NOT use ASSERT for the resource request, or user input.

### Deprecated API {#deprecated-api}

**#DEPRECATEDAPI.1**: The code MUST not use any deprecated API.

Table 1.1 EDK II Deprecated APIs

| Category | Deprecated API | Replacement |
| --- | --- | --- |
| BaseLib | StrCpy | StrCpyS |
|  | StrnCpy | StrnCpys |
|  | StrCat | StrCatS |
|  | StrnCat | StrnCats |
|  | AsciiStrCpy | AsciiStrCpyS |
|  | AsciiStrnCpy | AsciiStrnCpys |
|  | AsciiStrCat | AsciiStrCatS |
|  | AsciiStrnCat | AsciiStrnCats |
|  | UnicodeStrToAsciiStr | UnicodeStrToAsciiStrS |
|  | AsciiStrToUnicodeStr | AsciiStrToUnicodeStrS |
| PcdLib | [Lib]PcdSet[Ex]8 | [Lib]PcdSet[Ex]8S |
|  | [Lib]PcdSet[Ex]16 | [Lib]PcdSet[Ex]16S |
|  | [Lib]PcdSet[Ex]32 | [Lib]PcdSet[Ex]32S |
|  | [Lib]PcdSet[Ex]64 | [Lib]PcdSet[Ex]64S |
|  | [Lib]PcdSet[Ex]Ptr | [Lib]PcdSet[Ex]PtrS |
|  | [Lib]PcdSet[Ex]Bool | [Lib]PcdSet[Ex]BoolS |
| PrintLib | UnicodeValueToString | UnicodeValueToStringS |
|  | AsciiValueToString | AsciiValueToStringS |
| UefiLib | GetVariable | GetVariable2 |
|  | GetEfiGlobalVariable | GetEfiGlobalVariable2 |

#### Race Condition {#race-condition}

**#RACECONDITION.1**: The code MUST be careful of Time-of-Check/Time-of-Use (TOC/TOU) attack for the data crossing a trusted region, such as flash region access, SMM communication buffer access. The right way is to copy the data from an untrusted region to a trusted region and only access the data in the trusted region.

**#RACECONDITION.2**: The code MUST be careful of race conditions for the Bootstrap Processor (BSP) and Application Processors (AP). The BSP and AP may run different code in different trusted regions. Identify and Keep security critical sections short and simple.

**Policy**

**#POLICY.BLAKLIST.1:** If a prohibited list is used, a system error on getting prohibited list data MUST cause a prohibited list match and verification failure.

**#POLICY.BLAKLIST.2:** If a prohibited list is used, the prohibited list match MUST always cause a verification failure, no matter if the allowed list matches or not.

**#POLICY.WHITELIST.1:** If an allowed list is used, any error on getting allowed list data MUST cause verification failure.

### Environment {#environment}

**#ENVIRONMENT.RUNTIME.1**: The runtime module MUST be built with 4K alignment so that a Runtime image can be protected by the OS. ([SecurityEnhancement](https://www.gitbook.com/book/edk2-docs/a-tour-beyond-bios-mitigate-buffer-overflow-in-ue/details))

**#ENVIRONMENT.UEFI.1**: The boot module MAY be built with 4K alignment so that it can be protected by firmware.

**#ENVIRONMENT.NX.1**: The Code region SHOULD be set to ReadOnly (RO), and Data region SHOULD be set to NonExecutable (NX). (SecurityEnhancement)

**#ENVIRONMENT.NX.2**: The unallocated memory SHOULD be non-present or at least Non-Executable.

**#ENVIRONMENT.STACK.1**: Stack SHOULD be set to be NX. (SecurityEnhancement)

**#ENVIRONMENT.STACK.2**: Stack Guard SHOULD be enabled to catch stack overflow.

**#ENVIRONMENT.HEAP.1**: Heap SHOULD be set to be NX for data. [SecurityEnhancement]

**#ENVIRONMENT.HEAP.2**: A platform MAY use heap guard before release to check potential heap overflow.

**#ENVIRONMENT.ASLR.1**: A platform MAY enable Address Space Layout Randomization (ASLR). (SecurityEnhancement)

**#ENVIRONMENT.ASLR.2**: If ASLR is used, the platform MUST not expose any randomized information, such as a function address in a module, global data address, or the CPU architecture state address.

**#ENVIRONMENT.ASLR.3**: If ASLR is used, the platform MUST choose appropriate entropy. Too small of entropy may make ASLR not useful. Too much entropy may impact memory allocation in a resource-constrained environment.

**#ENVIRONMENT.CONTROLFLOW.1**: Control Flow Guard MAY be enabled to prevent Return Oriented Program (ROP), Call Oriented Program (COP)/Jump Oriented Program (JOP) attack. ([CET EDKII](https://github.com/tianocore/tianocore.github.io/wiki/CET-in-SMM))

### Crypto {#crypto}

**#CRYPTO.1**: A platform SHOULD NOT use any deprecated crypto-algorithm.

**#CRYPTO.2**: A platform SHOULD NOT implement its personally owned crypto algorithms or protocols.

**#CRYPTO.3**: A platform MUST follow cryptographic standards exactly.

**#CRYPTO.HASH.1**: A platform SHOULD use Secure Hash Algorithm (SHA) 256 equivalent or stronger.

**#CRYPTO.HASH.2**: A platform SHOULD NOT use SHA1 or Message Digest (MD) 4, MD5.

**#CRYPTO.SYM.1**: A platform SHOULD use Advanced Encryption Standard (AES) equivalent or stronger.

**#CRYPTO.SYM.2**: The key MUST NOT be saved in flash as plain text.

**#CRYPTO.ASYM.1**: A platform SHOULD use Rivest-Shamir-Adleman algorithm (RSA) or Elliptic curve cryptography (ECC) equivalent or stronger.

**#CRYPTO.ASYM.2**: The private key MUST NOT be saved in flash as plain text.

**#CRYPTO.RANDOM.1**: A platform SHOULD use an approved random number generator.

### Password {#password}

**#PASSWORD.1**: The password plaintext MUST NOT be saved to a variable. Alternative: 1) save SALT+HASH to a variable, 2) save to Hardware directly, 3) save to System Management RAM (SMRAM) for S3.

**#PASSWORD.2**: The password update MUST be in a secure environment, such as SMM, or before EndOfDxe.

**#PASSWORD.3**: The password in firmware MUST meet common password criteria (strength, update, algorithm, retry time, old password check, password lost, etc)

**#PASSWORD.4**: The password MAY be used to for authentication, (Entering setup page, setup variable access, WIFI PSK), for decryption (TLS private certificate)

**#PASSWORD.5**: The password in memory MUST be cleared after use. NOTE: The secrete MAY be in a global data region, stack or heap.

**#PASSWORD.6**: The password MUST NOT be hardcoded in the code.

**#PASSWORD.7**: If the code needs to compare the plain text password, the code MUST always compare all characters of the string, instead of breaking on the first mismatch.

**#PASSWORD.8**: Salt MUST be added to resist rainbow table attack.

**#PASSWORD.9**: Hash generation MUST add enough iteration to make sure the hash calculation is slow.

### Secret {#secret}

**#SECRET.1**: The secret MUST NOT be saved in a variable or disk directly as plain text. The secret includes but is not limited to the user password, hard drive password, Trusted Computing Group (TCG) OPAL password, or Trusted Platform Module (TPM) platform author value, network password, or private certificate password.

**#SECRET.2**: The secret in memory MUST be cleared after use, including usernames, passwords, keys, and other sensitive security information. NOTE: The secret MAY be in a global data region, stack or heap. The buffer content should be zeroed before released.

**#SECRET.3**: The secret MUST NOT be hardcoded in the code.

**#SECRET.4**: If the code needs to compare the secret, the code MUST always compare the entire data before completion.

**#SECRET.5**: The length of the secret MUST be large enough to resist a brute force attack.

### Network {#network}

**#NETWORK.1**: The network driver MUST always validate the packet from the network. Don’t trust any length, size, offset field.

**#NETWORK.2**: Each layer if the network driver MUST validate its own header.

**#NETWORK.TLS.1**: The public cert MUST be stored in the UEFI authenticated variable or read-only region flash region.

**#NETWORK.TLS.2**: The private cert plain text MUST NOT be stored to readable flash region.

**#NETWORK.WIFI.1**: The WIFI password plain text MUST NOT be stored to readable flash region.

### Hardware {#hardware}

**#HARDWARE.1**: The untrusted input from hardware MUST be verified, such as Dual-Inline-Memory-Modules (DIMM) Serial Presence Detect (SPD) data, Universal Serial Bus (USB) descriptor, Bluetooth Low Energy (BLE) advisory information, etc.

### DMA {#dma}

**#DMA.1**: The device Direct Memory Access (DMA) MUST be disabled by default, either via Peripheral Component Interconnect (PCI) Bus Master Enable (BME) or Input/Output Memory Management Unit (IOMMU) engine. ([IOMMU EDK II](https://firmware.intel.com/sites/default/files/Intel_WhitePaper_Using_IOMMU_for_DMA_Protection_in_UEFI.pdf))

**#DMA.2**: The device DMA MUST be enabled if and only if it is requested to perform a transaction. After completing the transaction, the device DMA MUST be disabled.

**#DMA.3**: If an IOMMU engine is used for DMA protection, the IOMMU MUST cover all physical DRAM regions.

**#DMA.4**: The DMA capable region MUST have no overlap with any other existing code region or data region.

**#DMA.5**: The IOMMU engine SHOULD be configured for fine granularity control. The DMA capable region SHOULD be per device in the DXE phase.

**#DMA.6**: The DMA in a debug device in debug image MAY be enabled at all times.

### Other {#other}

**#SIDECHANNEL.1:** The high privilege code (SMM) MUST use SpeculationBarrier() after validation of untrusted data but before use to mitigate [Bounds Check Bypass](https://software.intel.com/security-software-guidance/software-guidance/bounds-check-bypass). (SideChannel)

**#SIDECHANNEL.2:** The high privilege code (SMM) MUST use StuffRsb before RSM to mitigate [Branch Target Injection](https://software.intel.com/security-software-guidance/software-guidance/branch-target-injection). (SideChannel)

**#MDS.1:** The high privilege code (SMM) MUST rendezvous all logical processors both on entry to and exit from SMM to ensure that a sibling logical processor does not reload data into microarchitectural structures after the automatic flush. ([MDS](https://software.intel.com/security-software-guidance/insights/deep-dive-intel-analysis-microarchitectural-data-sampling))