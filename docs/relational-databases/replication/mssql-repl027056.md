---
description: MSSQL_REPL027056
title: MSSQL_REPL027056 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL027056 error
ms.assetid: 92d62f3c-b8ae-482e-a348-2e9a8ee9786e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 9292c4aa16f19f3b1c6e8cb2cd034345eb628ca1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97432199"
---
# <a name="mssql_repl027056"></a>MSSQL_REPL027056
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>메시지 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|27056|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|병합 프로세스에서 '%1'의 생성 기록을 변경할 수 없습니다. 문제를 해결하려면 자세한 기록 로깅으로 동기화를 다시 시작하고 기록할 출력 파일을 지정하십시오.|  
  
## <a name="explanation"></a>설명  
 일반적으로 이 오류는 과도하게 커진 병합 복제 시스템 테이블에서 발생한 경합으로 인해 생깁니다. 게시 보존 기간이 긴 경우에 주로 시스템 테이블이 방대해지며 이는 보존 기간 동안 메타데이터가 이러한 테이블에 저장되기 때문입니다.  
  
## <a name="user-action"></a>사용자 동작  
 **이 문제를 해결하려면**  
  
1.  병합 에이전트에 대한 -**DownloadGenerationsPerBatch** 및 **-UploadGenerationsPerBatch** 매개 변수 값을 줄여 오류를 발생시키는 근본 문제를 해결하는 동안 처리가 계속 진행되도록 합니다. 에이전트 프로필 및 명령줄에서 에이전트 매개 변수를 지정할 수 있습니다. 자세한 내용은 다음을 참조하세요.  
  
    -   [복제 에이전트 프로필 작업](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [복제 에이전트의 명령 프롬프트 매개 변수 보기 및 수정&#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)에 할당될 최소 및 최대 메모리 양을 설정합니다.  
  
2.  게시 보존 기간에 대해 가능한 낮은 설정 값을 지정합니다. 자세한 내용은 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)을(를) 참조하세요.  
  
3.  병합 복제 유지 관리의 한 부분으로 병합 복제와 연결된 **MSmerge_contents**, **MSmerge_genhistory** 및 **MSmerge_tombstone**, **MSmerge_current_partition_mappings** 및 **MSmerge_past_partition_mappings** 시스템 테이블의 증가를 확인하십시오. 이러한 테이블의 인덱스를 주기적으로 다시 만듭니다. 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
