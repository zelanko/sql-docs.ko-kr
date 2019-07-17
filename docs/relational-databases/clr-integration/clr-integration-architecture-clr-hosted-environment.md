---
title: CLR 호스 티 드 환경 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- type-safe code [CLR integration]
- UNSAFE permission set
- run-time environments [CLR integration]
- common language runtime [SQL Server], about CLR integration
- application domains [CLR integration]
- host protection attributes [CLR integration]
- managed code [SQL Server], common language runtime
- permission sets [CLR integration]
- reliability [CLR integration]
- SAFE permission set
- code access security [CLR integration]
- EXTERNAL_ACCESS permission set
- verifying type safety
- scalability [CLR integration]
- hosted environments [CLR integration]
- HPAs [CLR integration]
ms.assetid: d280d359-08f0-47b5-a07e-67dd2a58ad73
author: rothja
ms.author: jroth
ms.openlocfilehash: cdef6129f6cdc513382a747e82d84dd27fc433eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068486"
---
# <a name="clr-integration-architecture---clr-hosted-environment"></a>CLR 통합 아키텍처 - CLR 호스팅 환경
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  .NET Framework CLR(공용 언어 런타임)과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 통합을 사용하면 데이터베이스 프로그래머가 Visual C#, Visual Basic .NET, 및 Visual C++와 같은 언어를 사용할 수 있습니다. 프로그래머가 이러한 언어를 사용하여 작성할 수 있는 비즈니스 논리의 종류에는 함수, 저장 프로시저, 트리거, 데이터 형식, 집계 등이 포함됩니다.  
  
  CLR에는 가비지 수집되는 메모리, 선점형 스레딩, 메타데이터 서비스(형식 리플렉션), 코드 안정성, 코드 액세스 보안 등의 기능이 있습니다. CLR에서는 메타데이터를 사용하여 클래스를 찾아 로드하고, 메모리에 인스턴스를 배치하고, 메서드 호출을 확인하고, 네이티브 코드를 생성하고, 보안을 강화하며, 런타임 컨텍스트 경계를 설정합니다.  
  
 CLR과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 모두 런타임 환경이지만 메모리, 스레드 및 동기화를 처리하는 방식에 있어서 서로 다릅니다. 이 항목에서는 모든 시스템 리소스가 균일하게 관리되도록 이 두 런타임이 어떻게 통합되는지에 대해 설명합니다. 또한 안정적이고 안전한 사용자 코드 실행 환경을 제공하기 위해 CLR CAS(코드 액세스 보안)와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안이 통합되는 방법에 대해서도 다룹니다.  
  
## <a name="basic-concepts-of-clr-architecture"></a>CLR 아키텍처의 기본 개념  
 .NET Framework에서 프로그래머는 클래스의 구조(예: 클래스의 필드나 속성)와 메서드를 정의하여 클래스를 구현하는 고급 언어로 코드를 작성합니다. 이러한 메서드 일부는 정적 함수일 수 있습니다. 프로그램을 컴파일하면 어셈블리라는 파일이 생성되는데 이 어셈블리 파일에는 MSIL([!INCLUDE[msCoName](../../includes/msconame-md.md)] Intermediate Language)로 컴파일된 코드 및 종속 어셈블리에 대한 모든 참조가 포함된 매니페스트가 들어 있습니다.  
  
> [!NOTE]  
>  어셈블리는 CLR 아키텍처의 필수 요소로, .NET Framework에서 응용 프로그램 코드를 패키징, 배포 및 버전 관리하는 단위입니다. 어셈블리를 사용하면 데이터베이스 안에 응용 프로그램 코드를 배포하고 완전한 데이터베이스 응용 프로그램을 일관된 방법으로 관리, 백업 및 복원할 수 있습니다.  
  
 어셈블리 매니페스트에는 프로그램에 정의되어 있는 모든 구조, 필드, 속성, 클래스, 상속 관계, 함수 및 메서드를 설명하는 어셈블리 메타데이터가 들어 있습니다. 어셈블리 매니페스트는 어셈블리의 ID를 설정하고, 어셈블리 구현을 구성하는 파일을 지정하고, 어셈블리를 구성하는 형식 및 리소스를 지정하며, 컴파일 타임의 다른 어셈블리에 대한 종속성을 항목별로 요약하고, 어셈블리가 제대로 실행되는 데 필요한 권한 집합을 지정합니다. 이 정보는 런타임에 참조를 확인하고, 버전 바인딩 정책을 적용하고, 로드된 어셈블리의 무결성을 확인하는 데 사용됩니다.  
  
 .NET Framework에서는 응용 프로그램에서 메타데이터에 캡처할 수 있는 추가적인 정보를 클래스, 속성, 함수 및 메서드에 주석으로 추가할 수 있는 사용자 지정 특성을 지원합니다. 모든 .NET Framework 컴파일러는 이러한 주석을 해석 없이 사용하고 어셈블리 메타데이터로 저장합니다. 이러한 주석은 다른 메타데이터와 같은 방식으로 검사할 수 있습니다.  
  
 관리 코드는 운영 체제에서 직접 실행되는 대신 CLR에서 실행되는 MSIL입니다. 관리 코드 응용 프로그램은 자동 가비지 수집, 런타임 형식 확인, 보안 지원 등과 같은 CLR 서비스를 얻습니다. 이러한 서비스는 관리 코드 응용 프로그램의 일관된 플랫폼 및 언어 독립적인 동작을 제공하는 데 도움이 됩니다.  
  
