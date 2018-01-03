---
title: "관리 콘솔 (분석 플랫폼 시스템)를 사용 하 여 어플라이언스에 모니터링"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 294ba6ac-b1ff-46ea-ba32-d8b32cb4cdc2
caps.latest.revision: "26"
ms.openlocfilehash: db27003d4e1efd54a179551f585fb23ce9c0ed82
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="monitor-the-appliance-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 어플라이언스에 모니터
관리 콘솔 어플라이언스 상태, 상태 및 성능 정보를 표시 하는 SQL Server PDW 웹 응용 프로그램은 합니다. 사용자가 Internet Explorer를 통해 관리 콘솔에 연결 합니다.  
  
## <a name="About"></a>관리 콘솔 정보  
![어플라이언스 콘솔 홈](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**어플라이언스**  
홈  
어플라이언스 상태 요약을 제공합니다.  
  
상태  
각 노드 내에서 각 모니터링 대상된 구성 요소의 상태를 나타내는 표시기와 함께 어플라이언스 토폴로지를 표시 합니다. 개별 노드의 현재 상태 및 노드 구성 요소의 속성을 볼 수 있습니다.  
  
하드웨어 및 소프트웨어 경고가 표시 됩니다.  
  
성능 모니터  
성능 모니터 그래프를 표시합니다.  
  
**병렬 데이터 웨어하우스**  
홈  
PDW 상태 요약을 제공합니다.  
  
세션  
활성 PDW 사용자 세션을 표시합니다. 이 리소스 경합을 모니터링할 수 있습니다.  
  
쿼리  
실행 되는 쿼리 및 최근에 완료 된 쿼리 목록을 표시합니다. 있는 경우 관련된 오류를 표시 합니다. 또한 쿼리 실행 계획 및 노드 실행 정보에 대 한 세부 정보를 볼 수 있는 기능을 제공 합니다.  
  
로드  
표시 합니다. 있는 경우 계획, PDW 부하 및 관련된 오류의 현재 상태를 로드 합니다.  
  
백업/복원  
백업 및 복원 작업을 PDW의 로그를 표시 합니다.  
  
상태  
PDW 토폴로지를 각 노드 내에서 각 모니터링 대상된 구성 요소의 상태를 나타내는 표시기와 함께 표시 됩니다. 개별 노드의 현재 상태 및 노드 구성 요소의 속성을 볼 수 있습니다.  
  
하드웨어 및 소프트웨어 경고가 표시 됩니다.  
  
리소스  
PDW 리소스 잠금 및 현재 상태 목록을 표시합니다.  
  
저장소  
PDW 저장소 사용을 요약합니다.  
  
성능 모니터  
PDW 성능 모니터 그래프를 표시합니다.  
  
**HDInsight**  
홈  
HDInsight 상태의 요약을 제공합니다.  
  
HDFS  
HDInsight 공간 사용률을 요약 하 고 상위 10 개의 공간 사용자를 나열 합니다.  
  
맵/감소  
MapReduce 작업의 상태를 요약합니다.  
  
상태  
HDInsight 토폴로지를 각 노드 내에서 각 모니터링 대상된 구성 요소의 상태를 나타내는 표시기와 함께 표시 됩니다. 개별 노드의 현재 상태 및 노드 구성 요소의 속성을 볼 수 있습니다.  
  
하드웨어 및 소프트웨어 경고가 표시 됩니다.  
  
저장소  
HDInsight 저장소 사용을 요약합니다.  
  
성능 모니터  
성능 모니터 그래프를 표시합니다.  
  
> [!NOTE]  
> 관리 콘솔에는 1024 x 768 화면 해상도 있습니다. 관리 콘솔에서 가장 효율적으로 1280 X 1024 이상의 화면 해상도 표시합니다.  
  
## <a name="Connect"></a>관리 콘솔에 연결  
관리 콘솔에 연결 하는 데 필요 합니다.  
  
-   At 최소 Internet Explorer 버전 10입니다.  
  
-   관리 콘솔에 액세스할 수 있는 권한. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   컨트롤 노드 클러스터의 IP 주소입니다.  SQL Server PDW 관리자에서이 가져옵니다.  
  
관리 콘솔에 연결 하려면 컨트롤 노드 클러스터의 IP 주소를 검색 하 Internet Explorer 및 https를 사용 합니다. 예를 들어, 컨트롤 노드 클러스터의 IP 주소는 `10.192.63.102`, 입력 `https://10.192.63.102` 브라우저 주소 표시줄에 있습니다. 첫 번째 화면에서 요청 하는 프로그램 **로그인** 및 **암호**합니다. 중 하나는 SQL Server 인증 로그인 및 암호 또는 Windows 인증 로그인 및 Windows 암호를 제공 합니다. Windows 인증 로그인을 사용 하는 경우 관리 콘솔 가장을 사용 합니다.  
  
## <a name="RelatedTasks"></a>관리 콘솔 작업  
관리 콘솔에서 다음을 모니터링 하는 기능을 제공 합니다.  
  
|||  
|-|-|  
|**정보 유형**|**관리 콘솔에 액세스 하는 방법**|  
|어플라이언스의 전체 상태|클릭 **기기 상태** 위쪽 메뉴에서 또는 **홈**합니다.|  
|,|클릭 **경고**합니다. 자세한 내용은 참조 [관리 콘솔 경고 이해 &#40; 분석 플랫폼 시스템 &#41; ](understanding-admin-console-alerts.md).|  
|어플라이언스 구성 요소 및 해당 상태|클릭 **기기 상태** 위쪽 메뉴에서 또는 **홈**합니다.|  
|모니터 요청 (쿼리, 로드, 백업 및 복원 포함)|클릭 **세션** 현재 활성 또는 최근에 사용한 세션을 볼 수 있습니다.<br /><br />클릭 **쿼리** 현재 활성 또는 최근 쿼리를 볼 수 있습니다. 쿼리에 대 한 표시 되는 정보에 로드, 백업 및 복원에 포함 됩니다.<br /><br />클릭 **잠금** 활성 잠금 볼 수 있습니다.|  
|부하, 백업 및 복원에 대 한 추가 정보를 모니터링 합니다.|클릭 **로드** 또는 **백업/복원**합니다.|  
|성능 정보|클릭 **성능 모니터**합니다.|  
  
## <a name="see-also"></a>관련 항목:  
[어플라이언스 모니터링 &#40; 분석 플랫폼 시스템 &#41;](appliance-monitoring.md)  
  
