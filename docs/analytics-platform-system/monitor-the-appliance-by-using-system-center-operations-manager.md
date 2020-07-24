---
title: System Center Operations Manager를 사용 하 여 AP 모니터링
description: SCOM (System Center Operations Manager)을 사용 하 여 APS (분석 플랫폼 시스템) 어플라이언스를 모니터링할 수 있습니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 539c18efe43afcf5436c6913c20cab081974b7f5
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86941125"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>System Center Operations Manager 분석 플랫폼 시스템을 사용 하 여 모니터링
SCOM (System Center Operations Manager)을 사용 하 여 APS (분석 플랫폼 시스템) 어플라이언스를 모니터링할 수 있습니다.
  
## <a name="before-you-begin"></a>시작하기 전에  
  
### <a name="prerequisites"></a>필수 조건  
  
1.  System Center Operations Manager 2007 R2, 2012 또는 2012 s p 1을 설치 하 고 실행 해야 합니다.  
  
2.  SQL Server 2008 R2 Native Client 또는 SQL Server 2012 Native Client가 설치 되어 있어야 합니다.  
  
3.  SQL Server PDW 모니터링 하는 관리 팩을 설치, 가져오기 및 구성 해야 합니다. 이러한 작업을 수행 하는 지침은 다음 문서를 참조 하세요.  
  
    -   [SCOM 관리 팩 &#40;Analytics Platform System&#41;를 설치 합니다.](install-the-scom-management-packs.md)  
  
    -   [PDW &#40;Analytics Platform System 용 SCOM 관리 팩을 가져옵니다&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [분석 플랫폼 시스템 &#40;분석 플랫폼 시스템을 모니터링 하도록 SCOM을 구성&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>SCOM을 사용 하 여 SQL Server PDW를 모니터링 하려면  
SCOM 관리 팩을 구성한 후 SCOM의 모니터링 창을 클릭 하 고 **SQL Server 어플라이언스** 로 드릴 다운 한 다음 **병렬 데이터 웨어하우스를 Microsoft SQL Server**합니다. 병렬 데이터 웨어하우스 Microsoft SQL Server 아래에는 경고, 어플라이언스, 어플라이언스 다이어그램 및 노드의 네 가지 선택 옵션이 있습니다.  
  
### <a name="alerts"></a>경고  
경고를 통해 관리할 현재 경고를 찾을 수 있습니다.  
  
![경고](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>어플라이언스  
어플라이언스는 현재 환경에서 검색 되 고 모니터링 되는 SQL Server PDW 어플라이언스를 검색 합니다. 기기가 여기에 표시 되지 않고이에 대 한 ODBC 연결을 만든 경우 사용자의 PDWWatcher 계정에 문제가 있을 수 있습니다. "모니터링 안 함"으로 표시 되는 경우 사용자의 PDWMonitor 계정에 문제가 있을 수 있습니다. SCOM은 실시간으로 변경 하지 않지만 정기적으로 모니터링 하 고 모니터링을 위해 정기적으로 쿼리를 전송 하기 위해 새 어플라이언스를 확인 합니다.  
  
![장비](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>어플라이언스 다이어그램  
어플라이언스 다이어그램 페이지에서 트리 보기를 사용 하 여 어플라이언스의 상태를 볼 수 있습니다.  
  
![어플라이언스 다이어그램](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>노드  
마지막으로, 노드 보기를 사용 하 여 각 노드를 통해 어플라이언스의 상태를 볼 수 있습니다.  
  
![노드](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>참고 항목  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[분석 플랫폼 시스템&#41;&#40;관리 콘솔 경고 이해](understanding-admin-console-alerts.md)  
  
