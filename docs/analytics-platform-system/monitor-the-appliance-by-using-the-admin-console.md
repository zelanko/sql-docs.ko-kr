---
title: 관리 콘솔을 사용 하 여 모니터링
description: 분석 플랫폼 시스템의 경우 관리 콘솔은 어플라이언스 상태, 상태 및 성능 정보를 표시 하는 웹 응용 프로그램입니다. 사용자는 인터넷 브라우저를 통해 관리 콘솔에 연결 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 977e38016fbb58356d22ccfc5f783539e5f852d5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400940"
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>관리 콘솔-분석 플랫폼 시스템을 사용 하 여 어플라이언스 모니터링
관리 콘솔은 어플라이언스 상태, 상태 및 성능 정보를 표시 하는 SQL Server PDW 웹 응용 프로그램입니다. 사용자는 Internet Explorer를 통해 관리 콘솔에 연결 합니다.  
  
## <a name="About"></a>관리 콘솔 정보  
![어플라이언스 콘솔 홈](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**기기가**  
홈  
어플라이언스 상태를 간략히 요약 하 여 제공 합니다.  
  
상태  
각 노드 내에서 모니터링 되는 각 구성 요소의 상태를 표시 하는 표시기를 사용 하 여 어플라이언스 토폴로지를 표시 합니다. 개별 노드 및 노드 구성 요소의 속성에 대 한 현재 상태를 볼 수 있습니다.  
  
하드웨어 및 소프트웨어 경고를 표시 합니다.  
  
성능 모니터링  
성능 모니터 그래프를 표시 합니다.  
  
**병렬 데이터 웨어하우스**  
홈  
PDW 상태를 간략히 요약 하 여 제공 합니다.  
  
세션  
활성 PDW 사용자 세션을 표시 합니다. 이를 통해 리소스 경합을 모니터링할 수 있습니다.  
  
쿼리  
실행 중인 쿼리 및 최근에 완료 된 쿼리 목록을 표시 합니다. 관련 오류 (있는 경우)를 표시 합니다. 는 또한 쿼리 실행 계획 및 노드 실행 정보에 대 한 세부 정보를 볼 수 있는 기능을 제공 합니다.  
  
로드  
로드 계획, 현재 PDW 로드 상태 및 관련 오류 (있는 경우)를 표시 합니다.  
  
백업/복원  
PDW 백업 및 복원 작업의 로그를 표시 합니다.  
  
상태  
각 노드 내에서 모니터링 되는 각 구성 요소의 상태를 표시 하는 표시기를 사용 하 여 PDW 토폴로지를 표시 합니다. 개별 노드 및 노드 구성 요소의 속성에 대 한 현재 상태를 볼 수 있습니다.  
  
하드웨어 및 소프트웨어 경고를 표시 합니다.  
  
리소스  
PDW 리소스 잠금 목록과 현재 상태를 표시 합니다.  
  
스토리지  
PDW 저장소 사용률을 요약 합니다.  
  
성능 모니터링  
PDW 성능 모니터 그래프를 표시 합니다.  
 
> [!NOTE]  
> 관리 콘솔에는 1024x768 화면 해상도가 있습니다. 관리 콘솔은 1280 X 1024 이상의 화면 해상도로 가장 잘 표시 됩니다.  
  
## <a name="Connect"></a>관리 콘솔에 연결  
관리 콘솔에 연결 하려면 다음이 필요 합니다.  
  
-   Internet Explorer 버전 10 이상  
  
-   관리 콘솔에 액세스할 수 있는 권한 <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   제어 노드 클러스터의 IP 주소입니다.  SQL Server PDW 관리자에 게 문의 하세요.  
  
관리 콘솔에 연결 하려면 Internet Explorer 및 https를 사용 하 여 제어 노드 클러스터의 IP 주소를 찾습니다. 예를 들어, 제어 노드 클러스터의 IP 주소가 인 `10.192.63.102`경우 브라우저 주소 표시줄 `https://10.192.63.102` 에를 입력 합니다. 첫 번째 화면에서는 **로그인** 과 **암호**를 요청 합니다. SQL Server 인증 로그인 및 암호, Windows 인증 로그인 및 Windows 암호를 제공 합니다. Windows 인증 로그인을 사용 하는 경우 관리 콘솔에서 가장을 사용 합니다.  
  
## <a name="RelatedTasks"></a>관리 콘솔 작업  
관리 콘솔은 다음을 모니터링 하는 기능을 제공 합니다.  
  
|||  
|-|-|  
|**Information Type**|**관리 콘솔에서 액세스 하는 방법**|  
|기기의 전체 상태|위쪽 메뉴 또는 **홈**에서 **어플라이언스 상태** 를 클릭 합니다.|  
|경고|
  **경고**를 클릭합니다. 자세한 내용은 [분석 플랫폼 시스템&#41;&#40;관리 콘솔 경고 이해 ](understanding-admin-console-alerts.md)를 참조 하세요.|  
|어플라이언스 구성 요소 및 해당 상태|위쪽 메뉴 또는 **홈**에서 **어플라이언스 상태** 를 클릭 합니다.|  
|요청 모니터링 (쿼리, 로드, 백업 및 복원 포함)|**세션** 을 클릭 하 여 현재 활성 또는 최근 세션을 확인 합니다.<br /><br />현재 활성 또는 최근 쿼리를 보려면 **쿼리** 를 클릭 합니다. 쿼리에 대해 표시 되는 정보에는 로드, 백업 및 복원이 포함 됩니다.<br /><br />**잠금** 을 클릭 하면 활성 잠금이 표시 됩니다.|  
|로드, 백업 및 복원에 대 한 추가 정보를 모니터링 합니다.|**로드** 또는 **백업/복원**을 클릭 합니다.|  
|성능 정보|**성능 모니터**를 클릭 합니다.|  
  
## <a name="see-also"></a>참고 항목  
[어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](appliance-monitoring.md)  
  
