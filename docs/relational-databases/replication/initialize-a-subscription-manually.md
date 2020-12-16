---
description: 수동 구독 초기화
title: 수동 구독 초기화 | Microsoft 문서
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
ms.assetid: 27a1bc38-e498-4fff-8082-04b52aa4b22c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 4f782c5b58c2110eb2181b4ede639a62f9544b39
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479934"
---
# <a name="initialize-a-subscription-manually"></a>수동 구독 초기화
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 수동으로 구독을 초기화하는 방법에 대해 설명합니다. 구독을 초기화하는 데는 일반적으로 초기 스냅샷이 사용되지만 스키마 및 초기 데이터가 이미 구독자에 있는 경우에는 스냅샷을 사용하지 않고 게시에 대한 구독을 초기화할 수 있습니다.  
  

##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   데이터와 스키마가 구독자로 복사된 시점과 구독이 수동으로 초기화된 시점 간에 트랜잭션 복제를 사용하여 게시된 데이터베이스에서 작업이 수행된 경우에는 이러한 작업으로 인한 변경 내용은 구독자로 복제되지 않을 수 있습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 스키마를 구독 데이터베이스에 복사(일반적으로 데이터도 복사)하여 게시에 대한 구독을 초기화합니다. 해당 스키마와 데이터는 게시 데이터베이스와 일치해야 합니다. 그런 다음 새 구독 마법사의 **구독 초기화** 페이지에서 구독에 스키마와 데이터가 필요하지 않도록 지정합니다. 이 마법사의 액세스 방법은 [스냅샷 없이 트랜잭션 구독 초기화](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) 및 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)에서 수동으로 구독을 초기화하는 방법에 대해 설명합니다.  
  
 처음 구독을 동기화하는 경우 복제에 필요한 개체와 메타데이터가 구독 데이터베이스에 복사됩니다.  
  
#### <a name="to-initialize-a-subscription-to-a-publication-manually"></a>수동으로 게시에 대한 구독을 초기화하려면  
  
1.  스키마와 데이터가 구독 데이터베이스에 복사되었는지 확인합니다.  
  
2.  새 구독 마법사의 **구독 초기화** 페이지에 있는 **초기화** 확인란의 선택을 취소합니다. 복제 개체와 메타데이터만 복사해야 하는 각 구독에 대해서 이 작업을 수행합니다.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 수동으로 게시를 초기화할 수 있습니다.  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-transactional-publication"></a>트랜잭션 게시에 대한 끌어오기 구독을 수동으로 초기화하려면  
  
1.  스키마와 데이터가 구독 데이터베이스에 존재하는지 확인합니다. 자세한 내용은 [스냅샷 없이 트랜잭션 구독 초기화](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)에서 수동으로 구독을 초기화하는 방법에 대해 설명합니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)을 실행합니다. **\@publication**, **\@subscriber**, **\@destination_db** 의 게시된 데이터를 포함하는 구독자 측의 데이터베이스 이름, **\@subscription_type** 에 대해 **pull** 값, **\@sync_type** 에 대해 **replication support only** 를 지정합니다. 자세한 내용은 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)를 참조하세요.  
  
3.  구독자에서 [sp_addpullsubscription](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)을 실행합니다. 구독 업데이트에 대한 내용은 [Create an Updatable Subscription to a Transactional Publication](./publish/create-an-updatable-subscription-to-a-transactional-publication.md)를 참조하세요.  
  
4.  구독자에서 [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)를 실행합니다. 자세한 내용은 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)를 참조하세요.  
  
5.  배포 에이전트를 시작하여 복제 개체를 전송하고 게시자에서 최신 변경 내용을 다운로드합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)을 참조하세요.  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-transactional-publication"></a>트랜잭션 게시에 대한 밀어넣기 구독을 수동으로 초기화하려면  
  
1.  스키마와 데이터가 구독 데이터베이스에 존재하는지 확인합니다. 자세한 내용은 [스냅샷 없이 트랜잭션 구독 초기화](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)에서 수동으로 구독을 초기화하는 방법에 대해 설명합니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)을 실행합니다. **\@destination_db** 에 게시된 데이터를 포함하고 있는 구독자의 데이터베이스 이름, **\@subscription_type** 에 대해 **push** 값, **\@sync_type** 에 대해 **replication support only** 값을 지정합니다. 구독 업데이트에 대한 내용은 [Create an Updatable Subscription to a Transactional Publication](./publish/create-an-updatable-subscription-to-a-transactional-publication.md)를 참조하세요.  
  
3.  게시 데이터베이스의 게시자에서 [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)를 실행합니다. 자세한 내용은 [밀어넣기 구독 만들기](../../relational-databases/replication/create-a-push-subscription.md)을 참조하세요.  
  
4.  배포 에이전트를 시작하여 복제 개체를 전송하고 게시자에서 최신 변경 내용을 다운로드합니다. 자세한 내용은 [밀어넣기 구독 동기화](../../relational-databases/replication/synchronize-a-push-subscription.md)을 참조하세요.  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 대한 끌어오기 구독을 수동으로 초기화하려면  
  
1.  스키마와 데이터가 구독 데이터베이스에 존재하는지 확인합니다. 이 작업은 구독자에서 게시 데이터베이스의 백업을 복원하여 수행할 수 있습니다.  
  
2.  게시자에서 [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)을 실행합니다. **\@publication**, **\@subscriber**, **\@subscriber_db** 와 **\@subscription_type** 에 대해 **pull** 값을 지정합니다. 끌어오기 구독이 등록됩니다.  
  
3.  게시된 데이터가 포함된 데이터베이스의 게시자에서 [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)을 실행합니다. **\@sync_type** 에 **none** 값을 지정합니다.  
  
4.  구독자에서 [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)를 실행합니다. 자세한 내용은 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)를 참조하세요.  
  
5.  병합 에이전트를 시작하여 복제 개체를 전송하고 게시자에서 최신 변경 내용을 다운로드합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)을 참조하세요.  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-merge-publication"></a>병합 게시에 대한 밀어넣기 구독을 수동으로 초기화하려면  
  
1.  스키마와 데이터가 구독 데이터베이스에 존재하는지 확인합니다. 이 작업은 구독자에서 게시 데이터베이스의 백업을 복원하여 수행할 수 있습니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)을 실행합니다. **\@subscriber_db** 에 게시된 데이터를 포함하는 구독자 측의 데이터베이스 이름, **\@subscription_type** 에 대해 **push** 값, **\@sync_type** 에 대해 **none** 값을 지정합니다.  
  
3.  게시 데이터베이스의 게시자에서 [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)를 실행합니다. 자세한 내용은 [밀어넣기 구독 만들기](../../relational-databases/replication/create-a-push-subscription.md)을 참조하세요.  
  
4.  병합 에이전트를 시작하여 복제 개체를 전송하고 게시자에서 최신 변경 내용을 다운로드합니다. 자세한 내용은 [밀어넣기 구독 동기화](../../relational-databases/replication/synchronize-a-push-subscription.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [스냅샷 없이 트랜잭션 구독 초기화](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)   
 [복제된 데이터베이스 백업 및 복원](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
