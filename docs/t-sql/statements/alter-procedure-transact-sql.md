---
title: ALTER PROCEDURE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_PROCEDURE_TSQL
- ALTER_PROC_TSQL
- ALTER PROC
- ALTER PROCEDURE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROCEDURE statement
- stored procedure modifications [SQL Server]
- modifying stored procedures
- stored procedures [SQL Server], modifying
ms.assetid: ed9b2f76-11ec-498d-a95e-75b490a75733
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 70e3fbfe0ed0d255cbe6f27c410af96061ab7432
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982067"
---
# <a name="alter-procedure-transact-sql"></a>ALTER PROCEDURE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이전에 CREATE PROCEDURE 문을 실행하여 만든 프로시저를 수정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙(Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database
  
ALTER { PROC | PROCEDURE } [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }   
        [ VARYING ] [ = default ] [ OUT | OUTPUT ] [READONLY]  
    ] [ ,...n ]   
[ WITH <procedure_option> [ ,...n ] ]  
[ FOR REPLICATION ]   
AS { [ BEGIN ] sql_statement [;] [ ...n ] [ END ] }  
[;]  
  
<procedure_option> ::=   
    [ ENCRYPTION ]  
    [ RECOMPILE ]  
    [ EXECUTE AS Clause ]  
```  
  
```  
-- Syntax for SQL Server CLR Stored Procedure  
  
ALTER { PROC | PROCEDURE } [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }   
        [ = default ] [ OUT | OUTPUT ] [READONLY]  
    ] [ ,...n ]   
