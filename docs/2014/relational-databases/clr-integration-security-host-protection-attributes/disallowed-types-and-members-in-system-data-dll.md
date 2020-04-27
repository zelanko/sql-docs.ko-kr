---
title: System.object에서 허용 되지 않는 형식 및 멤버 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4233bc1ddd98d6fe678d9d37f1acd7a4b66b687e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62874365"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>System.Data.dll에 허용되지 않는 유형 및 멤버
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CLR (공용 `HostProtectionAttribute` 언어 통합) 프로그래밍에서는 `System.Security.Permissions.HostProtectionResource` `ExternalProcessMgmt`, `ExternalThreading` `MayLeakOnAbort` `SecurityInfrastructure` `SelfAffectingProcessMgmnt` `SelfAffectingThreading`,,,,, **sharedstate**, `Synchronization`또는 `UI`값을 사용 하 여 열거형을 지정 하는가 있는 형식 또는 멤버를 사용할 때를 허용 하지 않습니다. 다음 표에는 HPA(호스트 보호 특성) 값이 허용되지 않는 System.Data.dll 어셈블리의 멤버 및 유형이 나열되어 있습니다.  
  
> [!NOTE]  
>  이 목록은 지원되는 어셈블리에서 생성되었습니다. 자세한 내용은 [Supported .NET Framework Libraries](../clr-integration/database-objects/supported-net-framework-libraries.md)을 참조하세요.  
  
|유형 또는 멤버|HPA 값|  
|--------------------|--------------------|  
|System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteReader()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency..ctor()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Start()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Stop()|ExternalThreading|  
|System.Data.TypedDataSetGenerator|SharedState, Synchronization|  
|System.Xml.XmlDataDocument|동기화|  
  
## <a name="see-also"></a>참고 항목  
 [호스트 보호 특성 및 CLR 통합 프로그래밍](host-protection-attributes-and-clr-integration-programming.md)   
 [Microsoft.visualbasic에 허용 되지 않는 형식 및 멤버](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Mscorlib.dll에 허용 되지 않는 형식 및 멤버](disallowed-types-and-members-in-mscorlib-dll.md)   
 [System.object의 허용 되지 않는 형식 및 멤버](disallowed-types-and-members-in-system-dll.md)   
 [System.Core.dll에 허용되지 않는 유형 및 멤버](disallowed-types-and-members-in-system-core-dll.md)  
  
  
