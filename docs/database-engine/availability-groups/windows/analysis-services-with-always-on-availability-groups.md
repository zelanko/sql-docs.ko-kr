---
title: 가용성 그룹이 포함된 Analysis Services
description: Always On 가용성 그룹을 고가용성 솔루션으로 사용하는 경우 해당 그룹의 데이터베이스를 Analysis Services 테이블 형식 또는 다차원 솔루션의 데이터 원본으로 사용할 수 있습니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 14d16bfd-228c-4870-b463-a283facda965
author: MashaMSFT
ms.author: mathoma
manager: erikre
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 81fd6e4a9be7b27190491c6a36ef536e3c1ba669
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53212492"
---
# <a name="analysis-services-with-always-on-availability-groups"></a>Always On 가용성 그룹이 포함된 Analysis Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Always On 가용성 그룹은 미리 정의된 SQL Server 관계형 데이터베이스 컬렉션으로, 조건이 한 데이터베이스에서 장애 조치(failover)를 트리거하면 전체 데이터베이스에서 함께 장애 조치가 수행되고, 동일한 가용성 그룹에 있는 다른 인스턴스의 미러된 데이터베이스로 요청을 리디렉션합니다. 가용성 그룹을 고가용성 솔루션으로 사용하는 경우 해당 그룹의 데이터베이스를 Analysis Services 테이블 형식 또는 다차원 솔루션의 데이터 원본으로 사용할 수 있습니다. 가용성 데이터베이스를 사용할 경우 데이터 처리 또는 가져오기, 관계형 데이터 직접 쿼리(ROLAP 저장소 또는 DirectQuery 모드 사용), 쓰기 저장과 같은 모든 Analysis Services 작업이 예상대로 작동합니다.  
  
 처리 및 쿼리는 읽기 전용 작업입니다. 이러한 작업을 읽기 가능한 보조 복제본으로 오프로드하면 성능을 향상시킬 수 있습니다. 이 시나리오를 위해 추가적인 구성이 필요합니다. 이 항목의 검사 목록을 따라 모든 단계를 수행하십시오.  
  
 [필수 구성 요소](#bkmk_prereq)  
  
 [검사 목록: 읽기 전용 작업에 보조 복제본 사용](#bkmk_UseSecondary)  
  
 [Always On 가용성 데이터베이스를 사용하는 Analysis Services 데이터 원본 만들기](#bkmk_ssasAODB)  
  
 [구성 테스트](#bkmk_test)  
  
 [장애 조치 발생 후의 상황](#bkmk_whathappens)  
  
 [Always On 가용성 데이터베이스를 사용할 때의 쓰기 저장](#bkmk_writeback)  
  
##  <a name="bkmk_prereq"></a> 사전 요구 사항  
 모든 복제본에 대한 SQL Server 로그인이 있어야 합니다. 가용성 그룹, 수신기 및 데이터베이스를 구성하려면 **sysadmin** 이어야 하지만, 사용자인 경우 **db_datareader** 권한만 있으면 Analysis Services 클라이언트에서 데이터베이스에 액세스할 수 있습니다.  
  
 TDS(Tabular Data Stream) 프로토콜 버전 7.4 이상을 지원하는 데이터 공급자(예: SQL Server Native Client 11.0 또는 .NET Framework 4.02의 SQL Server용 공급자)를 사용하십시오.  
  
 **(읽기 전용 작업의 경우)**. 읽기 전용 연결에는 보조 복제본 역할을 구성해야 하고, 가용성 그룹은 라우팅 목록이 있어야 하며, Analysis Services 데이터 원본의 연결에는 가용성 그룹 수신기를 지정해야 합니다. 지침은 이 항목에 설명되어 있습니다.  
  
##  <a name="bkmk_UseSecondary"></a> 검사 목록: 읽기 전용 작업에 보조 복제본 사용  
 Analysis Services 솔루션에 쓰기 저장이 포함되지 않으면 데이터 원본 연결에 읽기 가능한 보조 복제본을 사용하도록 구성할 수 있습니다. 빠른 네트워크 연결인 경우 보조 복제본의 데이터 대기 시간이 매우 적어 주 복제본과 거의 동일한 데이터를 제공합니다. Analysis Services 작업에 보조 복제본을 사용하면 주 복제본에 대한 읽기-쓰기 경합을 줄이고 가용성 그룹에 있는 보조 복제본의 활용도를 높일 수 있습니다.  
  
 기본적으로 주 복제본에 대한 읽기/쓰기 및 읽기 전용 액세스가 모두 허용되며 보조 복제본에 대한 연결은 허용되지 않습니다. 보조 복제본에 대한 읽기 전용 클라이언트 연결을 설정하려면 추가적인 구성이 필요합니다. 구성에는 보조 복제본에 대한 설정이 필요하고 읽기 전용 라우팅 목록을 정의하는 T-SQL 스크립트를 실행해야 합니다. 다음 절차를 통해 이 두 단계를 수행했는지 확인합니다.  
  
> [!NOTE]  
>  다음 단계는 기존 Always On 가용성 그룹 및 데이터베이스를 전제로 합니다. 새 그룹을 구성하려면 새 가용성 그룹 마법사를 사용하여 그룹을 만들고 데이터베이스를 조인합니다. 마법사는 사전 요구 사항을 점검하고 각 단계에 대한 지침을 제공하고 초기 동기화를 수행합니다. 자세한 내용은 [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)을 참조하세요.  
  
#### <a name="step-1-configure-access-on-an-availability-replica"></a>1단계: 가용성 복제본에 대한 액세스 구성  
  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
    > [!NOTE]  
    >  이러한 단계는 [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)에서 가져왔으며, 이 링크는 이 작업 수행에 대한 추가 정보 및 다른 지침도 제공합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  복제본을 변경할 가용성 그룹을 클릭합니다. **가용성 복제본**을 확장합니다.  
  
4.  보조 복제본을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
5.  **가용성 복제본 속성** 대화 상자에서 다음과 같이 보조 역할에 대한 연결 액세스를 변경합니다.  
  
    -   **읽을 수 있는 보조** 드롭 목록에서 **읽기 전용만**을 선택합니다.  
  
    -   **주 역할의 연결** 드롭 목록에서 **모든 연결 허용**을 선택합니다. 기본값입니다.  
  
    -   필요에 따라 **가용성 모드** 드롭 목록에서 **동기 커밋**을 선택합니다. 이 단계는 필수는 아니지만 이 설정을 하면 주 복제본과 보조 복제본 사이에 데이터 패리티를 보장해 줍니다.  
  
         또한 이 속성은 계획된 장애 조치에는 필수입니다. 테스트 목적으로 계획된 수동 장애 조치를 수행하려면 주 복제본과 보조 복제본 둘 다에 대해 **가용성 모드** 를 **동기 커밋** 으로 설정합니다.  
  
#### <a name="step-2-configure-read-only-routing"></a>2단계: 읽기 전용 라우팅 구성  
  
1.  주 복제본에 연결합니다.  
  
    > [!NOTE]  
    >  이러한 단계는 [가용성 그룹에 대한 읽기 전용 라우팅 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)에서 가져왔으며, 이 링크는 이 작업 수행에 대한 추가 정보 및 다른 지침도 제공합니다.  
  
2.  쿼리 창을 열고 다음 스크립트를 붙여 넣습니다. 이 스크립트는 보조 복제본에 대한 읽기용 연결(기본적으로 해제됨)을 설정하고, 읽기 전용 라우팅 URL을 설정하고, 연결 요청 전달 우선 순위를 지정하는 라우팅 목록을 만드는 세 가지 작업을 수행합니다.  읽기용 연결을 허용하는 첫 번째 문은 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 이미 해당 속성을 설정한 경우 중복되지만 완전성을 위해 포함되었습니다.  
  
    ```  
    ALTER AVAILABILITY GROUP [AG1]  
     MODIFY REPLICA ON  
    N'COMPUTER01' WITH   
    (SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
  
    ALTER AVAILABILITY GROUP [AG1]  
     MODIFY REPLICA ON  
    N'COMPUTER01' WITH   
    (SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433'));  
  
    ALTER AVAILABILITY GROUP [AG1]  
     MODIFY REPLICA ON  
    N'COMPUTER02' WITH   
    (SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
  
    ALTER AVAILABILITY GROUP [AG1]  
     MODIFY REPLICA ON  
    N'COMPUTER02' WITH   
    (SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER02.contoso.com:1433'));  
  
    ALTER AVAILABILITY GROUP [AG1]   
    MODIFY REPLICA ON  
    N'COMPUTER01' WITH   
    (PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER02','COMPUTER01')));  
  
    ALTER AVAILABILITY GROUP [AG1]   
    MODIFY REPLICA ON  
    N'COMPUTER02' WITH   
    (PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER01','COMPUTER02')));  
    GO  
    ```  
  
3.  자리 표시자를 사용자 배포에 맞는 값으로 바꿔 스크립트를 수정합니다.  
  
    -   'Computer01'은 주 복제본을 호스팅하는 서버 인스턴스의 이름으로 바꿉니다.  
  
    -   'Computer02'는 보조 복제본을 호스팅하는 서버 인스턴스의 이름으로 바꿉니다.  
  
    -   'contoso.com'은 도메인 이름으로 바꾸거나, 모든 컴퓨터가 동일한 도메인인 경우 생략합니다. 수신기가 기본 포트를 사용하는 경우 포트 번호는 그대로 유지합니다. 실제로 수신기에서 사용하는 포트의 목록은 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]의 속성 페이지에 나와 있습니다.  
  
4.  스크립트를 실행합니다.  
  
     이제, 방금 구성한 그룹의 데이터베이스를 사용하는 Analysis Services 모델의 데이터 원본을 만듭니다.  
  
##  <a name="bkmk_ssasAODB"></a> Always On 가용성 데이터베이스를 사용하는 Analysis Services 데이터 원본 만들기  
 이 섹션에서는 가용성 그룹의 데이터베이스에 연결하는 Analysis Services 데이터 원본을 만드는 방법을 설명합니다. 이 지침을 따르면 이전 섹션의 단계에 따라 구성한 주 복제본(기본값) 또는 읽기 가능한 보조 복제본에 대한 연결을 구성할 수 있습니다. Always On 구성 설정 및 클라이언트의 연결 속성 설정이 주 복제본 또는 보조 복제본 사용 여부를 결정합니다.  
  
1.  [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]의 Analysis Services 다차원 및 데이터 마이닝 모델 프로젝트에서 **데이터 원본** 을 마우스 오른쪽 단추로 클릭하고 **새 데이터 원본**을 선택합니다. **새로 만들기** 를 클릭하여 새 데이터 원본을 만듭니다.  
  
     또는 테이블 형식 모델 프로젝트에서 모델 메뉴를 클릭한 다음 **데이터 원본에서 가져오기**를 클릭합니다.  
  
2.  연결 관리자의 공급자에서 TDS(Tabular Data Stream) 프로토콜을 지원하는 공급자를 선택합니다. SQL Server Native Client 11.0이 이 프로토콜을 지원합니다.  
  
3.  연결 관리자의 서버 이름에 *가용성 그룹 수신기*의 이름을 입력하고 그룹에서 사용할 수 있는 데이터베이스를 선택합니다.  
  
     가용성 그룹 수신기는 읽기/쓰기 요청의 경우 클라이언트 연결을 주 복제본으로 리디렉션하고, 연결 문자열에 읽기 전용을 지정한 경우 보조 복제본으로 리디렉션합니다. 장애 조치 동안 복제본 역할이 변경되므로(주 복제본은 보조 복제본이 되고 보조 복제본은 주 복제본이 됨) 항상 이에 따라 클라이언트 연결이 리디렉션되도록 수신기를 지정해야 합니다.  
  
     가용성 그룹 수신기의 이름을 확인하려면 데이터베이스 관리자에게 문의하거나 가용성 그룹의 인스턴스 중 하나에 연결하여 해당 Always On 가용성 구성을 확인하면 됩니다.   
  
4.  계속해서 연결 관리자의 왼쪽 탐색 창에서 **모두** 를 클릭하여 데이터 공급자의 속성 표를 확인합니다.  
  
     보조 복제본에 대한 읽기 전용 연결을 구성하는 경우 **애플리케이션 의도** 를 **READONLY** 로 설정합니다. 그렇지 않으면 연결을 주 복제본으로 리디렉션하는 **READWRITE** 기본값을 유지합니다.  
  
5.  가장 정보에서 **특정 Windows 사용자 이름 및 암호 사용**을 선택한 다음 데이터베이스에 대해 최소 **db_datareader** 이상의 권한이 있는 Windows 도메인 사용자 계정을 입력합니다.  
  
     **현재 사용자의 자격 증명 사용** 이나 **상속**을 선택하지 마십시오. **서비스 계정 사용**은 선택할 수 있지만, 해당 계정이 데이터베이스에 대한 읽기 권한이 있어야 합니다.  
  
     데이터 원본을 완료하고 데이터 원본 마법사를 닫습니다.  
  
6.  활성 서버에 대한 빠른 검색과 연결을 제공하려면 연결 문자열에 **MultiSubnetFailover=Yes** 를 추가합니다. 이 속성에 대한 자세한 내용은 [고가용성 재해 복구를 위한 SQL Server Native Client 지원](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)을 참조하십시오.  
  
     이 속성은 속성 표에 표시되지 않습니다. 속성을 추가하려면 데이터 원본을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 선택합니다. 연결 문자열에 `MultiSubnetFailover=Yes` 를 추가합니다.  
  
 이제 데이터 원본이 정의되었습니다. 이제 모델 작성을 진행할 수 있습니다. 데이터 원본 뷰부터 시작하거나, 테이블 형식 모델인 경우 관계 만들기를 시작합니다. 지금 가용성 데이터베이스에서 데이터를 검색해야 하는 경우(예를 들어 솔루션을 처리 또는 배포할 준비가 된 경우) 구성을 테스트하여 보조 복제본 데이터에 액세스할 수 있는지를 확인할 수 있습니다.  
  
##  <a name="bkmk_test"></a> 구성 테스트  
 보조 복제본을 구성하고 Analysis Services에서 데이터 원본 연결을 만든 후에는 처리 및 쿼리 명령이 보조 복제본으로 리디렉션되는지 확인할 수 있습니다. 또한 계획된 수동 장애 조치를 수행하여 이 시나리오에 대한 복구 계획을 확인할 수 있습니다.  
  
#### <a name="step-1-confirm-the-data-source-connection-is-redirected-to-the-secondary-replica"></a>1단계: 데이터 원본 연결이 보조 복제본으로 리디렉션되는지 확인  
  
1.  SQL Server Profiler를 시작하고 보조 복제본을 호스팅하는 SQL Server 인스턴스에 연결합니다.  
  
     추적이 실행되면 **SQL:BatchStarting** 및 **SQL:BatchCompleting** 이벤트가 데이터베이스 엔진 인스턴스에서 실행 중인 Analysis Services에서 실행한 쿼리를 보여 줍니다. 이러한 이벤트는 기본적으로 선택되므로 사용자는 추적을 시작하기만 하면 됩니다.  
  
2.  [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]에서 테스트할 데이터 원본 연결이 포함된 Analysis Services 프로젝트 또는 솔루션을 엽니다. 데이터 원본은 그룹의 인스턴스가 아닌 가용성 그룹 수신기를 지정해야 합니다.  
  
     이 단계는 중요합니다. 서버 인스턴스 이름을 지정할 경우 보조 복제본으로의 라우팅이 발생하지 않습니다.  
  
3.  SQL Server Profiler와 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] 를 나란히 볼 수 있도록 애플리케이션 창을 배열합니다.  
  
4.  솔루션을 배포하고 배포가 완료되면 추적을 중지합니다.  
  
     추적 창에 **Microsoft SQL Server Analysis Services**애플리케이션의 이벤트가 표시됩니다. 보조 복제본을 호스팅하는 서버 인스턴스의 데이터베이스에서 데이터를 검색하는 **SELECT** 문이 표시되면 수신기를 통해 보조 복제본에 연결되었음을 알 수 있습니다.  
  
#### <a name="step-2-perform-a-planned-failover-to-test-the-configuration"></a>2단계: 계획된 장애 조치를 수행하여 구성 테스트  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 에서 주 복제본 및 보조 복제본 둘 다 동기 커밋 모드로 구성되었고 현재 동기화되어 있는지 확인합니다.  
  
     다음 단계는 보조 복제본이 동기 커밋으로 구성되어 있다고 가정합니다.  
  
     동기화를 확인하려면 주 복제본과 보조 복제본을 호스팅하는 각 인스턴스에 대한 연결을 열고, 데이터베이스 폴더를 확장하고, 각 복제본에서 데이터베이스의 이름 뒤에 **(동기화됨)** 및 **(동기화 중)** 이 추가되어 있는지 확인합니다.  
  
    > [!NOTE]  
    >  이러한 단계는 [가용성 그룹의 계획된 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)에서 가져왔으며, 이 링크는 이 작업 수행에 대한 추가 정보 및 다른 지침도 제공합니다.  
  
2.  SQL Server Profiler에서 각 복제본에 대한 추적을 시작하고 추적을 나란히 표시합니다. 다음 단계에서는 추적을 비교하여 Analysis Services의 처리 또는 쿼리에 사용되는 SQL 쿼리가 한 복제본에서 다른 복제본으로 전환되는지 확인합니다.  
  
3.  Analysis Services 내에서 처리 또는 쿼리 명령을 실행합니다. 데이터 원본을 읽기 전용 연결로 구성했으므로 명령이 보조 복제본에서 실행됩니다.  
  
4.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 보조 복제본에 연결합니다.  
  
5.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
6.  장애 조치할 가용성 그룹을 마우스 오른쪽 단추로 클릭하고 **장애 조치(Failover)** 명령을 선택합니다. 그러면 가용성 그룹 장애 조치(failover) 마법사가 시작됩니다. 마법사에서 새로운 주 복제본으로 설정할 복제본을 선택합니다.  
  
7.  장애 조치가 성공했음을 확인합니다.  
  
    -   [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 가용성 그룹을 확장하고 (주) 및 (보조) 지정을 확인합니다. 이전에 주 복제본이었던 인스턴스가 이제 보조 복제본이 되었습니다.  
  
    -   대시보드에서 상태 문제가 검색되었는지 확인합니다. 가용성 그룹을 마우스 오른쪽 단추로 클릭하고 **대시보드 표시**를 선택합니다.  
  
8.  백 엔드에서 장애 조치가 완료될 때까지 1, 2분 기다립니다.  
  
9. Analysis Services 솔루션에서 처리 또는 쿼리 명령을 반복한 다음 SQL Server Profiler에서 추적을 나란히 표시하여 확인합니다. 새 보조 복제본이 된 다른 인스턴스에서 처리가 진행됨을 알 수 있습니다.  
  
##  <a name="bkmk_whathappens"></a> 장애 조치 발생 후의 상황  
 장애 조치(failover) 중에 보조 복제본은 주 역할로 전환되고 이전의 주 복제본은 보조 역할로 전환됩니다. 모든 클라이언트 연결이 종료되고 가용성 그룹 수신기의 소유권은 주 복제본 역할과 함께 새 SQL Server 인스턴스로 옮겨지며 수신기 엔드포인트는 새 인스턴스의 가상 IP 주소 및 TCP 포트에 바인딩됩니다. 자세한 내용은 이 항목 뒷부분에 있는 [가용성 복제본에 대한 클라이언트 연결 액세스 정보&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)와 같은 시스템 데이터베이스, 사용자 데이터베이스를 비롯하여 보조 복제본을 호스트하는 서버 인스턴스의 읽기/쓰기 데이터베이스에는 데이터를 쓸 수 있습니다.  
  
 처리 중 장애 조치가 발생하면 Analysis Services의 로그 파일 또는 출력 창에 다음과 같은 오류가 나타납니다. "OLE DB 오류: OLE DB 또는 ODBC 오류: 통신 연결 오류입니다. 08S01; TPC 공급자: 현재 연결은 원격 호스트에 의해 강제로 끊겼습니다. ; 08S01."  
  
 이 오류는 잠시 기다렸다가 다시 시도하면 해결됩니다. 가용성 그룹이 읽기 가능한 보조 복제본에 대해 올바로 구성된 경우 처리를 재시도하면 새 보조 복제본에서 처리가 재개됩니다.  
  
 오류가 지속되면 구성 문제일 가능성이 큽니다. 보조 복제본에 대한 라우팅 목록, 읽기 전용 URL, 읽기 전용 문제를 해결하기 위해 T-SQL 스크립트를 다시 실행해 볼 수 있습니다. 또한 주 복제본에서 모든 연결을 허용하는지 확인해야 합니다.  
  
##  <a name="bkmk_writeback"></a> Always On 가용성 데이터베이스를 사용할 때의 쓰기 저장  
 쓰기 저장은 Excel의 가상 분석을 지원하는 Analysis Services 기능입니다. 또한 이 기능은 사용자 지정 애플리케이션에서 예산 작성 및 예측 태스크에 일반적으로 사용됩니다.  
  
 쓰기 저장을 지원하려면 READWRITE 클라이언트 연결이 필요합니다. Excel에서 읽기 전용 연결에 대한 쓰기 저장을 시도하면 다음과 같은 오류가 발생합니다. 오류가 발생합니다. 오류가 발생합니다.  
  
 항상 읽기 가능한 보조 복제본에 액세스하도록 연결을 구성했다면 이제 주 복제본에 대한 READWRITE 연결을 사용하는 새 연결을 구성해야 합니다.  
  
 이렇게 하려면 Analysis Services 모델에 읽기/쓰기 연결을 지원하는 데이터 원본을 추가로 만들어야 합니다. 추가 데이터 원본을 만들 때는 읽기 전용 연결에 지정한 동일한 수신기 이름 및 데이터베이스를 사용합니다. 단, **애플리케이션 의도**는 수정하지 않고 READWRITE 연결을 지원하는 기본값을 그대로 둡니다. 이제 읽기/쓰기 데이터 원본을 기반으로 하는 새 팩트 또는 차원 테이블을 데이터 원본 뷰에 추가하고, 새 테이블에 쓰기 저장을 설정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&amp;#40;SQL Server&amp;#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [활성 보조 복제본: 읽기 가능한 보조 복제본&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Always On 가용성 그룹을 통한 운영 문제에 대한 Always On 정책&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)   
 [데이터 원본 만들기&#40;SSAS 다차원&#41;](../../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)   
 [차원 쓰기 저장(writeback) 설정](../../../analysis-services/multidimensional-models/bi-wizard-enable-dimension-writeback.md)  
  
  
