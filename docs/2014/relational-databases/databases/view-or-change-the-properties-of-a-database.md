---
title: 데이터베이스의 속성 보기 또는 변경 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- displaying databases
- database viewing [SQL Server]
- databases [SQL Server], viewing
- viewing databases
ms.assetid: 9e8ac097-84b7-46c7-85e3-c1e79f94d747
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10ad92286011f6f81fbaff5ab4908007e16bdd45
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528467"
---
# <a name="view-or-change-the-properties-of-a-database"></a>데이터베이스의 속성 보기 또는 변경
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]데이터베이스의 속성을 보거나 변경하는 방법에 대해 설명합니다. 데이터베이스 속성을 변경하면 수정 사항이 즉시 반영됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **데이터베이스의 속성을 보거나 변경하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   AUTO_CLOSE가 ON으로 설정되어 있으면 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 카탈로그 뷰의 일부 열과 DATABASEPROPERTYEX 함수는 데이터베이스에서 데이터를 검색할 수 없는 경우 NULL을 반환합니다. 이 문제를 해결하려면 USE 문을 실행하여 데이터베이스를 엽니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-or-change-the-properties-of-a-database"></a>데이터베이스의 속성을 보거나 변경하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 확인할 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **데이터베이스 속성** 대화 상자에서 해당 정보를 확인할 페이지를 선택합니다. 예를 들어 데이터 파일 및 로그 파일 정보를 보려면 **파일** 페이지를 선택합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-a-property-of-a-database-by-using-databasepropertyex"></a>DATABASEPROPERTYEX를 사용하여 데이터베이스의 속성을 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql) 시스템 함수를 사용하여 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 AUTO_SHRINK 데이터베이스 옵션 상태를 반환합니다. 반환 값이 1이면 해당 옵션이 ON으로 설정되어 있고 반환 값이 0이면 해당 옵션이 OFF로 설정되어 있음을 의미합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT DATABASEPROPERTYEX('AdventureWorks2012', 'IsAutoShrink');  
GO  
  
```  
  
#### <a name="to-view-the-properties-of-a-database-by-querying-sysdatabases"></a>sys.databases를 쿼리하여 데이터베이스의 속성을 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 카탈로그 뷰를 쿼리하여 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 여러 속성을 확인합니다. 이 예에서는 데이터베이스 ID 번호(`database_id`), 데이터베이스가 읽기 전용인지 읽기/쓰기인지 여부(`is_read_only`), 데이터베이스의 데이터 정렬(`collation_name`) 및 데이터베이스 호환성 수준(`compatibility_level`)을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT database_id, is_read_only, collation_name, compatibility_level  
FROM sys.databases WHERE name = 'AdventureWorks2012';  
GO  
  
```  
  
#### <a name="to-change-the-properties-of-a-database"></a>데이터베이스의 속성을 변경하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣습니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 스냅숏 격리 상태를 확인하고 속성 상태를 변경한 다음 변경 내용을 확인합니다.  
  
     스냅숏 격리 상태를 확인하려면 첫 번째 `SELECT` 문을 선택하고 **실행**을 클릭합니다.  
  
     스냅숏 격리 상태를 변경하려면 `ALTER DATABASE` 문을 선택하고 **실행**을 클릭합니다.  
  
     변경 내용을 확인하려면 두 번째 `SELECT` 문을 선택하고 **실행**을 클릭합니다.  
  
 [!code-sql[DatabaseDDL#AlterDatabase9](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase9)]  
  
## <a name="see-also"></a>관련 항목  
 [sys.databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [ALTER DATABASE SET HADR&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-hadr)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [ALTER DATABASE 데이터베이스 미러링&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)   
 [ALTER DATABASE 파일 및 파일 그룹 옵션&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)  
  
  
