---
title: 데이터베이스 스냅샷 삭제(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- removing database snapshots
- deleting database snapshots
- database snapshots [SQL Server], deleting
ms.assetid: ad70ec97-d5fb-41aa-b72a-915e74b61b76
author: stevestein
ms.author: sstein
ms.openlocfilehash: e0d9d912a092e581fad7d3d53504309f63ba1806
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970023"
---
# <a name="drop-a-database-snapshot-transact-sql"></a>데이터베이스 스냅샷 삭제(Transact-SQL)
  데이터베이스 스냅샷을 삭제하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터베이스 스냅샷이 삭제되고 스냅샷에 사용된 스파스 파일도 삭제됩니다. 또한 데이터베이스 스냅샷에 대한 모든 사용자 연결이 종료됩니다.  
  
## <a name="security"></a>보안  
  
###  <a name="permissions"></a><a name="Permissions"></a> 권한  
 DROP DATABASE 권한을 가진 사용자는 누구든지 데이터베이스 스냅샷을 삭제할 수 있습니다.  
  
##  <a name="how-to-drop-a-database-snapshot-using-transact-sql"></a><a name="TsqlProcedure"></a> 데이터베이스 스냅샷을 삭제하는 방법(Transact-SQL 사용)  
 **데이터베이스 스냅샷을 삭제하려면**  
  
1.  삭제할 데이터베이스 스냅샷을 확인합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 데이터베이스의 스냅샷을 확인할 수 있습니다. 자세한 내용은 [View a Database Snapshot &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md).  
  
2.  삭제할 데이터베이스 스냅샷의 이름을 지정하여 [DROP DATABASE](/sql/t-sql/statements/drop-database-audit-specification-transact-sql) 문을 실행합니다. 구문은 다음과 같습니다.  
  
     DROP DATABASE *database_snapshot_name* [ **,** ...*n* ]  
  
     여기서 *database_snapshot_name* 은 삭제할 데이터베이스 스냅샷의 이름입니다.  
  
####  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예에서는 원본 데이터베이스에 영향을 주지 않고 SalesSnapshot0600이라는 데이터베이스 스냅샷을 삭제합니다.  
  
```  
DROP DATABASE SalesSnapshot0600 ;  
```  
  
 SalesSnapshot0600에 대한 사용자 연결이 모두 종료되고 스냅샷에 사용되는 NTFS 파일 시스템 스파스 파일이 모두 삭제됩니다.  
  
> [!NOTE]  
>  데이터베이스 스냅샷이 사용하는 스파스 파일에 대한 자세한 내용은 [데이터베이스 스냅샷&#40;SQL Server&#41;](database-snapshots-sql-server.md)에서 데이터베이스의 스냅샷을 확인할 수 있습니다.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [데이터베이스 스냅샷 만들기&#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md)  
  
-   [데이터베이스 스냅샷 보기&#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)  
  
-   [데이터베이스를 데이터베이스 스냅샷으로 되돌리기](revert-a-database-to-a-database-snapshot.md)  
  

  
## <a name="see-also"></a>참고 항목  
 [DROP DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-audit-specification-transact-sql)   
 [데이터베이스 스냅샷&#40;SQL Server&#41;](database-snapshots-sql-server.md)  
  
  
