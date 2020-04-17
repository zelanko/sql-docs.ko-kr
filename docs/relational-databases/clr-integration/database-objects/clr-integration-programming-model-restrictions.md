---
title: CLR 통합 프로그래밍 모델 제한 | 마이크로 소프트 문서
description: SQL Server는 CREATE ASSEMBLY및 런타임에 처음 등록될 때 관리되는 데이터베이스 개체에 대한 코드 검사를 수행합니다.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], programming model restrictions
- assemblies [CLR integration], CREATE ASSEMBLY checks
- programming model restrictions [CLR integration]
- assemblies [CLR integration], runtime checks
ms.assetid: 2446afc2-9d21-42d3-9847-7733d3074de9
author: rothja
ms.author: jroth
ms.openlocfilehash: 83b73909cf1844796640a83910ee609eadd7dba4
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488550"
---
# <a name="clr-integration-programming-model-restrictions"></a>CLR 통합 프로그래밍 모델 제한 사항
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  관리되는 저장 프로시저 또는 기타 관리되는 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 빌드할 때 고려해야 할 특정 코드 검사가 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]은 데이터베이스에 처음 등록될 때, **CREATE ASSEMBLY** 문을 사용하고, 런타임에 관리 코드 어셈블리에 대한 검사를 수행합니다. 실제로 런타임에 접근할 수 없는 코드 경로가 어셈블리에 있을 수 있으므로 관리 코드는 런타임에도 검사됩니다.  따라서 특히 클라이언트 환경에서 실행되는 '안전하지 않은' 코드가 있는 경우 어셈블리가 차단되지 않고 호스팅된 CLR에서 실행되지 않도록 유연성 있게 타사 어셈블리를 등록할 수 있습니다. 관리 코드가 충족해야 하는 요구 사항은 어셈블리가 **SAFE,** **EXTERNAL_ACCESS**또는 **안전하지 않음으로**등록되어 있는지 여부에 따라 달라지며 가장 엄격한 경우 **다음과** 같습니다.  
  
 관리 코드 어셈블리에 적용되는 제한뿐 아니라 부여되는 코드 보안 권한도 있습니다. CLR(공용 언어 런타임)은 관리 코드에 대해 CAS(코드 액세스 보안)라는 보안 모델을 지원합니다. 이 모델에서는 코드 ID를 기반으로 어셈블리에 사용 권한이 부여됩니다. **SAFE,** **EXTERNAL_ACCESS**및 **안전하지 않은** 어셈블리에는 서로 다른 CAS 권한이 있습니다. 자세한 내용은 [CLR 통합 코드 액세스 보안](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)을 참조하십시오.  
  
## <a name="create-assembly-checks"></a>CREATE ASSEMBLY 검사  
 CREATE **ASSEMBLY** 문을 실행하면 각 보안 수준에 대해 다음 검사가 수행됩니다.  검사가 실패하면 오류 메시지와 함께 **어셈블리 만들기가** 실패합니다.  
  
### <a name="global-any-security-level"></a>전역(모든 보안 수준)  
 참조된 모든 어셈블리가 다음 조건을 하나 이상 충족해야 합니다.  
  
-   어셈블리가 데이터베이스에 이미 등록되었습니다.  
  
-   어셈블리가 지원되는 어셈블리 중 하나입니다. 자세한 내용은 [Supported .NET Framework Libraries](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)을 참조하세요.  
  
-   위치> **에서 CREATE 어셈블리를**사용하고 있으며 참조된 모든 어셈블리와 해당 종속성은 * \<>위치에서 *사용할 수 있습니다._\<_  
  
-   _\<바이트에서_ **만들기 어셈블리를**사용 하 고 > 모든 참조는 구분 된 바이트 공간을 통해 지정 됩니다.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 모든 **EXTERNAL_ACCESS** 어셈블리는 다음 기준을 충족해야 합니다.  
  
-   정적 필드가 정보 저장에 사용되지 않습니다. 읽기 전용 정적 필드는 허용됩니다.  
  
-   PEVerify 테스트에 통과합니다. MSIL 코드 및 관련된 메타데이터가 형식 안전성 요구 사항을 충족하는지 확인하는 PEVerify 도구(peverify.exe)는 .NET Framework SDK에 포함되어 있습니다.  
  
-   동기화, 예를 들어 **Synchronization속성** 클래스와 함께 사용 되지 않습니다.  
  
-   파이널라이저 메서드가 사용되지 않습니다.  
  
 다음 사용자 지정 특성은 **EXTERNAL_ACCESS** 어셈블리에서 허용되지 않습니다.  
  
-   System.ContextStaticAttribute  
  
-   System.MTAThreadAttribute  
  
-   System.Runtime.CompilerServices.MethodImplAttribute  
  
-   System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
  
-   System.Runtime.Remoting.Contexts.ContextAttribute  
  
-   System.Runtime.Remoting.Contexts.SynchronizationAttribute  
  
-   System.Runtime.InteropServices.DllImportAttribute  
  
-   System.Security.Permissions.CodeAccessSecurityAttribute  
  
-   System.Security.SuppressUnmanagedCodeSecurityAttribute  
  
-   System.Security.UnverifiableCodeAttribute  
  
-   System.STAThreadAttribute  
  
-   System.ThreadStaticAttribute  
  
### <a name="safe"></a>SAFE  
  
-   **모든 EXTERNAL_ACCESS** 어셈블리 조건이 검사됩니다.  
  
## <a name="runtime-checks"></a>런타임 검사  
 런타임에 코드 어셈블리에서 다음 조건이 검사됩니다. 이러한 조건 중 하나가 발견되면 관리 코드를 실행할 수 없으며 예외가 throw됩니다.  
  
### <a name="unsafe"></a>UNSAFE  
 byte 배열에서 **System.Reflection.Assembly.Load()** 메서드를 호출하거나 **Reflection.Emit** 네임스페이스를 사용하여 암시적으로 어셈블리를 로드하는 것은 허용되지 않습니다.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 모든 **안전하지 않은** 조건이 검사됩니다.  
  
 지원되는 어셈블리 목록에서 다음 HPA(호스트 보호 특성) 값이 주석으로 추가된 유형과 멤버는 모두 허용되지 않습니다.  
  
-   SelfAffectingProcessMgmt  
  
-   SelfAffectingThreading  
  
-   동기화  
  
-   SharedState  
  
-   ExternalProcessMgmt  
  
-   ExternalThreading  
  
-   SecurityInfrastructure  
  
-   MayLeakOnAbort  
  
-   UI  
  
 HPA 및 지원되는 어셈블리에서 허용되지 않는 형식 및 멤버 목록에 대한 자세한 내용은 [호스트 보호 특성 및 CLR 통합 프로그래밍을](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)참조하십시오.  
  
### <a name="safe"></a>SAFE  
 모든 **EXTERNAL_ACCESS** 조건이 검사됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [지원되는 .NET 프레임워크 라이브러리](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)   
 [CLR 통합 코드 액세스 보안](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [호스트 보호 특성 및 CLR 통합 프로그래밍](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [어셈블리 만들기](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
