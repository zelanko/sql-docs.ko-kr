---
title: "스냅숏 만들기 및 적용 | Microsoft 문서"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], applying
- snapshots [SQL Server replication], creating
ms.assetid: 631f48bf-50c9-4015-b9d8-8f1ad92d1ee2
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7fdc75559ffafea97e9ad3f4ef4b5e0788d7fb3d
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="create-and-apply-the-snapshot"></a>스냅숏 만들기 및 적용
  스냅숏은 복제가 생성된 후 스냅숏 에이전트에서 생성됩니다. 생성 방법은 다음과 같습니다.  
  
-   즉시. 기본적으로 병합 게시의 스냅숏은 새 게시 마법사에서 게시가 생성된 후 즉시 생성됩니다.  
  
-   예약된 시간. 새 게시 마법사의 **스냅숏 에이전트** 페이지에서 또는 저장 프로시저나 RMO(복제 관리 개체) 사용 시 일정을 지정합니다.  
  
-   수동. 명령 프롬프트 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 스냅숏 에이전트를 실행합니다. 에이전트 실행에 대한 자세한 내용은 [복제 에이전트 실행 파일 개념](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) 및 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)를 참조하세요.  
  
 병합 복제의 경우 스냅숏 에이전트가 실행될 때마다 스냅숏이 생성됩니다. 트랜잭션 복제의 경우 게시 속성 **immediate_sync**의 설정에 따라 스냅숏 생성이 달라집니다. 이 속성을 TRUE(새 게시 마법사 사용 시 기본 설정)로 설정하면 스냅숏 에이전트가 실행될 때마다 스냅숏이 생성되고 언제든지 스냅숏을 구독자에 적용할 수 있습니다. 이 속성을 FALSE( **sp_addpublication**사용 시 기본 설정)로 설정하면 스냅숏 에이전트가 마지막으로 실행된 후에 새 구독이 추가된 경우에만 스냅숏이 생성됩니다. 구독자는 동기화하기 위해 스냅숏 에이전트가 완료될 때까지 기다려야 합니다.  
  
 기본적으로 스냅숏이 생성되면 그 스냅숏은 배포자에 위치한 기본 스냅숏 폴더에 저장됩니다. 이동식 디스크나 CD-ROM과 같은 이동식 미디어 또는 기본 스냅숏 폴더 이외의 위치에 스냅숏 파일을 저장할 수도 있습니다. 또한 저장과 전송이 간단하도록 파일을 압축할 수 있고 스냅숏이 구독자에 적용되기 전 또는 적용된 후 스크립트를 실행할 수 있습니다. 이러한 옵션에 대한 자세한 내용은 [Snapshot Options](../../relational-databases/replication/snapshot-options.md)를 참조하세요.  
  
 스냅숏이 매개 변수가 있는 필터를 사용하는 병합 게시용인 경우 2단계 프로세스를 통해 스냅숏이 생성됩니다. 먼저 게시된 개체의 데이터를 제외하고 복제 스크립트와 스키마를 포함하는 스키마 스냅숏이 생성됩니다. 그런 후 스키마 스냅숏에서 복사된 스크립트 및 스키마를 포함하는 스냅숏과 구독의 파티션에 속해 있는 데이터를 사용하여 구독이 초기화됩니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)을(를) 참조하세요.  
  
 스냅숏이 게시자에 생성된 다음 기본 또는 대체 스냅숏 위치에 저장되면 스냅숏을 구독자로 전송하고 적용할 수 있습니다. 스냅숏이나 트랜잭션 복제에 대한 배포 에이전트 또는 병합 복제에 대한 병합 에이전트에서는 스냅숏을 전송하고 초기 동기화 중에 스키마 및 데이터 파일을 구독자의 구독 데이터베이스에 적용합니다. 새 구독 마법사를 사용할 경우 초기 동기화는 기본적으로 구독이 생성되는 즉시 발생합니다. 이 동작은 마법사의 **구독 초기화** 페이지에 있는 **초기화 시기** 옵션에서 제어할 수 있습니다. 구독을 초기화한 후 스냅숏이 생성되면 구독을 다시 초기화로 표시해야만 구독자에 적용됩니다. 자세한 내용은 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)를 참조하세요.  
  
 배포 에이전트 또는 병합 에이전트에서 초기 스냅숏을 적용한 후 에이전트에서는 후속 업데이트 및 다른 데이터의 수정 사항을 전파합니다. 스냅숏을 구독자로 배포 및 적용한 경우 초기 스냅숏 또는 새 스냅숏을 기다리는 구독자만 영향을 받습니다. 해당 게시에 대한 다른 구독자(게시된 데이터에 대한 삽입, 업데이트, 삭제, 기타 수정 사항을 이미 받은 구독자)는 영향을 받지 않습니다.  
  
 초기 스냅숏을 만들어서 적용하려면 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)를 참조하십시오.  
  
 기본 스냅숏 폴더 위치를 보거나 수정하려면 다음을 참조하십시오.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [기본 스냅숏 위치 지정&#40;SQL Server Management Studio&#41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)  
  
-   복제 프로그래밍 및 RMO 프로그래밍: [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
## <a name="see-also"></a>관련 항목:  
 [스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [스냅숏 폴더 보안 설정](../../relational-databases/replication/security/secure-the-snapshot-folder.md)   
 [sp_addpublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)  
  
  

