---
title: MSSQLSERVER_8651 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8651 (Database Engine error)
ms.assetid: 4cc3498d-5449-4c4e-b1f9-3271831c725a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 43a385350a05edee3759ab83d318e365f5b4f3e4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85031881"
---
# <a name="mssqlserver_8651"></a>MSSQLSERVER_8651
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|8651|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|MEMGRANT_ERR|  
|메시지 텍스트|최소 쿼리 메모리를 사용할 수 없어서 요청한 작업을 수행할 수 없습니다. '쿼리 당 최소 메모리' 서버 구성 옵션의 구성 값을 줄이십시오.|  
  
## <a name="explanation"></a>설명  
 다른 프로세스에서 서버 메모리를 사용하고 있어 서버의 메모리가 부족합니다.  
  
## <a name="user-action"></a>사용자 동작  
 '쿼리 당 최소 메모리' 서버 구성 옵션의 구성 값을 줄이거나 서버에 대한 쿼리 로드를 줄이십시오.  
  
 다음 목록은 메모리 오류 문제를 해결하는 데 도움이 되는 일반적인 단계를 간략히 설명합니다.  
  
1.  다른 애플리케이션 또는 서비스가 현재 서버의 메모리를 사용 중인지 확인합니다. 중요도가 낮은 애플리케이션이나 서비스에서 메모리를 덜 사용하도록 다시 구성합니다.  
  
2.  **SQL Server: Buffer Manager**, **SQL Server: Memory Manager**에 대한 성능 모니터 카운터 수집을 시작합니다.  
  
3.  다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 구성 매개 변수를 확인합니다.  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
     비정상적인 설정이 있는지 확인하고 필요할 경우 수정합니다. 기본 설정은 SQL Server 온라인 설명서의 "서버 구성 옵션 설정"을 참조하십시오.  
  
4.  동시 세션 및 현재 실행 중인 쿼리 수와 같은 작업을 확인합니다.  
  
 다음 동작으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 수 있는 메모리를 늘릴 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 외에 다른 애플리케이션이 리소스를 사용 중인 경우 이 애플리케이션을 중지하거나 별도의 서버에서 실행합니다. 이렇게 하면 외부 메모리 가중을 없앨 수 있습니다.  
  
-   **max server memory**를 구성한 경우 설정값을 늘립니다.  
  
 다음 DBCC 명령을 실행하여 몇 가지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 캐시를 비웁니다.  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 문제가 지속되면 추가적인 조사를 수행하고 작업을 줄여야 할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [DBCC FREESYSTEMCACHE &#40;Transact-sql&#41;](/sql/t-sql/database-console-commands/dbcc-freesystemcache-transact-sql)   
 [DBCC FREESESSIONCACHE &#40;Transact-sql&#41;](/sql/t-sql/database-console-commands/dbcc-freesessioncache-transact-sql)   
 [DBCC FREEPROCCACHE &#40;Transact-sql&#41;](/sql/t-sql/database-console-commands/dbcc-freeproccache-transact-sql)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [SQL Server, Buffer Manager 개체](../performance-monitor/sql-server-buffer-manager-object.md)   
 [SQL Server, Memory Manager 개체](../performance-monitor/sql-server-memory-manager-object.md)  
  
  
