---
title: "테이블 삭제 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_TABLE_TSQL
- DROP TABLE
dev_langs:
- TSQL
helpviewer_keywords:
- removing indexes
- table removal [SQL Server]
- deleting indexes
- dropping data
- deleting tables
- dropping indexes
- removing constraints
- removing permissions
- DROP TABLE statement
- removing tables
- deleting triggers
- removing data
- dropping tables
- deleting permissions
- dropping triggers
- deleting constraints
- removing triggers
- deleting data
- dropping constraints
- dropping permissions
ms.assetid: 0b6f2b6f-3aa3-4767-943f-43df3c3c5cfd
caps.latest.revision: 61
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 22fa2a1da83dfef0743c089256fcd1e18af9b54c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-table-transact-sql"></a>DROP TABLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  하나 이상의 테이블 정의 및 해당 테이블의 모든 데이터, 인덱스, 트리거, 제약 조건 및 권한 지정을 제거합니다. 모든 보기 또는 삭제 된 테이블을 참조 하는 저장된 프로시저를 명시적으로 삭제 해야를 사용 하 여 [DROP VIEW](../../t-sql/statements/drop-view-transact-sql.md) 또는 [DROP PROCEDURE](../../t-sql/statements/drop-procedure-transact-sql.md)합니다. 테이블에 종속성을 보고를 사용 하 여 [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP TABLE [ IF EXISTS ] [ database_name . [ schema_name ] . | schema_name . ]  
table_name [ ,...n ]  
[ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name   
[;]  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 테이블이 생성된 데이터베이스 이름입니다.  
  
 database_name이 현재 데이터베이스이거나 database_name이 tempdb이고 object_name이 #으로 시작하는 경우 Microsoft Azure SQL Database는 세 부분으로 구성된 이름 형식 database_name.[schema_name].object_name을 지원합니다. Microsoft Azure SQL Database는 네 부분으로 구성된 이름을 지원하지 않습니다.  
  
 *경우에 존재*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 조건에 따라 이미 있는 경우에 테이블을 삭제 합니다.  
  
 *schema_name*  
 테이블이 속한 스키마의 이름입니다.  
  
 *table_name*  
 제거할 테이블의 이름입니다.  
  
## <a name="remarks"></a>주의  
 DROP TABLE로 FOREIGN KEY 제약 조건에 의해 참조되는 테이블을 삭제할 수 없습니다. 참조하는 FOREIGN KEY 제약 조건 또는 참조하는 테이블을 먼저 삭제해야 합니다. 참조하는 테이블과 기본 키를 포함하는 테이블이 하나의 DROP TABLE 문에서 삭제되는 경우 참조하는 테이블이 먼저 나열되어야 합니다.  
  
 모든 데이터베이스에서 여러 테이블을 삭제할 수 있습니다. 삭제될 다른 테이블의 기본 키를 참조하는 테이블이 삭제되는 경우 외래 키가 있는 참조하는 테이블은 참조되는 기본 키를 포함한 테이블보다 먼저 나열되어야 합니다.  
  
 테이블을 삭제하면 해당 테이블에 있는 규칙이나 기본값의 바인딩이 해제되고 해당 테이블과 연결된 제약 조건이나 트리거가 자동으로 삭제됩니다. 테이블을 다시 만들려면 해당 규칙과 기본값을 다시 바인딩하고 트리거를 다시 만들어야 하며 필요한 제약 조건을 모두 추가해야 합니다.  
  
 DELETE를 사용 하 여 테이블의 모든 행을 삭제 하는 경우 *tablename* TRUNCATE TABLE 문을 사용 하거나, 테이블이 삭제 될 때까지 존재 합니다.  
  
 129개 이상의 익스텐트를 사용하는 큰 테이블 및 인덱스는 논리적 단계와 물리적 단계를 통해 삭제됩니다. 논리적 단계에서는 테이블에 사용되는 기존 할당 단위가 할당 취소로 표시되고 트랜잭션이 커밋될 때까지 잠깁니다. 물리적 단계에서는 할당 취소로 표시된 IAM 페이지가 물리적으로 일괄 삭제됩니다.  
  
 FILESTREAM 특성이 있는 VARBINARY(MAX) 열이 포함된 테이블을 삭제해도 파일 시스템에 저장된 데이터는 제거되지 않습니다.  
  
> [!IMPORTANT]  
>  동일한 일괄 처리에서 동일한 테이블에 대해 DROP TABLE과 CREATE TABLE을 실행할 수는 없습니다. 이를 실행하면 예기치 않은 오류가 발생할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 테이블이 속한 스키마에 대한 ALTER 권한, 테이블에 대한 CONTROL 권한 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-a-table-in-the-current-database"></a>1. 현재 데이터베이스에서 테이블 삭제  
 다음 예에서는 현재 데이터베이스에서 `ProductVendor1` 테이블과 해당 데이터 및 인덱스를 제거합니다.  
  
```  
DROP TABLE ProductVendor1 ;  
```  
  
### <a name="b-dropping-a-table-in-another-database"></a>2. 다른 데이터베이스에서 테이블 삭제  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 `SalesPerson2` 테이블을 삭제합니다. 이 예는 서버 인스턴스의 모든 데이터베이스에서 실행할 수 있습니다.  
  
```  
DROP TABLE AdventureWorks2012.dbo.SalesPerson2 ;  
```  
  
### <a name="c-dropping-a-temporary-table"></a>3. 임시 테이블 삭제  
 다음 예에서는 임시 테이블을 만들고 존재 여부를 테스트한 다음 테이블을 삭제하고 다시 존재 여부를 테스트합니다. 이 예제에서는 사용 하지 않는 **IF EXISTS** 부터 사용할 수 있는 구문 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]합니다.  
  
```  
CREATE TABLE #temptable (col1 int);  
GO  
INSERT INTO #temptable  
VALUES (10);  
GO  
SELECT * FROM #temptable;  
GO  
IF OBJECT_ID(N'tempdb..#temptable', N'U') IS NOT NULL   
DROP TABLE #temptable;  
GO  
--Test the drop.  
SELECT * FROM #temptable;  
  
```  
  
### <a name="d-dropping-a-table-using-if-exists"></a>4. IF EXISTS를 사용 하 여 테이블 삭제  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 다음 예제에서는 t 1 이라는 테이블을 만듭니다. 다음 두 번째 문은 테이블을 삭제 합니다. 세 번째 문은 아무 작업도 수행 하므로 테이블 문서가 이미 삭제 되었지만 오류가 발생 하지 않습니다.  
  
```  
CREATE TABLE T1 (Col1 int);  
GO  
DROP TABLE IF EXISTS T1;  
GO  
DROP TABLE IF EXISTS T1;  
```  
  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_spaceused&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [TRUNCATE table&#40; Transact SQL &#41;](../../t-sql/statements/truncate-table-transact-sql.md)   
 [DROP view&#40; Transact SQL &#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [DROP procedure&#40; Transact SQL &#41;](../../t-sql/statements/drop-procedure-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  