## <a name="design-goals-of-clr-integration"></a>CLR 통합의 디자인 목표  
 CLR 통합은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 CLR 호스팅 환경에서 사용자 코드를 실행하는 것을 의미하며 여기에는 다음과 같은 디자인 목표가 적용됩니다.  
  
###### <a name="reliability-safety"></a>안정성(보안)  
 사용자 코드는 사용자 응답을 요청하는 메시지 상자를 표시하거나 프로세스를 종료하는 것과 같이 데이터베이스 엔진 프로세스의 무결성을 손상시키는 작업을 수행할 수 없습니다. 또한 사용자 코드는 데이터베이스 엔진 메모리 버퍼 또는 내부 데이터 구조를 덮어쓸 수 없습니다.  
  
###### <a name="scalability"></a>확장성  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 CLR은 일정 예약 및 메모리 관리를 위한 내부 모델이 서로 다릅니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 스레드가 정기적으로 또는 잠금이나 I/O 대기 중일 때 자동으로 실행이 해제되는 공동의 비선점형 스레딩 모델을 지원합니다. 반면 CLR은 선점형 스레딩 모델을 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내에서 실행되는 사용자 코드에서 운영 체제 스레딩 기본 형식을 직접 호출할 수 있으면 사용자 코드가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 태스크 스케줄러에 제대로 통합되지 않고 시스템의 확장성을 떨어뜨릴 수 있습니다. CLR은 가상 메모리와 실제 메모리를 구분하지 않지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 실제 메모리를 직접 관리하고 구성 가능한 한도 내에서만 실제 메모리를 사용해야 합니다.  
  
 수천 개의 동시 사용자 세션을 지원하도록 확장 가능한 RDBMS(관계형 데이터베이스 관리 시스템)의 경우에는 스레딩, 일정 예약 및 메모리 관리 모델이 다르기 때문에 통합하기 어렵습니다. 아키텍처에서는 스레딩, 메모리 및 동기화 기본 형식을 위한 API(응용 프로그래밍 인터페이스)를 직접 호출하는 사용자 코드로 인해 시스템의 확장성에 문제가 발생하지 않아야 합니다.  
  
###### <a name="security"></a>보안  
 데이터베이스에서 실행되는 사용자 코드는 테이블과 열 같은 데이터베이스 개체에 액세스할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 및 권한 부여 규칙을 준수해야 합니다. 또한 데이터베이스 관리자는 데이터베이스에서 실행되는 사용자 코드를 통해 파일 같은 운영 체제 리소스에 대한 액세스 및 네트워크 액세스를 제어할 수 있어야 합니다. Transact-SQL과 같이 관리되지 않는 언어와 달리 관리되는 프로그래밍 언어는 이와 같은 리소스에 액세스하기 위한 API를 제공하기 때문에 액세스 제어가 중요합니다. 시스템에서는 사용자 코드가 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 프로세스 외부에서 컴퓨터 리소스에 액세스할 수 있는 안전한 방법을 제공해야 합니다. 자세한 내용은 [CLR Integration Security](../../relational-databases/clr-integration/security/clr-integration-security.md)을 참조하세요.  
  
###### <a name="performance"></a>성능  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 실행되는 관리되는 사용자 코드는 서버 외부에서 실행되는 동일한 코드와 비교할 수 있을 정도의 계산 성능을 가지고 있어야 합니다. 관리되는 사용자 코드에서 데이터베이스에 액세스하면 네이티브 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용할 때보다 속도가 느립니다. 자세한 내용은 [CLR 통합의 성능을](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)합니다.  
  
## <a name="clr-services"></a>CLR Services  
 CLR은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와의 CLR 통합에 대한 디자인 목표를 달성하는 데 도움이 되는 여러 가지 서비스를 제공합니다.  
  
