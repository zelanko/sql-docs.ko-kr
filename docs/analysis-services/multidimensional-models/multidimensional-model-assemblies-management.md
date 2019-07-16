---
title: 다차원 모델 어셈블리 관리 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5b7b04f074dcd11eec022a689f865454681d2ae8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165722"
---
# <a name="multidimensional-model-assemblies-management"></a>다차원 모델 어셈블리 관리
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 MDX(Multidimensional Expressions) 및 DMX(Data Mining Extensions) 언어에 사용할 수 있는 다양한 내장 함수를 제공합니다. 이러한 함수를 사용하여 표준 통계 계산을 비롯하여 계층에서의 멤버 이동에 이르는 모든 작업을 수행할 수 있습니다. 그러나 복잡하고 강력한 다른 제품에서도 그렇듯이 제품의 기능을 더 확장할 필요성은 언제나 있기 마련입니다.  
  
 따라서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 또는 데이터베이스에 어셈블리를 추가할 수 있습니다. 어셈블리를 사용하면 Microsoft Visual Basic .NET 또는 Microsoft Visual C#과 같은 CLR(공용 언어 런타임) 언어를 사용하여 사용자 정의 외부 함수를 만들 수 있습니다. 또한 Microsoft Visual Basic 또는 Microsoft Visual C++와 같은 COM(구성 요소 개체 모델) 자동화 언어도 사용할 수 있습니다.  
  
> [!IMPORTANT]  
>  COM 어셈블리는 보안 위험을 내포할 수 있습니다. 이러한 위험 및 기타 고려 사항으로 인해 COM 어셈블리는 [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]에서 더 이상 사용되지 않습니다. COM 어셈블리는 후속 릴리스에서 지원되지 않을 수 있습니다.  
  
 어셈블리를 사용하면 MDX와 DMX의 비즈니스 기능을 확장할 수 있습니다. 원하는 기능을 작성하여 DLL(동적 링크 라이브러리)과 같은 라이브러리에 추가한 후 이 라이브러리를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 어셈블리로 추가하면 됩니다. 그런 다음 MDX 및 DMX 식, 프로시저, 계산, 동작 및 클라이언트 애플리케이션에서 라이브러리의 공용 메서드를 사용자 정의 함수로 사용할 수 있습니다.  
  
 새 프로시저와 함수가 포함된 어셈블리는 서버에 추가할 수 있습니다. 어셈블리를 사용하여 서버에서 제공하지 않는 사용자 지정 기능을 향상시키거나 추가할 수 있으며, MDX(Multidimensional Expressions), DMX(Data Mining Extensions) 또는 저장 프로시저에 새 함수를 추가할 수도 있습니다. 어셈블리는 사용자 지정 애플리케이션이 실행되는 위치에서 로드되며 어셈블리 이진 파일의 복사본은 서버에 데이터베이스 데이터와 함께 저장됩니다. 어셈블리가 제거되면 복사된 어셈블리도 서버에서 제거됩니다.  
  
 어셈블리는 두 가지 형식의 수 있습니다. COM 및 CLR입니다. CLR 어셈블리는 C#, Visual Basic .NET, Managed C++ 등의 .NET Framework 프로그래밍 언어로 개발됩니다. COM 어셈블리는 서버에 등록해야 하는 COM 라이브러리입니다.  
  
 어셈블리는 <xref:Microsoft.AnalysisServices.Server> 또는 <xref:Microsoft.AnalysisServices.Database> 개체에 추가할 수 있습니다. 서버 어셈블리는 서버에 연결된 사용자나 서버에 있는 개체가 호출할 수 있습니다. 데이터베이스 어셈블리는 데이터베이스에 연결된 <xref:Microsoft.AnalysisServices.Database> 개체 또는 사용자만 호출할 수 있습니다.  
  
 단순 <xref:Microsoft.AnalysisServices.Assembly> 개체는 기본 정보(이름 및 ID), 파일 컬렉션 및 보안 사양으로 구성되어 있습니다.  
  
 파일 컬렉션은 디버깅 파일이 어셈블리 파일을 통해 로드된 경우 로드된 어셈블리 파일과 해당 디버깅 파일(.pdb)을 참조합니다. 어셈블리 파일은 애플리케이션이 해당 파일을 정의한 위치에서 로드되면 복사본은 서버에 데이터와 함께 저장됩니다. 어셈블리 파일의 복사본은 서버가 시작될 때마다 어셈블리를 로드하는 데 사용됩니다.  
  
 보안 사양에는 어셈블리를 실행하는 데 사용되는 권한 집합과 가장이 포함되어 있습니다.  
  
