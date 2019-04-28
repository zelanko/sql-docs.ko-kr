---
title: 복제 프로그래밍 개념 | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- replication [SQL Server], planning
- programming [SQL Server replication], planning
- programming [SQL Server replication]
ms.assetid: 2cd846e7-5bf3-4144-8772-703c4f439a2a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bf393a3e0f117098dc4a85bae3e6c68728f43a64
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721811"
---
# <a name="replication-programming-concepts"></a>복제 프로그래밍 개념
  복제 기능을 사용하는 애플리케이션을 개발하려면 먼저 다음과 같은 일반적인 계획 단계를 따르는 것이 좋습니다.  
  
1.  복제 토폴로지를 정의합니다.  
  
2.  애플리케이션 기능을 정의합니다.  
  
3.  보안을 계획합니다.  
  
4.  개발 환경을 선택합니다.  
  
5.  적절한 복제 프로그래밍 인터페이스를 선택합니다.  
  
 이 항목의 나머지 부분에서는 이러한 단계를 좀 더 자세히 설명합니다. 이 항목에는 계획 프로세스에 대한 이해를 돕기 위해 예가 포함되었습니다.  
  
## <a name="defining-the-replication-topology"></a>복제 토폴로지 정의  
 복제 프로그래밍의 첫 번째 단계는 애플리케이션의 복제 토폴로지를 정의하는 것입니다. 기존 구독자의 데이터에 액세스하는 클라이언트 애플리케이션과 같이 기존의 복제 토폴로지를 사용할 애플리케이션을 작성하는 경우에는 다음 단계로 진행하십시오.  
  
> [!NOTE]  
>  경우에 따라서는 애플리케이션이 복제 토폴로지를 배포하는 용도로만 사용될 수 있습니다.  
  
 복제 토폴로지 정의는 다음을 포함하여 여러 요인에 따라 달라질 수 있습니다.  
  
-   복제된 데이터를 업데이트해야 하는지 여부 및 업데이트 수행자  
  
-   일관성, 자율성 및 대기 시간 측면에서의 데이터 배포 요구 사항  
  
-   비즈니스 사용자, 기술 인프라, 네트워크와 보안, 데이터 특성 등을 포함한 복제 환경  
  
-   복제 및 복제 옵션 유형  
  
-   복제 토폴로지 및 복제 토폴로지와 복제 유형의 관계  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제를 처음 사용하는 경우 [복제 유형](../types-of-replication.md)을 참조하세요.  
  
## <a name="defining-application-functionality"></a>애플리케이션 기능 정의  
 복제 토폴로지를 정의한 후에는 애플리케이션이 제공할 기능을 결정해야 합니다. 이러한 기능은 구독을 동기화하는 스크립트부터 복제를 구성하는 사용자 인터페이스가 포함된 애플리케이션에 이르기까지 다양합니다. 복제는 다음과 같은 일발적인 프로그래밍 태스크를 지원합니다.  
  
-   복제 설정  
  
-   구독자 동기화  
  
-   복제 토폴로지 유지 관리  
  
-   복제 토폴로지 모니터링  
  
-   복제 문제 해결  
  
 복제 기능을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 제공하는 다른 기능과 결합하여 애플리케이션을 확장하는 방법도 일반적으로 사용됩니다. 다음 표에서는 복제 애플리케이션에 제공할 수 있는 몇 가지 확장 기능을 보여 줍니다.  
  
