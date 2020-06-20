---
title: MSSQLSERVER_844 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 844 (Database Engine error)
ms.assetid: 2060c886-1226-4066-bc0c-de90a1cfb82b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 55ab248466e7552f1265b047c559ca397d204148
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053614"
---
# <a name="mssqlserver_844"></a>MSSQLSERVER_844
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|844|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|BUFLATCH_TIMEOUT_CONTINUE|  
|메시지 텍스트|버퍼 래치를 기다리는 동안 시간이 초과되었습니다.-- 유형 %d, bp %p, 페이지 %d:%d, 상태 %#x, 데이터베이스 ID: %d, 할당 단위 ID: %I64d%ls, 태스크 0x%p : %d, 대기 시간 %d, 플래그 0x%I64x, 소유 태스크 0x%p.  계속 대기합니다.|  
  
## <a name="explanation"></a>설명  
 프로세스에서 래치를 얻기 위해 대기 중입니다. 이 문제는 완료하는 데 시간이 너무 오래 걸리는 I/O 작업으로 인해 발생할 수 있습니다. 일반적으로 이 오류 유형은 시스템 프로세스를 차단하는 다른 태스크로 인해 발생합니다. 하드웨어 오류로 인해 이 오류가 발생하는 경우도 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 이 오류가 발생하는 것을 방지하려면 다음을 시도하십시오.  
  
-   작업을 줄이십시오.  
  
-   오류 로그 또는 이벤트 로그에서 관련 I/O 오류를 검사하십시오. I/O 오류는 일반적으로 디스크 오류를 나타냅니다.  
  
-   잠겨 있는 태스크 및 기타 오류에 대한 오류 로그를 검사하십시오.  
  
-   어설션과 같은 오류가 자주 발생하면 이 문제를 해결하십시오.  
  
 오류가 지속되면 Microsoft 고객 서비스 지원 센터에 문의하십시오.  
  
  
