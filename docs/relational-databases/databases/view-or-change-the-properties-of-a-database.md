---
title: 데이터베이스의 속성 보기 또는 변경 | Microsoft 문서
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dc1e6d1021e1e7cf30a683d8c81c625a56b9766c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68127064"
---
# <a name="view-or-change-the-properties-of-a-database"></a>데이터베이스의 속성 보기 또는 변경
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]데이터베이스의 속성을 보거나 변경하는 방법에 대해 설명합니다. 데이터베이스 속성을 변경하면 수정 사항이 즉시 반영됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **데이터베이스의 속성을 보거나 변경하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   AUTO_CLOSE가 ON으로 설정되어 있으면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 일부 열과 DATABASEPROPERTYEX 함수는 데이터베이스에서 데이터를 검색할 수 없는 경우 NULL을 반환합니다. 이 문제를 해결하려면 데이터베이스를 엽니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 데이터베이스의 속성을 변경하려면 데이터베이스에 대한 ALTER 권한이 필요합니다. 데이터베이스의 속성을 보려면 최소한 공용 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-or-change-the-properties-of-a-database"></a>데이터베이스의 속성을 보거나 변경하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 확인할 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **데이터베이스 속성** 대화 상자에서 해당 정보를 확인할 페이지를 선택합니다. 예를 들어 데이터 파일 및 로그 파일 정보를 보려면 **파일** 페이지를 선택합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 Transact-SQL은 데이터베이스의 속성을 확인하고 변경하는 여러 방법을 제공합니다. 데이터베이스의 속성을 보려는 경우 [DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수 및 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰를 사용할 수 있습니다. 데이터베이스의 속성을 변경하려는 경우에는 사용 중인 환경에 적합한 ALTER DATABASE 문 버전([ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md) 또는 [ALTER DATABASE(Azure SQL Database))](../../t-sql/statements/alter-database-azure-sql-database.md)을 사용할 수 있습니다. 데이터베이스 범위 속성을 보려면 [sys.database_scoped_configurations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 카탈로그 뷰를 사용하고 데이터베이스 범위 속성을 변경하려면 [ALTER DATABASE SCOPED CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 문을 사용합니다.  
  
#### <a name="to-view-a-property-of-a-database-by-using-the-databasepropertyex-function"></a>DATABASEPROPERTYEX 함수를 사용하여 데이터베이스의 속성을 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결한 다음 해당 속성을 보려는 데이터베이스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 시스템 함수를 사용하여 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 AUTO_SHRINK 데이터베이스 옵션 상태를 반환합니다. 반환 값이 1이면 해당 옵션이 ON으로 설정되어 있고 반환 값이 0이면 해당 옵션이 OFF로 설정되어 있음을 의미합니다.  
  
    ```sql  
    SELECT DATABASEPROPERTYEX('AdventureWorks2012', 'IsAutoShrink');  
    ```  
  
#### <a name="to-view-the-properties-of-a-database-by-querying-sysdatabases"></a>sys.databases를 쿼리하여 데이터베이스의 속성을 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결한 다음 해당 속성을 보려는 데이터베이스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰를 쿼리하여 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 여러 속성을 확인합니다. 이 예에서는 데이터베이스 ID 번호(`database_id`), 데이터베이스가 읽기 전용인지 읽기/쓰기인지 여부(`is_read_only`), 데이터베이스의 데이터 정렬(`collation_name`) 및 데이터베이스 호환성 수준(`compatibility_level`)을 반환합니다.  
  
    ```sql  
    SELECT database_id, is_read_only, collation_name, compatibility_level  
    FROM sys.databases WHERE name = 'AdventureWorks2012';  
    ```  
  
#### <a name="to-view-the-properties-of-a-database-scoped-configuration-by-querying-sysdatabases_scoped_configuration"></a>sys.databases_scoped_configuration를 쿼리하여 데이터베이스 범위 구성의 속성을 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결한 다음 해당 속성을 보려는 데이터베이스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sys.database_scoped_configurations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 카탈로그 뷰를 쿼리하여 현재 데이터베이스의 여러 속성을 확인합니다.  
  
    ```sql  
    SELECT configuration_id, name, value, value_for_secondary  
    FROM sys.database_scoped_configurations;  
    ```  
  
     더 많은 예제를 보려면 [sys.database_scoped_configurations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)  
  
#### <a name="to-change-the-properties-of-a-sql-server-2016-database-using-alter-database"></a>ALTER DATABASE를 사용하여 SQL Server 2016 데이터베이스의 속성을 변경하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣습니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 스냅샷 격리 상태를 확인하고 속성 상태를 변경한 다음 변경 내용을 확인합니다.  
  
     스냅샷 격리 상태를 확인하려면 첫 번째 `SELECT` 문을 선택하고 **실행**을 클릭합니다.  
  
     스냅샷 격리 상태를 변경하려면 `ALTER DATABASE` 문을 선택하고 **실행**을 클릭합니다.  
  
     변경 내용을 확인하려면 두 번째 `SELECT` 문을 선택하고 **실행**을 클릭합니다.  
  
     [!code-sql[DatabaseDDL#AlterDatabase9](../../relational-databases/databases/codesnippet/tsql/view-or-change-the-prope_1.sql)]  
  
#### <a name="to-change-the-database-scoped-properties-using-alter-database-scoped-configuration"></a>ALTER DATABASE SCOPED CONFIGURATION을 사용하여 데이터베이스 범위 속성을 변경하려면  
  
1.  SQL Server 인스턴스에서 데이터베이스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣습니다. 다음 예에서는 보조 데이터베이스의 MAXDOP를 주 데이터베이스의 값으로 설정합니다.  
  
    ```sql  
    ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = PRIMARY   
    ```  
  
## <a name="see-also"></a>참고 항목  
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER DATABASE(Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [ALTER DATABASE SCOPED CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [sys.database_scoped_configurations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)  

  
  
