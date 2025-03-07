---
title: Prevent Antivirus and DLP Tools from Blocking or Crashing Microsoft Teams
ms.author: meerak
author: cloud-writer
manager: dcscontentpm
ms.date: 07/26/2024
audience: Admin
ms.topic: troubleshooting
search.appverid:
  - SPO160
  - MET150
ms.assetid:
appliesto:
  - New Microsoft Teams
  - Classic Microsoft Teams
ms.custom:
  - sap:Teams Clients\Windows Desktop
  - CI 106370
  - CSSTroubleshoot
ms.reviewer: davidsle
description: Provides instructions to add Teams to antivirus and DLP applications so that it can start correctly.
---

# Prevent Antivirus and DLP Tools from Blocking or Crashing Microsoft Teams

Third-party antivirus, reliability monitoring and data loss prevention (DLP) applications can interfere with the Microsoft Teams app and webview2, leading to unexpected app exits and performance degradations of the Teams client. When you use non-Microsoft antivirus or DLP applications in PCs, you can include or approve the use of the Teams app, Teams updater and [Edge Webview2](https://developer.microsoft.com/en-us/microsoft-edge/webview2/?form=MA13LH) on the computers, to improve application stability and efficency.

## New Teams

To prevent issues with starting or using the new Teams app, *add all the following processes* to the exclusion list in the antivirus software that you’re using:

- `msedgewebview2.exe`
- `ms-teams.exe`
- `ms-teamsupdate.exe`
- `ms-teams_autostarter.exe`

Alternatively, you can add the processes to the allowlist for programs in your DLP application. The method to accomplish this addition varies. For specific instructions, contact your DLP application’s manufacturer.

The MSIX installer installs the new Teams app in the WindowsApps folder instead of the user profile folder, where the classic Teams app is installed. Because users can’t write to the WindowsApps folder, this location adds better protection against attacks that try to alter the installation of the Teams app.

**Note**: The MSIX installer and all files in the same directory are signed with a Microsoft certificate.

The name of the folder where the new Teams app is installed is dynamic and it changes when the app’s version is updated. The folder name begins with MSTeams_, ends with _8wekyb3d8bbwe, and includes the app’s version number in between.  For example, MSTeams_23247.1112.2396.409_x64_8wekyb3d8bbwe.

### Location of the Teams installation folder

To add the Teams processes to either the exclusion list or the Safe list/Allow list, you can find their location by using the following steps:

1. Open Windows PowerShell and type the following cmdlet to determine the location of the installation files:
   `Get-AppPackage -name "msteams"`

   The output includes the value of the **InstallLocation** parameter such as C:\Program Files\WindowsApps\ MSTeams_23247.1112.2396.409_x64_8wekyb3d8bbwe.
1. To view the individual files, open **Task Manager** and select **More details**.
1. On the **Details** tab, locate and right-click **ms-teams.exe** and select **Open file location**.

## Classic Teams

To prevent issues with starting the classic Teams app, add the following processes to the exclusion list in the antivirus software that you’re using:

- `C:\Users\*\AppData\Local\Microsoft\Teams\current\teams.exe`
- `C:\Users\*\AppData\Local\Microsoft\Teams\update.exe`
- `C:\Users\*\AppData\Local\Microsoft\Teams\current\squirrel.exe`
- `C:\Users\*\AppData\Local\Microsoft\TeamsMeetingAddin`

Alternatively, you can add the processes to the allowlist for programs in your DLP application. The method to accomplish this addition varies. For specific instructions, contact your DLP application’s manufacturer.


## DLLs / tools which may cause the above described issues
- Crowdstrike (Umppc*.dll)
- Beyond Trust
- Avecto
- Aternity
- zscaler
- ControlUp
- ctxapclient64, Citrix App Protection 
- McAfee
- Trellix [Verify to use Drive Encryption 7.4.2, to improve your experience on teams](https://docs.trellix.com/bundle/drive-encryption-v7-4-x-hotfix7421-release-notes/resource/prod-drive-encryption-v7-4-x-cat-release-notes.pdf)
- NahimicOSD
- PGHook.dll
- sysfer.dll – Symantec Endpoint Protection
- PSDPUIHandler.dll (Konica Minolta copier Explorer plugin interferes with files upload to the app)
- ghijt64**.dll – Qianxin Tianqing HookBase
- dragdrophookdll**.dll – ManageEngine UEMS Agent
- skgsec64.dll – Max Software Keylogger
- nlutmgrhook_x64.dll – Nuance NaturallySpeaking

- sgephook.dll – SkyGuard Endpoint Security
- CLSCBase.dll, CLSUInject.dll – DataClasys User Client
- ctxdodhook64.dll – Citrix ICA Service
- ftagtctr.dll – Frontier Technology DRM Agent
- supershieldhookcpy64.dll – PC Pitstop SuperShield
- winhafnt64.dll – Ocular Agent
- ghijt64.dll 
- etraldr.dll – Encourage Technologies ESS Rec Agent
- clpbm64.dll – Manufacturer Endpoint Agent
- ismcfilehook64.dll – Quality ISMC Client
- f_nxa.dll – Fasoo DRM
- qmdlphook64.dll – Qianxin Tianqing DLP
- cymemdef64.dll – Cylance Desktop Security
- aswhook.dll – Avast Antivirus
- n64hooks.dll – NetRatings NetSight
- arelliaacactioni64.dll – Thycotic Application Control
- screenhooks64.dll – TightVNC
- nxgrdh64.dll, nxipc64.dll – Netrix Agent
- keyman64.dll – Keyman Engine
- nvspcap64.dll – NVIDIA ShadowPlay
- ctxdodhook64.dll – Citrix ICA Service
- watermarkhook64.dll – Qianxin Tianqing Watermark
- detoured.dll – Frontier Technology DRM Agent
- injumon64.dll – Ztsment Data Protection
- epclient64.dll – Citrix ICA Client
- safewrapper.dll – 360 Safe Security
- dynamicdll64.dll – EsafeNet Cobra DocGuard
- prntm64.dll – Manufacturer Endpoint Agent
- ss3devprops.dll – ASUS Sonic Suite 3
- nahimic2osd.dll, audiodevprops2.dll, nahimicvrdevprops.dll  – Nahimic Audio

## Other dlls which impact both webview2 and teams desktop client
Users should verify the presence of the dll, and validate both ownership and integrity.
- uhk64.dll  
- winncap364.dll  
- imfph64.dll  
- csprnthk.dll  
- tsafedoc64.dll  
- bsijt64.dll  
- ldsmartenc64.dll  
- ldxghijt64.dll  
- dgapia64.dll  
- sdckern.dll  
- ctiuser.dll  
- encappctrl64.dll  
- wincept64.dll  
- lpghijt64.dll  
- vozokopot.dll  
- hkapi.x64.dll  
- monfileop64.dll  
- tmailhook64.dll  
- f_lph.dll  
- hookcreateprocessinternal64.dll  
- dsefilesystemext64.dll  
- ldwatermarkhook64.dll  
- core64.dll  
- libwire_api_monitor_4.4.0.9.1662362401.dll  
- estoutgo64.dll  
- printhk64.dll  
- ldgetprintcontent64.dll  
- mozartbreathprotect.dll  
- cryptacl.dll  
- oeareader64.dll  
- sbieoutside.dll  
- cssguard64.dll  
- winahframe64.dll  
- sdwhf2130.dll  
- dsloaderinj.x64.dll  
- xpspntdll64_6016.dll  
- cptlwa64.dll  
- emcnt64.dll  
- ldprintmonitor64.dll  
- guard64.dll  

Let me know if you need any more formatting changes!
## Reference
- [How to create an Application Control exception or stop sysfer.dll injection into a process with Endpoint Protection](https://knowledge.broadcom.com/external/article/181736/how-to-create-an-application-control-exc.html)
- [New Teams desktop app fails to render video](https://learn.microsoft.com/en-us/microsoftteams/troubleshoot/meetings/new-teams-desktop-app-fail-render-video)

#### Third-party information disclaimer

The third-party products that this article discusses are manufactured by companies that are independent of Microsoft. Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.

Third-party contact disclaimer

Microsoft provides third-party contact information to help you find additional information about this topic. This contact information may change without notice. Microsoft does not guarantee the accuracy of third-party contact information.

Third-party information and solution disclaimer

The information and the solution in this document represents the current view of Microsoft Corporation on these issues as of the date of publication. This solution is available through Microsoft or through a third-party provider. Microsoft does not specifically recommend any third-party provider or third-party solution that this article might describe. There might also be other third-party providers or third-party solutions that this article does not describe. Because Microsoft must respond to changing market conditions, this information should not be interpreted to be a commitment by Microsoft. Microsoft cannot guarantee or endorse the accuracy of any information or of any solution that is presented by Microsoft or by any mentioned third-party provider.

Microsoft makes no warranties and excludes all representations, warranties, and conditions whether express, implied, or statutory. These conditions include but are not limited to representations, warranties, or conditions of title, non-infringement, satisfactory condition, merchantability, and fitness for a particular purpose, regarding any service, solution, product, or any other materials or information. In no event will Microsoft be liable for any third-party solution that this article mentions.

Still need help? Go to [Microsoft Support Community](https://answers.microsoft.com).