|기능|예제|  
|-------------------|-------------|  
|SMO([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects)를 사용하여 서버 관리|관리자가 복제 토폴로지에 데이터베이스를 게시자로 연결하고 구성할 수 있는 애플리케이션입니다.|  
|ADO.NET을 사용하여 데이터 액세스|사용자가 오프라인 상태에서 프로그래밍 방식으로 로컬 구독자 데이터베이스의 복제된 판매 데이터에 액세스하고 데이터를 변경한 다음 단추를 클릭하여 다시 연결한 후 끌어오기 구독을 동기화할 수 있는 애플리케이션입니다.|  
  
## <a name="planning-for-security"></a>보안 계획  
 보안은 모든 애플리케이션에서 중요하며 보안 계획은 코드 작성을 시작하기 전에 마쳐야 합니다. 애플리케이션 보안은 데이터베이스 보안, 복제 보안 및 보안 코드 작성이라는 세 부분으로 나눌 수 있습니다.  
  
 다음 항목에서는 보안에 대한 정보를 제공합니다.  
  
-   [SQL Server 복제 보안](../security/view-and-modify-replication-security-settings.md)  
  
-   [SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 보안 센터](../../security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
## <a name="choosing-a-development-environment"></a>개발 환경 선택  
 복제 애플리케이션을 개발할 때는 세 가지 기본적인 개발 환경을 고려할 수 있습니다. 각 개발 환경에서는 동일한 복제 기능에 액세스할 수 있지만, 몇 가지 예외도 있습니다. 복제 애플리케이션은 다음과 같은 환경에서 개발할 수 있습니다.  
  
-   **관리 코드**  
  
     [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 프로그래밍과 .NET CLR(공용 언어 런타임)의 이점을 활용하는 개체 지향 개발 환경입니다. 관리 코드는 .NET 개발 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 애플리케이션 모두에 대해 권장되는 프로그래밍 환경입니다. 관리되는 복제 인터페이스를 사용하면 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 알지 못해도 개체 지향 방식으로 복제 관리 기능을 프로그래밍할 수 있으며 스크립트를 통해 사용할 수 없는 복제 에이전트를 실행할 때 몇 가지 콜백 기능이 제공됩니다. 관리 코드는 재사용 가능한 구성 요소와 사용자 인터페이스 애플리케이션을 개발하기 위한 최상의 환경입니다.  
  
-   **스크립팅**  
  
     일련의 명령을 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트의 복제 시스템 저장 프로시저로 실행하거나 배치 파일의 명령으로 실행하는 간단한 애플리케이션입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 종속 프로세스 관리 공급자를 사용하여 관리되는 환경에서 스크립트를 실행할 수 있지만 콜백 기능을 제공하는 관리되는 복제 인터페이스를 사용하여 동일한 기능을 구현할 수 있습니다. 스크립팅은 복제 서버 설치와 같이 콜백 기능이 필요하지 않고 몇 번만 실행할 태스크를 실행하는 데 가장 적합한 환경입니다.  
  
-   **네이티브 코드**  
  
     CLR에서 코드를 관리하지 못하도록 시스템 또는 COM 개체에 대한 직접 액세스를 사용하는 개체 지향 개발 환경입니다. 네이티브 코드 복제 인터페이스는 더 이상 사용되지 않거나 지원되지 않습니다. 자세한 내용은 [SQL Server 복제에서 사용되지 않는 기능](../deprecated-features-in-sql-server-replication.md) 또는 [복제의 이전 버전과의 호환성](../replication-backward-compatibility.md)을 참조하세요.  
  
## <a name="choose-the-appropriate-replication-programming-interface"></a>적절한 복제 프로그래밍 인터페이스 선택  
 계획 프로세스의 마지막 단계는 선택한 개발 환경에서 원하는 복제 기능을 구현하는 적절한 복제 프로그래밍 인터페이스를 선택하는 것입니다. 다음 표에서는 사용할 수 있는 복제 프로그래밍 인터페이스를 보여 줍니다.  
  
|인터페이스|환경|용도|  
|---------------|-----------------|----------|  
|[복제 관리 개체 개념](replication-management-objects-concepts.md)|관리 코드|관리, 모니터링 및 동기화|  
|<xref:Microsoft.SqlServer.Replication>|관리 코드|동기화|  
|<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|관리 코드|사용자 지정 논리를 병합 동기화 프로세스에 통합하기 위한 비즈니스 논리 처리기 생성|  
|[복제 저장 프로시저&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql)|스크립팅|관리 및 모니터링|  
|[Replication Agent Executables Concepts](replication-agent-executables-concepts.md)|스크립팅|동기화|  
  
## <a name="example"></a>예제  
 [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)]에서는 전 세계 200명의 영업 담당자에게 데이터를 게시해야 합니다. 영업 담당자들은 자주 이동하기 때문에 랩톱 컴퓨터나 PDA(개인용 정보 단말기)를 사용하여 고객 데이터를 변경하고 새 주문을 추가해야 합니다. 변경 내용은 영업 담당자가 랩톱을 네트워크에 연결할 때 게시자에 동기화되어야 합니다.  
  
 이 애플리케이션의 계획 단계는 다음과 같습니다.  
  
1.  이 애플리케이션의 복제 토폴로지는 이미 있지만 클라이언트에서 새 끌어오기 구독을 만들어야 합니다. 게시 작업에서는 매개 변수가 있는 필터를 사용하여 각 영업 담당자에게 고유한 데이터 집합을 복제해야 합니다.  
  
2.  영업 애플리케이션에 필요한 일반적인 데이터 액세스 이외에 이 애플리케이션에서는 영업 사원이 단추를 클릭하여 필요할 때 끌어오기 구독을 동기화할 수 있어야 합니다. 이 애플리케이션은 영업 담당자가 설치하고 실행할 것이므로 클라이언트에서 구독을 구성하고 초기 스냅숏을 적용할 수 있는 기능도 필요합니다. 필요한 경우 애플리케이션에서는 연결이 발견되면 구독을 자동으로 동기화할 수 있도록 Windows에서 제공하는 무선 연결 감지 인프라를 사용할 수도 있습니다.  
  
3.  게시자에 연결할 때 Windows 인증 및 VPN(가상 사설망)을 사용하는 것을 포함하여 복제와 관련된 모든 보안 지침을 따릅니다. 웹 동기화를 구현하는 경우에는 SSL(Secure Sockets Layer) 연결을 사용합니다. 자세한 내용은 [웹 동기화 구성](../configure-web-synchronization.md)을 참조하세요.  
  
4.  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]의 기능을 활용하려면 관리되는 코드 언어를 사용하여 응용 프로그램을 개발합니다.  
  
5.  이러한 요구 사항을 고려했을 때 이 애플리케이션에 필요한 모든 복제 기능은 RMO(복제 관리 개체) 관리 인터페이스를 사용하여 구현할 수 있습니다.  
  
 이 시나리오 예는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 포함된 예제 응용 프로그램에서 구현되었습니다.  
  
  
