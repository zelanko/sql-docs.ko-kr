---
title: 어셈블리 디자인 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- designing assemblies [SQL Server]
- assemblies [CLR integration], designing
ms.assetid: 9c07f706-6508-41aa-a4d7-56ce354f9061
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ad5135eb8141cc84bc6e5bddc8bd8477f4699b9e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62874926"
---
# <a name="designing-assemblies"></a>어셈블리 디자인
  이 항목에서는 어셈블리를 디자인할 때 고려해야 할 다음 요소들에 대해 설명합니다.  
  
-   어셈블리 패키징  
  
-   어셈블리 보안 관리  
  
-   어셈블리에 대한 제한  
  
## <a name="packaging-assemblies"></a>어셈블리 패키징  
 어셈블리에는 해당 클래스 및 메서드에 두 개 이상의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 루틴 및 유형에 대한 기능이 포함될 수 있습니다. 대부분의 경우, 특히 이러한 루틴의 메서드가 상호 호출하는 클래스를 공유하는 경우에는 관련된 기능을 수행하는 루틴의 기능을 같은 어셈블리 내에 패키징하는 것이 바람직합니다. 예를 들어 CLR(공용 언어 런타임) 트리거와 CLR 저장 프로시저에 대한 데이터 항목 관리 태스크를 수행하는 클래스를 같은 어셈블리에 패키징할 수 있습니다. 그 이유는 이러한 클래스에 대한 메서드가 덜 관련된 태스크 보다는 상호 호출할 가능성이 높기 때문입니다.  
  
 코드를 어셈블리에 패키징할 때는 다음을 고려해야 합니다.  
  
