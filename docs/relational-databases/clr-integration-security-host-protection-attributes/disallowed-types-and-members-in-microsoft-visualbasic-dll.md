---
title: 형식 및 멤버 Microsoft.VisualBasic.dll에 허용 되지 않는 | Microsoft Docs
ms.custom: ''
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
manager: craigg
ms.openlocfilehash: 76f71a4920e2980161032c519eb1fb3dacd12da3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47844421"
---
# <a name="disallowed-types-and-members-in-microsoftvisualbasicdll"></a>Microsoft.VisualBasic.dll에 허용되지 않는 유형 및 멤버
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공용 언어 통합 (CLR) 프로그래밍 형식 또는 멤버에는 사용할 수 없게 하는 **HostProtectionAttribute** 를 지정 하는 **System.Security.Permissions.HostProtectionResource** 열거형의 값을 사용 하 여 **ExternalProcessMgmt**, **ExternalThreading**하십시오 **MayLeakOnAbort**, **SecurityInfrastructure**, **SelfAffectingProcessMgmnt**합니다 **SelfAffectingThreading**, **: SharedState**, **동기화**, 또는 **UI**합니다. 다음 표에서의 형식과 멤버를 **Microsoft.VisualBasic.dll** 인 HPA (호스트 보호 특성) 값이 허용 되지 않는 어셈블리입니다.  
  
> [!NOTE]  
>  이 목록은 지원되는 어셈블리에서 생성되었습니다. 자세한 내용은 [Supported .NET Framework Libraries](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)을 참조하세요.  
  
|**형식 또는 멤버**|**HPA 값**|  
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
|Microsoft.VisualBasic.Logging.FileLogTraceListener.Close()|Synchronization|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.Dispose()|Synchronization|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.Flush()|Synchronization|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.GetSupportedAttributes()|Synchronization|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.TraceData()|Synchronization|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.TraceEvent()|Synchronization|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.Write()|Synchronization|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.WriteLine()|Synchronization|  
|Microsoft.VisualBasic.Logging.Log|ExternalProcessMgmt|  
|Microsoft.VisualBasic.MyServices.ClipboardProxy|ExternalProcessMgmt|  
|Microsoft.VisualBasic.MyServices.FileSystemProxy|ExternalProcessMgmt|  
|Microsoft.VisualBasic.MyServices.RegistryProxy|ExternalProcessMgmt|  
|Microsoft.VisualBasic.MyServices.SpecialDirectoriesProxy|ExternalProcessMgmt|  
  
## <a name="see-also"></a>관련 항목  
 [호스트 보호 특성 및 CLR 통합 프로그래밍](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Mscorlib.dll에 허용 되지 않는 유형 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [Disallowed Types and Members in System.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [System.Data.dll에 허용 되지 않는 유형 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)   
 [System.Core.dll에 허용되지 않는 형식 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
  
  
