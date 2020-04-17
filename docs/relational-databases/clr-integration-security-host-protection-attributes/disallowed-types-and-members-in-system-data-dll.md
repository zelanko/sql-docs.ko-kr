---
title: System에서 허용되지 않는 유형 및 멤버.Data.dll | 마이크로 소프트 문서
descriptions: SQL Server CLR programming disallows a type or member with some values for the HostProtectionResource enum. This article lists System.Data.dll disallowed values.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
author: rothja
ms.author: jroth
ms.openlocfilehash: a8f875476d5509c538b2fb47575b94369a5e1186
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486878"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>System.Data.dll에 허용되지 않는 유형 및 멤버
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]공통 언어 통합 (CLR) 프로그래밍은 **System.Security.Permission.HostProtectionResource** 열거형 **외부 프로세스Mgmt,** **외부 스레딩,** **MayLeakOnAbort,** **보안 인프라,** **Self비런싱 프로세스Mgmnt,** **Self비런싱스런싱, 공유** **상태,** **동기화,** 또는 **UI를**지정하는 **호스트 보호 특성이** 있는 형식 또는 멤버의 사용을 허용하지 않습니다. 다음 표에는 HPA(호스트 보호 특성) 값이 허용되지 않는 System.Data.dll 어셈블리의 멤버 및 유형이 나열되어 있습니다.  
  
> [!NOTE]  
>  이 목록은 지원되는 어셈블리에서 생성되었습니다. 자세한 내용은 [Supported .NET Framework Libraries](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)을 참조하세요.  
  
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
 [호스트 보호 특성 및 CLR 통합 프로그래밍](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Microsoft.VisualBasic.dll에서 허용되지 않는 형식 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [mscorlib.dll에서 허용되지 않는 형식 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [System.dll에서 허용되지 않는 형식 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [System.Core.dll에 허용되지 않는 유형 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
  
  