###### <a name="type-safety-verification"></a>형식 안전성 확인  
 형식 안전 코드는 명확하게 정의된 방법으로만 메모리 구조에 액세스하는 코드입니다. 예를 들어 올바른 개체 참조에 대해 형식 안전 코드는 실제 필드 멤버에 대응하는 고정 오프셋에서 메모리에 액세스할 수 있습니다. 그러나 개체에 속하는 메모리 범위 안이나 밖의 임의의 오프셋에서 메모리에 액세스하는 코드는 형식 안전 코드가 아닙니다. 어셈블리가 CLR에 로드되고 JIT(Just-In-Time) 컴파일을 사용하여 MSIL을 컴파일되기 전에 런타임에서는 코드의 형식 안전성을 검사하는 확인 단계를 수행합니다. 이 확인 과정을 통과한 코드는 형식 안전 코드라고 할 수 있습니다.  
  
###### <a name="application-domains"></a>응용 프로그램 도메인  
 CLR은 호스트 프로세스에서 관리 코드 어셈블리를 로드하고 실행할 수 있는 실행 영역이라는 개념으로 응용 프로그램 도메인을 지원합니다. 응용 프로그램 도메인 경계는 어셈블리 사이를 구분합니다. 어셈블리는 정적 변수와 데이터 멤버의 표시 유형 및 코드를 동적으로 호출할 수 있는지 여부를 기준으로 격리됩니다. 응용 프로그램 도메인은 코드를 로드하고 언로드하는 메커니즘이기도 합니다. 메모리에서 코드를 언로드하는 유일한 방법은 응용 프로그램 도메인을 언로드하는 것입니다. 자세한 내용은 [응용 프로그램 도메인 및 CLR 통합 보안](https://msdn.microsoft.com/library/54ee904e-e21a-4ee7-b4ad-a6f6f71bd473)합니다.  
  
###### <a name="code-access-security-cas"></a>CAS(코드 액세스 보안)  
 CLR 보안 시스템을 사용하면 코드에 사용 권한을 할당하여 관리 코드로 수행할 수 있는 작업의 유형을 제어할 수 있습니다. 코드 액세스 권한은 코드 ID(예: 어셈블리의 서명 또는 코드 원본)를 기준으로 할당됩니다.  
  
 CLR에는 컴퓨터 관리자가 설정할 수 있는 컴퓨터 차원의 정책이 있습니다. 이 정책은 컴퓨터에서 실행되는 모든 관리 코드에 대한 권한 부여를 정의합니다. 컴퓨터 차원의 정책 외에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 같은 호스트에서 관리 코드에 대한 추가적인 제한을 지정하는 데 사용할 수 있는 호스트 수준의 보안 정책도 있습니다.  
  
 .NET Framework의 관리되는 API가 코드 액세스 권한으로 보호되는 리소스에 대한 작업을 노출할 경우, API는 리소스에 액세스하기 전에 해당 사용 권한을 요청합니다. 이 요청이 발생하면 CLR 보안 시스템에서는 호출 스택에 포함된 모든 코드 단위(어셈블리)에 대한 포괄적인 검사를 트리거합니다. 전체 호출 체인에 사용 권한이 있는 경우에만 리소스에 대한 액세스가 허용됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 CLR 호스팅 환경 내에서는 Reflection.Emit API를 사용하여 관리 코드를 동적으로 생성할 수 없습니다. 이러한 코드는 적절한 CAS 권한을 가지고 있지 않기 때문에 런타임에 실패합니다. 자세한 내용은 [CLR 통합 코드 액세스 보안](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)합니다.  
  
###### <a name="host-protection-attributes-hpas"></a>HPA(호스트 보호 특성)  
 CLR은 .NET Framework의 일부인 관리되는 API에 대해 CLR 호스트에서 유용할 수 있는 특성으로 주석을 지정하기 위한 메커니즘을 제공합니다. 이러한 특성의 예를 들면 다음과 같습니다.  
  
-   SharedState: API가 공유 상태(예: 정적 클래스 필드)를 만들거나 관리하는 기능을 노출하는지 여부를 나타냅니다.  
  
-   Synchronization: API가 스레드 간 동기화 기능을 노출하는지 여부를 나타냅니다.  
  
-   ExternalProcessMgmt: API가 호스트 프로세스 제어 기능을 노출하는지 여부를 나타냅니다.  
  
 이러한 특성을 사용하면 호스트에서는 호스팅 환경에서 허용하지 않는 HPA 목록(예: SharedState 특성)을 지정할 수 있습니다. 이렇게 하면 CLR에서는 금지 목록에 포함된 HPA로 주석이 지정된 API를 호출하는 사용자 코드를 거부합니다. 자세한 내용은 [호스트 보호 특성 및 CLR 통합 프로그래밍](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)합니다.  
  
## <a name="how-sql-server-and-the-clr-work-together"></a>SQL Server와 CLR이 함께 작동하는 방법  
 이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 CLR의 스레딩, 일정 관리, 동기화 및 메모리 관리 모델을 통합하는 방법에 대해 설명합니다. 특히 이 섹션에서는 확장성, 안정성 및 보안 목표 측면에서의 통합을 검사합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내에서 CLR을 호스팅하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 CLR의 운영 체제 역할을 합니다. CLR에서는 스레딩, 일정 예약, 동기화 및 메모리 관리를 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 구현된 하위 수준의 루틴을 호출합니다. 이는 나머지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 엔진에서 사용하는 기본 형식과 동일합니다. 이 방식을 사용하면 확장성, 안정성 및 보안상 여러 가지 이점을 얻을 수 있습니다.  
  
###### <a name="scalability-common-threading-scheduling-and-synchronization"></a>확장성: 일반적인 스레딩, 예약 및 동기화  
 CLR에서는 사용자 코드를 실행하기 위한 경우나 내부적인 용도로 사용하기 위한 경우 모두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] API를 호출하여 스레드를 만듭니다. 여러 스레드를 동기화하기 위해 CLR에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동기화 개체를 호출합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스케줄러는 스레드가 동기화 개체를 대기하고 있을 때 다른 태스크의 일정을 예약할 수 있습니다. 예를 들어 CLR에서 가비지 수집을 시작하면 가비지 수집이 완료될 때까지 모든 스레드가 대기합니다. CLR 스레드 및 CLR 스레드에서 대기 중인 동기화 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스케줄러가 알고 있기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CLR과 관련되지 않은 다른 데이터베이스 태스크를 실행하는 스레드를 예약할 수 있습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CLR 동기화 개체의 잠금과 관련된 교착 상태를 검색한 후 일반적인 기술을 사용하여 교착 상태를 해결할 수 있습니다.  
  
 관리 코드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 선점형 모드로 실행됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스케줄러에는 리소스를 오랫동안 점유하고 있는 스레드를 확인하여 중지하는 기능이 있습니다. CLR 스레드를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스레드에 후크하는 기능은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스케줄러가 CLR의 "런어웨이" 스레드를 식별하여 해당 스레드의 우선 순위를 관리할 수 있음을 의미합니다. 이와 같은 런어웨이 스레드는 일시 중지되어 큐에 다시 배치됩니다. 런어웨이 스레드로 반복적으로 식별되는 스레드는 작업을 수행하는 다른 스레드가 실행될 수 있도록 일정 기간 동안 일시 중지됩니다.  
  
