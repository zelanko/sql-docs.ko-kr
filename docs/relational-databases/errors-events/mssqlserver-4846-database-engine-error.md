---
title: MSSQLSERVER_4846 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 4846 (Database Engine error)
ms.assetid: a455e809-1883-4c7d-b3e3-835ee5bfe258
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab2eeebe36e77791dac2a429e3d2e895b208cb13
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver4846"></a>MSSQLSERVER_4846
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|4846|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|BULKPROV_MEMORY|  
|메시지 텍스트|대량 데이터 공급자가 메모리를 할당하지 못했습니다.|  
  
## <a name="explanation"></a>설명  
메모리 할당이 실패했습니다.  
  
## <a name="user-action"></a>사용자 동작  
메모리 오류 문제를 해결하려면 다음과 같은 일반적인 단계를 따르십시오.  
  
1.  다른 응용 프로그램 또는 서비스가 현재 서버의 메모리를 사용 중인지 확인합니다. 중요도가 낮은 응용 프로그램이나 서비스에서 메모리를 덜 사용하도록 다시 구성합니다.  
  
2.  **SQL Server: Buffer Manager**, **SQL Server: Memory Manager**에 대한 성능 모니터 카운터 수집을 시작합니다.  
  
3.  다음 SQL Server 메모리 구성 매개 변수를 확인합니다.  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
    비정상적인 설정이 있는지 확인하고 필요할 경우 수정합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 메모리 요구 사항을 확인합니다. 기본 설정은 SQL Server 온라인 설명서의 "서버 구성 옵션 설정"을 참조하십시오.  
  
4.  DBCC MEMORYSTATUS 출력 결과를 확인하고 이러한 오류 메시지가 표시될 때 이 값이 어떻게 변경되는지 관찰합니다.  
  
5.  동시 세션 및 현재 실행 중인 쿼리 수와 같은 작업을 확인합니다.  
  
다음 동작으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 수 있는 메모리를 늘릴 수 있습니다.  
  
-   SQL Server 외에 다른 응용 프로그램이 리소스를 사용 중인 경우 이 응용 프로그램을 중지하거나 별도의 서버에서 실행합니다. 이렇게 하면 외부 메모리 가중을 없앨 수 있습니다.  
  
-   **max server memory**를 구성한 경우 설정값을 늘립니다.  
  
다음 DBCC 명령을 실행하여 몇 가지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 캐시를 비웁니다.  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
문제가 지속되면 추가적인 조사를 수행하고 작업을 줄여야 할 수 있습니다.  
  