-   CLR 사용자 정의 함수에 의존하는 CLR 사용자 정의 유형 및 인덱스는 영구 데이터가 어셈블리에 의존하는 데이터베이스에 포함되도록 만들 수 있습니다. 어셈블리의 코드를 수정하면 데이터베이스에 있는 어셈블리에 의존하는 영구 데이터가 있는 경우 보다 복잡해지는 경우가 많습니다. 따라서 일반적으로 사용자 정의 유형과 사용자 정의 함수를 사용하는 인덱스와 같이 영구 데이터 종속 관계에 의존하는 코드를 이러한 영구 데이터 종속 관계가 없는 코드와 구분하는 것이 좋습니다. 자세한 내용은 [어셈블리 구현](assemblies-implementing.md) 및 [ALTER ASSEMBLY &#40;transact-sql&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)를 참조 하세요.  
  
-   관리 코드의 조각에 더 높은 사용 권한이 필요한 경우 해당 코드를 높은 사용 권한이 필요하지 않은 코드와 별개의 어셈블리로 구분하는 것이 좋습니다.  
  
## <a name="managing-assembly-security"></a>어셈블리 보안 관리  
 관리 코드를 실행할 때 .NET Code Access Security로 보호되는 리소스를 어셈블리에서 어느 정도까지 액세스할 수 있는지를 제어할 수 있습니다. 이렇게 하려면 어셈블리를 만들거나 수정할 때 SAFE, EXTERNAL_ACCESS 또는 UNSAFE의 세 가지 권한 집합 중 하나를 지정 합니다.  
  
### <a name="safe"></a>SAFE  
 SAFE는 기본 사용 권한 집합이며 가장 제한적입니다. SAFE 권한을 사용하여 어셈블리에서 실행한 코드는 파일, 네트워크, 환경 변수 또는 레지스트리와 같은 외부 시스템 리소스에 액세스할 수 없습니다. SAFE 코드는 로컬 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의 데이터에 액세스하거나 로컬 데이터베이스 외부의 리소스에 액세스하지 않는 계산 및 비즈니스 논리를 수행할 수 있습니다.  
  
 대부분의 어셈블리는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 외부에 있는 리소스에 액세스할 필요 없이 계산 및 데이터 관리 태스크를 수행합니다. 따라서 어셈블리 사용 권한 집합으로 SAFE를 사용하는 것이 좋습니다.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS를 사용하면 어셈블리에서 파일, 네트워크, 웹 서비스, 환경 변수 및 레지스트리와 같은 특정 외부 시스템 리소스에 액세스할 수 있습니다. EXTERNAL ACCESS 권한이 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인만 EXTERNAL_ACCESS 어셈블리를 만들 수 있습니다.  
  
 SAFE 및 EXTERNAL_ACCESS 어셈블리에는 검증적으로 안전한 유형의 코드만 포함될 수 있습니다. 즉, 이러한 어셈블리에서만 유형 정의에 유효한 잘 정의된 진입점을 통해 클래스에 액세스할 수 있습니다. 따라서 이러한 유형은 코드에서 소유하지 않은 메모리 버퍼에 임의로 액세스할 수 없습니다. 또한 이러한 어셈블리는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로세스의 견고성에 악영향을 줄 수 있는 작업을 수행할 수 없습니다.  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE는 어셈블리에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내부 및 외부의 리소스에 대한 무제한적인 액세스를 제공합니다. UNSAFE 어셈블리 내에서 실행되는 코드는 비관리 코드를 호출할 수 있습니다.  
  
 또한 UNSAFE를 지정하면 어셈블리에 있는 코드에서 CLR 확인 프로그램에 의해 안전하지 않은 유형으로 간주되는 작업을 수행할 수 있습니다. 이러한 작업은 제어되지 않는 방식으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로세스 공간에서 메모리 버퍼에 액세스할 가능성이 있습니다. UNSAFE 어셈블리는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 공용 언어 런타임 중 하나의 보안 시스템을 손상시킬 수도 있습니다. UNSAFE 권한은 숙련된 개발자 또는 관리자가 가장 신뢰할 수 있는 어셈블리에만 부여해야 합니다. **Sysadmin** 고정 서버 역할의 멤버만 UNSAFE 어셈블리를 만들 수 있습니다.  
  
## <a name="restrictions-on-assemblies"></a>어셈블리에 대한 제한  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 어셈블리를 안정적이고 확장 가능한 방식으로 실행할 수 있도록 보장하기 위해 어셈블리에 있는 관리 코드에 특정 제한을 지정합니다. 즉, 서버의 견고성을 손상시킬 수 있는 작업은 SAFE 및 EXTERNAL_ACCESS 어셈블리에서 허용되지 않습니다.  
  
### <a name="disallowed-custom-attributes"></a>허용되지 않는 사용자 지정 특성  
 다음과 같은 사용자 지정 특성으로는 어셈블리에 주석을 지정할 수 없습니다.  
  
```  
System.ContextStaticAttribute  
System.MTAThreadAttribute  
System.Runtime.CompilerServices.MethodImplAttribute  
System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
System.Runtime.Remoting.Contexts.ContextAttribute  
System.Runtime.Remoting.Contexts.SynchronizationAttribute  
System.Runtime.InteropServices.DllImportAttribute   
System.Security.Permissions.CodeAccessSecurityAttribute  
System.STAThreadAttribute  
System.ThreadStaticAttribute  
```  
  
 또한 SAFE 및 EXTERNAL_ACCESS 어셈블리에는 다음과 같은 사용자 지정 특성으로 주석을 지정할 수 없습니다.  
  
```  
System.Security.SuppressUnmanagedCodeSecurityAttribute  
System.Security.UnverifiableCodeAttribute  
```  
  
### <a name="disallowed-net-framework-apis"></a>허용되지 않는 .NET Framework API  
 허용 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 되지 않는 **HostProtectionAttributes** 중 하나를 사용 하 여 주석이 추가 된 모든 API는 SAFE 및 EXTERNAL_ACCESS 어셈블리에서 호출할 수 없습니다.  
  
```  
eSelfAffectingProcessMgmt  
eSelfAffectingThreading  
eSynchronization  
eSharedState   
eExternalProcessMgmt  
eExternalThreading  
eSecurityInfrastructure  
eMayLeakOnAbort  
eUI  
```  
  
### <a name="supported-net-framework-assemblies"></a>지원되는 .NET Framework 어셈블리  
 CREATE ASSEMBLY를 사용하여 사용자 지정 어셈블리에서 참조하는 모든 어셈블리를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 로드해야 합니다. 다음 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 어셈블리는 이미 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 로드되어 있으므로 CREATE ASSEMBLY를 사용하지 않아도 사용자 지정 어셈블리에서 참조할 수 있습니다.  
  
```  
custommarshallers.dll  
Microsoft.visualbasic.dll  
Microsoft.visualc.dll  
mscorlib.dll  
system.data.dll  
System.Data.SqlXml.dll  
system.dll  
system.security.dll  
system.web.services.dll  
system.xml.dll  
System.Transactions  
System.Data.OracleClient  
System.Configuration  
```  
  
## <a name="see-also"></a>참고 항목  
 [어셈블리 &#40;데이터베이스 엔진&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [CLR 통합 보안](security/clr-integration-security.md)  
  
  
