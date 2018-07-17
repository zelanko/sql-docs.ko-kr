---
title: 저장 프로시저의 종속성 보기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], dependencies
- displaying stored procedure dependencies
- viewing stored procedure dependencies
ms.assetid: 6ae0a369-1bc7-4ae4-be89-2b483697cd1f
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c85d42da5d49d9d3836a029f6e191cec9a24c2f7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37332673"
---
# <a name="view-the-dependencies-of-a-stored-procedure"></a>저장 프로시저의 종속성 보기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 저장 프로시저 종속성을 보는 방법에 대해 설명합니다.  
  
##  <a name="Top"></a>   
-   **시작하기 전 주의 사항:**  [제한 사항](#Restrictions), [보안](#Security)  
  
-   **프로시저 종속성을 보려면:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 시스템 함수: **sys.dm_sql_referencing_entities**  
 참조된 엔터티에 대한 CONTROL 권한과 sys.dm_sql_referencing_entities에 대한 SELECT 권한이 필요합니다. 참조된 엔터티가 파티션 함수인 경우 데이터베이스에 대한 CONTROL 권한이 필요합니다. 기본적으로 SELECT 권한은 public에 부여됩니다.  
  
 시스템 함수: **sys.dm_sql_referenced_entities**  
 sys.dm_sql_referenced_entities에 대한 SELECT 권한 및 참조 엔터티에 대한 VIEW DEFINITION 권한이 필요합니다. 기본적으로 SELECT 권한은 public에 부여됩니다. 참조 엔터티가 데이터 수준 DDL 트리거인 경우 데이터베이스에 대한 ALTER DATABASE DDL TRIGGER 권한 또는 데이터베이스에 대한 VIEW DEFINITION 권한이 필요합니다. 참조 엔터티가 서버 수준 DDL 트리거인 경우 서버에 대한 VIEW ANY DEFINITION 권한이 필요합니다.  
  
 개체 카탈로그 뷰: **sys.sql_expression_dependencies**  
 데이터베이스에 대한 VIEW DEFINITION 권한과 데이터베이스의 sys.sql_expression_dependencies에 대한 SELECT 권한이 필요합니다. 기본적으로 SELECT 권한은 db_owner 고정 데이터베이스 역할의 멤버에게만 부여됩니다. SELECT와 VIEW DEFINITION 권한을 다른 사용자에게 부여하면 피부여자는 데이터베이스의 모든 종속성을 볼 수 있습니다.  
  
##  <a name="Procedures"></a> 저장 프로시저의 종속성을 보는 방법  
 다음 중 하나를 사용할 수 있습니다.  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **개체 탐색기에서 프로시저 종속성을 보려면**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 프로시저가 속한 데이터베이스를 확장한 다음 **프로그래밍 기능**을 확장합니다.  
  
3.  **저장 프로시저**를 확장하고 프로시저를 마우스 오른쪽 단추로 클릭한 다음 **종속성 보기**를 클릭합니다.  
  
4.  프로시저에 종속된 개체 목록을 확인합니다.  
  
5.  프로시저가 종속된 개체 목록을 확인합니다.  
  
6.  **확인**을 클릭합니다.  
  
###  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **쿼리 편집기에서 프로시저의 종속성을 보려면**  
  
 시스템 함수: **sys.dm_sql_referencing_entities**  
 이 함수는 프로시저에 종속된 개체를 표시합니다.  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 프로시저가 속한 데이터베이스를 확장합니다.  
  
3.  **파일** 메뉴에서 **새 쿼리** 를 클릭합니다.  
  
4.  다음 예를 복사하여 쿼리 편집기에 붙여 넣습니다. 첫 번째 예에서는 `uspVendorAllInfo` 데이터베이스의 모든 공급업체 이름, 해당 공급업체가 공급하는 제품, 신용 등급 및 사용 가능성을 반환하는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 프로시저를 만듭니다.  
  
    ```  
    USE AdventureWorks2008R2;  
    GO  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
    ```  
  
5.  프로시저가 생성된 후 두 번째 예에서는 sys.dm_sql_referencing_entities 함수를 사용하여 프로시저에 종속된 개체를 표시합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
    FROM sys.dm_sql_referencing_entities ('Purchasing.uspVendorAllInfo', 'OBJECT');   
    GO  
  
    ```  
  
 시스템 함수: **sys.dm_sql_referenced_entities**  
 이 함수는 프로시저에 종속된 개체를 표시합니다.  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 프로시저가 속한 데이터베이스를 확장합니다.  
  
3.  **파일** 메뉴에서 **새 쿼리** 를 클릭합니다.  
  
4.  다음 예를 복사하여 쿼리 편집기에 붙여 넣습니다. 첫 번째 예에서는 `uspVendorAllInfo` 데이터베이스의 모든 공급업체 이름, 해당 공급업체가 공급하는 제품, 신용 등급 및 사용 가능성을 반환하는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 프로시저를 만듭니다.  
  
    ```  
    USE AdventureWorks2008R2;  
    GO  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
    ```  
  
5.  프로시저가 생성된 후 두 번째 예에서는 sys.dm_sql_referenced_entities 함수를 사용하여 프로시저가 종속된 개체를 표시합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT referenced_schema_name, referenced_entity_name,  
    referenced_minor_name,referenced_minor_id, referenced_class_desc,  
    is_caller_dependent, is_ambiguous  
    FROM sys.dm_sql_referencing_entities ('Purchasing.uspVendorAllInfo', 'OBJECT');  
    GO  
    ```  
  
 개체 카탈로그 뷰: **sys.sql_expression_dependencies**  
 이 뷰는 프로시저가 종속된 개체 또는 프로시저에 종속된 개체를 표시합니다.  
  
 프로시저에 종속된 개체를 표시  
 1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 프로시저가 속한 데이터베이스를 확장합니다.  
  
3.  **파일** 메뉴에서 **새 쿼리** 를 클릭합니다.  
  
4.  다음 예를 복사하여 쿼리 편집기에 붙여 넣습니다. 첫 번째 예에서는 `uspVendorAllInfo` 데이터베이스의 모든 공급업체 이름, 해당 공급업체가 공급하는 제품, 신용 등급 및 사용 가능성을 반환하는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 프로시저를 만듭니다.  
  
    ```  
    USE AdventureWorks2008R2;  
    GO  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
    ```  
  
5.  프로시저가 생성된 후 두 번째 예에서는 sys.sql_expression_dependencies 뷰를 사용하여 프로시저에 종속된 개체를 표시합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_SCHEMA_NAME ( referencing_id ) AS referencing_schema_name,  
        OBJECT_NAME(referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        referencing_class_desc, referenced_class_desc,  
        referenced_server_name, referenced_database_name, referenced_schema_name,  
        referenced_entity_name,   
        COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
        is_caller_dependent, is_ambiguous  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    WHERE referenced_id = OBJECT_ID(N'Purchasing.uspVendorAllInfo')  
    GO  
    ```  
  
 프로시저가 종속된 개체 목록을 표시  
 1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 프로시저가 속한 데이터베이스를 확장합니다.  
  
3.  **파일** 메뉴에서 **새 쿼리** 를 클릭합니다.  
  
4.  다음 예를 복사하여 쿼리 편집기에 붙여 넣습니다. 첫 번째 예에서는 `uspVendorAllInfo` 데이터베이스의 모든 공급업체 이름, 해당 공급업체가 공급하는 제품, 신용 등급 및 사용 가능성을 반환하는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 프로시저를 만듭니다.  
  
    ```  
    USE AdventureWorks2008R2;  
    GO  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
    ```  
  
5.  프로시저가 생성된 후 두 번째 예에서는 sys.sql_expression_dependencies 뷰를 사용하여 프로시저가 종속된 개체를 표시합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        referencing_class_desc, referenced_class_desc,  
        referenced_server_name, referenced_database_name, referenced_schema_name,  
        referenced_entity_name,   
        COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
        is_caller_dependent, is_ambiguous  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    WHERE referencing_id = OBJECT_ID(N'Purchasing.uspVendorAllInfo');  
    GO  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [저장 프로시저 이름 바꾸기](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [sys.dm_sql_referencing_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.dm_sql_referenced_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
