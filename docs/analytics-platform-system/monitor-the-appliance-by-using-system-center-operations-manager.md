---
title: "System Center Operations Manager (APS)와 함께 모니터 어플라이언스"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de6cbf6e-f2e9-4877-94df-9c13b1182d56
caps.latest.revision: "14"
ms.openlocfilehash: 115d32ab8f633752dacfaf245017803bcdbfb8d3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="monitor-the-appliance-by-using-system-center-operations-manager"></a>System Center Operations Manager를 사용 하 여 어플라이언스에 모니터링
SQL Server PDW 및 HDInsight를 모니터링 하려면 System Center Operations Manager를 사용 하는 방법을 설명 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
  
### <a name="prerequisites"></a>필수 구성 요소  
  
1.  System Center Operations Manager 2007 R2, 2012 또는 2012 SP1 설치 되어 실행 중 이어야 합니다.  
  
2.  SQL Server 2008 R2 Native Client 또는 SQL Server 2012 Native Client를 설치 해야 합니다.  
  
3.  SQL Server PDW 및 HDInsight 모니터링 관리 팩을 설치 하 고 사용을 가져온, 게 구성 해야 합니다. 이러한 작업을 수행할 대 한 지침은 다음을 사용 합니다.  
  
    -   [SCOM 관리 팩 &#40; 설치 분석 플랫폼 시스템 &#41;](install-the-scom-management-packs.md)  
  
    -   [PDW &#40;에 대 한 SCOM 관리 팩 가져오기 분석 플랫폼 시스템 &#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [분석 플랫폼 시스템 &#40; 모니터링 하는 SCOM 구성 분석 플랫폼 시스템 &#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>SQL Server PDW SCOM으로 모니터링 하려면  
SCOM 관리 팩을 구성한 후 SCOM의 모니터링 창에서을 클릭 하 고 드릴 다운 하 **SQL Server 어플라이언스** 차례로 **Microsoft SQL Server 병렬 데이터 웨어하우스**합니다. Microsoft SQL Server 병렬 데이터 웨어하우스, 아래 네 가지 선택 사항이: 경고, 제품, 어플라이언스 다이어그램 및 노드.  
  
### <a name="alerts"></a>경고  
경고는 관리 해야 하는 현재 경고를 찾을 수 있습니다.  
  
![경고](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>어플라이언스  
어플라이언스는 사용자 환경에서 현재 검색 하 고 모니터링 대상 SQL Server PDW 어플라이언스를 찾을 수 있습니다. 어플라이언스에 여기 표시 되지 않습니다 것에 대 한 ODBC 연결을 만든 경우 다음 있을 수 있습니다 PDWWatcher 계정에 문제가 있습니다. 이러한 표시 "모니터링 안 함"으로 PDWMonitor 계정에 문제가 있을 수 있습니다. SCOM 실시간으로 변경 하지 않습니다 하지만 정기적으로 모니터링 하는 새 어플라이언스에 대 한 검사 정도가 소요 됩니다 하 고 정기적으로 모니터링 하기 위한 기기에 쿼리를 보냅니다.  
  
![어플라이언스](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>어플라이언스 다이어그램  
어플라이언스 다이어그램 페이지는 트리 보기와 어플라이언스의 상태 보기를 가져올 수 있습니다.  
  
![어플라이언스 다이어그램](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>노드  
마지막으로, 노드 보기를 사용 하면 각 노드를 통해 어플라이언스의 상태를 볼 수 있습니다.  
  
![노드](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>관련 항목:  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[관리 콘솔 경고 이해 &#40; 분석 플랫폼 시스템 &#41;](understanding-admin-console-alerts.md)  
  
