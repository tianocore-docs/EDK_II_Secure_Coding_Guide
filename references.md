<!--- @file
  references.md for EDK II Secure Coding Guide

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

# References {#references}

### Books and Papers {#books-and-papers}

[McConnell] _Code Complete: A Practical Handbook of Software Construction, Second Edition_, Steve McConnell, Microsoft, 2004, ISBN: 978-0735619678

[Maguire] _Writing Solid Code: Microsoft’s Techniques for Developing Bug-Free C Programs_, Steve Maguire, Microsoft, 1993, ISBN: 978-1556155512

[HowardLeBlanc] _Writing Secure Code: Practical Strategies and Proven Techniques for Building Secure Applications in a Networked World, Second Edition_, Michael Howard, David LeBlanc, Microsoft, 2004, ISBN: 978-0735617223

[Howard] _24 Deadly Sins of Software Security: Programming Flaws and How to Fix Them_, Michael Howard, David LeBlanc, John Viega, McGraw-Hill, 2009, ISBN: 978-0071626750

[Graff] [_Secure Coding: Principles_](http://www.securecoding.org/)[](http://www.securecoding.org/)[_&amp;_](http://www.securecoding.org/)[](http://www.securecoding.org/)[_Practices_](http://www.securecoding.org/), M.G. Graff and K.R. van Wyk, O’Reilly, 2002, ISBN: 978-0596002428

[Ransome] _Core Software Security: Security at the Source_, James Ransome and Anmol Misra, CRC Press, 2014, ISBN: 978-1466560956\. Particularly, chapters 5 and 9.

[Viega] _Secure Programming Cookbook for C and C++: Recipes for Cryptography, Authentication, Input Validation &amp; More_. John Viega, Matt Messier, O&#039;Reilly Media, 2003, ISBN: 978-0596003944

[ViegaMcGraw] _Building Secure Software: How to Avoid Security Problems the Right Way_, John Viega, Gary McGraw, Addison-Wesley Professional, 2001, ISBN: 978-0201721522

[Teer] _Solaris Systems Programming_, Chapter 9, Secure C Programming, Rich Teer, Prentice Hall, 2007, ISBN: 978-0768682236

[MITRE] System Engineering Guide, MITRE, Page 192, Security Code Review

### Web {#web}

[Android] “Android Secure Coding Standard”, [https://wiki.sei.cmu.edu/confluence/display/android/Android+Secure+Coding+Standard](https://wiki.sei.cmu.edu/confluence/display/android/Android+Secure+Coding+Standard)

[Apple] “Secure Coding Guide”, [https://developer.apple.com/library/mac/documentation/Security/Conceptual/SecureCodingGuide/Introduction.html](https://developer.apple.com/library/mac/documentation/Security/Conceptual/SecureCodingGuide/Introduction.html)

[Banned Function] Microsoft Security Development Lifecycle (SDL) Banned Function Calls, [https://msdn.microsoft.com/en-us/library/bb288454.aspx](https://msdn.microsoft.com/en-us/library/bb288454.aspx)

[Jordan] “Ten dos and don’ts for secure coding”, Michael Jordan, https://searchsecurity.techtarget.com/tip/Ten-dos-and-donts-for-secure-coding

[MDS] Deep Dive: Intel Analysis of Microarchitectural Data Sampling https://software.intel.com/security-software-guidance/insights/deep-dive-intel-analysis-microarchitectural-data-sampling

[Microsoft] “Security in Software Localization”, Mohamed Elgazzar, https://docs.microsoft.com/en-us/globalization/design/security-guidelines

[MicrosoftSDL] “What are the Microsoft SDL practices?”, [https://www.microsoft.com/en-us/securityengineering/sdl/practices](https://www.microsoft.com/en-us/securityengineering/sdl/practices)

[Msdn] “Guidelines for Writing Secure Code”, https://docs.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2010/ms182020(v=vs.100)

[Michael] “Defend Your Code with Top Ten Security Tips Every Developer Must Know”, Howard, Michael and Brown, Keith, [https://blogs.msdn.microsoft.com/laurasa/2012/07/25/defend-your-code-with-top-ten-security-tips-every-developer-must-know/](https://blogs.msdn.microsoft.com/laurasa/2012/07/25/defend-your-code-with-top-ten-security-tips-every-developer-must-know/)

[Mozilla] “Secure Development Guidelines”, [https://developer.mozilla.org/en-US/docs/Mozilla/Security/Secure_Development_Guidelines](https://developer.mozilla.org/en-US/docs/Mozilla/Security/Secure_Development_Guidelines)

[Linux] “Secure Programming for Linux and Unix HOWTO, Background, Sources of Design and Implementation Guidelines”, http://www.linux-tutorial.info/modules.php?name=Howto&amp;pagename=Secure-Programs-HOWTO/sources-of-guidelines.html

[OWASP] OWASP Secure Coding Practices, [https://www.owasp.org/index.php/OWASP_Secure_Coding_Practices_-_Quick_Reference_Guide](https://www.owasp.org/index.php/OWASP_Secure_Coding_Practices_-_Quick_Reference_Guide)

[RedHat] “Secure Coding”, [https://developers.redhat.com/topics/secure-coding/](https://developers.redhat.com/topics/secure-coding/)

[SEI] “SEI CERT C Coding Standard”, [https://wiki.sei.cmu.edu/confluence/display/c/SEI+CERT+C+Coding+Standard](https://wiki.sei.cmu.edu/confluence/display/c/SEI+CERT+C+Coding+Standard)

[SideChannel] Host Firmware Speculative Execution Side Channel Mitigation, https://software.intel.com/security-software-guidance/insights/host-firmware-speculative-execution-side-channel-mitigation

[SideChannel2] Deep Dive: Analyzing Potential Bounds Check Bypass Vulnerabilities, [https://software.intel.com/security-software-guidance/insights/deep-dive-analyzing-potential-bounds-check-bypass-vulnerabilities](https://software.intel.com/security-software-guidance/insights/deep-dive-analyzing-potential-bounds-check-bypass-vulnerabilities)

[SideChannel3] Security Best Practices for Side Channel Resistance, [https://software.intel.com/security-software-guidance/insights/security-best-practices-side-channel-resistance](https://software.intel.com/security-software-guidance/insights/security-best-practices-side-channel-resistance)

[SideChannel4] Guidelines for Mitigating Timing Side Channels Against Cryptographic Implementations, [https://software.intel.com/security-software-guidance/insights/guidelines-mitigating-timing-side-channels-against-cryptographic-implementations](https://software.intel.com/security-software-guidance/insights/guidelines-mitigating-timing-side-channels-against-cryptographic-implementations)

[Wheeler] “Secure Programming for Linux and Unix HOWTO -- Creating Secure Software”, David Wheeler, [http://www.dwheeler.com/secure-programs/](http://www.dwheeler.com/secure-programs/)

[Witteman] “Secure Application Programming in the presence of Side Channel Attack”, Marc Witteman, [https://www.riscure.com/uploads/2018/11/201708_Riscure_Whitepaper_Side_Channel_Patterns.pdf](https://www.riscure.com/uploads/2018/11/201708_Riscure_Whitepaper_Side_Channel_Patterns.pdf)

### Firmware Specific {#firmware-specific}

[CapsuleRecovery] Yao, Zimmer, [A Tour Beyond BIOS- Capsule Update and Recovery in EDK II](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Capsule_Update_and_Recovery_in_EDK_II.pdf), [https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Capsule_Update_and_Recovery_in_EDK_II.pdf](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Capsule_Update_and_Recovery_in_EDK_II.pdf)

[CET] Control Flow Enforcement Technology, [https://software.intel.com/sites/default/files/managed/4d/2a/control-flow-enforcement-technology-preview.pdf](https://software.intel.com/sites/default/files/managed/4d/2a/control-flow-enforcement-technology-preview.pdf)

[CET EDK II] CET in SMM [https://github.com/tianocore/tianocore.github.io/wiki/CET-in-SMM](https://github.com/tianocore/tianocore.github.io/wiki/CET-in-SMM)

[HSTI] Hardware Security Testability Specification https://msdn.microsoft.com/en-us/library/windows/hardware/mt712332.aspx

[IOMMU EDKII] Yao, Zimmer, A Tour Beyond BIOS Using IOMMU for DMA Protection,

[https://firmware.intel.com/sites/default/files/Intel_WhitePaper_Using_IOMMU_for_DMA_Protection_in_UEFI.pdf](https://firmware.intel.com/sites/default/files/Intel_WhitePaper_Using_IOMMU_for_DMA_Protection_in_UEFI.pdf)

[MemoryMap] Yao, Zimmer, A Tour Beyond BIOS Memory Map And Practices in UEFI BIOS, [https://github.com/tianocoredocs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Memory_Map_And_Practices_in_UEFI_BIOS_V2.pdf](https://github.com/tianocoredocs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Memory_Map_And_Practices_in_UEFI_BIOS_V2.pdf)

[MemoryProtection] Yao, Zimmer, [A Tour Beyond BIOS- Memory Protection in UEFI BIOS](https://www.gitbook.com/book/edk2-docs/a-tour-beyond-bios-memory-protection-in-uefi-bios/details), [https://www.gitbook.com/book/edk2-docs/a-tour-beyond-bios-memory-protection-in-uefi-bios/details](https://www.gitbook.com/book/edk2-docs/a-tour-beyond-bios-memory-protection-in-uefi-bios/details)

[MOR] TCG Platform Reset Attack Mitigation Specification, [https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf](https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)

[Profile] Yao, Zimmer, Zeng, Fan, A Tour Beyond BIOS Implementing Profiling in UEFI, [https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_Profiling_in_EDK_II.pdf](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_Profiling_in_EDK_II.pdf)

[S3Resume] Jiewen Yao, Vincent Zimmer, [A Tour Beyond BIOS Implementing S3 Resume with EDK II](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_S3_resume_with_EDKII_V2.pdf), [https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_S3_resume_with_EDKII_V2.pdf](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_S3_resume_with_EDKII_V2.pdf)

[SecurityEnhancement] Yao, Zimmer, A Tour Beyond BIOS Securiy Enhancement to Mitigate Buffer Overflow in UEFI, [https://www.gitbook.com/book/edk2-docs/a-tour-beyond-bios-mitigate-buffer-overflow-in-ue/details](https://www.gitbook.com/book/edk2-docs/a-tour-beyond-bios-mitigate-buffer-overflow-in-ue/details)

[SecurityDesign] Yao, Zimmer, [A Tour Beyond BIOS Security Design Guide in EDK II](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Security_Design_Guide_in_EDK_II.pdf), [https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Security_Design_Guide_in_EDK_II.pdf](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Security_Design_Guide_in_EDK_II.pdf)

[SecureMOR] Secure MOR implementation, [https://docs.microsoft.com/en-us/windows-hardware/drivers/bringup/device-guard-requirements](https://docs.microsoft.com/en-us/windows-hardware/drivers/bringup/device-guard-requirements)

[SmmComm] Yao, Zimmer, Zeng, A tour beyond BIOS secure SMM communciation, [https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Secure_SMM_Communication.pdf](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Secure_SMM_Communication.pdf)

[SMMProtection] Yao, SMM Protection in EDKII. [http://www.uefi.org/sites/default/files/resources/Jiewen%20Yao%20-%20SMM%20Protection%20in%20%20EDKII_Intel.pdf](http://www.uefi.org/sites/default/files/resources/Jiewen%20Yao%20-%20SMM%20Protection%20in%20%20EDKII_Intel.pdf)

[TCG OPAL] [Storage Work Group Storage Security Subsystem Class: Opal, Version 2.01 Final, Revision 1.00](https://trustedcomputinggroup.org/wp-content/uploads/TCG_Storage-Opal_SSC_v2.01_rev1.00.pdf), [https://trustedcomputinggroup.org/wp-content/uploads/TCG_Storage-Opal_SSC_v2.01_rev1.00.pdf](https://trustedcomputinggroup.org/wp-content/uploads/TCG_Storage-Opal_SSC_v2.01_rev1.00.pdf)

[TCG SIIS] [TCG Storage Interface Interactions Specification, Version 1.06, Revision 1.08](http://www.trustedcomputinggroup.org/wp-content/uploads/TCG_SWG_SIIS_Version_1_06_Revision_1_08_public-review.pdf), [https://www.trustedcomputinggroup.org/wp-content/uploads/TCG_SWG_SIIS_Version_1_06_Revision_1_08_public-review.pdf](https://www.trustedcomputinggroup.org/wp-content/uploads/TCG_SWG_SIIS_Version_1_06_Revision_1_08_public-review.pdf)

[TPM2] Trusted Platform Module Library Specification, Family “2.0”, Level 00, Revision 01.38 – September 2016, [https://trustedcomputinggroup.org/tpm-library-specification/](https://trustedcomputinggroup.org/tpm-library-specification/)

[TPM2 PFP] [PC Client Specific Platform Firmware Profile Specification Family “2.0”, Level 00 Revision 1.03 Version 51](https://trustedcomputinggroup.org/wp-content/uploads/PC-ClientSpecific_Platform_Profile_for_TPM_2p0_Systems_v51.pdf), [https://trustedcomputinggroup.org/wp-content/uploads/PC-ClientSpecific_Platform_Profile_for_TPM_2p0_Systems_v51.pdf](https://trustedcomputinggroup.org/wp-content/uploads/PC-ClientSpecific_Platform_Profile_for_TPM_2p0_Systems_v51.pdf)

[TPM2 EDK II] Yao, Zimmer, A Tour Beyond BIOS with the UEFI TPM2 Support in EDKII [https://firmware.intel.com/sites/default/files/resources/A_Tour_Beyond_BIOS_Implementing_TPM2_Support_in_EDKII.pdf](https://firmware.intel.com/sites/default/files/resources/A_Tour_Beyond_BIOS_Implementing_TPM2_Support_in_EDKII.pdf)

[WSMT] Windows SMM Security Table, [https://msdn.microsoft.com/en-us/library/windows/hardware/dn495660(v=vs.85).aspx#wsmt](https://msdn.microsoft.com/en-us/library/windows/hardware/dn495660(v=vs.85).aspx)

[http://download.microsoft.com/download/1/8/A/18A21244-EB67-4538-BAA2-1A54E0E490B6/WSMT.docx](http://download.microsoft.com/download/1/8/A/18A21244-EB67-4538-BAA2-1A54E0E490B6/WSMT.docx)

[Variable] Yao, Zimmer, Zeng, A Tour Beyond BIOS Implementing UEFI Authenticated Variables in SMM with EDKII – Verion 2, [https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_UEFI_Authenticated_Variables_in_SMM_with_EDKII_V2.pdf](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_UEFI_Authenticated_Variables_in_SMM_with_EDKII_V2.pdf)
