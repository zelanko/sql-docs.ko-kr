---
title: "복제 에이전트 프로필 | Microsoft 문서"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Distribution Agent, profiles
- replication [SQL Server], agents and profiles
- replication agent profiles [SQL Server]
- Merge Agent, profiles
- agents [SQL Server replication], profiles
- Queue Reader Agent, profiles
- profiles [SQL Server], replication agents
- Snapshot Agent, profiles
- Log Reader Agent, profiles
ms.assetid: 0e980725-e42f-4283-94cb-d8a6dba5df62
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a11a7821231d4c7fa3a8719a05bdd1a7bc49ff47
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="replication-agent-profiles"></a>복제 에이전트 프로필
  복제가 구성되면 에이전트 프로필 집합이 배포자에 설치됩니다. 에이전트 프로필에는 에이전트가 실행될 때마다 사용할 매개 변수 집합이 포함됩니다. 각 에이전트는 시작 과정 중에 배포자로 로그인하여 해당 프로필의 매개 변수에 대해 쿼리합니다. 웹 동기화를 사용하는 병합 구독의 경우 구독자에서 프로필을 다운로드하고 저장합니다. 프로필이 변경되면 다음에 병합 에이전트가 실행될 때 구독자에 있는 프로필이 업데이트됩니다. 웹 동기화에 대한 자세한 내용은 [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md)를 참조하십시오.  
  
 복제는 각 에이전트에 대한 기본 프로필과 로그 판독기 에이전트, 배포 에이전트 및 병합 에이전트에 대한 미리 정의된 추가 프로필을 제공합니다. 제공된 프로필뿐 아니라 응용 프로그램 요구 사항에 찾는 프로필을 만들 수 있습니다. 에이전트 프로필을 사용하면 해당 프로필에 연결된 모든 에이전트에 대해 키 매개 변수를 쉽게 변경할 수 있습니다. 예를 들어 스냅숏 에이전트가 20개인 상태에서 쿼리 제한 시간 값을 변경해야 하는 경우( **-QueryTimeout** 매개 변수) 스냅숏 에이전트에서 사용하는 프로필을 업데이트할 수 있으며 다음에 해당 유형의 모든 에이전트가 실행될 때 자동으로 새 값을 사용하여 시작됩니다.  
  
 에이전트의 여러 인스턴스에 대해 서로 다른 프로필을 사용할 수도 있습니다. 예를 들어 전화 접속 연결을 통해 게시자와 배포자에 연결하는 병합 에이전트는 **느린 연결** 프로필을 사용하여 느린 통신에 적합한 매개 변수 집합을 사용할 수 있습니다.  
  
> [!NOTE]  
>  명령줄에서 에이전트 매개 변수 값을 지정하면 해당 값이 에이전트 프로필에서 동일한 매개 변수에 설정된 값을 무시합니다.  
  
 **에이전트 프로필을 사용하고 수정하려면**  
  
-   [복제 에이전트 프로필 작업](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
## <a name="snapshot-agent-profiles"></a>스냅숏 에이전트 프로필  
 다음 표에서는 스냅숏 에이전트에 대한 기본 프로필에서 정의되는 매개 변수를 보여 줍니다. 이러한 매개 변수에 대한 자세한 내용은 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)를 참조하십시오.  
  
||기본|  
|-|-------------|  
|**-BcpBatchSize**|100000|  
|**-HistoryVerboseLevel**|2|  
|**-LoginTimeout**|15|  
|**-QueryTimeout**|1800|  
  
## <a name="log-reader-agent-profiles"></a>로그 판독기 에이전트 프로필  
 다음 표에서는 로그 판독기 에이전트 프로필에서 정의되는 매개 변수를 보여 줍니다. 표의 각 열은 명명된 프로필을 나타냅니다. 이러한 매개 변수에 대한 자세한 내용은 [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)를 참조하십시오.  
  
||기본|자세한 기록|  
|-|-------------|---------------------|  
|**-HistoryVerboseLevel**|1|2|  
|**-LoginTimeout**|15|15|  
|**-LogScanThreshold**|500000|500000|  
|**-PollingInterval**|5|5|  
|**-QueryTimeout**|1800|1800|  
|**-ReadBatchSize**|500|500|  
  
