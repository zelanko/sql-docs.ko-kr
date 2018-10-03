---
title: 피어 투 피어 토폴로지 관리(복제 Transact-SQL 프로그래밍) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: a3a71b93887b604dcd258143fde9e78dffb09cd3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47851979"
---
# <a name="administer-a-peer-to-peer-topology-replication-transact-sql-programming"></a>피어 투 피어 토폴로지 관리(복제 Transact-SQL 프로그래밍)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  피어 투 피어 토폴로지를 관리하는 것은 일반적인 트랜잭션 복제 토폴로지를 관리하는 것과 비슷하지만 특별히 고려해야 하는 영역도 많이 있습니다. 피어 투 피어 토폴로지 관리에서 주요한 차이점은 몇 가지 변경 작업의 경우 시스템을 *정지*해야 한다는 점입니다. 시스템 정지 과정에서는 모든 노드에서 게시된 테이블에 대한 작업을 중지하고 각 노드가 다른 모든 노드의 변경 내용을 받았는지 확인합니다. 자세한 내용은 [복제 토폴로지 정지&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)를 참조하세요.  
  
> [!NOTE]  
>  피어 투 피어 토폴로지에서는 배포자가 끌어오기 구독자보다 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용할 수 없습니다.  
  
### <a name="to-add-an-article-to-an-existing-configuration"></a>기존 구성에 아티클을 추가하려면  
  
1.  시스템을 정지합니다.  
  
2.  토폴로지의 각 노드에서 배포 에이전트를 중지합니다. 자세한 내용은 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) 또는 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)를 참조하세요.  
  
3.  CREATE TABLE 문을 실행하여 토폴로지의 각 노드에 새 테이블을 추가합니다.  
  
4.  [bcp 유틸리티](../../../tools/bcp-utility.md)를 사용하여 새 테이블의 데이터를 모든 노드에 수동으로 대량 복사합니다.  
  
5.  [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)을 실행하여 토폴로지의 각 노드에 새 아티클을 만듭니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
    > [!NOTE]  
    >  [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)이 실행된 후에는 복제를 통해 토폴로지의 구독에 아티클이 자동으로 추가됩니다.  
  
6.  토폴로지의 각 노드에서 배포 에이전트를 다시 시작합니다.  
  
### <a name="to-make-schema-changes-to-a-publication-database"></a>게시 데이터베이스의 스키마를 변경하려면  
  
1.  시스템을 정지합니다.  
  
2.  DDL(데이터 정의 언어) 문을 실행하여 게시된 테이블의 스키마를 수정합니다. 지원되는 스키마 변경에 대한 자세한 내용은 [게시 데이터베이스의 스키마 변경](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
3.  게시된 테이블에 대한 작업을 다시 시작하기 전에 시스템을 다시 정지합니다. 이렇게 하면 새 데이터 변경 내용을 복제하기 전에 모든 노드에서 스키마 변경 내용을 받도록 할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 개의 노드가 있는 기존 피어 투 피어 복제 토폴로지에 새 테이블 아티클을 추가하는 방법을 보여 줍니다.  
  
 [!code-sql[HowTo#sp_addp2particle_createtables](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_1.sql)]  
  
 [!code-sql[HowTo#sp_addp2particle_cmdline](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_2.sql)]  
  
 [!code-sql[HowTo#sp_addp2particle_createarticle](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_3.sql)]  
  
## <a name="see-also"></a>참고 항목  
 [관리&#40;복제&#41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [SQL Server 데이터베이스 백업 및 복원](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [피어 투 피어 트랜잭션 복제](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
