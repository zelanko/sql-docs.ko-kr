---
title: 백업 및 복원 전략(병합)
description: 병합 복제에 사용되는 데이터 백업 및 복원 전략
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], merge replication
- backups [SQL Server replication], merge replication
- restoring [SQL Server replication], merge replication
- merge replication [SQL Server replication], backup and restore
ms.assetid: b8ae31c6-d76f-4dd7-8f46-17d023ca3eca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 448688a54a245cadffa4c0c916d146e7c3e7e115
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75321990"
---
# <a name="strategies-for-backing-up-and-restoring-merge-replication"></a>병합 복제 백업 및 복원 전략
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  병합 복제의 경우 다음 데이터베이스를 정기적으로 백업합니다.  
  
-   게시자의 게시 데이터베이스  
  
-   배포자의 배포 데이터베이스  
  
-   구독자의 구독 데이터베이스  
  
-   게시자, 배포자 및 모든 구독자의 **master** 및 **msdb** 시스템 데이터베이스. 이러한 데이터베이스는 각각 그리고 관련 복제 데이터베이스와 동시에 백업되어야 합니다. 예를 들어 게시 데이터베이스를 백업할 때 게시자의 **master** 및 **msdb** 데이터베이스를 동시에 백업합니다. 게시 데이터베이스를 복원한 경우 **master** 및 **msdb** 데이터베이스의 복제 구성 및 설정이 게시 데이터베이스와 일치하는지 확인하십시오.  
  
 정기적인 로그 백업을 수행할 경우 모든 복제 관련 변경 내용은 로그 백업에 캡처됩니다. 로그 백업을 수행하지 않는 경우 복제와 관련된 설정이 변경될 때마다 백업을 수행해야 합니다. 자세한 내용은 [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md)을 참조하세요.  
  
 아래 자세히 설명된 게시 데이터베이스 백업 및 복원 접근 방법 중 하나를 선택한 다음 배포 데이터베이스 및 구독 데이터베이스에 대해 나열된 권장 사항을 따릅니다.  
  
## <a name="backing-up-and-restoring-the-publication-database"></a>게시 데이터베이스 백업 및 복원  
 병합 게시 데이터베이스를 복원하는 방법에는 두 가지가 있습니다. 백업에서 게시 데이터베이스를 복원한 다음에는 다음 작업 중 하나를 수행해야 합니다.  
  
-   게시 데이터베이스를 구독 데이터베이스와 동기화합니다.  
  
-   게시 데이터베이스에서 게시에 대한 모든 구독을 다시 초기화합니다.  
  
 이러한 방법 중 하나를 사용하면 복원을 수행한 후 게시자와 모든 구독자가 동기화됩니다.  
  
> [!NOTE]  
>  테이블에 ID 열이 포함되어 있는 경우 복원 후 올바른 ID 범위가 할당되도록 해야 합니다. 자세한 내용은 [ID 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)를 참조하세요.  
  
### <a name="synchronizing-the-publication-database"></a>게시 데이터베이스 동기화  
 게시 데이터베이스를 구독 데이터베이스와 동기화하면 복원된 백업에는 나타나지 않지만 게시 데이터베이스에서 이전에 적용한 변경 내용을 하나 이상의 구독 데이터베이스에서 업로드할 수 있습니다. 업로드할 수 있는 데이터는 게시가 필터링되는 방식에 따라 달라집니다.  
  
-   게시가 필터링되지 않은 경우 최신 구독자와 동기화하여 게시 데이터베이스를 최신 상태로 만들 수 있습니다.  
  
-   게시가 필터링된 경우 게시 데이터베이스를 최신 상태로 만들 수 없을 수도 있습니다. 각 구독이 동부, 서부, 남부 및 북부 중 한 지역에 대한 고객 데이터만 수신하도록 분할된 테이블을 고려해 봅시다. 각 데이터 파티션에 대해 최소 하나의 구독자가 있는 경우 각 파티션에 대해 구독자와 동기화하면 게시 데이터베이스가 최신 상태가 됩니다. 그러나 예를 들어 서부 파티션의 데이터가 구독자에 복제되지 않은 경우에는 게시자에서 이 데이터를 최신 상태로 만들 수 없습니다.  
  
> [!IMPORTANT]  
>  게시 데이터베이스를 구독 데이터베이스와 동기화하면 게시된 테이블이 백업에서 복원된 게시되지 않은 다른 테이블보다 더 최신 시점으로 복원될 수 있습니다.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]를 실행하는 구독자와 동기화하는 경우에는 구독이 익명일 수 없습니다. 구독은 클라이언트 구독 또는 서버 구독이어야 합니다(이전 릴리스에서는 로컬 구독과 전역 구독이라고 함).  
  
 밀어넣기 구독을 동기화하려면 [Synchronize a Push Subscription](../../../relational-databases/replication/synchronize-a-push-subscription.md) 및 [Synchronize a Pull Subscription](../../../relational-databases/replication/synchronize-a-pull-subscription.md)를 참조하십시오.  
  