## <a name="distribution-agent-profiles"></a>배포 에이전트 프로필  
 다음 표에서는 배포 에이전트 프로필에서 정의되는 매개 변수를 보여 줍니다. 표의 각 열은 명명된 프로필을 나타냅니다. 이러한 매개 변수에 대한 자세한 내용은 [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)를 참조하십시오.  
  
||기본|자세한 기록|Windows 동기화 관리자|데이터 일관성 오류 발생 시 계속|OLEDB 스트리밍에 대한 배포 프로필|  
|-|-------------|---------------------|-------------------------------------|-----------------------------------------|----------------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|2147473647|  
|**-CommitBatchSize**|100|100|100|100|100|  
|**-CommitBatchThreshold**|1000|1000|1000|1000|1000|  
|**-HistoryVerboseLevel**|1|2|1|1|1|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|  
|**-MaxBcpThreads**|1|1|1|1|1|  
|**-MaxDeliveredTransactions**|0|0|0|0|0|  
|**-OledbStreamThreshold**|NULL|NULL|NULL|NULL|32768|  
|**-PacketSize**|NULL|NULL|NULL|NULL|32768|  
|**-PollingInterval**|5|5|5|5|5|  
|**-QueryTimeout**|1800|1800|1800|1800|1800|  
|**-SkipErrors**|NULL|NULL|NULL|**-SkipErrors** 2601:2627:20598|NULL|  
|**-TransactionsPerHistory**|100|100|100|100|100|  
|**-UseOledbStreaming**|NULL|NULL|NULL|NULL|**-UseOledbStreaming**|  
  
## <a name="merge-agent-profiles"></a>병합 에이전트 프로필  
 다음 표에서는 병합 에이전트 프로필에서 정의되는 매개 변수를 보여 줍니다. 표의 각 열은 명명된 프로필을 나타냅니다. 이러한 매개 변수에 대한 자세한 내용은 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)를 참조하십시오.  
  
||기본|자세한 기록|Windows 동기화 관리자|행 개수 유효성 검사|행 개수 및 체크섬의 유효성 검사|느린 연결|고용량 서버 간|  
|-|-------------|---------------------|-------------------------------------|-------------------------|--------------------------------------|---------------|------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|100000|100000|100000|  
|**-ChangesPerHistory**|100|50|50|100|100|100|1000|  
|**-DestThreads**|2|1|1|1|1|1|4|  
|**-DownloadGenerationsPerBatch**|50|50|50|50|50|1|500|  
|**-DownloadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-DownloadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-FastRowCount**|1|1|1|1|1|1|1|  
|**-HistoryVerboseLevel**|2|3|1|1|2|1|2|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|15|15|  
|**-MaxDownloadChanges**|0|0|0|0|0|0|0|  
|**-MaxUploadChanges**|0|0|0|0|0|0|0|  
|**-MetadataRetentionCleanup**|1|1|1|1|1|1|1|  
|**-NumDeadlockRetries**|5|5|5|5|5|5|5|  
|**-ParallelUploadDownload**|NULL|NULL|NULL|NULL|NULL|NULL|1|  
|**-PollingInterval**|60|60|60|60|60|60|60|  
|**-QueryTimeout**|300|300|300|300|300|300|600|  
|**-QueueSizeMultiplier**|NULL|NULL|NULL|NULL|NULL|NULL|5|  
|**-SrcThreads**|2|2|2|2|2|1|3|  
|**-StartQueueTimeout**|0|0|0|0|0|0|0|  
|**-UploadGenerationsPerBatch**|50|50|50|50|50|1|500|  
|**-UploadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-UploadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-Validate**|0|0|0|1|3|0|0|  
|**-ValidateInterval**|60|60|60|60|60|60|60|  
  
## <a name="queue-reader-agent-profiles"></a>큐 판독기 에이전트 프로필  
 다음 표에서는 큐 판독기 에이전트에 대한 기본 프로필에서 정의되는 매개 변수를 보여 줍니다. 이러한 매개 변수에 대한 자세한 내용은 [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)를 참조하십시오.  
  
||기본|  
|-|-------------|  
|**-HistoryVerboseLevel**|1|  
|**-LoginTimeout**|15|  
|**-PollingInterval**|5|  
|**-QueryTimeout**|1800|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 에이전트 관리](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [복제 에이전트의 명령 프롬프트 매개 변수 보기 및 수정&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)   
 [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  
