---
title: 피어 투 피어 토폴로지 관리(복제 Transact-SQL 프로그래밍) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- transactional replication, peer-to-peer replication
ms.assetid: 4d0fa941-f9ea-4a14-aed9-34df593fc6f2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0cabfb4cd21de54dad2be1323fd29d8bb3bf076
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62629716"
---
# <a name="administer-a-peer-to-peer-topology-replication-transact-sql-programming"></a>피어 투 피어 토폴로지 관리(복제 Transact-SQL 프로그래밍)
  피어 투 피어 토폴로지를 관리하는 것은 일반적인 트랜잭션 복제 토폴로지를 관리하는 것과 비슷하지만 특별히 고려해야 하는 영역도 많이 있습니다. 피어 투 피어 토폴로지 관리에서 주요한 차이점은 몇 가지 변경 작업의 경우 시스템을 *정지*해야 한다는 점입니다. 시스템 정지 과정에서는 모든 노드에서 게시된 테이블에 대한 작업을 중지하고 각 노드가 다른 모든 노드의 변경 내용을 받았는지 확인합니다. 자세한 내용은 [복제 토폴로지 정지&#40;복제 Transact-SQL 프로그래밍&#41;](quiesce-a-replication-topology-replication-transact-sql-programming.md)를 참조하세요.  
  
> [!NOTE]  
>  피어 투 피어 토폴로지에서는 배포자가 끌어오기 구독자보다 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용할 수 없습니다.  
  
### <a name="to-add-an-article-to-an-existing-configuration"></a>기존 구성에 아티클을 추가하려면  
  
1.  시스템을 정지합니다.  
  
2.  토폴로지의 각 노드에서 배포 에이전트를 중지합니다. 자세한 내용은 [복제 에이전트 실행 파일 개념](../concepts/replication-agent-executables-concepts.md) 또는 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)를 참조하세요.  
  
3.  CREATE TABLE 문을 실행하여 토폴로지의 각 노드에 새 테이블을 추가합니다.  
  
4.  [bcp 유틸리티](../../../tools/bcp-utility.md)를 사용하여 새 테이블의 데이터를 모든 노드에 수동으로 대량 복사합니다.  
  
5.  [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)을 실행하여 토폴로지의 각 노드에 새 아티클을 만듭니다. 자세한 내용은 [아티클을 정의](../publish/define-an-article.md)을 참조하세요.  
  
    > [!NOTE]  
    >  [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)이 실행된 후에는 복제를 통해 토폴로지의 구독에 아티클이 자동으로 추가됩니다.  
  
6.  토폴로지의 각 노드에서 배포 에이전트를 다시 시작합니다.  
  
### <a name="to-make-schema-changes-to-a-publication-database"></a>게시 데이터베이스의 스키마를 변경하려면  
  
1.  시스템을 정지합니다.  
  
2.  DDL(데이터 정의 언어) 문을 실행하여 게시된 테이블의 스키마를 수정합니다. 지원되는 스키마 변경에 대한 자세한 내용은 [게시 데이터베이스의 스키마 변경](../publish/make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
3.  게시된 테이블에 대한 작업을 다시 시작하기 전에 시스템을 다시 정지합니다. 이렇게 하면 새 데이터 변경 내용을 복제하기 전에 모든 노드에서 스키마 변경 내용을 받도록 할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 개의 노드가 있는 기존 피어 투 피어 복제 토폴로지에 새 테이블 아티클을 추가하는 방법을 보여 줍니다.  
  
 [!code-sql[HowTo#sp_addp2particle_createtables](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_createtables)]  
  
 [!code-sql[HowTo#sp_addp2particle_cmdline](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_cmdline)]  
  
 [!code-sql[HowTo#sp_addp2particle_createarticle](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_createarticle)]  
  
## <a name="see-also"></a>관련 항목  
 [복제 관리 FAQ](frequently-asked-questions-for-replication-administrators.md)   
 [SQL Server 데이터베이스 백업 및 복원](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [피어 투 피어 트랜잭션 복제](../transactional/peer-to-peer-transactional-replication.md)  
  
  
