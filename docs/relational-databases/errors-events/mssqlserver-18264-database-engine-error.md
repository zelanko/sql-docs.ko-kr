---
title: MSSQLSERVER_18264 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 18264 (Database Engine error)
ms.assetid: 3050fc56-2be5-43cf-916b-50a3ac5f89aa
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0604f384a9366e2483b2eaef6bfcae111b9ebf8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver18264"></a>MSSQLSERVER_18264
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|Microsoft SQL Server|  
|이벤트 ID|18264|  
|이벤트 원본|MSSQLENGINE|  
|구성 요소|SQLEngine|  
|심볼 이름|STRMIO_DBDUMP|  
|메시지 텍스트|데이터베이스가 백업되었습니다. 데이터베이스: %s, 만든 날짜(시간): %s(%s), 덤프한 페이지 수: %d, 첫 번째 LSN: %s, 마지막 LSN: %s, 덤프 장치 수: %d, 장치 정보: (%s). 이 메시지는 정보 제공용이므로 사용자가 조치할 필요는 없습니다.|  
  
## <a name="explanation"></a>설명  
기본적으로 백업을 성공적으로 수행할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 시스템 이벤트 로그에 이 정보 메시지가 추가됩니다. 트랜잭션 로그를 자주 백업하는 경우 이러한 메시지는 바로 누적되므로 엄청난 오류 로그가 쌓여 다른 메시지를 찾기 힘들 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 추적 플래그 **3226**을 사용하여 이러한 로그 항목을 표시하지 않을 수 있습니다. 로그 백업을 자주 실행하거나 이러한 항목에 종속되는 스크립트가 없는 경우 이 추적 플래그를 설정하면 유용합니다.  
  
추적 플래그를 사용하는 방법은 SQL Server 온라인 설명서를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
[추적 플래그&#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
