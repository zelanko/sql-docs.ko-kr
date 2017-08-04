---
title: "고가용성 및 Master Data Services에 대 한 재해 복구 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: sabotta
ms.author: carlasab
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2afbf59101a0605dba2e79f09777160cb4de5cab
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---



# <a name="high-availability-and-disaster-recovery-for-master-data-services"></a>고가용성 및 재해 복구 Master Data Services에 대 한

**요약:** 이 문서에서는 AlwaysOn 가용성 그룹 구성에 호스트되는 MDS(Master Data Service)를 위한 솔루션에 대해 설명합니다. 이 문서에서는 SQL 2016 AlwaysOn AG(가용성 그룹)에 SQL 2016 Master Data Services를 설치 및 구성하는 방법을 설명합니다. 이 솔루션은 주로 SQL Server 데이터베이스에 호스트된 MDS 백엔드 데이터의 고가용성 및 재해 복구를 향상하는 데 사용됩니다.

## <a name="introduction"></a>소개


이 문서에 대 한 서비스 MDS (Master Data)는 AlwaysOn 가용성 그룹 구성에서 호스트 되는 솔루션에 설명 합니다. 문서에는 설치 하 고 SQL 2016 AlwaysOn 가용성 그룹 (AG)에 SQL 2016 MDS를 구성 하는 방법을 설명 합니다. 이 솔루션은 주로 SQL Server 데이터베이스에 호스트된 MDS 백엔드 데이터의 고가용성 및 재해 복구를 향상하는 데 사용됩니다.

솔루션을 구현 하려면이 문서에서 다루는 다음 작업을 완료 해야 합니다.