> [!NOTE]  
>  데이터에 액세스하거나 가비지 수집이 트리거될 정도로 많은 양의 메모리를 할당하는 장기 실행 관리 코드는 자동으로 해제됩니다. 반면 데이터에 액세스하지 않거나 가비지 수집이 트리거될 정도의 충분한 메모리를 할당하지 않는 장기 실행 관리 코드는 .NET Framework의 System.Thread.Sleep() 함수를 호출하여 명시적으로 해제해야 합니다.  
  
###### <a name="scalability-common-memory-management"></a>확장성: 일반적인 메모리 관리  
 CLR은 메모리를 할당하거나 할당을 취소하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 형식을 호출합니다. CLR에서 사용하는 메모리는 시스템의 총 메모리 사용량에 포함되기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 구성된 메모리 제한을 초과하지 않으면서 CLR과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 메모리를 차지하기 위해 서로 경쟁하지 않도록 할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 시스템 메모리가 제한되었을 때 CLR 메모리 요청을 거부할 수 있으며 다른 태스크에 메모리가 필요할 때 메모리 사용을 줄이도록 CLR에 요청할 수 있습니다.  
  
###### <a name="reliability-application-domains-and-unrecoverable-exceptions"></a>안정성:  응용 프로그램 도메인 및 복구할 수 없는 예외  
 .NET Framework API의 관리 코드에서 메모리 부족 또는 스택 오버플로와 같은 중대한 예외가 발견되었을 때 이러한 오류를 복구하여 API 구현의 의미를 일관되고 올바르게 유지하지 못하는 경우도 있습니다. 이러한 API는 이와 같은 오류에 대한 응답으로 스레드 중단 예외를 발생시킵니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 호스팅되는 경우 이러한 스레드 중단은 다음과 같이 처리됩니다. 즉, CLR이 응용 프로그램 도메인 내에서 스레드 중단이 발생한 모든 공유 상태를 검색합니다. CLR은 동기화 개체가 있는지 여부를 확인하여 이 작업을 수행합니다. 응용 프로그램 도메인에 공유 상태가 있으면 응용 프로그램 도메인 자체가 언로드됩니다. 응용 프로그램 도메인이 언로드되면 해당 응용 프로그램 도메인에서 현재 실행 중인 데이터베이스 트랜잭션이 중지됩니다. 공유 상태가 있는 경우 예외를 트리거한 세션 이외의 다른 사용자 세션도 이와 같은 중대한 예외의 영향을 받을 수 있기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 CLR은 공유 상태의 가능성을 줄이기 위한 조치를 취합니다. 자세한 내용은 .NET Framework 설명서를 참조하십시오.  
  
