---
title: 배포 데이터베이스에서 복제 된 명령 및 기타 정보 보기 (복제 Transact-sql 프로그래밍) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 86ced6fd281da2e47ddaa31cab7fa977767b98d6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74164958"
---
# <a name="view-replicated-commands-and-other-information-in-the-distribution-database-replication-transact-sql-programming"></a>배포 데이터베이스의 복제된 명령 및 기타 정보 보기(복제 Transact-SQL 프로그래밍)
  트랜잭션 복제를 사용하는 경우 트랜잭션 명령은 배포 에이전트에서 해당 명령을 모든 구독자에 전파하거나 구독자의 배포 에이전트에서 변경 내용을 끌어올 때까지 배포 데이터베이스에 저장됩니다. 이와 같이 배포 데이터베이스에서 보류 중인 명령은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 볼 수 있습니다. 자세한 내용은 [복제 저장 프로시저&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql)를 참조하세요.  
  
### <a name="to-view-replicated-commands-from-all-transactional-publications-in-the-distribution-database"></a>배포 데이터베이스의 모든 트랜잭션 게시에서 복제된 명령을 보려면  
  
1.  배포 데이터베이스의 배포자에서 [sp_browsereplcmds](/sql/relational-databases/system-stored-procedures/sp-browsemergesnapshotfolder-transact-sql)를 실행합니다.  
  
### <a name="to-view-replicated-commands-in-the-distribution-database-from-a-specific-article-or-from-a-specific-database-published-using-transactional-replication"></a>트랜잭션 복제를 사용하여 게시된 특정 데이터베이스 또는 특정 아티클에서 배포 데이터베이스의 복제된 명령을 보려면  
  
1.  (옵션) 게시 데이터베이스의 게시자에서 [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql)을 실행합니다. ** \@게시** 및 ** \@아티클을**지정 하십시오. 결과 집합의 **article id** 값을 확인합니다.  
  
2.  배포 데이터베이스의 배포자에서 [sp_browsereplcmds](/sql/relational-databases/system-stored-procedures/sp-browsemergesnapshotfolder-transact-sql)를 실행합니다. 필드 ** \@Article_id**에 대해 2 단계의 문서 ID를 지정 합니다. 필드 ** \@Publisher_database_id**에 대 한 게시 데이터베이스의 ID를 지정 합니다 .이 ID는 [sys.debug](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 카탈로그 뷰의 **database_id** 열에서 가져올 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 복제 모니터링](../monitoring-replication.md)  
  
  