1.  [설치 및 Windows Server 장애 조치 클러스터 (WSFC)를 설정](#windows-server-failover-cluster-wsfc)합니다.

2.  [AlwaysOn AG 설정](#sql-server-alwayson-availability-group)합니다.

3.  [WSFC 노드에서 실행 하는 MDS 구성](#configure-mds-to-run-on-an-wsfc-node)합니다.

위의 섹션 뒤에 지침 기술을 간략하게 소개 합니다. 기술에 대 한 자세한 내용은 각 섹션에 연결 된 문서를 검토 하십시오.

이 문서에서 설명 하는이 솔루션은 각 데이터베이스에 여러 개의 동기 또는 비동기 복제본 SQL Server AlwaysOn AG 위에 빌드됩니다. 하나의 복제본만 트랜잭션 (사용자 요청을 수락)를 허용 합니다. 주 복제본입니다.

각 복제본이이 솔루션의 중앙 집중식된 공유 저장소가 있으므로 자체적인 저장소를 있습니다. 소프트웨어 오류 나 주 복제본에 영향을 주는 하드웨어 오류가 있는 경우 주 복제본은 자동 또는 수동으로 구성 및 상황에 따라 동기 또는 비동기 복제본에 조치 장애 수 있습니다. 이 사용자에 게 중단 최소화 하면서 데이터베이스의 고가용성을 보장합니다.

일반적으로 비동기 복제본은 주 복제본의 데이터 센터에서 원격 데이터 센터에서 호스팅됩니다. 재해 시나리오의 경우 주 복제본 다른 데이터 센터로 조치할 수 있습니다. 이 데이터베이스의 재해 복구를 보장합니다.

이 문서에서 설명 하는 솔루션 데모 목적을 위해 다음 버전의 소프트웨어를 사용 합니다. 이전 버전에는 잠재적으로 약간의 차이가와 동일 하 게 작동 해야 합니다.

-   서버 장애 조치 클러스터와 Windows Server 2012 r 2

-   SQL Server 2016 Master 데이터 서비스 기능

솔루션은 두 개의 Vm을 사용 하는 또한 **MDS HA1** 및 **MDS HA2**, 두 개의 복제본을 호스팅해야 합니다. SQL Server AlwaysOn AG에서 지 원하는,으로 MDS는 사용할 수는 복제본의 수를 제한 하지 않습니다.

이 문서에서는 Windows Server, Windows Server 장애 조치 클러스터, SQL Server AlwaysOn 및 SQL Server MDS에 대 한 기본 지식이 있다고 가정 합니다.

## <a name="what-is-not-covered"></a>적용 되지 않는 기능

이 문서는 다음 적용 되지 않습니다.

-   IIS, 웹 서버에서 마스터를 호스트 하는 방법을 데이터 서비스에서 UI를 항상 사용 가능 하 고 재해 발생 후 복구할 수 있습니다. MDS에서는 항상 사용 가능 IIS 및 부하 분산을 표준 기술을 작동할 여기 수 있도록 IIS의 모든 특정 요구 사항을 적용 하지 않습니다.

-   MDS 백 엔드에서 고가용성 (HA)를 지원 하기 위해 SQL Server AlwaysOn (FCI) 장애 조치 클러스터를 사용 하는 방법. SQL Server 장애 조치 클러스터링은 다른 HA 솔루션 및 SQL Server에서 공식적으로 지원 되 고 MDS와 함께 작동 합니다.

-   MDS 백 엔드에서 HA를 지원 하기 위해 SQL Server 장애 조치 클러스터 (FCI) 및 AlwaysOn AG의 하이브리드 솔루션을 사용 하는 방법. 하이브리드 솔루션 MDS와 함께 작동 합니다.

## <a name="design-consideration"></a>디자인 고려 사항

그림 1에는 AlwaysOn AG에서 주로 사용 되는 일반적인 구성을 보여 줍니다. 주 데이터 센터에서 두 복제본이 동기 커밋 관계와 하 고 복제본을 모두 투표 권한이 있습니다. 이 주 복제본이 실패 하는 경우 HA를 개선 하기 위해 주로 사용 됩니다.

재해 복구 데이터 센터에이 비동기 커밋 주와 관계가 있는 보조 복제본입니다. 이 데이터 센터는 일반적으로 기본 데이터 센터와 다른 지리적 지역에 있습니다. 보조 복제본에 투표 권한을 있지 않습니다.

이 구성은 경우 주 데이터 센터에 화재, 지진 등의 재해 복구를 달성 하기 위해 사용 됩니다. 구성에서 두 HA 및 상대적으로 낮은 비용으로 재해를 복구 합니다.

![AlwaysOn 가용성 그룹에 대 한 일반적인 구성](media/Fig1_TypicalConfig.png)

그림 1. 일반적인 AlwaysOn 가용성 그룹 구성

재해 복구를 필요 하지 않으면, 복제본을 보조 데이터 센터에 있이 필요가 없습니다. HA를 개선 하기 위해 필요한 경우 동기 복제본이 더 많은 정보가 포함 된 동일한 기본 데이터 센터에 있을 수 있습니다.

따라서 것이 중요 시나리오 및 요구 사항을 고려 하 고 비동기 및 동기 복제본의 수를 선택 하려면, 및 되는 데이터 센터가 있습니다에 템플릿을 저장 해야 합니다.

## <a name="windows-server-failover-cluster-wsfc"></a>Windows Server 장애 조치 클러스터 (WSFC)

이 섹션에서는 다음 작업에 설명 합니다.

1.  [Windows 장애 조치 클러스터 기능을 설치](#install-failover-cluster-feature)합니다.

2.  [Windows Server 장애 조치 클러스터 만들기](#create-a-windows-server-failover-cluster)합니다.

그림 1 이전 섹션에 나와 있는 것 처럼 Windows Server 장애 조치 클러스터 (WSFC)이이 문서에서 설명 하는 솔루션에 포함 되어 있습니다. SQL AlwaysOn 오류 검색 및 장애 조치에 대 한 WFSC에 의존 하기 때문에 WSFC를 설정 해야 합니다.

WSFC는 응용 프로그램 및 서비스의 고가용성을 향상 시키는 기능입니다. Microsoft 장애 조치 클러스터 서비스에서 해당 인스턴스에서 실행 중인와 독립적인 windows 서버 인스턴스의 그룹으로 구성 합니다. Windows server 인스턴스 (또는 노드 때때로 이라고 하는 대로) 서로 통신할 수 있으며 실패 감지를 수행할 수 있도록 연결 되어 있습니다. WSFC 오류 감지 및 장애 조치 기능을 제공 합니다. 클러스터의 노드 또는 서비스가 실패 하는 경우 다음에 오류가 검색 되 면 및 실패 한 노드에서 호스팅되는 서비스를 제공 하기 시작 자동 또는 수동으로 다른 노드로 합니다. 따라서 사용자는만 서비스에서 최소 중단 될 및 서비스 가용성이 향상 됩니다.  

### <a name="prerequisites"></a>필수 구성 요소

모든 인스턴스에서 Windows Server 운영 체제를 설치 하 고 모든 업데이트가 패치 합니다.

>[!NOTE] 
>**매우 권장** 동일한 Windows 버전 및 잠재적인 비 호환성 문제를 방지 하기 위해 모든 인스턴스에서 설정 같은 기능을 설치 합니다.

### <a name="install-failover-cluster-feature"></a>장애 조치 클러스터 기능 설치

Windows 서버 인스턴스마다 각 인스턴스에서 WSFC 기능을 설치 하려면 다음 단계를 완료 합니다. 관리자 권한이 필요 합니다.

1.  열기 **서버 관리자** Windows Server 및 클릭 **역할 및 기능 추가** 오른쪽 창에서. 이 시작 됩니다는 **역할 및 추가 기능 마법사**합니다.

2.  클릭 **다음** 씩 증가 하는 **기능** 페이지.

3.  선택 된 **장애 조치 클러스터링** 확인란을 클릭 하 고 **다음** 설치를 완료 합니다. 그림 2를 참조 하십시오.

    에 대 한을 확인 하 여 메시지 **장애 조치 클러스터링에 필요한 기능 추가**, 클릭 **기능 추가**합니다. 그림 3을 참조 하십시오.

    ![역할 및 기능 추가 마법사, 장애 조치 클러스터링](media/Fig2_SelectFeatures.png)

    그림 2

    ![역할 및 기능 마법사를 장애 조치 클러스터에 필요한 추가](media/Fig3_RequiredFeaturesFailover.png)

    그림 3

4.  에 **확인** 페이지를 클릭 **설치** 장애 조치 클러스터링 기능을 설치 합니다.

5.  에 **결과** 페이지에서 오류 및 경고 없이 성공적으로 설치 되어 모든 항목이 있는지 확인 합니다.

### <a name="create-a-windows-server-failover-cluster"></a>Windows Server 장애 조치(Failover) 클러스터 만들기

모든 인스턴스에서 WSFC 기능이 설치 된 후에 WSFC를 구성할 수 있습니다. 노드 하나에서이 작업을 수행 하기만 합니다.

1.  열기 **서버 관리자** Windows Server 및 클릭 **장애 조치 클러스터 관리자** 에 **도구** 관리자를 시작 하려면 오른쪽 위 모서리에 메뉴.

2.  **장애 조치 클러스터 관리자**, 클릭 **구성 유효성 검사** 오른쪽 창에서. 그림 4 참조 하십시오.

    ![장애 조치 클러스터 관리자에서 구성 유효성 검사](media/Fig4_ValidateConfig.png)

    그림 4

3.  에 **구성 유효성 검사** **마법사**, 클릭 **다음**합니다.

4.  에 **서버 선택 또는 클러스터** 대화 상자를 클릭 한 다음 SQL Server를 호스트 하는 서버 이름 추가 **다음**합니다. 그림 5 참조 합니다.

    이 예에서는 두 개의 인스턴스, MDS HA1와 MDS HA2 추가 했습니다.

    ![구성 마법사, 서버 선택 또는 클러스터 페이지 유효성 검사](media/Fig5_AddServer.png)

    그림 5

5.  에 **테스트 옵션** 페이지 **모든 테스트를 실행**, 클릭 하 고 **다음**합니다.

6.  클릭 **다음** 유효성 검사를 완료 합니다.

    **Validating** 페이지 표시 등의 진행 상황 및 **요약** 페이지 유효성 검사 요약을 보여 줍니다. 그림 6과 7을 참조 하십시오.

7.  에 **요약** 페이지에서 경고 또는 오류 메시지를 확인 합니다.

    오류를 수정 해야 합니다. 그러나 경고는 문제가 아닐 수 있습니다. 경고 메시지는 "테스트 된 항목의 요구 사항을 충족할 수 있지만 확인 해야 리"를 의미 합니다. 예를 들어 그림 7에서는 "확인 디스크 액세스 대기 시간" 경고를 일시적으로 다른 작업에 사용 되 고 디스크 때문일 수 있습니다 및 무시할 수 있습니다. 각 경고에 대 한 온라인 설명서 및 자세한 내용은 오류 메시지를 확인 해야 합니다. 그림 7을 참조 하십시오.
 
    ![유효성 검사 구성 마법사, 유효성 검사 중 페이지](media/Fig6_ValidationTests.png)

    그림 6

    ![유효성 검사 구성 마법사, 요약 페이지](media/Fig7_ValidationSummary.png)

    그림 7

8.  에 **요약** 페이지를 확인 하는 **검사 된 노드를 사용 하 여 클러스터 만들기** 확인란을 선택한 다음 클릭 **마침** 시작 하는 **클러스터 만들기** **마법사**합니다.

9.  에 **클러스터 만들기** **마법사**, 클릭 **다음**합니다.

10. 에 **클러스터 관리 액세스 지점** 페이지, WSFC 클러스터 이름을 입력 한 다음 클릭 **다음**합니다. 이 예제에서는 사용 됨 "MDS-HA" 클러스터 이름입니다. 그림 8 참조 합니다.

    ![클러스터 이름 입력](media/Fig8_EnterClusterName.png)

    그림 8

11. 계속 클릭 **다음** 클러스터 만들기를 완료 합니다. **요약의 클러스터 MDS-HA** 섹션 클러스터 정보가 표시 됩니다. 그림 9를 참조 하십시오.

    ![클러스터에 대 한 요약 정보 보기](media/Fig9_ClusterSummary.png)

    그림 9

    나중에 노드를 추가 하는 경우 클릭 **노드 추가** 의 오른쪽 창에서 작업 **장애 조치 클러스터 관리자**합니다.

참고:

-   모든 Windows Server 버전에서 WSFC 기능을 사용 하지 못할 수도 있습니다. 버전에이 기능이 있는지 확인 합니다.

-   Active directory에 WSFC를 설정 하는 적절 한 권한이 있는지 확인 합니다. 모든 문제가 있으면 [장애 조치 클러스터 단계별 가이드: Active Directory에서 계정 구성](https://technet.microsoft.com/library/cc731002(v=ws.10).aspx)합니다.

WSFC에 대 한 정보를 자세한 참조 [장애 조치 클러스터](https://technet.microsoft.com/library/cc732488(v=ws.10).aspx)합니다.

## <a name="sql-server-alwayson-availability-group"></a>SQL Server AlwaysOn 가용성 그룹

이 섹션에서는 다음 작업에 설명 합니다.

1.  [Enable SQL Server AlwaysOn 가용성 그룹](#enable-sql-server-alwayson-availability-group-on-every-sql-server-instance)합니다.

2.  [가용성 그룹 만들기](#create-an-availability-group)합니다.

3.  [유효성을 검사 하 고 가용성 그룹을 테스트](#validation-and-test-the-availability-group)합니다.

Sql Server AlwaysOn 솔루션 SQLServer 데이터베이스에 대 한 고가용성 및 재해 복구를 제공합니다. AlwaysOn에는 두 가지 가능한 해결 방법이 있습니다.
두 WSFC 위에 구축 됩니다.

-   AlwaysOn 가용성 그룹 (AG)

-   AlwaysOn 장애 조치 클러스터 인스턴스 (FCI).

AG은 데이터베이스 수준 고가용성을 향상 시킵니다. (사용자 데이터베이스 집합) AG와 해당 가상 네트워크 이름은 wsfc에서 리소스 그룹으로 등록 됩니다.

FCI는 인스턴스 수준 고가용성을 향상 시킵니다. SQL Server 서비스 및 관련된 서비스는 wsfc에서 리소스 그룹으로 등록 됩니다. 또한 FCI 솔루션 WFC 클러스터의 모든 노드에 사용할 수 있어야 하는 SAN 또는 SMB 파일 공유와 같은 대칭 공유 디스크 저장소가 필요 합니다.


### <a name="prerequisites"></a>필수 구성 요소

-   모든 노드의 SQL Server를 설치 합니다. 자세한 내용은 [SQL Server 2016 설치](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server)를 참조하세요.

-   (권장) 모든 노드에 대해 정확히 동일한 SQL Server 기능 집합 및 버전을 설치 합니다. 특히, MDS 설치 되어야 합니다.

-   (권장) 모든 SQL Server 인스턴스에서 동일한 구성을 사용 합니다. 특히, 동일한 서버 데이터 정렬에서 모든 SQL Server 인스턴스에 구성 되어야 합니다.

-   (권장) 모든 SQL Server 인스턴스를 실행 하는 동일한 서비스 계정을 사용 합니다. 그렇지 않으면 SQL Server 인스턴스는 서로 통신할 수 있는지 확인 하려면 각 SQL Server 인스턴스에 대 한 권한을 부여 해야 합니다.

-   Windows 방화벽 설정을 서로 통신 하는 SQL Server 인스턴스에 수 있는지 확인 합니다.

### <a name="enable-sql-server-alwayson-availability-group-on-every-sql-server-instance"></a>모든 SQL Server 인스턴스에서 enable SQL Server AlwaysOn 가용성 그룹

1.  에 **SQL Server 구성 관리자** 클릭 **SQL Server 서비스** 왼쪽된 창에서 마우스 오른쪽 단추로 클릭 **SQL Server** 클릭 한 다음 확인 하 고 오른쪽 창에서 **속성**합니다. 그림 10 참조 합니다.

    ![SQL Server 속성 창](media/Fig10_SQLServerProperties.png)

    그림 10

2.  에 **SQL Server (MSSQLSERVER)** **속성** 대화 상자를 클릭는 **AlwaysOn 고가용성** 탭을 선택 합니다는 **AlwaysOn 가용성 그룹 사용** 확인란 합니다. 에 값을 표시 하는 경우는 **Windows 장애 조치 클러스터 이름** 텍스트 상자 클릭 **확인** 를 계속 합니다. 그림 11을 참조 하십시오.

    ![AlwaysOn 가용성 그룹 옵션을 사용 하도록 설정](media/Fig11_EnableAlwaysOn.png)

    그림 11

3.  경고 페이지가 표시 되 면 클릭 **확인** 를 계속 합니다. 그림 12를 참조 하십시오.

    ![서비스를 다시 시작 및 중지를 확인 하십시오.](media/Fig12_WarningServiceStopStart.png)

    그림 12

4.  클릭 **다시 시작**, 다시 시작 하는 **SQL Server** 서비스 하 고이 변경 내용을 적용 합니다. 그림 10 참조 합니다.

>[!NOTE] 
>사용 하 여 SQL Server 서비스를 실행 하는 서비스 계정은 변경할 수는 **SQL Server 구성 관리자**합니다. 클릭는 **로그온** 탭에 **SQL Server (MSSQLSERVER)** **속성** 대화 상자. 그림 11을 참조 하십시오.

### <a name="create-an-availability-group"></a>가용성 그룹 만들기

모든 SQL Server 인스턴스에서 AlwaysOn 기능을 활성화 한 후 노드 하나에서 MDS 데이터베이스를 포함 하는 새 AG 만듭니다.

AG 기존 데이터베이스에만 만들 수 있습니다. 따라서 어느 한 노드에서 MDS 데이터베이스를 만들 또는 임시 데이터베이스를 만들 하 고 다음 임시 데이터베이스를 삭제 합니다. 이 예제에서는 emptyMDS 데이터베이스를 만든 하 AG이 MDS 데이터베이스에 만듭니다.

1.  시작 **SQL Server Management Studio** (**SSMS**) 노드에서 적절 한 자격 증명으로 로컬 SQL Server 인스턴스에 연결 합니다.

2.  SSMS에서 열고는 **새 쿼리** 빈 데이터베이스를 만듭니다. 다음 스크립트 창 및 실행 합니다. C: 대체\\전체 백업을 수행 하는 데 사용할 임시 위치를 사용 합니다.

    ```
    CREATE DATABASE MDS\_Sample
    GO
    BACKUP DATABASE MDS\_Sample TO DISK='C:\\temp'
    GO
    ```

    >[!NOTE] 
    >전체 데이터베이스 백업 작업이이 데이터베이스에는 AG 만드는 필요 합니다.

3.  에 **개체 탐색기**를 확장 하 고는 **AlwaysOn 고가용성** 폴더 **새 가용성 그룹 마법사** 시작 하는 **새 가용성 그룹 마법사**합니다. 그림 13을 참조 하십시오.

    ![새 가용성 그룹 시작 마법사](media/Fig13_AvailabilityGroupsFolder.png)

    그림 13

4.  에 **새 가용성 그룹** 마법사를 클릭 하 여 **다음** 표시 하는 **이름 지정** 페이지. AG에 대 한 이름을 입력 한 다음 클릭 **다음**합니다. 그림 14를 참조 하십시오.

    ![가용성 그룹의 이름을 입력 합니다.](media/Fig14_AvailabilityGroupName.png)

    그림 14

5.  만든 데이터베이스를 클릭는 **데이터베이스 선택** 페이지를 선택한 다음 클릭 **다음**합니다. 그림 15를 참조 하십시오.

    ![데이터베이스 선택](media/Fig15_AvailabilityGroupSelectDatabase.png)

    그림 15

6.  에 **복제본 지정** 페이지를 클릭 하 여 다른 복제본을 추가 **Add Replica**합니다. 이 페이지는 이미 복제본으로 현재, 로컬 SQL Server 인스턴스를 나열합니다. 그림 16을 참조 하십시오.

7.  에 **서버에 연결** 대화 상자, 적절 한 자격 증명을 추가 하 고 클릭 **연결**합니다.

    ![SQL Server 인스턴스에 연결](media/Fig16_AddReplicaConnectServer.png)

    그림 16

    이제 두 개의 복제본 목록에 표시 되어야 합니다. 복제본으로 다른 노드를 추가 하려면이 단계를 반복 합니다. 그림 17을 참조 하십시오.

    ![복제본 목록 보기](media/Fig17_AvailabilityGroupSQLReplicas.png)

    그림 17

    각 복제본에 대해 다음을 구성 **동기 커밋**, **자동 장애 조치**, 및 **읽기용 보조 복제본** 설정 합니다. 그림을 참조 하세요
17.

    **동기 커밋**: 이렇게 하는 경우 트랜잭션을 커밋하는 데이터베이스의 주 복제본에서 다음 트랜잭션이 에서도 커밋되기 다른 모든 동기 복제본입니다. 비동기 커밋 작업이 반드시이 하 고 주 복제본 뒤에 지연 될 수 있습니다.

    일반적으로 동일한 데이터 센터에 두 개의 노드가 있는 경우에 동기 커밋을 사용 해야 합니다. 여러 데이터 센터에 있더라도 동기 커밋 데이터베이스 성능이 느려질 수 있습니다.

    이 확인란을 선택 하지 않으면 비동기 커밋 ´ ù.

    **자동 장애 조치:** 다운 주 복제본이 있는 경우 AG가 자동으로 해당 보조 복제본으로 장애 조치 자동 장애 조치를 선택 합니다. 동기 커밋으로 복제본에만 사용할 수 있습니다.

    **읽기 가능한 보조:** 기본적으로 사용자가 모든 보조 복제본에 연결할 수 없습니다. 이렇게 하면 사용자가 읽기 전용 액세스 권한이 있는 보조 복제본에 연결할 수 있습니다.

8.  에 **복제본 지정** 페이지는 **수신기** 탭 하 고 다음을 수행 합니다. 그림 18을 참조 하십시오.

    a.  클릭 **가용성 그룹 수신기를 만드는** 을 MDS 데이터베이스 연결에 대 한 가용성 그룹 수신기를 설치 합니다.

    b.  입력 한 **수신기 DNS 이름**, MDSSQLServer 등입니다.

    c.  에 기본 SQL 포트 1433을 입력에서 **포트** 입력란.

    d.  DHCP의 입력는 **네트워크 모드** 텍스트 상자 및 클릭 한 다음 **다음** 를 계속 합니다.

    >[!NOTE] 
    >필요에 따라 "고정 IP"으로 선택할 수 있습니다는 **네트워크 모드** 고정 IP를 입력 합니다. 포트 1433 이외의 포트를 입력할 수 있습니다. 

    ![수신기를 구성](media/Fig18_AvailabilityGroupCreateListener.png)

    그림 18

9.  에 **데이터 동기화 선택** 페이지 **전체**, 고 모든 노드에 액세스할 수 있는 네트워크 공유를 지정 합니다. 계속하려면 **다음** 을 클릭합니다. 그림 19를 참조 하십시오.

    이 네트워크 공유 데이터베이스 백업을 보조 복제본을 만드는 저장에 사용 됩니다. 조직에 대해 사용할 수 없는 경우에 다른 데이터 동기화 기본 설정을 선택 합니다. 참조 [SQL Server 2016 AlwaysOn 가용성 그룹](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server) 보조 복제본을 만드는 다른 옵션을 사용 하는 방법에 있습니다. 또한 그림 17 다른 옵션을 나열합니다.

    ![데이터 동기화를 구성 합니다.](media/Fig19_AvailabilityGroupDataSync.png)

    그림 19 

10. 에 **유효성 검사** 페이지에서 모든 유효성 검사를 성공적으로 전달 하 고 오류를 수정 해야 합니다. 계속하려면 **다음** 을 클릭합니다.

11. 에 **요약** 페이지에서 모든 구성 설정을 검토 하 고 클릭 **마침**합니다. 이 가용성 그룹을 만들려고 하 고 구성 합니다.

12. 에 **결과** 페이지에서 필요한 모든 단계 완료 된 되었는지 확인 합니다.

### <a name="validation-and-test-the-availability-group"></a>유효성 검사 및 테스트 가용성 그룹

1.  SSMS를 열고에서 방금 만든 수신기 DNS 이름에 연결 된 [가용성 그룹을 만드는](#create-an-availability-group) 섹션. 이 예제에서는 MDSSQLServer 되었기 합니다.

2.  **개체 탐색기**를 확장 하 고는 **AlwaysOn 고가용성** 폴더, 방금 AG에서 만든 마우스 오른쪽 단추로 클릭은 [가용성 그룹을 만드는](#create-an-availability-group) 섹션을 선택한 다음 클릭 **대시보드 표시**합니다. 그림 20을 참조 하십시오. 새 AG와 해당 복제본의 상태가 표시 됩니다.

    ![대시보드 보기](media/Fig20_ShowDashboard.png)

    그림 20 

3.  클릭 **장애 조치** 동기 복제본에서 비동기 복제본으로 장애 조치를 수행 하 합니다. 이 해당 장애 조치가 문제 없이 올바르게 실행 확인 합니다.

 AlwaysOn 설정 완료 됩니다.

AlwaysOn 가용성 그룹에 대 한 자세한 내용은 참조 [SQL Server 2016 AlwaysOn 가용성 그룹](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server)합니다.

## <a name="configure-mds-to-run-on-an-wsfc-node"></a>WSFC 노드에서 실행 하는 MDS 구성

이 문서에 제공 된이 솔루션에는 WSFC에서 실행 되는 MDS 백 엔드 데이터베이스를 하기만 합니다. 웹 응용 프로그램 및 MDS 구성 관리자 같은 MDS의 다른 부분으로 MDS AG에 연결할 수 노드 WSFC의 또는 WSFC에서 외부에서 실행할 수 있습니다.

1.  열기 **마스터 데이터 서비스 구성 관리자** 한 노드에서 클릭 **데이터베이스 구성**, 클릭 하 고 **Create Database** 시작 하는 **데이터베이스 만들기 마법사**합니다.

2.  에 **데이터베이스 서버** 페이지에서, AG 수신기 DNS 이름에 입력는 **SQL Server 인스턴스** 텍스트 상자 클릭 **연결 테스트**, 클릭 하 고 **다음**합니다. 그림 21을 참조 하십시오.

    ![AG 수신기와 데이터베이스 서버 구성](media/Fig21_MDSDatabaseServerListener.png)

    그림 21

3.  에 **데이터베이스** 페이지에서 만든 데이터베이스의 이름을 입력 합니다는 [가용성 그룹을 만드는](#create-an-availability-group) 섹션을 선택한 다음 클릭 **다음**합니다. 그림 22를 참조 하십시오.

    ![데이터베이스 만들기 및 구성](media/Fig22_MDSCreateDatabase.png)

    그림 22

4.  완료 된 **데이터베이스 만들기** **마법사**합니다. 자세한 내용은 참조 [Master Data Services 설치 및 구성](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration)합니다.

5.  클릭 **웹 응용 프로그램** 에 **마스터 데이터 서비스 구성 관리자** 웹 응용 프로그램을 구성을 클릭 한 다음 **적용** MDS에 설정을 적용 하기. 그림 23을 참조 하십시오. 자세한 내용은 참조 [Master Data Services 설치 및 구성](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration)합니다.

    ![웹 응용 프로그램 구성](media/Fig23_MDSWebApplication.png)

    그림 23

    MDS 설치 프로그램이 완료 됩니다. 모든 노드에서 실행할 MDS를 설정 하려면 위의 단계를 반복할 수 있습니다. 백 엔드 데이터베이스는 동일한 AG에 같습니다.

6.  이전에 임시 데이터베이스를 만든 경우 (참조 [가용성 그룹을 만드는](#create-an-availability-group) 섹션) AlwaysOn AG를 만들려면 다음 삭제 해야 임시 데이터베이스

    마스터 데이터 서비스에 대 한 자세한 내용은를 참조 [Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds)합니다.

## <a name="conclusion"></a>결론

이 백서를 설정 하 고 SQL Server AlwaysOn 가용성 그룹 위에 Master Data Services 백 엔드 데이터베이스를 구성 하는 방법을 살펴보았습니다. 이 구성은 Master Data Services 백 엔드 데이터베이스에 고가용성 및 재해 복구를 제공합니다. 이 구성을 구현 하려면 Windows Server 장애 조치 클러스터를 SQL Server AlwaysOn 가용성 그룹, 및 Master Data Services 설치 및 구성 해야 합니다.

## <a name="feedback"></a>피드백

이 백서가 도움이 되었습니까? 보내 주십시오 여러분의 의견을 클릭 하 여 **주석** 문서 맨 위에 있는 합니다. 

사용자 의견에 배포 하는 백서의 품질을 개선 하는 데 도움이 됩니다. 


