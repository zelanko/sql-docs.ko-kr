---
title: 트랜잭션 복제에 대해 통합 백업 사용 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- transactional replication, backup and restore
- sp_replicationdboption
- sync with backup [SQL Server replication]
- coordinated backups [SQL Server replication]
- backups [SQL Server replication], transactional replication
ms.assetid: 73a914ba-8b2d-4f4d-ac1b-db9bac676a30
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a436351752045c742d21892c304b0ecad7b8f591
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661252"
---
# <a name="enable-coordinated-backups-for-transactional-replication"></a>트랜잭션 복제에 대해 통합 백업 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  트랜잭션 복제에 데이터베이스를 사용할 경우 모든 트랜잭션을 배포 데이터베이스에 배달하기 전에 반드시 백업하도록 지정할 수 있습니다. 배포자에 전파된 트랜잭션이 백업될 때까지 게시 데이터베이스의 트랜잭션 로그가 잘리지 않도록 배포 데이터베이스에 통합 백업을 사용할 수도 있습니다. 자세한 내용은 [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)을 참조하세요.  
  
### <a name="to-enable-coordinated-backups-for-a-database-published-with-transactional-replication"></a>트랜잭션 복제를 사용하여 게시된 데이터베이스에 대해 통합 백업을 사용하도록 설정하려면  
  
1.  게시자에서 [DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) 함수를 사용하여 게시 데이터베이스의 **IsSyncWithBackup** 속성을 반환합니다. 해당 함수에서 **1**을 반환하면 게시된 데이터베이스에 대해 통합 백업이 이미 사용되고 있는 것입니다.  
  
2.  1단계의 해당 함수에서 **0**을 반환하면 게시 데이터베이스의 게시자에서 [sp_replicationdboption&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)을 실행합니다. **\@optname**에 **sync with backup** 값을 지정하고 **\@value**에 **true** 값을 지정합니다.  
  
    > [!NOTE]  
    >  **sync with backup** 옵션을 **false**로 변경하면 로그 판독기 에이전트가 실행된 후 또는 한 번의 간격이 지난 후(로그 판독기 에이전트가 계속 실행되는 경우) 게시 데이터베이스의 잘린 부분이 업데이트됩니다. 최대 간격은 **MessageInterval** 에이전트 매개 변수로 제어되며 기본값은 30초입니다.  
  
### <a name="to-enable-coordinated-backups-for-a-distribution-database"></a>배포 데이터베이스에 통합 백업을 사용하도록 설정하려면  
  
1.  배포자에서 [DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) 함수를 사용하여 배포 데이터베이스의 **IsSyncWithBackup** 속성을 반환합니다. 해당 함수에서 **1**을 반환하면 배포 데이터베이스에 대해 통합 백업이 이미 사용되고 있는 것입니다.  
  
2.  1단계의 해당 함수에서 **0**을 반환하면 배포 데이터베이스의 배포자에서 [sp_replicationdboption&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)을 실행합니다. **\@optname**에 **sync with backup** 값을 지정하고 **\@value**에 **true** 값을 지정합니다.  
  
### <a name="to-disable-coordinated-backups"></a>통합 백업을 사용하지 않도록 설정하려면  
  
1.  게시 데이터베이스의 게시자 또는 배포 데이터베이스의 배포자에서 [sp_replicationdboption&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)을 실행합니다. **\@optname**에 **sync with backup** 값을 지정하고 **\@value**에 **false** 값을 지정합니다.  
  
  