## <a name="calling-user-defined-functions"></a>사용자 정의 함수 호출  
 어셈블리의 사용자 정의 함수를 호출하는 방법은 전부 정규화된 이름을 사용해야 한다는 것을 제외하고는 내장 함수를 호출하는 방법과 동일합니다. 예를 들어 다음과 같이 MDX 쿼리에는 MDX에서 필요한 형식을 반환하는 사용자 정의 함수가 포함됩니다.  
  
```  
Select MyAssembly.MyClass.MyStoredProcedure(a, b, c) on 0 from Sales  
```  
  
 사용자 정의 함수는 CALL 키워드를 사용하여 호출할 수도 있습니다. CALL 키워드는 레코드 집합이나 void 값을 반환하는 사용자 정의 함수에 사용해야 합니다. 현재 큐브 또는 데이터 마이닝 모델과 같이 MDX 또는 DMX 문이나 스크립트의 컨텍스트 내에 있는 개체에 사용자 정의 함수가 종속되어 있는 경우에는 CALL 키워드를 사용할 수 없습니다. MDX 또는 DMX 쿼리 외부에서 호출되는 함수는 대개 관리 기능을 수행하기 위해 AMO 개체 모델을 사용할 때 사용합니다. 예를 들어 MDX 문에서 `MyVoidProcedure(a, b, c)` 함수를 사용하려면 다음과 같은 구문을 사용합니다.  
  
```  
Call MyAssembly.MyClass.MyVoidProcedure(a, b, c)  
```  
  
 어셈블리를 사용하면 공통 코드를 개발한 후 이를 단일 위치에 저장하여 재사용할 수 있으므로 데이터베이스 개발이 간편해집니다. 클라이언트 소프트웨어 개발자는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 대한 함수 라이브러리를 만들어 해당 애플리케이션과 함께 배포할 수 있습니다.  
  
 어셈블리와 사용자 정의 함수 이름은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 함수 라이브러리의 함수 이름 또는 다른 어셈블리의 함수 이름과 중복되게 지정할 수 있습니다. 해당 정규화된 이름을 사용하여 사용자 정의 함수를 호출하기만 하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 올바른 프로시저를 사용할 수 있습니다. 보안을 유지하고 다른 클래스 라이브러리에 있는 중복 이름을 호출하는 것을 방지하기 위해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 저장 프로시저에 정규화된 이름만 사용해야 합니다.  
  
 특정 CLR 어셈블리에서 사용자 정의 함수를 호출하려면 다음과 같이 사용자 정의 함수 앞에 어셈블리 이름, 전체 클래스 이름 및 프로시저 이름이 와야 합니다.  
  
 *AssemblyName*.*FullClassName*.*ProcedureName*(*Argument1*, *Argument2*, ...)  
  
 이전 버전의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]와의 호환성을 위해 다음과 같은 구문도 사용할 수 있습니다.  
  
 *AssemblyName*!*FullClassName*!*ProcedureName*(*Argument1*, *Argument2*, ...)  
  
 COM 라이브러리가 다중 인터페이스를 지원하는 경우에는 다음과 같이 인터페이스 ID를 사용하여 프로시저 이름을 지정할 수도 있습니다.  
  
 *AssemblyName*!*InterfaceID*!*ProcedureName*(*Argument1*, *Argument2*, ...)  
  
## <a name="security"></a>보안  
 어셈블리 보안은 코드 액세스 보안 모델인 .NET Framework 보안 모델에 기반을 둡니다. .NET Framework는 런타임에서 완전히 신뢰할 수 있는 코드와 부분적으로 신뢰할 수 있는 코드를 모두 호스팅할 수 있다고 가정하는 코드 액세스 보안 메커니즘을 지원합니다. 일반적으로 .NET Framework 코드 액세스 보안을 통해 보호되는 리소스는 액세스를 허용하기 전에 먼저 해당 사용 권한을 요구하는 관리 코드에 의해 래핑됩니다. 사용 권한 요청은 호출 스택의 어셈블리 수준에 있는 모든 호출자가 해당 리소스 사용 권한을 가지고 있는 경우에만 충족됩니다.  
  
 어셈블리의 경우 **PermissionSet** 개체에 **Assembly** 속성이 설정된 상태로 실행 권한이 전달됩니다. 관리 코드가 받게 되는 사용 권한은 적용된 보안 정책에 따라 결정됩니다. 세 가지 수준의 정책 적용에 비-되어 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 호스 티 드 환경: enterprise, 컴퓨터 및 사용자. 코드가 받게 되는 유효한 사용 권한 목록은 이 3가지 수준에서 확보하는 사용 권한의 공통 사항에 따라 결정됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 CLR을 호스트하면서 호스트 수준 보안 정책을 CLR에 제공합니다. 이 정책은 항상 적용되는 위의 3가지 정책 수준 아래에 있는 추가 정책 수준입니다. 이 정책은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 만든 모든 애플리케이션 도메인에 대해 설정됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 호스트 수준 정책은 시스템 어셈블리에 대한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 고정 정책과 사용자 어셈블리에 대한 사용자 지정 정책을 조합한 것입니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 호스트 정책에서 사용자 지정 부분은 어셈블리 소유자가 각 어셈블리에 대한 3가지 권한 집합 중 어떤 것을 지정하는지에 따라 달라집니다.  
  
