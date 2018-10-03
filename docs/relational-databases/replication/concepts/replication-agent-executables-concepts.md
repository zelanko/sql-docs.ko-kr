---
title: 복제 에이전트 실행 파일 개념 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- programming interfaces [SQL Server replication]
- programming [SQL Server replication], agents
- replication [SQL Server], agents and profiles
- agents [SQL Server replication], executables
- command prompt [SQL Server replication]
ms.assetid: cba476df-d4ea-44c9-bb86-81488971e328
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ead289095f53693a7e6a487fa2a07a7c94df6219
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47791821"
---
# <a name="replication-agent-executables-concepts"></a>복제 에이전트 실행 파일 개념
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  다음과 같은 방법으로 복제 에이전트를 프로그래밍 방식으로 제어할 수 있습니다.  
  
-   <xref:Microsoft.SqlServer.Replication> 네임스페이스의 관리되는 에이전트 프로그래밍 인터페이스를 사용합니다.  
  
-   제공된 매개 변수 집합을 사용하여 명령 프롬프트에서 에이전트 실행 파일을 호출합니다.  
  
 명령 프롬프트에서 복제 에이전트를 직접 호출하면 배치 파일의 명령줄 스크립팅을 통해 에이전트에 프로그래밍 방식으로 액세스할 수 있습니다. 명령 프롬프트에서 호출된 에이전트는 에이전트를 호출하거나 배치 파일을 시작한 사용자의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 보안 계정으로 실행됩니다.  
  
 실행 파일을 사용하면 다음과 같은 복제 에이전트 인스턴스를 실행할 수 있습니다.  
  
-   [복제 배포 에이전트](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [복제 로그 판독기 에이전트](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
-   [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
 복제 에이전트를 호출할 때 성능 프로필을 사용하여 에이전트 실행 파일에 정의된 매개 변수 집합을 자동으로 전달할 수 있습니다. 자세한 내용은 [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 명령 프롬프트에서 복제 에이전트를 호출하는 방법을 보여 줍니다. RMO(복제 관리 개체)를 사용하여 복제 에이전트를 호출할 수도 있습니다. 자세한 내용은 [구독 동기화&#40;복제&#41;](../../../relational-databases/replication/synchronize-subscriptions-replication.md)를 참조하세요.  
  
> [!NOTE]  
>  이 예에서는 가독성을 높이기 위해 줄 바꿈이 추가되었지만 배치 파일에서 명령은 단일 행으로 작성해야 합니다.  
  
### <a name="running-the-snapshot-agent"></a>스냅숏 에이전트 실행  
 이 예제 배치 파일은 명령 프롬프트에서 스냅숏 에이전트를 호출하여 **AdvWorksSalesOrdersMerge** 게시에 대한 스냅숏을 생성합니다. (아래의 스크립트는 [!INCLUDE[ssSQL15_md](../../../includes/sssql15-md.md)] 파일(버전 130) 경로를 사용합니다. [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 버전의 파일을 가리키도록 스크립트를 조정해야 합니다.)  
  
```  
REM -- Declare variables  
SET Publisher=%InstanceName%;  
SET PublicationDB=AdventureWorks2012;   
SET Publication=AdvWorksSalesOrdersMerge;   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\130\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1 ;  
  
```  
  
### <a name="running-the-distribution-agent"></a>배포 에이전트 실행  
 이 예제 배치 파일은 명령 프롬프트에서 배포 에이전트를 호출하여 **AdvWorksProductTran** 게시의 변경 내용을 밀어넣기 구독자에게 계속 복제합니다.  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksProductsTran;  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4 ;  
  
```  
  
### <a name="running-the-merge-agent"></a>병합 에이전트 실행  
 이 예제 배치 파일은 명령 프롬프트에서 병합 에이전트를 호출하여 끌어오기 구독을 **AdvWorksSalesOrdersMerge** 게시에 동기화합니다.  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksSalesOrdersMerge;  
  
REM --Start the Merge Agent with concurrent upload and download processes.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\REPLMERG.EXE" -Publication %Publication%    
-Publisher %Publisher%  -Subscriber  %Subscriber%  -Distributor %Publisher%    
-PublisherDB %PublicationDB%  -SubscriberDB %SubscriptionDB% -PublisherSecurityMode 1    
-OutputVerboseLevel 2  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1    
-Validate 3  -ParallelUploadDownload 1 ;  
  
```  
  
  
