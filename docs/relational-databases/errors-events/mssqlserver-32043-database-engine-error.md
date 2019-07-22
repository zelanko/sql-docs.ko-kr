---
title: MSSQLSERVER_32043 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 32043 (Database Engine error)
ms.assetid: a0c48ae3-4c8c-419c-afb5-579fcefac01d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8d7de359bcc478f821252f35344dd1b539a8beed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041176"
---
# <a name="mssqlserver32043"></a>MSSQLSERVER_32043
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|32043|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQLErrorNum32043|  
|메시지 텍스트|'복원되지 않은 로그'에 대한 경고가 발생했습니다. '%d'의 현재 값이 임계값 '%d'을(를) 초과합니다.|  
  
## <a name="explanation"></a>설명  
이 데이터베이스 미러링 이벤트는 미러 서버 인스턴스에서 발생하며 복원되지 않은 로그의 양이 사용자 지정 임계값에 도달했음을 나타냅니다. 일반적으로 이 이벤트는 두 시스템 간 대역폭이 감소했거나 로드가 증가한 경우와 같은 시스템 성능의 변경으로 인해 발생합니다.  
  
복원되지 않은 로그는 미러 서버 인스턴스에서 수신하여 디스크에 기록되었지만 미러 데이터베이스를 복원하기 위해 대기 중인 로그입니다. 복원되지 않은 로그의 양(KB)은 현재 장애 조치(Failover) 시간을 계산하는 데 유용한 성능 메트릭입니다. 이 시간은 데이터베이스를 복구하고 이 데이터베이스를 온라인 상태로 만드는 데 필요한 짧은 추가 시간과 더불어 복원되지 않은 로그에 적용할 때 필요하며 장애 조치 시간의 주요 요소입니다.  
  
> [!NOTE]  
> 자동 장애 조치의 경우 시스템이 오류를 감지하는 데 걸리는 시간은 장애 조치 시간과 관계가 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
주 서버 인스턴스 및 미러 서버 인스턴스의 로드를 확인하고 문제의 원인이 된 해당 네트워크 연결을 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스 미러링&#40;SQL Server&#41;](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[미러링 성능 메트릭에 대해 경고 임계값 및 경고 사용&#40;SQL Server&#41;](~/database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
