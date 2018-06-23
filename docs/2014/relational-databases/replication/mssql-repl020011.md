---
title: MSSQL_REPL020011 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_REPL020011 error
ms.assetid: f72072d7-bbb6-48ad-ac88-afa74aeb4d58
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b4b3ceb8ea7498053b7dde311213cfb7bea5fb99
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093500"
---
# <a name="mssqlrepl020011"></a>MSSQL_REPL020011
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|20011|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|'%2'에서 '%1'을(를) 실행할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 로그 판독기 에이전트가 **sp_replcmds**(프로세스가 \<ServerName>에서 'sp_replcmds'를 실행할 수 없음) 또는 **sp_repldone**(프로세스가 \<ServerName>에서 'sp_repldone'를 실행할 수 없음)을 실행하는 경우와 같이 트랜잭션 복제 처리 중 여러 상황에서 이 오류가 발생할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 방금 백업에서 복원한 데이터베이스에서 이 오류가 발생한 경우에는 **sp_replrestart** 실행을 비롯해 백업 및 복원 설명서에서 간략하게 설명한 단계를 수행했는지 확인하십시오. 자세한 내용은 [스냅숏 및 트랜잭션 복제의 백업 및 복원을 위한 전략](administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)을(를) 참조하세요.  
  
 이 오류는 내부 처리 오류입니다. 이 오류가 복원이 아닌 다른 상황에서 발생한 경우에는 일반적으로 복제를 제거하고 다시 구성해야 합니다. 복제를 제거할 수 없으면 고객 지원 담당자에 문의하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)   
 [sp_replcmds&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql)   
 [sp_repldone&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repldone-transact-sql)  
  
  