### <a name="reinitializing-all-subscriptions"></a>모든 구독 다시 초기화  
 모든 구독을 다시 초기화하면 모든 구독자가 복원된 게시 데이터베이스와 일관된 상태로 변합니다. 이러한 접근 방법은 토폴로지 전체를 지정된 게시 데이터베이스 백업에 나타난 이전 상태로 되돌리려는 경우 사용합니다. 예를 들어 잘못 수행된 일괄 처리 작업을 복구하기 위한 메커니즘으로 게시 데이터베이스를 이전 시점으로 복원하는 경우 모든 구독을 다시 초기화할 수 있습니다.  
  
 이 방법을 선택하는 경우 게시 데이터베이스를 복원한 다음 다시 초기화된 구독자로 배달할 새 스냅샷을 즉시 만듭니다.  
  
 구독을 다시 초기화하려면 [Reinitialize a Subscription](../../../relational-databases/replication/reinitialize-a-subscription.md)를 참조하십시오.  
  
 스냅샷을 만들고 적용하려면 [Create 및 Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)및 [Create a Snapshot for a Merge Publication with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)를 참조하십시오.  
  
## <a name="backing-up-and-restoring-the-distribution-database"></a>배포 데이터베이스 백업 및 복원  
 병합 복제를 사용하는 경우에는 배포 데이터베이스를 정기적으로 백업해야 합니다. 사용하는 백업이 배포자를 사용하는 모든 게시의 최단 보존 기간을 넘기지 않은 한 특별 고려 사항 없이 배포 데이터베이스를 복원할 수 있습니다. 예를 들어 보존 기간이 10일, 20일, 30일인 3개의 게시가 있는 경우 데이터베이스 복원에 사용되는 백업은 10일보다 더 오래된 것이면 안 됩니다. 배포 데이터베이스는 병합 복제에서 제한된 역할을 가집니다. 즉, 변경 추적에 사용된 데이터를 저장하지 않으며 구독 데이터베이스로 전달될 병합 복제 변경 내용에 대해 트랜잭션 복제에서와 같이 임시 스토리지를 제공하지 않습니다.  
  
## <a name="backing-up-and-restoring-a-subscription-database"></a>구독 데이터베이스 백업 및 복원  
 구독 데이터베이스를 성공적으로 복구하려면 구독 데이터베이스를 백업하기 전에 구독자를 게시자와 동기화해야 하며 구독 데이터베이스가 복원된 후에도 구독자와 게시자를 동기화해야 합니다.  
  
-   구독 데이터베이스를 백업하기 전에 게시자와 동기화하면 백업에서 구독자를 복원할 때 구독이 여전히 게시 보존 기간 내에 있게 됩니다. 예를 들어 보존 기간이 10일인 게시를 가정해 봅시다. 8일 전에 마지막 동기화를 수행했으며 지금 백업을 수행했습니다. 백업을 4일 후에 복원하면 마지막 동기화는 보존 기간을 지난 12일 전에 발생한 셈이 됩니다. 이 경우 구독자를 다시 초기화해야 합니다. 백업 전에 구독자를 동기화한 경우 구독 데이터베이스는 보존 기간을 초과하지 않게 됩니다.  
  
     백업은 구독자가 구독하는 모든 게시의 최단 보존 기간을 넘기지 않아야 합니다. 예를 들어 구독자가 각각 보존 기간이 10일, 20일, 30일인 3개의 게시를 구독하는 경우 데이터베이스 복원에 사용되는 백업은 10일보다 더 오래된 것이면 안 됩니다.  
  
-   복원 후 구독 데이터베이스를 각 해당 게시와 동기화하면 게시자의 모든 변경 내용이 구독자에 적용되어 최신 상태가 됩니다.  
  
 게시 보존 기간을 설정하려면 [구독에 대한 만료 기간 설정](../../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)을 참조하세요.  
  
 밀어넣기 구독을 동기화하려면 [Synchronize a Push Subscription](../../../relational-databases/replication/synchronize-a-push-subscription.md) 및 [Synchronize a Pull Subscription](../../../relational-databases/replication/synchronize-a-pull-subscription.md)를 참조하십시오.  
  
## <a name="backing-up-and-restoring-a-republishing-database"></a>재게시 데이터베이스 백업 및 복원  
 데이터베이스가 게시자에서 데이터를 구독한 다음 같은 데이터를 다른 구독 데이터베이스로 게시하면 이 데이터베이스는 재게시 데이터베이스가 됩니다. 재게시 데이터베이스를 복원하는 경우 이 항목의 "게시 데이터베이스 백업 및 복원"과 "구독 데이터베이스 백업 및 복원"에 설명된 지침을 따르십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 데이터베이스 백업 및 복원](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [복제된 데이터베이스 백업 및 복원](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)  
  
  
