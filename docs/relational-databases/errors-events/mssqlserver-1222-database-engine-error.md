---
title: "MSSQLSERVER_1222 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1222 (Database Engine error)
ms.assetid: c5b1c2f4-f591-4cc1-aa17-204636a27f29
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 88e274efe280363b51f7abfbcea02d54b0d66148
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver1222"></a>MSSQLSERVER_1222
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|1222|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LK_TIMEOUT|  
|메시지 텍스트|잠금 요청 제한 시간이 초과되었습니다.|  
  
## <a name="explanation"></a>설명  
이 쿼리에서 대기할 수 있는 시간보다 긴 시간 동안 다른 트랜잭션이 요청된 리소스에 대해 잠금을 보유하고 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
이 문제를 완화하려면 다음 태스크를 수행하십시오.  
  
1.  가능한 경우 요청한 리소스에 대한 잠금을 보유한 트랜잭션을 찾으십시오. **sys.dm_os_waiting_tasks** 및 **sys.dm_tran_locks** 동적 관리 뷰를 사용하세요.  
  
2.  트랜잭션이 여전히 잠금을 보유 중이면 트랜잭션을 종료하십시오(가능한 경우).  
  
3.  쿼리를 다시 실행하십시오.  
  
이 오류가 자주 발생하면 잠금 제한 시간을 변경하거나 문제가 되는 트랜잭션을 수정하여 잠금을 보유하는 시간을 줄이십시오.  
  

