---
title: PDW 서비스 상태
description: 분석 플랫폼 시스템에 대 한 PDW (병렬 데이터 웨어하우스) 서비스 상태입니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2789c8b74420a56a32d08a0339d4ee6d3cc112d1
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400851"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>분석 플랫폼 시스템에 대 한 병렬 데이터 웨어하우스 서비스 상태
Microsoft Analytics Platform System Configuration Manager의 병렬 데이터 웨어하우스 **서비스 상태** 페이지에는 모든 SQL Server PDW 서비스의 현재 상태가 표시 되 고 PDW 서비스를 중지 하 고 시작할 수 있는 기능이 제공 됩니다. 이는 PDW 서비스를 시작 및 중지 하는 데 유일 하 게 지원 되는 방법입니다. 개별 구성 요소 또는 서비스는 개별적으로 시작할 수 없습니다.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>어플라이언스 서비스를 시작 하거나 중지 하려면  
  
1.  어플라이언스 서비스를 시작 하려면 **어플라이언스 시작**을 클릭 합니다.  
  
2.  어플라이언스 서비스를 중지 하려면 **어플라이언스 중지**를 클릭 합니다.  
  
어플라이언스 **시작** 및 **어플라이언스 중지**를 사용 하 여 어플라이언스 서비스를 시작 및 중지 하는 경우에는 **적용** 을 클릭할 필요가 없습니다.  
  
![DWConfig 어플라이언스 PDW 서비스](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> PDW 지역을 중지 하면 노드에서 PDW 에이전트 (sqldwagent)도 중지 됩니다. PDW 에이전트는 상태 모니터링을 보고 하는 PDW 제어 노드가 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
[&#40;Analytics Platform System&#41;에서 AP 어플라이언스를 켜고 끕니다.](power-the-aps-appliance-on-or-off.md)  
  
