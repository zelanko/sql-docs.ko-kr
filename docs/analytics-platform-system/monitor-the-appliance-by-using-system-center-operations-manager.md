---
title: SCOM-Analytics Platform System 사용 하 여 모니터 | Microsoft Docs
description: Analytics Platform System (APS) 어플라이언스를 모니터링 하려면 System Center Operations Manager (SCOM)를 사용 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3c43734dbd7ef1a766f3f1258f97565ab82e175d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62639860"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>System Center Operations Manager-Analytics Platform System 사용 하 여 모니터
Analytics Platform System (APS) 어플라이언스를 모니터링 하려면 System Center Operations Manager (SCOM)를 사용 합니다.
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
  
### <a name="prerequisites"></a>사전 요구 사항  
  
1.  System Center Operations Manager 2007 R2, 2012 또는 2012 SP1 설치 하 고 실행 해야 합니다.  
  
2.  SQL Server 2008 R2 Native Client 또는 SQL Server 2012 Native Client를 설치 해야 합니다.  
  
3.  SQL Server PDW 모니터링 관리 팩을 설치 하 고 사용을 가져온, 게 구성 해야 합니다. 지침은 다음 문서를 사용 하 여 이러한 작업을 수행 하 합니다.  
  
    -   [SCOM 관리 팩을 설치 &#40;Analytics Platform System&#41;](install-the-scom-management-packs.md)  
  
    -   [PDW 용 SCOM 관리 팩 가져오기 &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [Analytics Platform System을 모니터링 하도록 SCOM 구성 &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>SQL Server PDW SCOM 사용 하 여 모니터링  
SCOM 관리 팩을 구성한 후 SCOM의 모니터링 창에서 클릭 하 고 드릴 다운 하 **SQL Server 어플라이언스** 차례로 **Microsoft SQL Server 병렬 데이터 웨어하우스**합니다. Microsoft SQL Server 병렬 데이터 웨어하우스를 아래 가지 네 가지 방법이 있습니다. 경고, 어플라이언스, 어플라이언스 다이어그램 및 노드를 선택 합니다.  
  
### <a name="alerts"></a>,  
경고는 관리 하는 현재 경고를 찾을 수 있습니다.  
  
![Alerts](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>어플라이언스  
어플라이언스는 환경에는 현재 검색 및 모니터링 SQL Server PDW Appliance을 찾을 수 있습니다. 어플라이언스 여기 표시 되지 않습니다 하 고이 대 한 ODBC 연결을 만든 경우 다음 있을 수 있습니다 PDWWatcher 계정에 문제가 있습니다. "모니터링 안 함"으로 표시 될 경우 있을 PDWMonitor 계정에 문제가 있습니다. SCOM을 실시간으로 변경 하지 않습니다 하지만 정기적으로 모니터링 하는 새 어플라이언스에 대 한 확인 하므로 환자를 되며 정기적으로 모니터링 하는 것에 대 한 어플라이언스로 쿼리를 보냅니다.  
  
![Appliances](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>어플라이언스 다이어그램  
어플라이언스 다이어그램 페이지는 트리 뷰를 사용 하 여 어플라이언스의 상태 참조를 가져올 수 있습니다.  
  
![어플라이언스 다이어그램](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>노드  
마지막으로, 노드 보기를 사용 하는 각 노드 어플라이언스의 상태를 확인할 수 있습니다.  
  
![Nodes](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>관련 항목  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[이해 관리 콘솔 경고 &#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md)  
  
