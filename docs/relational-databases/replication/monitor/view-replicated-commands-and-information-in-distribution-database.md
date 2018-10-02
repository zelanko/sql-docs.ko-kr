---
title: 배포 데이터베이스에서 복제된 명령 및 정보 보기 | Microsoft 문서
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_browsereplcmds
- transactional replication, monitoring
- distribution databases [SQL Server replication], viewing replicated commands
- viewing replicated commands
ms.assetid: 9c20acec-8fab-4483-b9c1-dfe3768f85dd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d332096aee2c38f2cd16c4fa90296ef80b2b15e0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47701151"
---
# <a name="view-replicated-commands-and-information-in-distribution-database"></a>배포 데이터베이스에서 복제된 명령 및 정보 보기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  트랜잭션 복제를 사용하는 경우 트랜잭션 명령은 배포 에이전트에서 해당 명령을 모든 구독자에 전파하거나 구독자의 배포 에이전트에서 변경 내용을 끌어올 때까지 배포 데이터베이스에 저장됩니다. 이와 같이 배포 데이터베이스에서 보류 중인 명령은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 볼 수 있습니다. 자세한 내용은 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)를 참조하세요.  
  
### <a name="to-view-replicated-commands-from-all-transactional-publications-in-the-distribution-database"></a>배포 데이터베이스의 모든 트랜잭션 게시에서 복제된 명령을 보려면  
  
1.  배포 데이터베이스의 배포자에서 [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md)를 실행합니다.  
  
### <a name="to-view-replicated-commands-in-the-distribution-database-from-a-specific-article-or-from-a-specific-database-published-using-transactional-replication"></a>트랜잭션 복제를 사용하여 게시된 특정 데이터베이스 또는 특정 아티클에서 배포 데이터베이스의 복제된 명령을 보려면  
  
1.  (옵션) 게시 데이터베이스의 게시자에서 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)을 실행합니다. **@publication** 및 **@article**을 지정합니다. 결과 집합의 **article id** 값을 확인합니다.  
  
2.  배포 데이터베이스의 배포자에서 [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md)를 실행합니다. (옵션) **@article_id**을 참조하세요. (옵션) **@publisher_database_id**에 게시 데이터베이스의 ID를 지정합니다. 이 ID는 **sys.databases** 카탈로그 뷰의 [database_id](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 열에서 얻을 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 복제 모니터링](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
