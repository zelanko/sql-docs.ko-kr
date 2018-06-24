---
title: 데이터베이스 스냅숏 삭제(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- removing database snapshots
- deleting database snapshots
- database snapshots [SQL Server], deleting
ms.assetid: ad70ec97-d5fb-41aa-b72a-915e74b61b76
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3bf95fcb0280c401c4777efe543766fad47de24f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080437"
---
# <a name="drop-a-database-snapshot-transact-sql"></a>데이터베이스 스냅숏 삭제(Transact-SQL)
  데이터베이스 스냅숏을 삭제하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터베이스 스냅숏이 삭제되고 스냅숏에 사용된 스파스 파일도 삭제됩니다. 또한 데이터베이스 스냅숏에 대한 모든 사용자 연결이 종료됩니다.  
  
## <a name="security"></a>보안  
  
###  <a name="Permissions"></a> Permissions  
 DROP DATABASE 권한을 가진 사용자는 누구든지 데이터베이스 스냅숏을 삭제할 수 있습니다.  
  
##  <a name="TsqlProcedure"></a> 데이터베이스 스냅숏을 삭제하는 방법(Transact-SQL 사용)  
 **데이터베이스 스냅숏을 삭제하려면**  
  
1.  삭제할 데이터베이스 스냅숏을 확인합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 데이터베이스의 스냅숏을 확인할 수 있습니다. 자세한 내용은 [데이터베이스 스냅숏 보기&#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)에서 데이터베이스의 스냅숏을 확인할 수 있습니다.  
  
2.  삭제할 데이터베이스 스냅숏의 이름을 지정하여 [DROP DATABASE](/sql/t-sql/statements/drop-database-audit-specification-transact-sql) 문을 실행합니다. 구문은 다음과 같습니다.  
  
     DROP DATABASE *database_snapshot_name* [ **,**...*n* ]  
  
     여기서 *database_snapshot_name* 은 삭제할 데이터베이스 스냅숏의 이름입니다.  
  
####  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예에서는 원본 데이터베이스에 영향을 주지 않고 SalesSnapshot0600이라는 데이터베이스 스냅숏을 삭제합니다.  
  
```  
DROP DATABASE SalesSnapshot0600 ;  
```  
  
 SalesSnapshot0600에 대한 사용자 연결이 모두 종료되고 스냅숏에 사용되는 NTFS 파일 시스템 스파스 파일이 모두 삭제됩니다.  
  
> [!NOTE]  
>  데이터베이스 스냅숏이 사용하는 스파스 파일에 대한 자세한 내용은 [데이터베이스 스냅숏&#40;SQL Server&#41;](database-snapshots-sql-server.md)에서 데이터베이스의 스냅숏을 확인할 수 있습니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [데이터베이스 스냅숏 만들기&#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md)  
  
-   [데이터베이스 스냅숏 보기&#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)  
  
-   [데이터베이스를 데이터베이스 스냅숏으로 되돌리기](revert-a-database-to-a-database-snapshot.md)  
  

  
## <a name="see-also"></a>관련 항목  
 [DROP DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-audit-specification-transact-sql)   
 [데이터베이스 스냅숏&#40;SQL Server&#41;](database-snapshots-sql-server.md)  
  
  
