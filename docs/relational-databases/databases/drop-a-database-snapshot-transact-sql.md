---
title: "데이터베이스 스냅숏 삭제(Transact-SQL) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing database snapshots
- deleting database snapshots
- database snapshots [SQL Server], deleting
ms.assetid: ad70ec97-d5fb-41aa-b72a-915e74b61b76
caps.latest.revision: "36"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 941d0f44ca37d0b2e9b7df202b9650cf172dd352
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="drop-a-database-snapshot-transact-sql"></a>데이터베이스 스냅숏 삭제(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 데이터베이스 스냅숏을 삭제하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스 스냅숏이 삭제되고 스냅숏에 사용된 스파스 파일도 삭제됩니다. 또한 데이터베이스 스냅숏에 대한 모든 사용자 연결이 종료됩니다.  
  
## <a name="security"></a>보안  
  
###  <a name="Permissions"></a> Permissions  
 DROP DATABASE 권한을 가진 사용자는 누구든지 데이터베이스 스냅숏을 삭제할 수 있습니다.  
  
##  <a name="TsqlProcedure"></a> 데이터베이스 스냅숏을 삭제하는 방법(Transact-SQL 사용)  
 **데이터베이스 스냅숏을 삭제하려면**  
  
1.  삭제할 데이터베이스 스냅숏을 확인합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 데이터베이스의 스냅숏을 확인할 수 있습니다. 자세한 내용은 [데이터베이스 스냅숏 보기&#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)에서 데이터베이스의 스냅숏을 확인할 수 있습니다.  
  
2.  삭제할 데이터베이스 스냅숏의 이름을 지정하여 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md) 문을 실행합니다. 구문은 다음과 같습니다.  
  
     DROP DATABASE *database_snapshot_name* [ **,**...*n* ]  
  
     여기서 *database_snapshot_name* 은 삭제할 데이터베이스 스냅숏의 이름입니다.  
  
####  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예에서는 원본 데이터베이스에 영향을 주지 않고 SalesSnapshot0600이라는 데이터베이스 스냅숏을 삭제합니다.  
  
```  
DROP DATABASE SalesSnapshot0600 ;  
```  
  
 SalesSnapshot0600에 대한 사용자 연결이 모두 종료되고 스냅숏에 사용되는 NTFS 파일 시스템 스파스 파일이 모두 삭제됩니다.  
  
> [!NOTE]  
>  데이터베이스 스냅숏이 사용하는 스파스 파일에 대한 자세한 내용은 [데이터베이스 스냅숏&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)에서 데이터베이스의 스냅숏을 확인할 수 있습니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [데이터베이스 스냅숏 만들기&#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [데이터베이스 스냅숏 보기&#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [데이터베이스를 데이터베이스 스냅숏으로 되돌리기](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)  
  
  
## <a name="see-also"></a>참고 항목  
 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [데이터베이스 스냅숏&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
