---
title: MSSQLSERVER_32044 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 32044 (Database Engine error)
ms.assetid: f2d073be-d9a1-4837-8a38-028d3e3403bd
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: db727a30a97c0692c27ead6e1964efdd4ab256ab
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver32044"></a>MSSQLSERVER_32044
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|32044|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQLErrorNum32044|  
|메시지 텍스트|'미러 커밋 오버헤드'에 대한 경고가 발생했습니다. '%d'의 현재 값이 임계값 '%d'을(를) 초과합니다.|  
  
## <a name="explanation"></a>설명  
이 데이터베이스 미러링 이벤트는 주 서버 인스턴스에서 실행되어 집계 커밋 대기 시간이 데이터베이스 미러링으로 인해 사용자 지정 임계값에 도달했거나 초과했음을 나타냅니다. 대기 시간은 트랜잭션의 수와 각 트랜잭션에 걸린 시간의 곱입니다. 예를 들어 1000개의 트랜잭션 * 1밀리초의 경우와 1개의 트랜잭션 \* 1000밀리초의 경우 모두 1000밀리초의 대기 시간이 계산됩니다. 커밋 대기 시간의 증가는 트랜잭션 개수의 급증, 로그 전송 지연, 미러 서버 인스턴스에 대한 로그 플러시 지연에 의해 발생할 수 있습니다.  
  
미러 커밋 오버헤드의 양은 동기화 작업의 현재 성능에 미치는 영향을 평가하는 데 도움이 되는 성능 메트릭입니다. 이 메트릭은 보호 우선 모드에만 해당됩니다. 보호 우선 모드는 동기적이므로 주 서버 인스턴스는 미러 서버 인스턴스로 로그 레코드를 보낸 후 미러 서버 인스턴스에서 디스크에 로그 레코드를 기록했음을 확인할 때까지 트랜잭션에 대한 커밋을 기다립니다. 로그 레코드는 미러 데이터베이스로 복원되기를 기다리는 동안 미러 서버 인스턴스의 디스크에 남아 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
주 서버 인스턴스 및 미러 서버 인스턴스의 로드를 확인하고 문제의 원인이 된 해당 네트워크 연결을 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스 미러링&#40;SQL Server&#41;](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[미러링 성능 메트릭에 대해 경고 임계값 및 경고 사용&#40;SQL Server&#41;](~/database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
