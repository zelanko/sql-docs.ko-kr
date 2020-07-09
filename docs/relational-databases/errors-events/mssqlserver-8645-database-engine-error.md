---
title: MSSQLSERVER_8645 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8645 (Database Engine error)
ms.assetid: 63d6d6d7-3850-4061-8e96-b1fa665e3180
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1b206d4e5381112e0731376e2639d4fa1516c867
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765304"
---
# <a name="mssqlserver_8645"></a>MSSQLSERVER_8645
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|8645|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|MEMTIMEDOUT_ERR|  
|메시지 텍스트|메모리 리소스가 쿼리를 실행하기를 기다리는 동안 시간이 초과되었습니다. 쿼리를 다시 실행하십시오.|  
  
## <a name="explanation"></a>설명  
리소스 풀 'default'에서 메모리 리소스가 쿼리를 실행하기를 기다리는 동안 시간이 초과되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
리소스 관리자를 사용하지 않는 경우 전체 서버 상태 및 부하를 확인하고 리소스 풀 또는 작업 그룹 설정을 확인하는 것이 좋습니다.  
  
다음 목록은 메모리 오류 문제를 해결하는 데 도움이 되는 일반적인 단계를 간략히 설명합니다.  
  
1.  다른 애플리케이션 또는 서비스가 현재 서버의 메모리를 사용 중인지 확인합니다. 중요도가 낮은 애플리케이션이나 서비스에서 메모리를 덜 사용하도록 다시 구성합니다.  
  
2.  **SQL Server: Buffer Manager**, **SQL Server: Memory Manager**에 대한 성능 모니터 카운터 수집을 시작합니다.  
  
3.  다음 SQL Server 메모리 구성 매개 변수를 확인합니다.  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
    비정상적인 설정이 있는지 확인하고 필요할 경우 수정합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 향상된 메모리 요구 사항을 확인합니다. 기본 설정은 SQL Server 온라인 설명서의 "서버 구성 옵션 설정"을 참조하십시오.  
  
4.  DBCC MEMORYSTATUS 출력 결과를 확인하고 이러한 오류 메시지가 표시될 때 이 값이 어떻게 변경되는지 관찰합니다.  
  
5.  동시 세션 및 현재 실행 중인 쿼리 수와 같은 작업을 확인합니다.  

다음 동작으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 수 있는 메모리를 늘릴 수 있습니다.  
  
-   SQL Server 외에 다른 애플리케이션이 리소스를 사용 중인 경우 이 애플리케이션을 중지하거나 별도의 서버에서 실행합니다. 이렇게 하면 외부 메모리 가중을 없앨 수 있습니다.  
  
-   **max server memory**를 구성한 경우 설정값을 늘립니다.  
  
다음 DBCC 명령을 실행하여 몇 가지 SQL Server 메모리 캐시를 비웁니다.  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
문제가 지속되면 추가적인 조사를 수행하고 작업을 줄여야 할 수 있습니다.  
  
