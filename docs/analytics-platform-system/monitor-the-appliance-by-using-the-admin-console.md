---
title: 관리 콘솔-분석 플랫폼 시스템 모니터링 | Microsoft Docs
description: Analytics Platform System에 대 한 관리 콘솔 어플라이언스 상태, 상태 및 성능 정보를 표시 하는 웹 응용 프로그램을 됩니다. 사용자가 인터넷 브라우저를 통해 관리 콘솔에 연결합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d094f809052222238806e679e38c6578422fd9aa
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909853"
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>관리 콘솔-Analytics Platform System을 사용 하 여 어플라이언스 모니터링
관리 콘솔 어플라이언스 상태, 상태 및 성능 정보를 표시 하는 SQL Server PDW 웹 응용 프로그램은 사용자가 Internet Explorer를 통해 관리 콘솔에 연결합니다.  
  
## <a name="About"></a>관리 콘솔에 대 한  
![어플라이언스 콘솔 홈](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**어플라이언스**  
홈  
어플라이언스 상태 요약을 제공합니다.  
  
상태  
각 노드 내에서 각 모니터링 대상된 구성 요소의 상태를 표시 하는 표시기를 사용 하 여 어플라이언스 토폴로지를 표시 합니다. 개별 노드의 현재 상태 및 노드 구성 요소의 속성을 볼 수 있습니다.  
  
하드웨어 및 소프트웨어 경고가 표시 됩니다.  
  
성능 모니터  
성능 모니터 그래프를 표시합니다.  
  
**병렬 데이터 웨어하우스**  
홈  
PDW 상태 요약을 제공합니다.  
  
세션  
활성 PDW 사용자 세션을 표시합니다. 이 리소스 경합을 모니터링할 수 있습니다.  
  
쿼리  
실행 중인 쿼리 및 최근에 완료 된 쿼리 목록을 표시합니다. 있는 경우 관련된 오류가 표시 됩니다. 또한 쿼리 실행 계획 및 정보의 노드 실행 세부 정보를 확인 하는 기능을 제공 합니다.  
  
로드  
표시 있으면 계획, PDW 로드 되 고 관련된 오류의 현재 상태를 로드 합니다.  
  
백업/복원  
백업 및 복원 작업을 PDW의 로그를 표시 합니다.  
  
상태  
각 노드 내에서 각 모니터링 대상된 구성 요소의 상태를 표시 하는 표시기를 사용 하 여 PDW 토폴로지를 표시 합니다. 개별 노드의 현재 상태 및 노드 구성 요소의 속성을 볼 수 있습니다.  
  
하드웨어 및 소프트웨어 경고가 표시 됩니다.  
  
리소스  
PDW 리소스 잠금은 목록과 현재 상태를 표시합니다.  
  
스토리지  
PDW 저장소 사용률을 요약 되어 있습니다.  
  
성능 모니터  
PDW 성능 모니터 그래프를 표시합니다.  
 
> [!NOTE]  
> 관리 콘솔에는 1024 x 768 이상의 화면 해상도 있습니다. 관리 콘솔에 1280 X 1024 이상의 화면 해상도 사용 하 여 최상의 표시 됩니다.  
  
## <a name="Connect"></a>관리 콘솔에 연결  
관리 콘솔에 연결할 필요 합니다.  
  
-   에 최소 Internet Explorer 버전 10입니다.  
  
-   관리자 콘솔에 액세스 권한입니다. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   제어 노드 클러스터의 IP 주소입니다.  SQL Server PDW 관리자에서이 얻습니다.  
  
관리 콘솔에 연결 하려면 제어 노드 클러스터의 IP 주소로 이동 하 여 Internet Explorer 및 https를 사용 합니다. 예를 들어 제어 노드 클러스터의 IP 주소 `10.192.63.102`를 입력 `https://10.192.63.102` 브라우저 주소 표시줄에 있습니다. 첫 번째 화면에서 요청 하 **로그인** 하 고 **암호**합니다. 중 하나는 SQL Server 인증 로그인 및 암호를 Windows 인증 로그인 및 Windows 암호를 제공 합니다. Windows 인증 로그인을 사용 하는 경우 관리 콘솔의 가장을 사용 합니다.  
  
## <a name="RelatedTasks"></a>관리 콘솔 작업  
다음을 모니터링 하는 기능을 제공 하는 관리자 콘솔:  
  
|||  
|-|-|  
|**정보 유형**|**관리 콘솔에 액세스 하는 방법**|  
|어플라이언스의 전반적인 상태|클릭 **어플라이언스 상태** 위쪽 메뉴에서 또는 **홈**합니다.|  
|,|클릭 **경고**합니다. 자세한 내용은 [관리 콘솔 경고 이해 &#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md)합니다.|  
|어플라이언스 구성 요소 및 해당 상태|클릭 **어플라이언스 상태** 위쪽 메뉴에서 또는 **홈**합니다.|  
|모니터 요청 (쿼리, 로드, 백업 및 복원 포함)|클릭 **세션** 현재 활성 또는 최근 세션을 확인 합니다.<br /><br />클릭 **쿼리** 현재 활성 또는 최근 쿼리를 확인 합니다. 쿼리에 대 한 표시 정보를 로드, 백업 및 복원에 포함 되어 있습니다.<br /><br />클릭 **잠금을** 활성 잠금 확인 합니다.|  
|로드, 백업 및 복원에 대 한 추가 정보를 모니터링 합니다.|클릭 **로드** 하거나 **백업/복원**합니다.|  
|성능 정보|클릭 **성능 모니터**합니다.|  
  
## <a name="see-also"></a>관련 항목  
[어플라이언스 모니터링 &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
