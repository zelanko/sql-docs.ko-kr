---
title: MSSQLSERVER_1222 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1222 (Database Engine error)
ms.assetid: c5b1c2f4-f591-4cc1-aa17-204636a27f29
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8b8b22939e29f7f89faf3755d9da45db949179d0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969693"
---
# <a name="mssqlserver_1222"></a>MSSQLSERVER_1222
    
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
  
  
