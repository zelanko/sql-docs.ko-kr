---
title: "Master Data Services에 대한 고가용성 및 재해 복구 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fe2bcae7a0f5694cf744df9c7d44b6fd2253c4b8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="high-availability-and-disaster-recovery-for-master-data-services"></a>Master Data Services에 대한 고가용성 및 재해 복구

**요약:** 이 문서에서는 AlwaysOn 가용성 그룹 구성에 호스트되는 MDS(Master Data Service)를 위한 솔루션에 대해 설명합니다. 이 문서에서는 SQL 2016 AlwaysOn AG(가용성 그룹)에 SQL 2016 Master Data Services를 설치 및 구성하는 방법을 설명합니다. 이 솔루션은 주로 SQL Server 데이터베이스에 호스트된 MDS 백엔드 데이터의 고가용성 및 재해 복구를 향상하는 데 사용됩니다.

## <a name="introduction"></a>소개


이 문서에서는 AlwaysOn 가용성 그룹 구성에 호스트되는 MDS(Master Data Service)를 위한 솔루션에 대해 설명합니다. 이 문서에서는 SQL 2016 AlwaysOn AG(가용성 그룹)에 SQL 2016 MDS를 설치 및 구성하는 방법을 설명합니다. 이 솔루션은 주로 SQL Server 데이터베이스에 호스트된 MDS 백엔드 데이터의 고가용성 및 재해 복구를 향상하는 데 사용됩니다.

솔루션을 구현하려면 이 문서에서 다루는 다음 작업을 완료해야 합니다.

