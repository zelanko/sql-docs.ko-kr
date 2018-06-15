---
title: PDW 서비스 상태-분석 플랫폼 시스템 | Microsoft Docs
description: 분석 플랫폼 시스템에 대 한 병렬 데이터 웨어하우스 (PDW) 서비스 상태입니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e2252bb821f9522515f1625b0fc118323cb50d1f
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539003"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>분석 플랫폼 시스템에 대 한 병렬 데이터 웨어하우스 서비스 상태
병렬 데이터 웨어하우스 **서비스 상태** 페이지 Microsoft 분석 플랫폼 시스템 구성 관리자에서 모든 SQL Server PDW 서비스의 현재 상태를 표시 하 고 PDW 서비스 중지 및 시작 하는 기능을 제공 합니다. 이것이 PDW 서비스 시작 및 중지에 대 한 지원 되는 유일한 방법입니다. 개별 구성 요소 또는 서비스를 시작할 수 없습니다 독립적으로 확인 합니다.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>어플라이언스 서비스 시작 또는 중지 하려면  
  
1.  어플라이언스 서비스를 시작 하려면 **기기 시작**합니다.  
  
2.  어플라이언스 서비스를 중지 하려면 클릭 **중지 기기**합니다.  
  
클릭 하 여 필요 없는 **적용** 시작 하 고 사용 하 여 어플라이언스 서비스를 중지 하는 경우 **기기 시작** 및 **중지 기기**합니다.  
  
![DWConfig 어플라이언스 PDW 서비스](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> PDW 영역을 중지 HDInsight 지역이의 노드에서 PDW 에이전트 (sqldwagent) 중지 됩니다. HDInsight 지역은 여전히 작동 상태 모니터링은 사용할 수 없습니다. (PDW 에이전트 PDW 제어 노드 상태 모니터링을 보고 하기 위해 필요 합니다.)  
  
## <a name="see-also"></a>관련 항목:  
[APS 기기를 켜거나 전원을 &#40;분석 플랫폼 시스템&#41;](power-the-aps-appliance-on-or-off.md)  
  
