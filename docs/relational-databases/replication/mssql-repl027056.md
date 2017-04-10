---
title: "MSSQL_REPL027056 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_REPL027056 오류"
ms.assetid: 92d62f3c-b8ae-482e-a348-2e9a8ee9786e
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_REPL027056
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|27056|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|병합 프로세스에서 '%1'의 생성 기록을 변경할 수 없습니다. 문제를 해결하려면 자세한 기록 로깅으로 동기화를 다시 시작하고 기록할 출력 파일을 지정하십시오.|  
  
## 설명  
 일반적으로 이 오류는 과도하게 커진 병합 복제 시스템 테이블에서 발생한 경합으로 인해 생깁니다. 게시 보존 기간이 긴 경우에 주로 시스템 테이블이 방대해지며 이는 보존 기간 동안 메타데이터가 이러한 테이블에 저장되기 때문입니다.  
  
## 사용자 동작  
 **이 문제를 해결하려면**  
  
1.  값을 줄이려면-**DownloadGenerationsPerBatch** 및 **-UploadGenerationsPerBatch** 처리를 허용 하도록 병합 에이전트에 대 한 매개 변수를 기본 해결 하는 동안 계속 실행 오류가 발생 합니다. 에이전트 프로필 및 명령줄에서 에이전트 매개 변수를 지정할 수 있습니다. 참조 항목:  
  
    -   [복제 에이전트 프로필 작업](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [보기 및 복제 에이전트 명령 프롬프트 매개 변수 & #40; 수정 SQL Server Management Studio & #41;](../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
    -   [복제 에이전트 실행 파일 개념](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)합니다.  
  
2.  게시 보존 기간에 대해 가능한 낮은 설정 값을 지정합니다. 자세한 내용은 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)를 참조하세요.  
  
3.  병합 복제에 대 한 유지 관리의 일환으로, 병합 복제와 관련 된 시스템 테이블의 증가 확인 가끔: **MSmerge_contents**, **MSmerge_genhistory**, 및 **MSmerge_tombstone**, **MSmerge_current_partition_mappings**, 및 **MSmerge_past_partition_mappings**합니다. 이러한 테이블의 인덱스를 주기적으로 다시 만듭니다. 자세한 내용은 참조 [다시 구성 및 인덱스 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)합니다.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  