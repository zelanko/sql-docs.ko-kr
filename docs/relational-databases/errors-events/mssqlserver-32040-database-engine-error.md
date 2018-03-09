---
title: "MSSQLSERVER_32040 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 32040 (Database Engine error)
ms.assetid: 709219b1-f8b2-4696-8923-dd2e91492eb8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 31deb4cd25b24e70de09309196989ac60aa8006e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver32040"></a>MSSQLSERVER_32040
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|32040|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQLErrorNum32040|  
|메시지 텍스트|'보내지 않은 가장 오래된 트랜잭션'에 대한 경고가 발생했습니다. '%d'의 현재 값이 임계값 '%d'을(를) 초과합니다.|  
  
## <a name="explanation"></a>설명  
이 데이터베이스 미러링 이벤트는 주 서버 인스턴스에서 발생하며 보내지 않은 가장 오래된 트랜잭션 기간이 사용자 지정 임계값에 도달했음을 나타냅니다. 일반적으로 이 이벤트는 두 시스템 간 대역폭이 감소했거나 로드가 증가한 경우와 같은 시스템 성능의 변경으로 인해 발생합니다.  
  
보내지 않은 가장 오래된 트랜잭션 기간은 보내지 않은 트랜잭션의 시간(분)을 기준으로 잠재적 데이터 손실을 측정하는 데 유용한 성능 메트릭입니다. 이 메트릭은 성능 우선 모드 세션과 특히 관련이 있습니다. 그러나 파트너의 연결이 끊어져 미러링이 일시 중지되거나 일시 중단되면 이 메트릭은 보호 우선 모드 세션과도 관련이 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
주 서버 인스턴스 및 미러 서버 인스턴스의 로드를 확인하고 문제의 원인이 된 해당 네트워크 연결을 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스 미러링&#40;SQL Server&#41;](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[미러링 성능 메트릭에 대해 경고 임계값 및 경고 사용&#40;SQL Server&#41;](~/database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