###### <a name="security-permission-sets"></a>보안: 권한 집합  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 데이터베이스에 배포되는 코드의 안정성 및 보안 요구 사항을 사용자가 지정할 수 있습니다. 어셈블리를 데이터베이스에 업로드 되 면 어셈블리의 작성자 하나를 지정할 수 세 가지 권한 집합이 해당 어셈블리에 대 한 합니다. SAFE, EXTERNAL_ACCESS 및 UNSAFE 합니다.  
  
|||||  
|-|-|-|-|  
|권한 집합|SAFE|EXTERNAL_ACCESS|UNSAFE|  
|코드 액세스 보안|실행 전용|실행 및 외부 리소스 액세스|제한 없음|  
|프로그래밍 모델 제한|예|사용자 계정 컨트롤|제한 없음|  
|안정성 요구 사항|예|예|아니요|  
|네이티브 코드 호출 기능|아니요|아니요|예|  
  
 SAFE는 허용되는 프로그래밍 모델 측면에서 연결된 제한 사항이 있는 가장 안정적인 보안 모드입니다. SAFE 어셈블리에는 충분한 실행 권한이 제공되며, 계산을 수행하고, 로컬 데이터베이스에 액세스할 수 있습니다. SAFE 어셈블리는 형식이 안전해야 하며 비관리 코드를 호출할 수 없습니다.  
  
 UNSAFE는 데이터베이스 관리자만 만들 수 있는 고도로 신뢰할 수 있는 코드에 사용됩니다. 이 신뢰되는 코드는 코드 액세스 보안 제한이 없으며 비관리(네이티브) 코드를 호출할 수 있습니다.  
  
 EXTERNAL_ACCESS는 중급 보안 옵션을 제공하며 코드가 데이터베이스 외부의 리소스에 액세스하도록 허용하지만 여전히 SAFE 수준의 안정성과 보안을 갖습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 호스트 수준의 CAS 정책 계층을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 카탈로그에 저장되어 있는 권한 집합에 기초하여 세 가지 권한 집합 중 하나를 부여하는 호스트 정책을 설정합니다. 데이터베이스 내에서 실행되는 관리 코드는 항상 이러한 코드 액세스 권한 집합 중 하나를 가져옵니다.  
  
### <a name="programming-model-restrictions"></a>프로그래밍 모델 제한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리 코드에 대한 프로그래밍 모델에서는 여러 호출에 걸쳐 유지되는 상태를 사용하거나 여러 사용자 세션에서 상태를 공유할 필요가 없는 함수, 프로시저 및 형식을 작성해야 합니다. 또한 앞에서 설명한 것처럼 공유 상태가 있을 경우 애플리케이션의 안정성 및 확장성에 영향을 주는 중대한 예외가 발생할 수 있습니다.  
  
 이러한 점을 고려하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 클래스의 정적 변수와 정적 데이터 멤버는 사용하지 않는 것이 좋습니다. SAFE 및 EXTERNAL_ACCESS 어셈블리의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 CREATE ASSEMBLY 시간에 해당 어셈블리의 메타데이터를 검사하고 정적 데이터 멤버와 변수가 사용된 경우 어셈블리를 만드는 데 오류가 발생합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 으로 주석이 지정 된.NET Framework Api 호출을 허용 하지 않습니다 합니다 **: SharedState**, **동기화** 하 고 **ExternalProcessMgmt** 호스트 보호 특성입니다. 이로 인해 SAFE 및 EXTERNAL_ACCESS 어셈블리에서는 상태를 공유하고, 동기화를 수행하며, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스의 무결성에 영향을 주는 API를 호출하지 못합니다. 자세한 내용은 [CLR 통합 프로그래밍 모델 제한 사항](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CLR 통합 보안](../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [통합된 CLR의 성능](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)  
  
  
