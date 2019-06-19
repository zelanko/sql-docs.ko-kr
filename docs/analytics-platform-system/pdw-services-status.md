---
title: PDW 서비스 상태-Analytics Platform System | Microsoft Docs
description: Analytics Platform System에 대 한 상태를 서비스 하는 병렬 데이터 웨어하우스 (PDW).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6892bfcca05e0f85039dddee65a54b485a7ed433
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63027557"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>Analytics Platform System에 대 한 병렬 데이터 웨어하우스 서비스 상태
병렬 데이터 웨어하우스 **서비스 상태** 페이지는 Microsoft Analytics Platform System Configuration Manager에서 모든 SQL Server PDW 서비스의 현재 상태가 표시 되며 PDW 서비스 중지 및 시작 하는 기능을 제공 합니다. 이것이 PDW 서비스 시작 및 중지에 대 한 지원 되는 유일한 방법입니다. 개별 구성 요소 또는 서비스를 시작할 수 없습니다 독립적으로 참고 합니다.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>어플라이언스 서비스 시작 또는 중지 하려면  
  
1.  어플라이언스 서비스를 시작 하려면 **기기 시작**합니다.  
  
2.  어플라이언스 서비스를 중지 하려면 클릭 **어플라이언스 중지**합니다.  
  
클릭 필요는 없습니다 **적용** 시작 하 고 사용 하 여 어플라이언스 서비스를 중지 하는 경우 **어플라이언스 시작** 하 고 **중지 어플라이언스**합니다.  
  
![DWConfig 어플라이언스 PDW 서비스](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> PDW 영역을 중지 노드에서 PDW 에이전트 (sqldwagent) 중지 됩니다. PDW 에이전트 상태 모니터링을 보고 하려면 PDW 제어 노드에 필요 합니다.  
  
## <a name="see-also"></a>관련 항목  
[APS 어플라이언스를 켜거나 전원을 &#40;Analytics Platform System&#41;](power-the-aps-appliance-on-or-off.md)  
  
