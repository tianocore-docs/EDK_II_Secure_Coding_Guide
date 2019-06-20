<!--- @file
  SMM.md for EDK II Secure Coding Guide

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

## SMM {#smm}

**#SMM.0:** Applications and functions should use the least privilege that will get the job done. If DXE or Runtime can finish the work, don’t use SMM.

**#SMM.1**: SMM module MUST lock SMM, at SmmReadyToLock.

*   **#SMM.1.1**: Boot firmware MUST set SMRAM Range Register (SMRR) for Top Segment (TSEG) correctly at SmmReadyToLock for all processors.
*   **#SMM.1.2**: Boot firmware MUST use TSEG only and MUST NOT use A/B Segment (ABSEG) as SMRAM.
*   **#SMM.1.3**: Boot firmware MUST remove SMRAMC_D_OPEN at SmmReadyToLock.
*   **#SMM.1.4**: Boot firmware MUST set SMRAMC_D_LOCK at SmmReadyToLock.
*   **#SMM.1.5**: Boot firmware MUST close all unnecessary services at SmmReadyToLock, such as the capability to register a new SMM driver into SMRAM.
*   **#SMM.1.6**: All the above locks MUST be performed in the S3 resume path before the control is transferred to OS waking vector.

**#SMM.2**: SMM module MUST NOT call any code outside of SMRAM, after SmmReadyToLock. (SMMProtection)

*   **#SMM.2.1**: Boot firmware MUST make sure there is an SMM code call outside of SMRAM after SmmReadyToLock.
*   **#SMM.2.2**: UEFI/PI Boot firmware MUST make sure there is NOT boot services or UEFI protocols are called from SMM code after SmmReadyToLock.
*   **#SMM.2.3**: UEFI/PI Boot firmware MUST make sure there is NOT runtime services are called from SMM code after SmmReadyToLock.
*   **#SMM.2.4**: UEFI/PI Boot firmware MUST make sure there are NOT dynamic PCDs that are accessed from SMM code after SmmReadyToLock.
*   **#SMM.2.5**: UEFI/PI Boot firmware MUST choose the library or MACRO correctly to make sure these libraries or MACROs do not call outside of SMRAM after SmmReadyToLock.
*   **#SMM.2.6**: All the above restrictions MUST be performed in the S3 resume path.
*   **#SMM.2.7**: Boot firmware MUST enable ExecutionDisable (XD) feature provided by Intel CPU.
*   **#SMM.2.8**: If the hardware supports SMM_Code_Access_Chk Model Specific Register (MSR), boot firmware MUST enable SMM_CODE_ACCESS for all processors.

**#SMM.3**: SMM module MUST check any communication memory between SMM and non-SMM, to make sure it does not impact the integrity, confidentiality or availability of SMM. ([SmmComm](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Secure_SMM_Communication.pdf))

*   **#SMM.3.1**: Boot firmware SMM module MUST check any data from a non-SMM component, to make sure the data buffer is NOT overlapped with SMRAM.
*   **#SMM.3.2**: If the data buffer contains a pointer, the Boot firmware SMM module MUST check the pointer to make sure the buffer pointed is NOT overlapped with SMRAM.
*   **#SMM.3.3**: If the data buffer is from MMIO BAR, the Boot firmware SMM module MUST check the pointer to make sure the buffer pointed is NOT overlapped with SMRAM.
*   **#SMM.3.4**: Boot firmware SMM module MUST calculate the data buffer carefully to avoid integer overflow.
*   **#SMM.3.5**: Boot firmware SMM module MUST copy the communication buffer to SMRAM before the check, to resist TOC/TOU or DMA attacks.

**#SMM.4**: SMM module MUST check any communication memory between SMM and non-SMM, to make sure it does not impact the integrity, confidentiality or availability of VMM. (SmmComm)

*   **#SMM.4.1**: Boot firmware SMM module MUST check any data from a non-SMM component, to make sure the data buffer is a fixed communication buffer range. “Fixed” here means a buffer used for Boot firmware SMM only, such as ReservedMemory, ACPINvs, or UefiRuntimeServicesData.
*   **#SMM.4.2**: If the data buffer contains a pointer, the Boot firmware SMM module MUST check the pointer to make sure the buffer pointed is in a fixed communication buffer range.
*   **#SMM.4.3**: If the data buffer is from MMIO BAR, the Boot firmware SMM module MUST check the pointer to make sure the buffer pointed is in MMIO range.
*   **#SMM.4.4**: Boot firmware SMM module MUST calculate the data buffer carefully to avoid integer overflow.
*   **#SMM.4.5**: Boot firmware SMM module MUST set the DRAM region to be not-present other than SMRAM and the fixed communication buffer range.

**#SMM.5**: SMM module MUST check MMIO access, to make sure it does not impact any bits which can only be accessed in SMM, or which only need to be accessed in VMM. Such as Intel Virtualization Technology for Direct I/O (VTd) BAR or Serial Peripheral Interface (SPI) BAR.

*   **#SMM.5.1**: If the data buffer is from MMIO BAR, Boot firmware SMM module MAY check if the BAR is the same as the original value in preboot, and deny the access if the BAR is changed.

**#SMM.6**: SMM module MUST be built with 4K alignment so that the SMM image can be protected with section attributes by SMM. (MemoryProtection)

*   **#SMM.6.1**: SMM module MUST be built with 4K alignment.
*   **#SMM.6.2**: The code section of the SMM image MUST be set as read-only in the page table.
*   **#SMM.6.3**: The data section of the SMM image MUST be set as non-executable in the page table.
*   **#SMM.6.4**: The SMM entrypoint code MUST be read-only.
*   **#SMM.6.5**: The platform MUST configure SMM with a static page table.
*   **#SMM.6.6**: The page table itself MUST be Read-Only.
*   **#SMM.6.7**: The Global Descriptor Table (GDT), Interrupt Description Table (IDT) MUST be Read-Only. (The only exception is IA32 GDT with stack guard enabled because stack switch need task switch)
*   **#SMM.6.8**: All other SMRAM data must be non-executable. (Stack, Heap)

**#SMM.7**: A platform MUST remove any unnecessary System Management Interrupt (SMI) handlers. ([Profile](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_Profiling_in_EDK_II.pdf))

*   **#SMM.7.1**: A platform MAY enable SMI handler profile feature to check all SMI handlers.

**#SMM.8**: An SMM module SHOULD use a read-only page to save the critical data structure. As such this critical data structure is locked after SmmReadyToLock.



**#SMM.10**: An SMM module MUST use a read-only page for any S3 data, that needs to be referred before SMM rebase in the S3 resume phase.

**#SMM.11:** If Control Flow Enhancement Technology (CET) is supported, the SMM MUST enable CET to prevent ROP attack. ([CET EDK II](https://github.com/tianocore/tianocore.github.io/wiki/CET-in-SMM))