1.  [WSFC(Windows Server 장애 조치 클러스터)를 설치 및 설정](#windows-server-failover-cluster-wsfc)합니다.

2.  [AlwaysOn AG를 설정](#sql-server-alwayson-availability-group)합니다.

3.  [WSFC 노드에서 실행하는 MDS를 구성](#configure-mds-to-run-on-an-wsfc-node)합니다.

위의 섹션에서는 지침에 이어 기술을 간략히 소개합니다. 기술에 대한 자세한 내용은 각 섹션에 연결된 문서를 검토하십시오.

이 문서에서 설명하는 이 솔루션은 각 데이터베이스에 여러 개의 동기 또는 비동기 복제본이 있는 SQL Server AlwaysOn AG를 기반으로 작성되었습니다. 하나의 복제본만 트랜잭션을 허용합니다(사용자 요청을 수락). 이는 주 복제본입니다.

각 복제본에는 자체 저장소가 있으므로 이 솔루션에는 중앙 집중식 공유 저장소가 없습니다. 주 복제본에 영향을 주는 소프트웨어 오류나 하드웨어 오류가 있는 경우 주 복제본은 자동 또는 수동으로 구성 및 상황에 따라 동기 또는 비동기 복제본에 장애 조치될 수 있습니다. 이는 사용자에게 중단을 최소화한 데이터베이스의 고가용성을 보장합니다.

일반적으로 비동기 복제본은 주 복제본 데이터 센터에서 멀리 떨어진 데이터 센터에서 호스팅됩니다. 재해 시나리오의 경우 주 복제본이 다른 데이터 센터로 장애 조치될 수 있습니다. 이는 데이터베이스의 재해 복구를 보장합니다.

이 문서에서 설명하는 솔루션은 예시용으로 다음 버전의 소프트웨어를 사용합니다. 이전 버전은 동일한 작동해야 하며, 잠재적으로 약간의 차이가 있습니다.

-   Server 장애 조치(Failover) 클러스터가 있는 Windows Server 2012 R2

-   Master Data Service 기능이 있는 SQL Server 2016

또한 솔루션은 **MDS-HA1** 및 **MDS-HA2**의 두 개의 VM을 사용하여 두 개의 복제본을 호스팅합니다. SQL Server AlwaysOn AG에서 지원되는 한, MDS는 사용할 수 있는 복제본의 수를 제한하지 않습니다.

이 문서에서는 사용자가 Windows Server, Windows Server 장애 조치(Failover) 클러스터, SQL Server AlwaysOn 및 SQL Server MDS에 대한 기본 지식이 있다고 가정합니다.

## <a name="what-is-not-covered"></a>다루지 않는 내용

이 문서에서는 다음을 다루지 않습니다.

-   재해 후 웹 서버에서 Master Data Service UI를 호스팅하는 IIS의 고가용성 및 복구 가능을 구현하는 방법. MDS는 IIS의 특정 요구 사항을 적용하지 않으므로 IIS의 고가용성 및 부하 분산을 가능케 하는 표준 기술도 여기서 함께 작동할 수 있습니다.

-   MDS 백 엔드에서 HA(고가용성)를 지원하기 위해 SQL Server AlwaysOn 장애 조치 (FCI) 클러스터를 사용하는 방법. SQL Server 장애 조치(failover) 클러스터링은 다른 HA 솔루션이며 SQL Server에서 공식적으로 지원되고 MDS와 함께 작동합니다.

-   MDS 백 엔드에서 HA를 지원하기 위해 SQL Server 장애 조치(failover) 클러스터 (FCI) 및 AlwaysOn AG의 하이브리드 솔루션을 사용하는 방법. 하이브리드 솔루션은 MDS와 함께 작동합니다.

## <a name="design-consideration"></a>설계 고려 사항

그림 1에는 AlwaysOn AG에서 주로 사용되는 일반적인 구성이 나와 있습니다. 주 데이터 센터에는 동기 커밋 관계가 있는 두 복제본이 있으며, 두 복제본에는 모두 투표 권한이 있습니다. 이는 주 복제본이 실패하는 경우 HA를 개선하기 위해 주로 사용됩니다.

재해 복구 데이터 센터에는 주 복제본과 함께 비동기 커밋 관계가 있는 보조 복제본이 있습니다. 이 데이터 센터는 일반적으로 기본 데이터 센터와 지리적으로 다른 지역에 있습니다. 보조 복제본에는 투표 권한이 없습니다.

이 구성은 주 데이터 센터에 화재, 지진 등의 재해가 발생한 경우 복구를 달성하기 위해 사용됩니다. 구성은 상대적으로 낮은 비용으로 두 HA 및 재해 복구를 달성합니다.

![AlwaysOn 가용성 그룹을 위한 일반적인 구성](media/Fig1_TypicalConfig.png)

그림 1. 일반적인 AlwaysOn 가용성 그룹 구성

재해 복구를 고려할 필요가 없는 경우 복제본을 보조 데이터 센터에 둘 필요가 없습니다. HA를 개선해야 하는 경우 더 많은 동기 복제본을 동일한 주 데이터 센터에 둘 수 있습니다.

따라서 시나리오 및 요구 사항을 고려하고, 필요한 비동기 및 동기 복제본의 수와 복제본을 두어야 하는 데이터 센터를 선택하는 것이 중요합니다.

## <a name="windows-server-failover-cluster-wsfc"></a>WSFC(Windows Server 장애 조치(Failover) 클러스터)

이 섹션에서는 다음 작업에 대해 설명합니다.

1.  [Windows 장애 조치(Failover) 클러스터 기능을 설치](#install-failover-cluster-feature)합니다.

2.  [Windows Server 장애 조치(Failover) 클러스터를 만듭니다](#create-a-windows-server-failover-cluster).

이전 섹션의 그림 1에 나와 있는 것처럼 이 문서에서 설명하는 솔루션에는 WSFC(Windows Server 장애 조치(Failover) 클러스터)가 포함되어 있습니다. SQL AlwaysOn은 오류 검색 및 장애 조치를 위해 WFSC에 의존하므로 WSFC를 설정해야 합니다.

WSFC는 응용 프로그램 및 서비스의 고가용성을 향상시키는 기능입니다. 해당 인스턴스에서 실행 중인 Microsoft 장애 조치(Failover) 클러스터 서비스와 독립적인 Windows Server 인스턴스의 그룹으로 구성됩니다. Windows Server 인스턴스(때때로 노드라고도 함)가 연결되어 있어 서로 통신할 수 있으며 실패 감지를 수행할 수 있습니다. WSFC는 오류 감지 및 장애 조치 기능을 제공합니다. 클러스터의 노드 또는 서비스가 실패하고 오류가 감지되면 다른 노드가 자동 또는 수동으로 시작되어 실패한 노드에서 호스트된 서비스를 제공합니다. 따라서 사용자는 중단이 최소화된 서비스를 경험하게 되며, 서비스 가용성이 향상됩니다.  

### <a name="prerequisites"></a>필수 구성 요소

모든 인스턴스에서 Windows Server 운영 체제를 설치하고 모든 업데이트를 패치합니다.

>[!NOTE] 
>잠재적인 비 호환성 문제를 방지하기 위해 모든 인스턴스에서 동일한 Windows 버전 및 동일한 기능 집합을 설치하는 것이 **매우 권장**됩니다.

### <a name="install-failover-cluster-feature"></a>장애 조치(Failover) 클러스터 기능 설치

Windows Server 인스턴스마다 다음 단계를 완료하여 각 인스턴스에 WSFC 기능을 설치합니다. 관리자 권한이 필요합니다.

1.  Windows Server에서 **서버 관리자**를 열고 오른쪽 창에서 **역할 및 기능 추가**를 클릭합니다. 그러면 **역할 및 기능 추가 마법사**가 시작됩니다.

2.  **기능** 페이지가 표시될 때까지 **다음**을 클릭합니다.

3.  **장애 조치 클러스터링** 확인란을 선택한 다음 **다음**을 클릭하여 설치를 완료합니다. 그림 2를 참조하세요.

    **장애 조치 클러스터링에 필요한 기능 추가**를 확인하는 메시지가 표시되면 **기능 추가**를 클릭합니다. 그림 3을 참조하세요.

    ![역할 및 기능 추가 마법사, 장애 조치 클러스터링](media/Fig2_SelectFeatures.png)

    그림 2

    ![역할 및 기능 추가 마법사, 장애 조치 클러스터링에 필요](media/Fig3_RequiredFeaturesFailover.png)

    그림 3

4.  **확인** 페이지에서 **설치**를 클릭하여 장애 조치 클러스터링 기능을 설치합니다.

5.  **결과** 페이지에서 오류 및 경고 없이 모든 항목이 성공적으로 설치되었는지 확인합니다.

### <a name="create-a-windows-server-failover-cluster"></a>Windows Server 장애 조치(Failover) 클러스터 만들기

모든 인스턴스에서 WSFC 기능이 설치된 후에 WSFC를 구성할 수 있습니다. 이 작업은 노드 하나에서 수행하면 됩니다.

1.  Windows Server에서 **서버 관리자**를 열고 오른쪽 위 모서리에 있는 **도구** 메뉴에서 **장애 조치 클러스터 관리자**를 클릭하여 관리자를 시작합니다.

2.  **장애 조치 클러스터 관리자**에서 오른쪽 창에서 **구성 유효성 검사**를 클릭합니다. 그림 4를 참조하세요.

    ![장애 조치 클러스터 관리자, 구성 유효성 검사](media/Fig4_ValidateConfig.png)

    그림 4

3.  **구성 유효성 검사** **마법사**에서 **다음**을 클릭합니다.

4.  **서버 또는 클러스터 선택** 대화 상자에서 SQL Server를 호스트할 서버 이름을 추가하고 **다음**을 클릭합니다. 그림 5를 참조하세요.

    이 예에서는 두 개의 인스턴스, MDS-HA1과 MDS-HA2를 추가했습니다.

    ![구성 마법사 유효성 검사, 서버 또는 클러스터 선택 페이지](media/Fig5_AddServer.png)

    그림 5

5.  **테스트 옵션** 페이지에서 **모든 테스트 실행**을 클릭하고 **다음**을 클릭합니다.

6.  **다음**을 클릭하여 유효성 검사를 완료합니다.

    **유효성 검사 중** 페이지에 진행 상황이 표시되고, **요약** 페이지에 유효성 검사 요약이 표시됩니다. 그림 6과 7을 참조하세요.

7.  **요약** 페이지에서 경고 또는 오류 메시지를 확인합니다.

    오류를 수정해야 합니다. 그러나 경고는 문제가 아닐 수 있습니다. 경고 메시지는 “테스트된 항목이 요구 사항을 충족하나, 사용자의 확인이 필요한 항목이 있습니다”라는 의미입니다. 예를 들어 그림 7에서는 “디스크 액세스 대기 시간 유효성 검사” 경고가 표시되는데, 디스크가 일시적으로 다른 작업에 사용되었기 때문일 수 있으며 이는 무시할 수 있습니다. 각 경고 및 오류 메시지에 대한 자세한 내용은 온라인 설명서를 확인해야 합니다. 그림 7을 참조하세요.
 
    ![유효성 검사 구성 마법사, 유효성 검사 중 페이지](media/Fig6_ValidationTests.png)

    그림 6

    ![구성 마법사 유효성 검사, 요약 페이지](media/Fig7_ValidationSummary.png)

    그림 7

8.  **요약** 페이지에서 **유효성 검사된 노드를 사용하여 클러스터 만들기** 확인란이 선택되어 있는지 확인한 다음 **마침**을 클릭하여 **클러스터 만들기** **마법사**를 시작합니다.

9.  **클러스터 만들기** **마법사**에서 **다음**을 클릭합니다.

10. **클러스터 관리를 위한 액세스 지점** 페이지에서 WSFC 클러스터 이름을 입력하고 **다음**을 클릭합니다. 이 예제에서는 클러스터 이름으로 “MDS-HA”를 사용합니다. 그림 8을 참조하세요.

    ![클러스터 이름 입력](media/Fig8_EnterClusterName.png)

    그림 8

11. 클러스터 만들기를 완료하려면 **다음**을 클릭하여 계속합니다. **클러스터 MDS-HA의 요약** 섹션에 클러스터 정보가 표시됩니다. 그림 9를 참조하세요.

    ![클러스터에 대한 요약 정보 보기](media/Fig9_ClusterSummary.png)

    그림 9

    나중에 노드를 추가해야 하는 경우 **장애 조치 클러스터 관리자**의 오른쪽 창에서 **노드 추가** 작업을 클릭합니다.

참고:

-   WSFC 기능은 모든 Windows Server 버전에서 사용할 수 있는 것은 아닙니다. 버전에 이 기능이 있는지 확인합니다.

-   Active Directory에 WSFC를 설정하는 적절한 권한이 있는지 확인합니다. 문제가 있으면 [장애 조치 클러스터 단계별 가이드: Active Directory에서 계정 구성](https://technet.microsoft.com/library/cc731002(v=ws.10).aspx)을 참조하세요.

WSFC에 대한 더 자세한 내용은 [장애 조치 클러스터](https://technet.microsoft.com/library/cc732488(v=ws.10).aspx)를 참조하세요.

## <a name="sql-server-alwayson-availability-group"></a>SQL Server AlwaysOn 가용성 그룹

이 섹션에서는 다음 작업에 대해 설명합니다.

1.  [SQL Server AlwaysOn 가용성 그룹을 사용하도록 설정](#enable-sql-server-alwayson-availability-group-on-every-sql-server-instance)합니다.

2.  [가용성 그룹을 만듭니다](#create-an-availability-group).

3.  [가용성 그룹을 유효성 검사하고 테스트](#validation-and-test-the-availability-group)합니다.

SQL Server AlwaysOn 솔루션은 SQL Server 데이터베이스에 대한 고가용성 및 재해 복구를 제공합니다. AlwaysOn에는 가능한 두 가지 솔루션이 있습니다.
두 솔루션 모두 WSFC를 기반으로 구축됩니다.

-   AlwaysOn AG(가용성 그룹)

-   AlwaysOn FCI(장애 조치(failover) 클러스터 인스턴스).

AG는 데이터베이스 수준의 고가용성을 향상시킵니다. AG(사용자 데이터베이스 집합)와 해당 가상 네트워크 이름은 WSFC에서 리소스로 등록됩니다.

FCI는 인스턴스 수준의 고가용성을 향상시킵니다. SQL Server 서비스 및 관련된 서비스는 WSFC에서 리소스로 등록됩니다. 또한 FCI 솔루션은 WFC 클러스터의 모든 노드에 사용할 수 있어야 하는 SAN 또는 SMB 파일 공유와 같이 대칭 공유 디스크 저장소가 필요합니다.


### <a name="prerequisites"></a>필수 구성 요소

-   모든 노드에서 SQL Server를 설치합니다. 자세한 내용은 [SQL Server 2016 설치](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server)를 참조하세요.

-   (권장) 모든 노드에서 정확히 동일한 SQL Server 기능 집합 및 버전을 설치합니다. 특히, MDS를 설치해야 합니다.

-   (권장) 모든 SQL Server 인스턴스에서 동일한 구성을 사용합니다. 특히, 동일한 서버 데이터 정렬이 모든 SQL Server 인스턴스에 구성되어야 합니다.

-   (권장) 동일한 구성을 사용하여 모든 SQL Server 인스턴스를 실행합니다. 그렇지 않으면 SQL Server 인스턴스가 서로 통신할 수 있는지 확인하기 위해 각 SQL Server 인스턴스에 대한 권한을 부여해야 합니다.

-   Windows 방화벽 설정을 통해 SQL Server 인스턴스가 서로 통신하는지 확인합니다.

### <a name="enable-sql-server-alwayson-availability-group-on-every-sql-server-instance"></a>모든 SQL Server 인스턴스에서 SQL Server AlwaysOn 가용성 그룹을 사용하도록 설정

1.  **SQL Server 구성 관리자**의 왼쪽 창에서 **SQL Server 서비스**를 클릭하고 오른쪽 창에서 **SQL Server**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 그림 10을 참조하세요.

    ![SQL Server 속성 창](media/Fig10_SQLServerProperties.png)

    그림 10

2.  **SQL Server(MSSQLSERVER)** **속성** 대화 상자에서 **AlwaysOn 고가용성** 탭을 클릭한 다음 **AlwaysOn 가용성 그룹 사용** 확인란을 선택합니다. **Windows 장애 조치 클러스터 이름** 텍스트 상자에 값이 표시되는 경우 **확인**을 클릭하여 계속합니다. 그림 11을 참조하세요.

    ![AlwaysOn 가용성 그룹 사용 옵션](media/Fig11_EnableAlwaysOn.png)

    그림 11

3.  경고 페이지가 표시되면 **확인**을 클릭하여 계속합니다. 그림 12를 참조하세요.

    ![서비스를 중지 및 다시 시작 확인](media/Fig12_WarningServiceStopStart.png)

    그림 12

4.  **다시 시작**을 클릭하여 **SQL Server** 서비스를 다시 시작하고 이 변경 내용을 적용합니다. 그림 10을 참조하세요.

>[!NOTE] 
>**SQL Server 구성 관리자**를 사용하여 SQL Server 서비스를 실행하는 서비스 계정을 변경할 수 있습니다. **SQL Server(MSSQLSERVER)** **속성**대화 상자에서 **로그온** 탭을 클릭합니다. 그림 11을 참조하세요.

### <a name="create-an-availability-group"></a>가용성 그룹 만들기

모든 SQL Server 인스턴스에서 AlwaysOn 기능을 활성화한 후 한 노드에서 MDS 데이터베이스를 포함하는 새 AG를 만듭니다.

AG는 기존 데이터베이스에서만 만들 수 있습니다. 따라서 한 노드에서 MDS 데이터베이스를 만들거나 임시 데이터베이스를 만든 다음, 임시 데이터베이스를 삭제합니다. 이 예제에서는 emptyMDS 데이터베이스를 만들고 AG를 이 MDS 데이터베이스에 만듭니다.

1.  노드에서 **SQL Server Management Studio**(**SSMS**)를 시작하고 적절한 자격 증명으로 로컬 SQL Server 인스턴스에 연결합니다.

2.  SSMS에서 **새 쿼리** 창을 열고 다음 스크립트 창을 실행하여 빈 데이터베이스를 만듭니다. C:\\temp를 전체 백업을 수행하는 데 사용할 위치로 바꿉니다.

    ```
    CREATE DATABASE MDS\_Sample
    GO
    BACKUP DATABASE MDS\_Sample TO DISK='C:\\temp'
    GO
    ```

    >[!NOTE] 
    >전체 데이터베이스 백업은 이 데이터베이스에 AG를 만드는 데 필요합니다.

3.  **개체 탐색기**에서 **AlwaysOn 고가용성** 폴더를 확장하고 **새 가용성 그룹 마법사**를 클릭하여 **새 가용성 그룹 마법사**를 시작합니다. 그림 13을 참조하세요.

    ![새 가용성 그룹 마법사 시작](media/Fig13_AvailabilityGroupsFolder.png)

    그림 13

4.  **새 가용성 그룹** 마법사에서 **다음**을 클릭하여 **이름 지정** 페이지를 표시합니다. AG에 사용할 이름을 입력하고 **다음**을 클릭합니다. 그림 14를 참조하세요.

    ![가용성 그룹의 이름 입력](media/Fig14_AvailabilityGroupName.png)

    그림 14

5.  **데이터베이스 선택** 페이지에서 만든 데이터베이스를 클릭하고 **다음**을 클릭합니다. 그림 15를 참조하세요.

    ![데이터베이스 선택](media/Fig15_AvailabilityGroupSelectDatabase.png)

    그림 15

6.  **복제본 지정** 페이지에서 **복제본 추가**를 클릭하여 다른 복제본을 추가합니다. 이 페이지는 이미 복제본으로 현재 로컬 SQL Server 인스턴스를 나열합니다. 그림 16을 참조하세요.

7.  **서버에 연결** 대화 상자에서 적절한 자격 증명을 추가하고 **연결**을 클릭합니다.

    ![SQL Server 인스턴스에 연결](media/Fig16_AddReplicaConnectServer.png)

    그림 16

    이제 두 개의 복제본이 목록에 표시됩니다. 복제본으로 다른 노드를 추가하려면 이 단계를 반복합니다. 그림 17을 참조하세요.

    ![복제본 목록 보기](media/Fig17_AvailabilityGroupSQLReplicas.png)

    그림 17

    각 복제본의 경우 다음 **동기 커밋**, **자동 장애 조치** 및 **읽기용 보조** 설정을 구성합니다. 그림을 참조하세요.
17.

    **동기 커밋**: 이는 트랜잭션이 데이터베이스의 주 복제본에 커밋되는 경우 트랜잭션이 다른 모든 동기 복제본에도 커밋됨을 보장합니다. 비동기 커밋은 이를 보장하지 않으며 주 복제본보다 뒤떨어질 수도 있습니다.

    일반적으로 동일한 데이터 센터에 두 개의 노드가 있는 경우 동기 커밋을 사용하도록 설정해야 합니다. 서로 다른 데이터 센터에 있는 경우 동기 커밋은 데이터베이스 성능이 느려질 수도 있습니다.

    이 확인란을 선택하지 않으면 비동기 커밋이 사용됩니다.

    **자동 장애 조치:** 주 복제본이 다운되는 경우 자동 장애 조치가 선택되어 있으면 AG가 자동으로 해당 보조 복제본에 장애 조치합니다. 이는 동기 커밋을 사용하는 복제본에서만 사용할 수 있습니다.

    **읽기용 보조:** 기본적으로 사용자는 보조 복제본에 연결할 수 없습니다. 사용자는 읽기 전용 액세스 권한이 있는 보조 복제본에 연결할 수 있습니다.

8.  **복제본 지정** 페이지에서 **수신기** 탭을 클릭하고 다음을 수행합니다. 그림 18을 참조하세요.

    a.  **가용성 그룹 수신기 만들기**를 클릭하여 MDS 데이터베이스 연결에 대한 가용성 그룹 수신기를 설정합니다.

    b.  MDSSQLServer와 같은 **수신기 DNS 이름**을 입력합니다.

    c.  **포트** 텍스트 상자에 기본 SQL 포트 1433을 입력합니다.

    d.  **네트워크 모드** 텍스트 상자에 DHCP를 입력하고 **다음**을 클릭하여 계속합니다.

    >[!NOTE] 
    >필요에 따라 **네트워크 모드**로 “고정 IP”를 선택하고 고정 IP를 입력할 수 있습니다. 또한 1433이 아닌 포트를 입력할 수 있습니다. 

    ![수신기 구성](media/Fig18_AvailabilityGroupCreateListener.png)

    그림 18

9.  **데이터 동기화 선택** 페이지에서 **전체**를 클릭하고 모든 노드가 액세스할 수 있는 네트워크 공유를 지정합니다. 계속하려면 **다음** 을 클릭합니다. 그림 19를 참조하세요.

    이 네트워크 공유는 데이터베이스 백업을 저장하여 보조 복제본을 만드는 데 사용됩니다. 이를 조직에서 사용할 수 없는 경우 다른 데이터 동기화 기본 설정을 선택합니다. 다른 옵션을 사용하여 보조 복제본을 만드는 방법은 [SQL Server 2016 AlwaysOn 가용성 그룹](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server)을 참조하세요. 또한 그림 17에 다른 옵션이 나열되어 있습니다.

    ![데이터 동기화 구성](media/Fig19_AvailabilityGroupDataSync.png)

    그림 19 

10. **유효성 검사** 페이지에서 모든 유효성 검사를 성공적으로 전달하고 오류를 수정했는지 확인합니다. 계속하려면 **다음** 을 클릭합니다.

11. **요약** 페이지에서 모든 구성 설정을 검토하고 **마침**을 클릭합니다. 그러면 가용성 그룹이 만들어지고 구성됩니다.

12. **결과** 페이지에서 필요한 모든 단계가 완료되었는지 확인합니다.

### <a name="validation-and-test-the-availability-group"></a>가용성 그룹의 유효성 검사 및 테스트

1.  SSMS를 열고 [가용성 그룹 만들기](#create-an-availability-group) 섹션에서 방금 만든 수신기 DNS 이름에 연결합니다. 이 예제에서는 MDSSQLServer입니다.

2.  **개체 탐색기**에서 **AlwaysOn 고가용성** 폴더를 확장하고 [가용성 그룹 만들기](#create-an-availability-group) 섹션에서 방금 만든 AG를 마우스 오른쪽 단추로 클릭한 다음, **대시보드 표시**를 클릭합니다. 그림 20을 참조하세요. 새 AG 및 해당 복제본의 상태가 표시됩니다.

    ![대시보드 보기](media/Fig20_ShowDashboard.png)

    그림 20 

3.  **장애 조치**를 클릭하여 동기 복제본 및 비동기 복제본으로 장애 조치를 수행합니다. 이는 해당 장애 조치가 문제 없이 올바르게 실행되었는지 확인하기 위한 것입니다.

 AlwaysOn 설정이 완료되었습니다.

AlwaysOn 가용성 그룹에 대한 자세한 내용은 [SQL Server 2016 AlwaysOn 가용성 그룹](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server)을 참조하세요.

## <a name="configure-mds-to-run-on-an-wsfc-node"></a>WSFC 노드에서 실행하는 MDS 구성

이 문서에 제공된 이 솔루션에는 WSFC에서 실행되는 MDS 백 엔드 데이터베이스만 필요합니다. 웹 응용 프로그램 및 MDS 구성 관리자와 같은 MDS의 다른 부분으로 MDS가 AG에 연결할 수 있는 한, WSFC 또는 WSFC 외부의 노드에서 실행될 수 있습니다.

1.  한 노드에서 **Master Data Service 구성 관리자**를 열고 **데이터베이스 구성**을 클릭하고 **데이터베이스 만들기**를 클릭하여 **데이터베이스 만들기 마법사**를 시작합니다.

2.  **데이터베이스 서버** 페이지에서 AG 수신기 DNS 이름을 **SQL Server 인스턴스** 텍스트 상자에 입력하고 **연결 테스트**, **다음**을 차례로 클릭합니다. 그림 21을 참조하세요.

    ![AG 수신기와 데이터베이스 서버 구성](media/Fig21_MDSDatabaseServerListener.png)

    그림 21

3.  **데이터베이스** 페이지에서 [가용성 그룹 만들기](#create-an-availability-group) 섹션에서 만든 데이터베이스의 이름을 입력하고 **다음**을 클릭합니다. 그림 22를 참조하세요.

    ![데이터베이스 만들기 및 구성](media/Fig22_MDSCreateDatabase.png)

    그림 22

4.  **데이터베이스 만들기** **마법사**를 완료합니다. 자세한 내용은 [Master Data Services 설치 및 구성](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration)을 참조하세요.

5.  **Master Data Service 구성 관리자**에서 **웹 응용 프로그램**을 클릭하여 웹 응용 프로그램을 구성한 다음 **적용**을 클릭하여 MDS에 설정을 적용합니다. 그림 23을 참조하세요. 자세한 내용은 [Master Data Services 설치 및 구성](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration)을 참조하세요.

    ![웹 응용 프로그램 구성](media/Fig23_MDSWebApplication.png)

    그림 23

    MDS 설정이 완료되었습니다. 위의 단계를 반복하여 모든 노드에서 실행할 MDS를 설정합니다. 백 엔드 데이터베이스는 동일한 AG에서 동일합니다.

6.  이전에 AlwaysOn AG를 만들기 위해 임시 데이터베이스를 만든 경우([가용성 그룹을 만들기](#create-an-availability-group) 섹션 참조) 임시 데이터베이스를 삭제해야 합니다.

    Master Data Service에 대한 자세한 내용은 [Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds)를 참조하세요.

## <a name="conclusion"></a>결론

이 백서에서 SQL Server AlwaysOn 가용성 그룹을 기반으로 하는 Master Data Services 백 엔드 데이터베이스를 설정 및 구성하는 방법을 살펴보았습니다. 이 구성은 Master Data Services 백 엔드 데이터베이스에 고가용성 및 재해 복구를 제공합니다. 이 구성을 구현하려면 Windows Server 장애 조치 클러스터, SQL Server AlwaysOn 가용성 그룹 및 Master Data Services를 설치 및 구성해야 합니다.

## <a name="feedback"></a>피드백

이 백서가 도움이 되었습니까? 문서 맨 위에 있는 **주석**을 클릭하여 여러분의 의견을 보내주세요. 

사용자 의견은 배포하는 백서의 품질 향상에 도움이 됩니다. 

