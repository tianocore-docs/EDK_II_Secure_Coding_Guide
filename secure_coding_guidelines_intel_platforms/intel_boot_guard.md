<!--- @file
  intel-boot-guard.md for EDK II Secure Coding Guide

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

### Intel® Boot Guard {#intel-boot-guard}

**#BootGuard.1**: A full secure/verified boot flow MUST include Intel® Boot Guard, OEM Boot Block (OBB) Verification.

**#BootGuard.2**: Intel® Boot Guard SHOULD be used to verify the Initial Boot Block (IBB).

**#BootGuard.3**: If Intel® Boot Guard is used, all IBB portion MUST be signed.

**#BootGuard.4**: If Intel® Boot Guard is used, the verification MUST happen in all boot path, including normal, S3, S4, capsule update, recovery.

**#BootGuard.5**: After the memory is initialized, the code in the IBB flash region MUST not be invoked. Only the memory copy MAY be invoked, including PSI service, PPI, and a callback function.

**#BootGuard.6**: After the memory is initialized, the data in the IBB flash region MUST not be referred. Only the memory copy MAY be referred, including HOB, global data in PPI, system state, GDT, IDT, Firmware Information Table (FIT), Boot Policy Manifest (BPM), Key Manifest (KM), etc.

**#BootGuard.7**: Once Intel® Boot Guard is enabled, there MUST be no way to disable it.

**#ObbVereification.1**: The IBB MUST be used to verify the OEM Boot Block (OBB).

**#ObbVereification.2**: Any OBB Firmware Volume images MUST be signed.

**#ObbVereification.3**: The verification MUST occur for the OBB code in memory.