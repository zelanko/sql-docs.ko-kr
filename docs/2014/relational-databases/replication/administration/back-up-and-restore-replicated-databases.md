---
title: 복제된 데이터베이스 백업 및 복원 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- backups [SQL Server replication]
- administering replication, restoring
- backing up replicated databases
- backups [SQL Server replication], about backups
- restoring replicated databases [SQL Server replication]
- recovery [SQL Server replication], about recovery
- restoring databases [SQL Server], replicated databases
- backing up databases [SQL Server], replicated databases
- restoring [SQL Server replication], about restoring
- recovery [SQL Server replication]
- replication [SQL Server], administering
- distribution databases [SQL Server replication], backing up
- restoring [SQL Server replication]
- administering replication, backing up
ms.assetid: 04588807-21e7-4bbe-9727-b72f692cffa7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: af4229037b9c34bbc9a0316ef073f294209be6d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62629644"
---
# <a name="back-up-and-restore-replicated-databases"></a>복제된 데이터베이스 백업 및 복원
  복제된 데이터베이스의 경우 데이터를 백업 및 복원할 때 특별히 주의를 기울여야 합니다. 이 항목에서는 각 복제 유형의 백업 및 복원 전략에 대한 기초 정보와 추가 정보 링크를 제공합니다.  
  
 복제에서는 복제된 데이터베이스를 백업이 생성된 서버 및 데이터베이스로 복원할 수 있습니다. 복제된 데이터베이스의 백업을 다른 서버 또는 데이터베이스로 복원할 경우 복제 설정은 유지되지 않습니다. 이 경우 백업 복원 후 모든 게시 및 구독을 다시 만들어야 합니다.  
  
> [!NOTE]  
>  로그 전달을 사용하는 경우 복제된 데이터베이스를 대기 서버로 복원할 수 있습니다. 자세한 내용은 [로그 전달 및 복제&#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md)를 참조하세요.  
  
 복제된 데이터베이스와 관련 시스템 데이터베이스를 정기적으로 백업해야 합니다. 다음 데이터베이스를 백업합니다.  
  
-   게시자의 게시 데이터베이스  
  
-   배포자의 배포 데이터베이스  
  
-   구독자의 구독 데이터베이스  
  
-   게시자, 배포자 및 모든 구독자의 **master** 및 **msdb** 시스템 데이터베이스. 이러한 데이터베이스는 각각 그리고 관련 복제 데이터베이스와 동시에 백업되어야 합니다. 예를 들어 게시 데이터베이스를 백업할 때 게시자의 **master** 및 **msdb** 데이터베이스를 동시에 백업합니다. 게시 데이터베이스를 복원한 경우 **master** 및 **msdb** 데이터베이스의 복제 구성 및 설정이 게시 데이터베이스와 일치하는지 확인하십시오.  
  
 정기적인 로그 백업을 수행할 경우 모든 복제 관련 변경 내용은 로그 백업에 캡처됩니다. 로그 백업을 수행하지 않는 경우 복제와 관련된 설정이 변경될 때마다 백업을 수행해야 합니다. 자세한 내용은 [Common Actions Requiring an Updated Backup](common-actions-requiring-an-updated-backup.md)을(를) 참조하세요.  
  
## <a name="backup-and-restore-strategies"></a>백업 및 복원 전략  
 복제 토폴로지의 각 노드를 백업하고 복원하는 전략은 사용하는 복제 유형에 따라 달라집니다. 각 복제 유형의 백업 및 복원 전략에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [스냅숏 및 트랜잭션 복제의 백업 및 복원을 위한 전략](strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)  
  
-   [병합 복제 백업 및 복원 전략](strategies-for-backing-up-and-restoring-merge-replication.md)  
  
 어떤 복구 전략을 사용하는지에 관계없이 항상 현재 복제 설정 스크립트를 안전한 위치에 보관해야 합니다. 서버에 오류가 발생하거나 테스트 환경을 설정해야 할 때는 서버 이름 참조를 변경하여 스크립트를 수정하고 이를 사용하여 복제 설정을 다시 만들 수 있습니다. 현재 복제 설정을 스크립팅할 뿐만 아니라 복제의 활성화 및 비활성화도 스크립팅해야 합니다. 복제 개체 스크립팅에 대한 자세한 내용은 [Scripting Replication](../scripting-replication.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 데이터베이스 백업 및 복원](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Best Practices for Replication Administration](best-practices-for-replication-administration.md)  
  
  