[ WITH EXECUTE AS Clause ]  
AS { EXTERNAL NAME assembly_name.class_name.method_name }  
[;]  
```  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER { PROC | PROCEDURE } [schema_name.] procedure_name  
    [ { @parameterdata_type } [= ] ] [ ,...n ]  
AS { [ BEGIN ] sql_statement [ ; ] [ ,...n ] [ END ] }  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *schema_name*  
 프로시저가 속한 스키마의 이름입니다.  
  
 *procedure_name*  
 변경할 프로시저의 이름입니다. 프로시저 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.  
  
 **;** *number*  
 같은 이름을 가진 여러 개의 프로시저가 하나의 DROP PROCEDURE 문을 사용하여 삭제될 수 있도록 이러한 프로시저를 그룹화하는 데 사용되는 기존의 선택적인 정수입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 **@** *parameter*  
 프로시저의 매개 변수입니다. 매개 변수는 2,100개까지 지정할 수 있습니다.  
  
 [ _type\_schema\_name_ **.** ] _data\_type_  
 매개 변수와 매개 변수가 속하는 스키마의 데이터 형식입니다.  
  
 데이터 형식 제한 사항에 대한 자세한 내용은 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)를 참조하세요.  
  
 VARYING  
 결과 집합이 출력 매개 변수로 사용되도록 지정합니다. 이 매개 변수는 저장 프로시저에 의해 동적으로 생성될 수 있으며 해당 내용은 여러 가지가 될 수 있습니다. 커서 매개 변수에만 적용됩니다. CLR 프로시저에는 이 옵션이 유효하지 않습니다.  
  
 *default*  
 매개 변수의 기본값입니다.  
  
 OUT | OUTPUT  
 매개 변수가 반환 매개 변수임을 나타냅니다.  
  
 READONLY  
 프로시저 본문 내에서 매개 변수를 업데이트하거나 수정할 수 없음을 나타냅니다. 매개 변수 형식이 테이블 반환 형식인 경우 READONLY를 지정해야 합니다.  
  
 RECOMPILE  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 이 프로시저에 대한 계획을 캐시하지 않고 런타임에 프로시저가 다시 컴파일됨을 나타냅니다.  
  
 ENCRYPTION  
 **적용 대상**: SQL Server([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상) 및 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 ALTER PROCEDURE 문의 원본 텍스트가 알아보기 어려운 형식으로 변환됩니다. 난독 처리된 출력은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 카탈로그 뷰 어디에서도 직접 표시되지 않습니다. 시스템 테이블 또는 데이터베이스 파일에 대한 액세스 권한이 없는 사용자는 변조된 텍스트를 검색할 수 없습니다. 그러나 [DAC 포트](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)를 통해 시스템 테이블에 액세스하거나 데이터베이스 파일에 직접 액세스할 수 있는 권한을 가진 사용자는 이 텍스트를 사용할 수 있습니다. 또한 디버거를 서버 프로세스에 연결할 수 있는 사용자는 런타임에 메모리에서 원래 프로시저를 검색할 수 있습니다. 시스템 메타데이터에 액세스하는 방법에 대한 자세한 내용은 [메타데이터 표시 유형 구성](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
 이 옵션을 사용하여 만든 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제의 일부로 게시할 수 없습니다.  
  
 CLR(공용 언어 런타임) 저장 프로시저에 대해 이 옵션을 지정할 수 없습니다.  
  
> [!NOTE]  
>  업그레이드하는 동안 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 **sys.sql_modules**에 저장된 난독 처리된 주석을 사용하여 프로시저를 다시 만듭니다.  
  
 EXECUTE AS  
 액세스된 후 저장 프로시저를 실행할 보안 컨텍스트를 지정합니다.  
  
 자세한 내용은 [EXECUTE AS 절&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)을 참조하세요.  
  
 FOR REPLICATION  

  
 복제용으로 만든 저장 프로시저가 구독자에서 실행되지 못하도록 지정합니다. FOR REPLICATION 옵션을 사용하여 만든 저장 프로시저는 저장 프로시저 필터로 사용되며 복제하는 동안에만 실행됩니다. FOR REPLICATION을 지정하면 매개 변수를 선언할 수 없습니다. CLR 프로시저에는 이 옵션이 유효하지 않습니다. FOR REPLICATION으로 만든 프로시저의 경우 RECOMPILE 옵션이 무시됩니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 { [ BEGIN ] *sql_statement* [;] [ ...*n* ] [ END ] }  
 프로시저 본문을 구성하는 하나 이상의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. 선택적 키워드인 BEGIN과 END를 사용하여 문을 묶을 수 있습니다. 자세한 내용은 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)에서 최선의 구현 방법, 일반적인 주의 및 제한 사항 섹션을 참조하세요.  
  
 EXTERNAL NAME _assembly\_name_ **.** _class\_name_ **.** _method\_name_  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 CLR 저장 프로시저가 참조할 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 어셈블리의 메서드를 지정합니다. *class_name*은 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자여야 하며 어셈블리에서 클래스로 존재해야 합니다. 클래스에 마침표( **.** )를 사용하여 네임스페이스 부분을 구분하는 네임스페이스로 한정된 이름이 있는 경우 클래스 이름은 대괄호( **[]** ) 또는 큰따옴표( **""** )를 사용하여 구분되어야 합니다. 지정한 메서드는 해당 클래스의 정적 메서드여야 합니다.  
  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CLR 코드를 실행할 수 없습니다. 공용 언어 런타임 모듈을 참조하는 데이터베이스 개체를 생성, 수정 및 삭제할 수 있지만 [clr enabled 옵션](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)을 설정할 때까지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이러한 참조를 실행할 수 없습니다. 이 옵션을 설정하려면 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용합니다.  
  
> [!NOTE]  
>  CLR 프로시저는 포함된 데이터베이스에서 지원되지 않습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 CLR 저장 프로시저로 수정할 수 없으며 그 반대의 경우도 마찬가지입니다.  
  
 ALTER PROCEDURE는 사용 권한을 변경하지 않으며 종속 저장 프로시저나 트리거에 영향을 주지 않습니다. 그러나 QUOTED_IDENTIFIER 및 ANSI_NULLS에 대한 현재 세션 설정은 저장 프로시저가 수정될 때 저장 프로시저에 포함됩니다. 이 설정이 처음 저장 프로시저를 만들 때 적용한 설정과 다르면 저장 프로시저의 동작은 달라질 수 있습니다.  
  
 이전 프로시저 정의가 WITH ENCRYPTION 또는 WITH RECOMPILE을 사용하여 만들어진 경우 이러한 옵션은 ALTER PROCEDURE에 포함된 경우에만 활성화됩니다.  
  
 저장 프로시저에 대한 자세한 내용은 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)를 참조하세요.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 프로시저에 대한 **ALTER** 권한이나 **db_ddladmin** 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `uspVendorAllInfo` 저장 프로시저를 만듭니다. 이 프로시저는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]를 공급하는 모든 공급업체 이름, 해당 공급업체가 공급하는 제품, 신용 등급 및 사용 가능성을 반환합니다. 이 프로시저를 만든 후 다른 결과 집합을 반환하도록 프로시저를 수정합니다.  
  
```  
  
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
  
 다음 예에서는 `uspVendorAllInfo` 저장 프로시저를 변경합니다. EXECUTE AS CALLER 절을 제거하고 지정된 제품을 제공하는 공급업체만 반환하도록 프로시저 본문을 수정합니다. `LEFT` 및 `CASE` 함수는 결과 집합의 모양을 사용자 지정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER PROCEDURE Purchasing.uspVendorAllInfo  
    @Product varchar(25)   
AS  
    SET NOCOUNT ON;  
    SELECT LEFT(v.Name, 25) AS Vendor, LEFT(p.Name, 25) AS 'Product name',   
    'Rating' = CASE v.CreditRating   
        WHEN 1 THEN 'Superior'  
        WHEN 2 THEN 'Excellent'  
        WHEN 3 THEN 'Above average'  
        WHEN 4 THEN 'Average'  
        WHEN 5 THEN 'Below average'  
        ELSE 'No rating'  
        END  
    , Availability = CASE v.ActiveFlag  
        WHEN 1 THEN 'Yes'  
        ELSE 'No'  
        END  
    FROM Purchasing.Vendor AS v   
    INNER JOIN Purchasing.ProductVendor AS pv  
      ON v.BusinessEntityID = pv.BusinessEntityID   
    INNER JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID   
    WHERE p.Name LIKE @Product  
    ORDER BY v.Name ASC;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```   
 Vendor               Product name  Rating    Availability  
-------------------- ------------- -------   ------------  
Proseware, Inc.      LL Crankarm   Average   No  
Vision Cycles, Inc.  LL Crankarm   Superior  Yes  
(2 row(s) affected)`  
```  

## <a name="see-also"></a>참고 항목  
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)   
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [EXECUTE AS&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [저장 프로시저&#40;데이터베이스 엔진&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [sys.procedures&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)  
  
  
