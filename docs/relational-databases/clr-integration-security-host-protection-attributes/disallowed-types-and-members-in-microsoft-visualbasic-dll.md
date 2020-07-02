---
title: Microsoft.VisualBasic.dll의 형식 및 멤버
description: HPA (호스트 보호 특성) 값이 허용 되지 않는 Microsoft.VisualBasic.dll 어셈블리의 멤버 및 형식을 나열 합니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: 45f55646-4bf1-4493-9f72-d1363c9a9ac6
author: rothja
ms.author: jroth
ms.openlocfilehash: 1de9adbca4c4cd0d6b71056dcb338e534f006a3e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727739"
---
# <a name="disallowed-types-and-members-in-microsoftvisualbasicdll"></a>Microsoft.VisualBasic.dll에 허용되지 않는 유형 및 멤버
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CLR (공용 언어 통합) 프로그래밍에서는 **Externalprocessmgmt**, **externalprocessor**, **MayLeakOnAbort**, **securityinfrastructure**, **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **sharedstate**, **Synchronization**또는 **UI**값을 사용 하 여 **HostProtectionResource** 열거형을 지정 하는 **HostProtectionAttribute** 을 포함 하는 형식 또는 멤버를 사용할 때를 허용 하지 않습니다. 다음 표에는 HPA (호스트 보호 특성) 값이 허용 되지 않는 **Microsoft.VisualBasic.dll** 어셈블리의 멤버 및 형식이 나와 있습니다.  
  
> [!NOTE]  
>  이 목록은 지원되는 어셈블리에서 생성되었습니다. 자세한 내용은 [Supported .NET Framework Libraries](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)을 참조하세요.  
  
|**유형 또는 멤버**|**HPA 값**|  
|------------------------|------------------------|  
|Microsoft.VisualBasic.ApplicationServices.ApplicationBase|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.ApplicationBase.ChangeCulture()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.ApplicationBase.get_Info()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.AssemblyInfo|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.BuiltInRoleConverter|SharedState|  
|Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.User|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.WebUser|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase|ExternalProcessMgmt|  
|Microsoft.VisualBasic.CompilerServices.HostServices|SharedState|  
|Microsoft.VisualBasic.CompilerServices.ProjectData.EndApp()|SelfAffectingProcessMgmt|  
|Microsoft.VisualBasic.CompilerServices.Utils.SetCultureInfo()|SelfAffectingThreading|  
|Microsoft.VisualBasic.DateAndTime.set_DateString()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.DateAndTime.set_TimeOfDay()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.DateAndTime.set_TimeString()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.DateAndTime.set_Today()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Audio|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Clock|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Computer|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.ComputerInfo|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Keyboard|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Mouse|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Network|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Ports|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.ServerComputer|ExternalProcessMgmt|  
|Microsoft.VisualBasic.FileIO.FileSystem|ExternalProcessMgmt|  
|Microsoft.VisualBasic.FileIO.SpecialDirectories|ExternalProcessMgmt|  
|Microsoft.VisualBasic.FileIO.TextFieldParser..ctor()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.FileSystem|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Interaction.CreateObject()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Interaction.DeleteSetting()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Interaction.GetObject()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Interaction.InputBox()|UI|  
|Microsoft.VisualBasic.Interaction.MsgBox()|UI|  
|Microsoft.VisualBasic.Logging.AspLog|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener..ctor()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.Close()|동기화|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.Dispose()|동기화|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.Flush()|동기화|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.GetSupportedAttributes()|동기화|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.TraceData()|동기화|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.TraceEvent()|동기화|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.Write()|동기화|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.WriteLine()|동기화|  
|Microsoft.VisualBasic.Logging.Log|ExternalProcessMgmt|  
|Microsoft.VisualBasic.MyServices.ClipboardProxy|ExternalProcessMgmt|  
|Microsoft.VisualBasic.MyServices.FileSystemProxy|ExternalProcessMgmt|  
|Microsoft.VisualBasic.MyServices.RegistryProxy|ExternalProcessMgmt|  
|Microsoft.VisualBasic.MyServices.SpecialDirectoriesProxy|ExternalProcessMgmt|  
  
## <a name="see-also"></a>참고 항목  
 [호스트 보호 특성 및 CLR 통합 프로그래밍](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [mscorlib.dll에서 허용 되지 않는 형식 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [System.dll에서 허용 되지 않는 형식 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [System.Data.dll에서 허용 되지 않는 형식 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)   
 [System.Core.dll에 허용되지 않는 유형 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
  
  