|권한 설정|Description|  
|------------------------|-----------------|  
|**안전**|내부 계산 권한을 부여합니다. 이 권한 집합은 .NET Framework의 보호된 리소스에 대해서는 액세스 권한을 할당하지 않습니다. **PermissionSet** 속성에 아무 것도 지정되지 않은 경우 어셈블리의 기본 권한 집합입니다.|  
|**ExternalAccess**|**Safe** 설정과 동일한 액세스 권한을 부여하며 외부 시스템 리소스에 액세스할 수 있는 권한을 추가로 제공합니다. 이 권한 집합은 이 시나리오상에서 유효한 것이며 보안을 보장하지는 않습니다. 그러나 안정성은 유지됩니다.|  
|**불안**|제한을 두지 않습니다. 이 권한 집합으로 실행되는 관리 코드에 대해서는 어떠한 보안이나 안정성도 보장되지 않습니다. 이 신뢰 수준에서 실행되는 코드에는 관리자가 포함한 사용자 지정 권한을 비롯하여 모든 권한이 부여됩니다.|  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 CLR를 호스팅하는 경우에는 스택 워크(stack-walk) 기반의 권한 확인이 네이티브 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 코드와의 경계에서 중지됩니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 어셈블리의 모든 관리 코드는 항상 위의 3가지 사용 권한 범주 중 하나에 속합니다.  
  
 COM 또는 관리되지 않는 어셈블리 루틴은 CLR 보안 모델을 지원하지 않습니다.  
  
### <a name="impersonation"></a>가장  
 관리 코드가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]외부의 리소스에 액세스할 때마다 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 어셈블리의 **ImpersonationMode** 속성 설정과 관련된 규칙을 따라 적절한 Windows 보안 컨텍스트에서 액세스가 이루어지도록 합니다. **Safe** 권한 설정을 사용하는 어셈블리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]외부의 리소스에 액세스할 수 없으므로 이러한 규칙은 **ExternalAccess** 및 **Unsafe** 권한 설정을 사용하는 어셈블리에만 적용됩니다.  
  
-   현재의 실행 컨텍스트가 Windows 인증 로그인과 일치하며 원래 호출자의 컨텍스트와 동일한 경우(즉, 중간에 EXECUTE AS가 없는 경우) [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 리소스에 액세스하기 전에 먼저 Windows 인증 로그인을 가장합니다.  
  
-   중간에 EXECUTE AS가 있어서 컨텍스트가 원래 호출자의 컨텍스트와 다르게 변경된 경우에는 외부 리소스에 액세스할 수 없습니다.  
  
 **ImpersonationMode** 속성은 **ImpersonateCurrentUser** 또는 **ImpersonateAnonymous**로 설정할 수 있습니다. 기본 설정 **ImpersonateCurrentUser**는 현재 사용자의 네트워크 로그인 계정으로 어셈블리를 실행합니다. **ImpersonateAnonymous** 설정을 사용하면 실행 컨텍스트가 서버의 Windows 로그인 사용자 계정인 IUSER_*servername* 과 일치하게 됩니다. 이 계정은 서버에 대해 제한된 권한을 갖는 인터넷 게스트 계정입니다. 이 컨텍스트에서 실행되는 어셈블리는 로컬 서버의 제한된 리소스에만 액세스할 수 있습니다.  
  
### <a name="application-domains"></a>애플리케이션 도메인  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 응용 프로그램 도메인을 직접 노출시키지 않습니다. 동일한 애플리케이션 도메인에서 실행되는 어셈블리 집합으로 인해 애플리케이션 도메인은 .NET Framework의 **System.Reflection** 네임스페이스를 사용하거나 다른 방법으로 실행 시 서로를 검색할 수 있으며 런타임에 바인딩된 방식으로 애플리케이션을 호출할 수 있습니다. 이러한 호출에 대해서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 권한 부여 기반의 보안 방식에서 사용되는 권한 확인이 수행됩니다.  
  
 애플리케이션 도메인 경계와 각 도메인에 속하는 어셈블리는 구현에 따라 달라지므로 동일한 애플리케이션 도메인 내에서 어셈블리를 찾는 방법에만 의존해서는 안 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [저장된 프로시저에 대 한 보안을 설정합니다.](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)   
 [저장된 프로시저 정의](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
