---
title: "MSSQLSERVER_1204 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1204 (Database Engine error)
ms.assetid: de6ece78-79de-484d-9224-ca0f7645815f
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 998595e1d253f0e09a18ec9970081798ea24f1b7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver1204"></a>MSSQLSERVER_1204
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|1204|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LK_OUTOF|  
|메시지 텍스트|SQL Server 데이터베이스 엔진 인스턴스에서 지금 LOCK 리소스를 가져올 수 없습니다. 활성 사용자가 적을 때 문을 다시 실행하십시오. 데이터베이스 관리자에게 이 인스턴스의 잠금 및 메모리 구성이나 장기 실행 트랜잭션을 확인하도록 요청하십시오.|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 리소스를 잠글 수 없습니다. 이 오류는 다음과 같은 문제로 인해 발생할 수 있습니다.  
  
-   다른 프로세스가 사용 중이거나 서버가 **max server memory** 옵션이 구성된 상태로 동작 중이어서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 운영 체제에서 더 많은 메모리를 할당할 수 없습니다.  
  
-   잠금 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용 가능한 메모리의 60% 이상을 사용하지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
SQL Server에 충분한 메모리를 할당할 수 없는 경우 다음을 시도하십시오.  
  
-   SQL Server 외에 다른 응용 프로그램이 리소스를 사용 중인 경우 이 응용 프로그램을 중지하거나 별도의 서버에서 실행합니다. 이렇게 하면 다른 프로세스에서 사용하는 메모리를 해제하여 SQL Server에서 사용할 수 있습니다.  
  
-   max server memory를 구성한 경우 설정값을 늘리십시오.  
  
잠금 관리자가 최대 가용 메모리 양을 사용한 경우 가장 많은 잠금을 보유한 트랜잭션을 확인하여 이를 종료하십시오. 다음 스크립트를 사용하여 가장 많은 잠금을 보유한 트랜잭션을 확인할 수 있습니다.  
  
```  
SELECT request_session_id, COUNT (*) num_locks  
FROM sys.dm_tran_locks  
GROUP BY request_session_id   
ORDER BY count (*) DESC  
```  
  
가장 높은 세션 ID를 확인하고 KILL 명령을 사용하여 종료하십시오.  
  
