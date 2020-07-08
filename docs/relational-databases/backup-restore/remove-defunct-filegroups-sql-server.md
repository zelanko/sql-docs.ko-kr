---
title: 존재하지 않는 파일 그룹 제거(SQL Server) | Microsoft 문서
description: 이 문서에서는 SQL Server에서 SQL Server Management Studio 또는 Transact-SQL을 사용하여 존재하지 않는 파일 그룹을 제거하는 방법을 보여 줍니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], defunct filegroups
- defunct filegroups
- restoring filegroups [SQL Server]
- deferred transactions
- filegroups [SQL Server], defunct
- unrestored filegroups
ms.assetid: 055f9c6a-5c18-4942-98e7-ec918f0ff975
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d26bb97408fa1a4118705bd60f0cd0ef10707722
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85669723"
---
# <a name="remove-defunct-filegroups-sql-server"></a>존재하지 않는 파일 그룹 제거(SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 존재하지 않는 파일 그룹을 제거하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
-   [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **존재하지 않는 파일 그룹을 제거하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   이 항목에서는 여러 개의 파일 또는 파일 그룹이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 관련된 내용 및 단순 모델의 경우 읽기 전용 파일 그룹과 관련된 내용을 다룹니다.  
  
-   오프라인 파일 그룹이 제거되면 파일 그룹의 모든 파일이 존재하지 않음 상태가 됩니다.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   복원되지 않은 파일 그룹을 복원할 필요가 없는 경우 데이터베이스에서 해당 파일 그룹을 제거하여 *존재하지 않는* 파일 그룹으로 만들 수 있습니다. 존재하지 않는 파일 그룹은 이 데이터베이스로 복원될 수 없지만 해당 메타데이터는 유지됩니다. 파일 그룹이 존재하지 않는 상태가 된 후 데이터베이스를 다시 시작할 수 있으며 복원된 파일 그룹 간에 데이터베이스의 일관성을 복구를 통해 유지할 수 있습니다.  
  
     예를 들어 데이터베이스에서 더 이상 필요하지 않은 오프라인 파일 그룹으로 인해 트랜잭션이 지연되는 문제를 해결하기 위한 한 가지 방법으로 파일 그룹을 존재하지 않는 상태로 만드는 것입니다. 파일 그룹이 오프라인 상태이므로 지연된 트랜잭션은 이 파일 그룹이 존재하지 않게 된 후에 지연된 상태에서 벗어납니다. 자세한 내용은 [지연된 트랜잭션&#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)에서 존재하지 않는 파일 그룹을 제거하는 방법에 대해 설명합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-remove-defunct-filegroups"></a>존재하지 않는 파일 그룹을 제거하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 파일을 삭제할 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **파일** 페이지를 선택합니다.  
  
4.  **데이터베이스 파일** 표에서 삭제할 파일을 선택하고 **제거**를 클릭한 다음 **확인**을 클릭합니다.  
  
5.  **파일 그룹** 페이지를 선택합니다.  
  
6.  **행** 표에서 삭제할 파일 그룹을 선택하고 **제거**를 클릭한 다음 **확인**을 클릭합니다.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-remove-defunct-filegroups"></a>존재하지 않는 파일 그룹을 제거하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. (**참고:** 이 예제에서는 파일과 파일 그룹이 이미 있다고 가정합니다. 이러한 개체를 만들려면 [ALTER DATABASE 파일 및 파일 그룹 옵션](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) 항목의 예제 B를 참조하세요. 첫 번째 예에서는 `test1dat3` 절과 함께 `test1dat4` 문을 사용하여 존재하지 않는 파일 그룹에서 `ALTER DATABASE` 및 `REMOVE FILE` 파일을 제거합니다. 두 번째 예에서는 `Test1FG1`절을 사용하여 존재하지 않는 파일 그룹 `REMOVE FILEGROUP` 을 제거합니다.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat3 ;  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat4 ;  
GO  
  
```  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILEGROUP Test1FG1 ;  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE 파일 및 파일 그룹 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)   
 [지연된 트랜잭션&#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)   
 [파일 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [파일 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [온라인 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [페이지 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
