---
title: 표준 시간대 구성
description: 표준 시간대 페이지를 사용 하 여 APS (분석 플랫폼 시스템) 어플라이언스의 모든 노드에 대 한 표준 시간대를 설정할 수 있습니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1da16790d011a628bc2536de051eb1181f06b8cf
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401392"
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>어플라이언스 표준 시간대 구성-분석 플랫폼 시스템
**표준 시간대** 페이지를 사용 하 여 APS (분석 플랫폼 시스템) 어플라이언스의 모든 노드에 대 한 표준 시간대를 설정할 수 있습니다.  
  
## <a name="to-set-the-time-zone"></a>표준 시간대를 설정 하려면  
  
1.  Configuration Manager를 시작 합니다. 자세한 내용은 [Configuration Manager &#40;Analytics Platform System&#41;시작 ](launch-the-configuration-manager.md)을 참조 하세요.  
  
2.  Configuration Manager의 **서비스 상태** 페이지를 사용 하 여 어플라이언스 서비스를 중지 합니다. 지침은 [PDW 서비스 상태 &#40;분석 플랫폼 시스템&#41;](pdw-services-status.md) 을 참조 하세요.  
  
3.  Configuration Manager 왼쪽 창에서 **표준 시간대**를 클릭 합니다. **표준 시간대** 드롭다운 메뉴에서 원하는 표준 시간대를 선택 합니다. 사용자의 위치에 따라 **일광 절약 시간제에 맞게 자동으로 시계를 조정**하는 옆의 상자를 선택 하도록 선택할 수도 있습니다.  
  
4.  **적용** 을 클릭 하 여 변경 내용을 저장 합니다.  
  
5.  Configuration Manager의 **서비스 상태** 페이지를 사용 하 여 어플라이언스 서비스를 다시 시작 합니다. 권한을 변경 하려는 경우 어플라이언스를 다시 시작 하기 전에이 작업을 수행할 수 있습니다.  
  
![DWConfig 어플라이언스 시간](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>참고 항목  
[Configuration Manager &#40;Analytics Platform System을 시작&#41;](launch-the-configuration-manager.md)  
  
