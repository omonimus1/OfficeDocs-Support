---
title: Prevent Antivirus and DLP Tools from Blocking or Crashing Microsoft Teams
manager: dcscontentpm
ms.date: 03/11/2025
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
description: Provides instructions to prevent antivirus and DLP applications from blocking or crashing the Microsoft Teams app.
---

# Prevent antivirus and DLP tools from blocking or crashing Microsoft Teams

Third-party antivirus, reliability monitoring and data loss prevention (DLP) applications can interfere with the Microsoft Teams app and [Edge WebView2](https://developer.microsoft.com/en-us/microsoft-edge/webview2/?form=MA13LH), causing the app to exit unexpectedly and Teams client performance degradation. When you use non-Microsoft antivirus or DLP applications on desktops, you can include or approve the use of the Teams app, the executable that automatically updates the Teams app, and Edge Webview2 to improve application stability and efficency.

## New Teams

To prevent issues starting or using the new Teams app, add all of the following processes to the exclusion list in the antivirus software that you're using:

- `msedgewebview2.exe`
- `ms-teams.exe`
- `ms-teamsupdate.exe`
- `ms-teams_autostarter.exe`

Alternatively, you can add the processes to the allowlist for programs in your DLP application. The method to accomplish this addition varies. For specific instructions, contact your DLP application's manufacturer.

The MSIX installer installs the new Teams app in the `WindowsApps` folder instead of the user profile folder, where the classic Teams app is installed. Because users can't write to the `WindowsApps` folder, this location adds better protection against attacks that try to alter the installation of the Teams app.

**Note**: The MSIX installer and all files in the same directory are signed with a Microsoft certificate.

The name of the folder where the new Teams app is installed is dynamic and it changes when the app's version is updated. The folder name begins with `MSTeams_`, ends with `_8wekyb3d8bbwe`, and includes the app's version number in between.  For example, `MSTeams_23247.1112.2396.409_x64_8wekyb3d8bbwe`.

### Location of the Teams installation folder

To add the Teams processes to either the exclusion list or the Safe list/Allow list, you can find their location by using the following steps:

1. Open Windows PowerShell and run the following cmdlet to determine the location of the installation files:

   ```powershell
   Get-AppPackage -name "msteams"
   ```

   The result includes the value of the **InstallLocation** parameter, such as `C:\Program Files\WindowsApps\MSTeams_23247.1112.2396.409_x64_8wekyb3d8bbwe`.
1. To view the individual files, open **Task Manager** and select **Details**.
1. On the **Details** tab, locate and right-click **ms-teams.exe** and select **Open file location**.

## Classic Teams

To prevent issues starting the classic Teams app, add the following processes to the exclusion list in the antivirus software that you're using:

- `C:\Users\*\AppData\Local\Microsoft\Teams\current\teams.exe`
- `C:\Users\*\AppData\Local\Microsoft\Teams\update.exe`
- `C:\Users\*\AppData\Local\Microsoft\Teams\current\squirrel.exe`
- `C:\Users\*\AppData\Local\Microsoft\TeamsMeetingAddin`

Alternatively, you can add the processes to the allowlist for programs in your DLP application. The method to accomplish this addition varies. For specific instructions, contact your DLP application's manufacturer.

## Applications that may block or crash Teams

The following table lists applications and their associated DLLs that are known to potentially block or cause Teams to crash.

| Application | Associated DLLs |
| --- | --- |
| 360 Safe Security| `safewrapper.dll`|
| ASUS Sonic Suite 3| `ss3devprops.dll`|
| Aternity||
| Avast Antivirus| `aswhook.dll`|
| Avecto (now BeyondTrust)| `PGHook.dll`|
| BeyondTrust||
| Citrix App Protection| `ctxapclient64.dll`|
| Citrix ICA Client| `epclient64.dll`|
| Citrix ICA Service| `ctxdodhook64.dll`|
| ControlUp||
| CrowdStrike Falcon Sensor| `Umppc*.dll`|
| Cylance Desktop Security| `cymemdef64.dll`|
| DataClasys User Client| `CLSCBase.dll`, `CLSUInject.dll`|
| Encourage Technologies ESS Rec Agent| `etraldr.dll`|
| Esafenet Cobra DocGuard| `dynamicdll64.dll`|
| Fasoo DRM| `f_nxa.dll`|
| Frontier Technology DRM Agent| `ftagtctr.dll`, `detoured.dll`|
| Keyman Engine| `keyman64.dll`|
| Konica Minolta copier explorer plugin| `PSDPUIHandler.dll`|
| ManageEngine Unified Endpoint Management and Security (UEMS) Agent| `DragDrophook.dll`|
| Manufacturer Endpoint Agent| `clpbm64.dll`, `prntm64.dll`|
| Max Software Keylogger| `skgsec64.dll`|
| McAfee||
| Nahimic| `NahimicOSD.dll`, `Nahimic2OSD.dll`, `AudioDevProps2.dll`, `NahimicVRDevProps.dll`|
| NetRatings NetSight| `n64hooks.dll`|
| Netrix Agent| `nxgrdh64.dll`, `nxipc64.dll`|
| Nuance NaturallySpeaking| `nlutmgrhook_x64.dll`|
| NVIDIA ShadowPlay| `nvspcap64.dll`|
| Ocular Agent| `winhafnt64.dll`|
| PC Matic SuperShield| `SuperShieldHookCpy64.dll`|
| QiAnXin Tianqing DLP| `qmdlphook64.dll`|
| QiAnXin Tianqing HookBase| `ghijt64*.dll`|
| QiAnXin Tianqing Watermark| `watermarkhook64.dll`|
| Quality ISMC Client| `ismcfilehook64.dll`|
| SkyGuard Endpoint Security| `sgephook.dll`|
| Symantec Endpoint Protection| `sysfer.dll`|
| Thycotic Application Control| `ArelliaACActioni64.dll`|
| TightVNC| `screenhooks64.dll`| 
| Trellix Drive Encryption||
| Zscaler||
| Ztsment Data Protection| `injumon64.dll`|

## Other DLLs that may impact the Teams desktop client and Edge WebView2

Addtionally, the following DLLs are known to impact the Teams desktop client and Edge WebView2. You should verify the presence of the DLLs, and verify ownership and integrity.

- `bsijt64.dll`
- `core64.dll`
- `cptlwa64.dll`
- `cryptacl.dll`
- `csprnthk.dll`
- `cssguard64.dll`
- `ctiuser.dll`
- `dgapia64.dll`
- `dsefilesystemext64.dll`
- `dsloaderinj.x64.dll`
- `emcnt64.dll`
- `encappctrl64.dll`
- `estoutgo64.dll`
- `f_lph.dll`
- `guard64.dll`
- `hkapi.x64.dll`
- `hookcreateprocessinternal64.dll`
- `imfph64.dll`
- `ldgetprintcontent64.dll`
- `ldprintmonitor64.dll`
- `ldsmartenc64.dll`
- `ldwatermarkhook64.dll`
- `ldxghijt64.dll`
- `libwire_api_monitor_4.4.0.9.1662362401.dll`
- `lpghijt64.dll`
- `monfileop64.dll`
- `mozartbreathprotect.dll`
- `oeareader64.dll`
- `printhk64.dll`
- `sbieoutside.dll`
- `sdckern.dll`
- `sdwhf2130.dll`
- `tmailhook64.dll`
- `tsafedoc64.dll`
- `uhk64.dll`
- `vozokopot.dll`
- `winahframe64.dll`
- `wincept64.dll`  
- `winncap364.dll`
- `xpspntdll64_6016.dll`  
  
[!INCLUDE [Third-party information disclaimer](../../includes/third-party-information-disclaimer.md)]
[!INCLUDE [Third-party contact disclaimer](../../includes/third-party-contact-disclaimer.md)]

**Third-party information and solution disclaimer**

The information and the solution in this document represents the current view of Microsoft Corporation on these issues as of the date of publication. This solution is available through Microsoft or through a third-party provider. Microsoft does not specifically recommend any third-party provider or third-party solution that this article might describe. There might also be other third-party providers or third-party solutions that this article does not describe. Because Microsoft must respond to changing market conditions, this information should not be interpreted to be a commitment by Microsoft. Microsoft cannot guarantee or endorse the accuracy of any information or of any solution that is presented by Microsoft or by any mentioned third-party provider.

Microsoft makes no warranties and excludes all representations, warranties, and conditions whether express, implied, or statutory. These conditions include but are not limited to representations, warranties, or conditions of title, non-infringement, satisfactory condition, merchantability, and fitness for a particular purpose, regarding any service, solution, product, or any other materials or information. In no event will Microsoft be liable for any third-party solution that this article mentions.

Still need help? Go to [Microsoft Support Community](https://answers.microsoft.com).
