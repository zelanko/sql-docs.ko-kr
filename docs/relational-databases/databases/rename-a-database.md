---
title: "데이터베이스 이름 바꾸기 | Microsoft 문서"
ms.custom: 
ms.date: 11/20/2017
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
- databases [SQL Server], renaming
- renaming databases
ms.assetid: 44c69d35-abcb-4da3-9370-5e0bc9a28496
caps.latest.revision: "19"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7660b2175a9f854567dd8e168171b0909a151957
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="rename-a-database"></a>데이터베이스 이름 바꾸기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 사용자 정의 데이터베이스의 이름을 바꾸는 방법에 대해 설명합니다. 데이터베이스 이름에는 식별자 규칙에서 허용하는 모든 문자를 사용할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **데이터베이스의 이름을 바꾸려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Follow Up:**  [After renaming a database](#FollowUp)  

> [!NOTE]
> Azure SQL Database에서 데이터베이스의 이름을 바꾸려면 [ALTER DATABASE(Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md) 문을 사용합니다. Azure SQL Data Warehouse 또는 Parallel Data Warehouse에서 데이터베이스의 이름을 바꾸려면 [RENAME(Transact-SQL)](/t-sql/statements/rename-transact-sql) 문을 사용합니다.
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   시스템 데이터베이스 이름은 바꿀 수 없습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-rename-a-database"></a>데이터베이스 이름을 바꾸려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  데이터베이스를 사용하고 있지 않는지 확인하고 [데이터베이스를 단일 사용자 모드로 설정](../../relational-databases/databases/set-a-database-to-single-user-mode.md)합니다.  
  
3.  **데이터베이스**를 확장하고 이름을 바꿀 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **이름 바꾸기**를 클릭합니다.  
  
4.  새 데이터베이스 이름을 입력하고 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-rename-a-database"></a>데이터베이스 이름을 바꾸려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예에서는 `AdventureWorks2012` 데이터베이스의 이름을 `Northwind`로 변경합니다.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
###  <a name="TsqlExample"></a>   
##  <a name="FollowUp"></a> 후속 작업: 데이터베이스의 이름을 바꾼 후  
 데이터베이스 이름을 바꾼 후 **master** 데이터베이스를 백업합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE(Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [데이터베이스 식별자](../../relational-databases/databases/database-identifiers.md)  
  
  
