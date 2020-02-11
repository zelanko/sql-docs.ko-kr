---
title: 호스트 보호 특성 및 CLR 통합 프로그래밍 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- HostProtectionAttribute [CLR integration]
- common language runtime [SQL Server], host protection attributes
- disallowed types and members [CLR integration]
- common language runtime [SQL Server], disallowed types and members
- HPAs [CLR integration]
ms.assetid: 268078df-63ca-4c03-a8e7-7108bcea9697
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 68f1f114002ab0ef38c7565a523723a06958048d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62874349"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>호스트 보호 특성 및 CLR 통합 프로그래밍
  CLR(공용 언어 런타임)은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]부터 시작하여, [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]와 같은 CLR 호스트에 유용할 수 있는 특성으로 .NET Framework의 일부인 관리되는 API(응용 프로그래밍 인터페이스)에 주석을 추가하는 메커니즘을 제공합니다. 이러한 HPA(호스트 보호 특성)의 예는 다음과 같습니다.  
  
-   
  `SharedState`: API가 공유 상태(예: 정적 클래스 필드)를 만들거나 관리하는 기능을 노출하는지 여부를 나타냅니다.  
  
-   
  `Synchronization`: API가 스레드 간 동기화 기능을 노출하는지 여부를 나타냅니다.  
  
-   
  `ExternalProcessMgmt`: API가 호스트 프로세스 제어 기능을 노출하는지 여부를 나타냅니다.  
  
 이러한 특성을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 CAS(코드 액세스 보안)를 통해 호스팅된 환경에서 허용하지 않는 HPA 목록을 지정합니다. CAS 요구 사항은 3가지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 권한 집합인 `SAFE`, `EXTERNAL_ACCESS` 또는 `UNSAFE` 중 하나에 의해 지정됩니다. 이러한 세 보안 수준 중 하나는 `CREATE ASSEMBLY` 문을 사용하여 어셈블리를 서버에 등록할 때 지정됩니다. 
  `SAFE` 또는 `EXTERNAL_ACCESS` 권한 집합 내에서 실행되는 코드는 `System.Security.Permissions.HostProtectionAttribute` 특성이 적용된 특정 유형이나 멤버를 사용해서는 안 됩니다. 자세한 내용은 [어셈블리 만들기](../clr-integration/assemblies/creating-an-assembly.md) 및 [CLR 통합 프로그래밍 모델 제한](../clr-integration/database-objects/clr-integration-programming-model-restrictions.md)을 참조 하세요.  
  
 
  `HostProtectionAttribute`는 호스트가 허용하지 않는 특정 코드 구문을 유형이나 메서드로 식별한다는 점에서 안정성 향상 방법일 뿐 보안 권한은 아닙니다. 
  `HostProtectionAttribute`를 사용하면 호스트의 안정성을 보호하도록 돕는 프로그래밍 모델이 적용됩니다.  
  
## <a name="host-protection-attributes"></a>호스트 보호 특성  
 HPA는 호스트 프로그래밍 모델에 맞지 않고 다음과 같이 안정성 위협의 증가 수준을 나타내는 형식이나 멤버를 식별합니다.  
  
-   심각하지 않습니다.  
  
-   서버에서 관리하는 사용자 코드를 불안정하게 만들 수 있습니다.  
  
-   서버 프로세스 자체를 불안정하게 만들 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]값이 `HostProtectionAttribute` `System.Security.Permissions.HostProtectionResource` `ExternalProcessMgmt`, `ExternalThreading`, `MayLeakOnAbort` `SecurityInfrastructure`, `Synchronization` `UI`,, `SelfAffectingProcessMgmnt`,, 또는 인 열거형을 지정 하는가 있는 형식 또는 멤버의 사용을 허용 하지 않습니다. `SelfAffectingThreading` `SharedState` 이로 인해 상태를 공유할 수 있게 하거나, 동기화를 수행하거나, 종료할 때 리소스 누출을 일으키거나 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스의 무결성에 영향을 주는 멤버를 어셈블리가 호출할 수 없습니다.  
  
### <a name="disallowed-types-and-members"></a>허용되지 않는 유형 및 멤버  
 다음 항목에서는 `HostProtectionResource`에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값이 허용되지 않는 유형과 멤버를 식별합니다.  
  
> [!NOTE]  
>  이러한 항목에 있는 목록은 지원되는 어셈블리에서 생성되었습니다.  자세한 내용은 [Supported .NET Framework Libraries](../clr-integration/database-objects/supported-net-framework-libraries.md)을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [Microsoft.VisualBasic.dll에 허용되지 않는 유형 및 멤버](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 HPA 값이 허용되지 않는 Microsoft.VisualBasic.dll의 유형 및 멤버가 나열되어 있습니다.  
  
 [mscorlib.dll에 허용되지 않는 유형 및 멤버](disallowed-types-and-members-in-mscorlib-dll.md)  
 HPA 값이 허용되지 않는 mscorlib.dll의 유형 및 멤버를 표시합니다.  
  
 [Disallowed Types and Members In System.dll](disallowed-types-and-members-in-system-dll.md)  
 HPA 값이 허용되지 않는 System.dll의 유형 및 멤버를 표시합니다.  
  
 [System.Data.dll에 허용되지 않는 유형 및 멤버](disallowed-types-and-members-in-system-data-dll.md)  
 HPA 값이 허용되지 않는 System.Data.dll의 유형 및 멤버를 표시합니다.  
  
 [System.Core.dll에 허용되지 않는 유형 및 멤버](disallowed-types-and-members-in-system-core-dll.md)  
 HPA 값이 허용되지 않는 System.Core.dll의 유형 및 멤버를 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CLR 통합 코드 액세스 보안](../clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 통합 프로그래밍 모델 제한 사항](../clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [어셈블리 만들기](../clr-integration/assemblies/creating-an-assembly.md)  
  
  
