---
description: CREATE VIEW(Transact-SQL)
title: CREATE VIEW(Transact-SQL)
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE VIEW
- VIEW_TSQL
- VIEW
- CREATE_VIEW_TSQL
- SCHEMABINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table creation [SQL Server], CREATE VIEW
- views [SQL Server], creating
- CREATE VIEW statement
- updatable partitioned views
- tables [SQL Server], virtual
- updatable views
- modifying partitioned views
- virtual tables [SQL Server]
- number of columns per view
- partitioned views [SQL Server], creating
- WITH ENCRYPTION clause
- WITH CHECK OPTION clause
- partitioned views [SQL Server], modifying
- partitioned views [SQL Server], replication
- distributed partitioned views [SQL Server]
- views [SQL Server], indexed views
- maximum number of columns per view
ms.assetid: aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1545d389f19aeee3c1cefa2e17bcc8c60bcd495
ms.sourcegitcommit: 71985f03656a30381b2498ac5393aaf86f670bf3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88602198"
---
# <a name="create-view-transact-sql"></a>CREATE VIEW(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  쿼리에 의해 내용(열과 행)이 정의되는 가상 테이블을 만듭니다. 이 문을 사용하여 데이터베이스에서 하나 이상의 테이블에 있는 데이터의 뷰를 만들 수 있습니다. 예를 들어 뷰는 다음과 같은 용도로 사용할 수 있습니다.  
  
-   각 사용자가 데이터베이스를 보는 시각에 초점을 맞추고 데이터 조작을 간소화하며 사용자 지정할 수 있습니다.  
  
-   뷰는 원본이 되는 기본 테이블에 직접 액세스할 수 있는 권한을 부여하지 않고 뷰를 통해 데이터에 액세스하도록 하기 때문에 보안 메커니즘으로 사용할 수 있습니다.  
  
-   이전 버전과 호환되는 인터페이스를 통해 스키마가 변경된 기존 테이블을 에뮬레이트할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE [ OR ALTER ] VIEW [ schema_name . ] view_name [ (column [ ,...n ] ) ]
[ WITH <view_attribute> [ ,...n ] ]
AS select_statement
[ WITH CHECK OPTION ]
[ ; ]  
  
<view_attribute> ::=
{  
    [ ENCRYPTION ]  
    [ SCHEMABINDING ]  
    [ VIEW_METADATA ]
}
```  
  
```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE VIEW [ schema_name . ] view_name [  ( column_name [ ,...n ] ) ]   
AS <select_statement>   
[;]  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수

OR ALTER  
 **적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1부터)   
  
 이미 있는 경우에만 뷰를 조건부로 변경합니다. 
 
 *schema_name*  
 뷰가 속한 스키마의 이름입니다.  
  
 *view_name*  
 뷰의 이름입니다. 뷰 이름은 반드시 식별자에 적용되는 규칙을 준수해야 합니다. 뷰 소유자 이름을 지정하는 것은 선택 사항입니다.  
  
 *column*  
 뷰에 있는 열에 사용할 이름입니다. 열이 산술 식, 함수 또는 상수에서 파생된 경우, 일반적으로 조인 때문에 둘 이상의 열이 같은 이름을 갖는 경우, 뷰의 열이 파생된 열과 다른 이름을 갖는 경우에만 열 이름이 필요합니다. SELECT 문에서 열 이름을 할당할 수도 있습니다.  
  
 *column*을 지정하지 않으면 뷰 열의 이름과 SELECT 문에 있는 열의 이름이 같아집니다.  
  
> [!NOTE]  
>  뷰에 대한 열에서 열 이름에 대한 사용 권한은 기본 데이터의 원본에 상관없이 CREATE VIEW 또는 ALTER VIEW 문에 적용할 수 있습니다. 예를 들어 CREATE VIEW 문에서 **SalesOrderID** 열에 사용 권한이 부여된 경우 ALTER VIEW 문은 **SalesOrderID** 열에 **OrderRef** 등의 다른 이름을 지정할 수 있으며 여전히 **SalesOrderID**를 사용하는 뷰에 연결된 사용 권한을 가집니다.  
  
 AS  
 뷰가 수행할 동작을 지정합니다.  
  
 *select_statement*  
 뷰를 정의하는 SELECT 문입니다. 이 문은 둘 이상의 테이블과 다른 뷰를 사용할 수 있습니다. 생성된 뷰의 SELECT 절에 참조된 개체 중에서 선택하려면 알맞은 사용 권한이 있어야 합니다.  
  
 뷰가 한 특정 테이블의 행과 열로 된 간단한 하위 집합일 필요는 없습니다. 복잡도에 구애받지 않고 SELECT 절이 있는 둘 이상의 테이블 또는 다른 뷰를 사용하여 뷰를 만들 수 있습니다.  
  
 인덱싱된 뷰 정의에서 SELECT 문은 반드시 단일 테이블 문 또는 선택적 집계가 있는 복수 테이블 JOIN이어야 합니다.  
  
 뷰를 정의하는 SELECT 절에는 다음을 포함할 수 없습니다.  
  
-   SELECT 문의 선택 목록에 TOP 절도 함께 있는 경우를 제외한 ORDER BY 절  
  
    > [!IMPORTANT]  
    >  ORDER BY 절은 뷰 정의의 TOP 또는 OFFSET 절에서 반환되는 행을 결정하기 위한 용도로만 사용됩니다. 쿼리 자체에서 ORDER BY를 지정하지 않으면 ORDER BY 절은 뷰 쿼리 시 정렬된 결과를 보장하지 않습니다.  
  
-   INTO 키워드  
  
-   OPTION 절  
  
-   임시 테이블 또는 테이블 변수 참조  
  
 *select_statement*가 SELECT 문을 사용하므로 \<join_hint> 및 \<table_hint> 힌트를 FROM 절에서 지정된 대로 사용해야 합니다. 자세한 내용은 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md) 및 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)를 참조하세요. 
  
 *select_statement*에는 UNION 또는 UNION ALL로 구분된 함수 및 여러 SELECT 문을 사용할 수 있습니다.  
  
 CHECK OPTION  
 뷰에 대해 실행된 모든 데이터 수정 명령문이 *select_statement* 내의 기준 집합을 준수하도록 설정합니다. 뷰를 통해 행을 수정한 경우에는 WITH CHECK OPTION을 사용하여 수정이 커밋된 후에도 계속 뷰를 통해 데이터를 볼 수 있도록 합니다.  
  
> [!NOTE]
>  CHECK OPTION은 뷰를 통해 이루어진 업데이트에만 적용됩니다. 뷰의 기본 테이블에 직접 수행된 업데이트에는 적용되지 않습니다.  
  
 ENCRYPTION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 CREATE VIEW 문의 텍스트가 포함된 [sys.syscomments](../../relational-databases/system-compatibility-views/sys-syscomments-transact-sql.md)의 항목을 암호화합니다. WITH ENCRYPTION을 사용하면 뷰가 SQL Server 복제의 일부로 게시되지 않도록 할 수 있습니다.  
  
 SCHEMABINDING  
 기본 테이블의 스키마에 뷰를 바인딩합니다. SCHEMABINDING을 지정하면 뷰 정의에 영향을 미치는 방법으로 기본 테이블을 수정할 수 없습니다. 뷰 정의 자체를 먼저 수정하거나 삭제하여 수정할 테이블에 대해 종속성을 제거해야 합니다. SCHEMABINDING을 사용하는 경우 *select_statement*에 참조되는 테이블, 뷰 또는 사용자 정의 함수의 두 부분으로 구성된 이름(_schema_ **.** _object_)이 있어야 합니다. 참조된 개체는 모두 같은 데이터베이스에 있어야 합니다.  
  
 SCHEMABINDING 절로 만든 뷰에서 사용하는 뷰 또는 테이블은 뷰가 삭제되거나 변경되어 스키마 바인딩이 더 이상 존재하지 않는 경우에만 삭제할 수 있습니다. 그렇지 않으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류가 발생합니다. 또한 ALTER TABLE 문이 뷰 정의에 영향을 미치는 경우에는 스키마 바인딩이 있는 뷰에서 사용하는 테이블에서 이러한 문을 실행할 수 없습니다.  
  
 VIEW_METADATA  
 뷰를 참조하는 쿼리에 대해 찾아보기 모드 메타데이터가 요청된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 기본 테이블 대신 뷰에 대한 메타데이터 정보를 DB-Library, ODBC 및 OLE DB API에 반환하도록 지정합니다. 찾아보기 모드 메타데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 이 클라이언트 쪽 API에 반환하는 추가 메타데이터입니다. 이 메타데이터를 사용하면 클라이언트 쪽 API가 업데이트할 수 있는 클라이언트 쪽 커서를 구현할 수 있습니다. 찾아보기 모드 메타데이터에는 결과 집합의 열이 속한 기본 테이블에 대한 정보가 포함되어 있습니다.  
  
 VIEW_METADATA를 사용하여 만든 뷰의 경우 찾아보기 모드 메타데이터는 결과 집합의 뷰에서 열을 설명할 때 기본 테이블 이름 대신 뷰 이름을 반환합니다.  
  
 WITH VIEW_METADATA를 사용하여 뷰를 만드는 경우 뷰에 INSTEAD OF INSERT 또는 INSTEAD OF UPDATE 트리거가 있으면 **timestamp** 열을 제외한 모든 열을 업데이트할 수 있습니다. 업데이트할 수 있는 뷰에 대한 자세한 내용은 주의를 참조하세요.  
  
## <a name="remarks"></a>설명  
 현재 데이터베이스에서만 뷰를 만들 수 있습니다. CREATE VIEW는 쿼리 일괄 처리에서 첫째 문이어야 합니다. 최대 1,024개의 열을 뷰에 포함시킬 수 있습니다.  
  
 뷰를 통해 쿼리할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 문에 참조된 모든 데이터베이스 개체가 존재하는지, 문의 컨텍스트 내에서 유효한지, 데이터 변경 문이 데이터 무결성 규칙을 위반하지 않는지 확인합니다. 확인이 실패하면 오류 메시지가 반환됩니다. 성공적으로 확인한 경우 작업이 기본 테이블에 대한 동작으로 변환됩니다.  
  
 뷰가 삭제된 테이블이나 뷰에 종속된 경우 뷰를 사용하려고 하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류 메시지를 표시합니다. 새 테이블이나 뷰가 만들어지고 삭제된 테이블을 대체하기 위해 테이블 구조가 이전의 기본 테이블과 달라지지 않은 경우 뷰를 다시 사용할 수 있게 됩니다. 새 테이블이나 뷰 구조가 변경된 경우에는 뷰를 삭제하고 다시 만들어야 합니다.  
  
 SCHEMABINDING 절을 사용하여 뷰를 만들지 않은 경우 뷰의 기반이 되는 개체에 대한 변경 내용이 뷰의 정의에 영향을 주면 [sp_refreshview](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md)를 실행합니다. 그렇지 않으면 뷰를 쿼리할 때 예기치 않은 결과가 발생할 수 있습니다.  
  
 뷰를 만들면 뷰에 대한 정보가 [sys.views](../../relational-databases/system-catalog-views/sys-views-transact-sql.md), [sys.columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) 및 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 카탈로그 뷰에 저장됩니다. CREATE VIEW 문의 텍스트는 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 카탈로그 뷰에 저장됩니다.  
  
 **numeric** 또는 **float** 식으로 정의된 뷰에 인덱스를 사용하는 쿼리의 결과는 뷰에 인덱스를 사용하지 않는 유사한 쿼리와 다를 수 있습니다. 기본 테이블의 INSERT, DELETE 또는 UPDATE 동작 동안 발생하는 반올림 오류 때문에 이런 차이가 생길 수 있습니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 뷰가 만들어질 때 SET QUOTED_IDENTIFIER 및 SET ANSI_NULLS의 설정을 저장합니다. 이러한 원래 설정은 뷰를 사용할 때 뷰를 구문 분석하기 위해 사용되므로 뷰에 액세스할 때 SET QUOTED_IDENTIFIER 및 SET ANSI_NULLS의 클라이언트 세션 설정은 뷰 정의에 영향을 미치지 않습니다.  
  
## <a name="updatable-views"></a>업데이트할 수 있는 뷰  
 다음 조건이 만족되면 뷰를 통해 기본 테이블의 데이터를 수정할 수 있습니다.  
  
-   UPDATE, INSERT 및 DELETE 문을 비롯한 모든 수정은 하나의 기본 테이블에 있는 열만 참조해야 합니다.  
  
-   뷰에서 수정하는 열은 테이블 열에 있는 기본 데이터를 직접 참조해야 합니다. 다음과 같은 기타 방법으로 열이 파생되면 안 됩니다.  
  
    -   집계 함수: AVG, COUNT, SUM, MIN, MAX, GROUPING, STDEV, STDEVP, VAR 및 VARP  
  
    -   계산: 다른 열을 사용하는 식으로 열을 계산할 수 없습니다. 집합 연산자 UNION, UNION ALL, CROSSJOIN, EXCEPT 및 INTERSECT를 사용하여 구성한 열은 계산되지만 업데이트할 수 없습니다.  
  
-   수정하는 열이 GROUP BY, HAVING 또는 DISTINCT 절의 영향을 받지 않습니다.  
  
-   TOP는 위치에 관계없이 뷰의 *select_statement*에서 WITH CHECK OPTION 절과 함께 사용되지 않습니다.  
  
 이전의 제한이 뷰 자체에 적용되는 것과 마찬가지로 뷰의 FROM 절 하위 쿼리에 적용됩니다. 일반적으로 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 뷰 정의에서 특정 기본 테이블에 대해 이루어진 수정을 분명하게 추적할 수 있어야 합니다. 자세한 내용은 [뷰를 통해 데이터 수정](../../relational-databases/views/modify-data-through-a-view.md)을 참조하세요.  
  
 이전의 제한으로 인해 뷰를 통해 직접 데이터를 수정할 수 없는 경우 다음 방법을 사용하세요.  
  
-   **INSTEAD OF 트리거**  
  
     뷰를 업데이트할 수 있도록 뷰에 INSTEAD OF 트리거를 만들 수 있습니다. INSTEAD OF 트리거는 정의된 지점에서 데이터 수정 문 대신 실행됩니다. 이 트리거를 사용하면 데이터 수정 문을 처리할 일련의 동작을 지정할 수 있습니다. 따라서 특정 데이터 수정 문(INSERT, UPDATE 또는 DELETE)의 뷰에 INSTEAD OF 트리거가 있을 경우 문을 통해 해당 뷰를 업데이트할 수 있습니다. INSTEAD OF 트리거에 대한 자세한 내용은 [DML 트리거](../../relational-databases/triggers/dml-triggers.md)를 참조하세요.  
  
-   **분할 뷰**  
  
     뷰가 분할 뷰일 경우 특정 제한에 따라 뷰를 업데이트할 수 있습니다. 필요할 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 사용하고 있는 모든 테이블 및 뷰가 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 로컬 분할 뷰, 그리고 뷰의 테이블 중 하나 이상이 다른 서버나 원격 서버에 있는 분산형 분할 뷰로 구분합니다.  
  
## <a name="partitioned-views"></a>분할 뷰  
 분할 뷰란 구조가 같은 멤버 테이블이 UNION ALL로 정의되었으나 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 또는 연결된 데이터베이스 서버라고 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버의 자치 인스턴스 그룹에 여러 테이블로 따로 저장된 뷰입니다.  
  
> [!NOTE]  
>  데이터를 하나의 서버에 대해 로컬로 분할할 때는 분할된 테이블을 사용하는 것이 좋습니다. 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)을 참조하세요.  
  
 파티션 구성표를 디자인할 때 각 파티션에 포함할 데이터를 명확히 해야 합니다. 예를 들어 `Customers` 테이블의 데이터는 `Customers_33`에 있는 `Server1` 멤버 테이블, `Customers_66`에 있는 `Server2` 멤버 테이블 및 `Customers_99`에 있는 `Server3` 멤버 테이블의 세 위치에 분산되어 있습니다.  
  
 `Server1`의 분할 뷰는 다음과 같이 정의됩니다.  
  
```sql
--Partitioned view as defined on Server1  
CREATE VIEW Customers  
AS  
--Select from local member table.  
SELECT *  
FROM CompanyData.dbo.Customers_33  
UNION ALL  
--Select from member table on Server2.  
SELECT *  
FROM Server2.CompanyData.dbo.Customers_66  
UNION ALL  
--Select from member table on Server3.  
SELECT *  
FROM Server3.CompanyData.dbo.Customers_99;  
```  
  
 일반적으로 뷰의 형식이 다음과 같은 경우에 분할 뷰라고 합니다.  
  
```syntaxsql
SELECT <select_list1>  
FROM T1  
UNION ALL  
SELECT <select_list2>  
FROM T2  
UNION ALL  
...  
SELECT <select_listn>  
FROM Tn;  
```  
  
## <a name="conditions-for-creating-partitioned-views"></a>분할 뷰를 만들기 위한 조건  
  
1.  SELECT `list`  
  
    -   뷰 정의의 열 목록에서 멤버 테이블의 모든 열을 선택합니다.  
  
    -   각 `select list`의 같은 서수 위치에 있는 열은 데이터 정렬 등의 형식이 같아야 합니다. UNION의 경우와 같이 일반적으로 열이 암시적으로 변환할 수 있는 형식인 것으로는 충분하지 않습니다.  
  
         또한 적어도 하나 이상의 열(예: `<col>`)이 같은 서수 위치에 있는 모든 SELECT 목록에 표시되어야 합니다. 멤버 테이블 `T1, ..., Tn`에서 CHECK 제약 조건 `C1, ..., Cn`이 각각 `<col>`에 정의되는 것과 같이 `<col>`을 정의합니다.  
  
         `C1` 테이블에 정의되는 `T1` 제약 조건은 다음 형식을 따라야 합니다.  
  
        ```syntaxsql
        C1 ::= < simple_interval > [ OR < simple_interval > OR ...]  
        < simple_interval > :: =   
        < col > { < | > | \<= | >= | = < value >}   
        | < col > BETWEEN < value1 > AND < value2 >  
        | < col > IN ( value_list )  
        | < col > { > | >= } < value1 > AND  
        < col > { < | <= } < value2 >  
        ```
  
    -   제약 조건은 `<col>`의 지정된 값이 모두 `C1, ..., Cn` 제약 조건을 최대 하나까지 만족시켜 제약 조건이 결합되지 않거나 겹치지 않는 일련의 간격을 구성하도록 해야 합니다. 결합되지 않은 제약 조건이 정의된 `<col>` 열을 분할 열이라고 합니다. 분할 열 이름은 기본 테이블에 있는 이름과 다를 수 있습니다. 앞에서 언급한 분할 열의 조건을 만족시키려면 제약 조건이 활성화되어 트러스트된 상태여야 합니다. 제약 조건이 해제되면 ALTER TABLE의 CHECK CONSTRAINT *constraint_name* 옵션을 사용하고 WITH CHECK 옵션으로 제약 조건의 유효성을 검사하여 제약 조건 검사를 다시 설정하세요.  
  
         다음 예에서는 올바른 제약 조건 집합을 보여 줍니다.  
  
        ```syntaxsql
        { [col < 10], [col between 11 and 20] , [col > 20] }  
        { [col between 11 and 20], [col between 21 and 30], [col between 31 and 100] }  
        ```  
  
    -   SELECT 목록에 같은 열을 여러 번 사용할 수 없습니다.  
  
2.  분할 열  
  
    -   분할 열은 테이블에 있는 PRIMARY KEY의 일부입니다.  
  
    -   분할 열은 계산 열, ID 열, 기본 열 또는 **timestamp** 열이 될 수 없습니다.  
  
    -   멤버 테이블의 동일한 열에 제약 조건이 둘 이상 있는 경우에는 데이터베이스 엔진에서 뷰가 분할 뷰인지 여부를 결정할 때 모든 제약 조건을 고려하지 않고 무시합니다. 분할 뷰의 조건을 만족하려면 분할 열에 분할 제약 조건이 하나만 있어야 합니다.  
  
    -   분할 열의 업데이트 가능성에는 제한이 없습니다.  
  
3.  멤버 테이블 또는 기본 테이블 `T1, ..., Tn`  
  
    -   테이블은 4부분으로 된 이름 또는 OPENDATASOURCE나 OPENROWSET 기반 이름을 통해 참조되며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 다른 컴퓨터의 로컬 테이블 또는 테이블이 될 수 있습니다. OPENDATASOURCE 및 OPENROWSET 구문은 테이블 이름을 지정할 수 있으나 통과 쿼리는 지정할 수 없습니다. 자세한 내용은 [OPENDATASOURCE&#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md) 및 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)을 참조하세요.  
  
         하나 이상의 멤버 테이블이 원격이면 뷰를 분산형 분할 뷰라고 하며 추가 조건이 적용됩니다. 자세한 내용은 이 섹션의 뒷부분에서 설명합니다.  
  
    -   UNION ALL 문과 결합된 테이블 집합에 같은 테이블을 두 번 표시할 수 없습니다.  
  
    -   멤버 테이블은 테이블의 계산 열에 대해 만들어진 인덱스를 가질 수 없습니다.  
  
    -   멤버 테이블은 같은 수의 열에 모두 PRIMARY KEY 제약 조건이 있습니다.  
  
    -   뷰에 있는 모든 멤버 테이블의 ANSI 패딩 설정이 같습니다. **sp_configure**에 **user options** 옵션을 사용하거나 SET 문을 사용하여 설정할 수 있습니다.  
  
## <a name="conditions-for-modifying-data-in-partitioned-views"></a>분할된 뷰의 데이터를 수정하기 위한 조건  
 분할된 뷰의 데이터를 수정하는 문에는 다음 제한이 적용됩니다.  
  
-   기본 멤버 테이블에 이러한 열에 대한 DEFAULT 제약 조건이 있거나 Null 값을 허용해도 INSERT 문은 뷰의 모든 열에 대해 값을 제공합니다. DEFAULT 정의가 있는 멤버 테이블 열의 경우에는 문에 DEFAULT 키워드를 명시적으로 사용할 수 없습니다.  
  
-   분할 열에 삽입되는 값은 적어도 하나 이상의 기본 제약 조건을 만족합니다. 그렇지 않으면 제약 조건을 위반하여 INSERT 동작이 실패합니다.  
  
-   해당 멤버 테이블에 정의된 DEFAULT 값이 열에 포함되어 있어도 UPDATE 문은 SET 절에서 DEFAULT 키워드를 값으로 지정할 수 없습니다.  
  
-   하나 이상의 멤버 테이블에 ID 열이 있는 뷰의 열은 INSERT 또는 UPDATE 문을 사용하여 수정할 수 없습니다.  
  
-   멤버 테이블 중 하나에 **timestamp** 열이 포함되어 있으면 INSERT 또는 UPDATE 문을 사용하여 데이터를 수정할 수 없습니다.  
  
-   멤버 테이블 중 하나에 트리거나 ON UPDATE CASCADE/SET NULL/SET DEFAULT 또는 ON DELETE CASCADE/SET NULL/SET DEFAULT 제약 조건이 있으면 뷰를 수정할 수 없습니다.  
  
-   문에 멤버 테이블 또는 같은 뷰와 자체 조인이 있으면 분할 뷰에 대해 INSERT, UPDATE 및 DELETE 동작을 수행할 수 없습니다.  
  
-   **bcp** 또는 BULK INSERT 및 INSERT ... SELECT * FROM OPENROWSET(BULK...) 문은 분할 뷰로 데이터를 대량 가져오는 것을 지원하지 않습니다. 그러나 [INSERT](../../t-sql/statements/insert-transact-sql.md) 문을 사용하여 분할된 뷰에 여러 행을 삽입할 수 있습니다.  
  
    > [!NOTE]  
    >  분할 뷰를 업데이트하려면 사용자에게 멤버 테이블에 대한 INSERT, UPDATE 및 DELETE 권한이 있어야 합니다.  
  
## <a name="additional-conditions-for-distributed-partitioned-views"></a>분산형 분할 뷰에 대한 추가 조건  
 분산형 분할 뷰(하나 이상의 멤버 테이블이 원격일 때)의 경우 다음 추가 조건이 적용됩니다.  
  
-   업데이트의 영향을 받는 모든 노드에서 원자성을 보장하기 위해 분산 트랜잭션이 시작됩니다.  
  
-   작업할 INSERT, UPDATE 또는 DELETE 문에 대해 XACT_ABORT SET 옵션을 ON으로 설정합니다.  
  
-   분할 뷰에서 참조되는 **smallmoney** 형식의 원격 테이블 열은 **money**로 매핑됩니다. 따라서 로컬 테이블의 해당 열(SELECT 목록의 동일한 서수 위치에 있는 열)도 **money** 형식이어야 합니다.  
  
-   데이터베이스 호환성 수준 110 이상에서는 분할 뷰에서 참조되는 **smalldatetime** 형식의 원격 테이블 열이 **smalldatetime**으로 매핑됩니다. 로컬 테이블의 해당 열(SELECT 목록의 동일한 서수 위치에 있는 열)은 **smalldatetime**이어야 합니다. 이 동작은 분할 뷰에서 참조되는 **smalldatetime** 형식의 원격 테이블 열이 **datetime**으로 매핑되고 로컬 테이블의 해당 열이 **datetime** 형식이어야 하는 이전 버전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 동작에서 달라진 점입니다. 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  
  
-   분할 뷰의 연결된 서버는 루프백 연결 서버가 될 수 없습니다. 이 서버는 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 가리키는 연결된 서버입니다.  
  
 업데이트할 수 있는 분할 뷰 및 원격 테이블과 관련된 INSERT, UPDATE 및 DELETE 동작에 대해서는 SET ROWCOUNT 옵션의 설정이 무시됩니다.  
  
 멤버 테이블 및 분할 뷰 정의가 지정되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 쿼리를 효율적으로 사용하는 지능적 계획을 수립하여 멤버 테이블의 데이터에 액세스합니다. 쿼리 프로세서는 CHECK 제약 조건 정의를 사용하여 멤버 테이블에 키 값의 배포를 매핑합니다. 사용자가 쿼리를 실행하면 쿼리 프로세서가 WHERE 절에 지정된 값에 대한 매핑과 비교한 다음 멤버 서버 간 데이터 전송량을 최소화하도록 실행 계획을 수립합니다. 따라서 일부 멤버 테이블이 원격 서버에 있더라도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 분산 쿼리를 확인하여 전송할 분산 데이터의 양을 최소화할 수 있습니다.  
  
## <a name="considerations-for-replication"></a>복제 고려 사항  
 복제와 관련된 멤버 테이블에 분할 뷰를 만들려면 다음을 고려해야 합니다.  
  
-   기본 테이블이 업데이트 구독이 있는 트랜잭션 복제 또는 병합 복제와 관련된 경우에는 **uniqueidentifier** 열도 SELECT 목록에 포함되어야 합니다. 
  
     분할 뷰에 대한 INSERT 동작은 **uniqueidentifier** 열에 대해 NEWID() 값을 제공해야 합니다. **uniqueidentifier** 열에 대한 UPDATE 동작은 DEFAULT 키워드를 사용할 수 없으므로 NEWID()를 값으로 제공해야 합니다.  
  
-   뷰를 사용하여 수행된 업데이트의 복제는 서로 다른 두 데이터베이스에서 테이블이 복제될 때와 동일합니다. 서로 다른 복제 에이전트에서 테이블을 제공하며 업데이트 순서는 보장되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에는 CREATE VIEW 권한이 필요하고 뷰를 만들 구성표에는 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예제  

이 예에서는 AdventureWorks 2012 또는 AdventureWorksDW 데이터베이스를 사용합니다.  

### <a name="a-using-a-simple-create-view"></a>A. 간단한 CREATE VIEW 사용  
 다음 예에서는 간단한 `SELECT` 문을 사용하여 뷰를 만듭니다. 간단한 뷰는 열 조합을 자주 쿼리할 때 유용합니다. 이 뷰의 데이터는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `HumanResources.Employee` 및 `Person.Person` 테이블에 있습니다. 이 데이터는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]의 직원 이름과 채용 날짜 정보를 제공합니다. 입사일 추적 담당자에게 이 테이블의 모든 데이터에 액세스할 권한을 주지 않아도 해당 뷰를 만들 수 있습니다.  
  
```sql
CREATE VIEW hiredate_view  
AS   
SELECT p.FirstName, p.LastName, e.BusinessEntityID, e.HireDate  
FROM HumanResources.Employee e   
JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID ;  
GO  
  
```  
  
### <a name="b-using-with-encryption"></a>B. WITH ENCRYPTION 사용  
 다음 예에서는 `WITH ENCRYPTION` 옵션을 사용하여 계산 열, 이름이 바뀐 열 및 복수 열을 보여 줍니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
```sql
CREATE VIEW Purchasing.PurchaseOrderReject  
WITH ENCRYPTION  
AS  
SELECT PurchaseOrderID, ReceivedQty, RejectedQty,   
    RejectedQty / ReceivedQty AS RejectRatio, DueDate  
FROM Purchasing.PurchaseOrderDetail  
WHERE RejectedQty / ReceivedQty > 0  
AND DueDate > CONVERT(DATETIME,'20010630',101) ;  
GO  
  
```  
  
### <a name="c-using-with-check-option"></a>C. WITH CHECK OPTION 사용  
 다음 예에서는 5개의 테이블을 참조하고 데이터 수정을 허용하여 시애틀에 사는 직원에게만 적용하는 `SeattleOnly`라는 뷰를 보여 줍니다.  
  
```sql
CREATE VIEW dbo.SeattleOnly  
AS  
SELECT p.LastName, p.FirstName, e.JobTitle, a.City, sp.StateProvinceCode  
FROM HumanResources.Employee e  
INNER JOIN Person.Person p  
ON p.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN Person.BusinessEntityAddress bea   
    ON bea.BusinessEntityID = e.BusinessEntityID   
    INNER JOIN Person.Address a   
    ON a.AddressID = bea.AddressID  
    INNER JOIN Person.StateProvince sp   
    ON sp.StateProvinceID = a.StateProvinceID  
WHERE a.City = 'Seattle'  
WITH CHECK OPTION ;  
GO  
```  
  
### <a name="d-using-built-in-functions-within-a-view"></a>D. 뷰에서 기본 제공 함수 사용  
 다음 예에서는 기본 제공 함수를 포함하는 뷰 정의를 보여 줍니다. 함수를 사용할 때는 파생 열의 열 이름을 지정해야 합니다.  
  
```sql
CREATE VIEW Sales.SalesPersonPerform  
AS  
SELECT TOP (100) SalesPersonID, SUM(TotalDue) AS TotalSales  
FROM Sales.SalesOrderHeader  
WHERE OrderDate > CONVERT(DATETIME,'20001231',101)  
GROUP BY SalesPersonID;  
GO  

```  
  
### <a name="e-using-partitioned-data"></a>E. 분할된 데이터 사용  
 다음 예에서는 `SUPPLY1`, `SUPPLY2`, `SUPPLY3` 및 `SUPPLY4` 테이블을 사용합니다. 이러한 테이블은 서로 다른 국가/지역에 있는 4개 사무실의 공급자 테이블입니다.  
  
```sql
--Create the tables and insert the values.  
CREATE TABLE dbo.SUPPLY1 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 1 and 150),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY2 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 151 and 300),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY3 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 301 and 450),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY4 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 451 and 600),  
supplier CHAR(50)  
);  
GO  
--Create the view that combines all supplier tables.  
CREATE VIEW dbo.all_supplier_view  
WITH SCHEMABINDING  
AS  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY1  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY2  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY3  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY4;  
GO
INSERT dbo.all_supplier_view VALUES ('1', 'CaliforniaCorp'), ('5', 'BraziliaLtd')    
, ('231', 'FarEast'), ('280', 'NZ')  
, ('321', 'EuroGroup'), ('442', 'UKArchip')  
, ('475', 'India'), ('521', 'Afrique');  
GO  
```  
  
## <a name="examples-sssdw-and-sspdw"></a>예: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-creating-a-simple-view"></a>F. 간단한 뷰 만들기  
 다음 예는 원본 테이블에서 일부 열만 선택하여 뷰를 만듭니다.  
  
```sql
CREATE VIEW DimEmployeeBirthDates AS  
SELECT FirstName, LastName, BirthDate   
FROM DimEmployee;  
```  
  
### <a name="g-create-a-view-by-joining-two-tables"></a>G. 두 테이블을 조인하여 뷰 만들기  
 다음 예에서는 `OUTER JOIN`이 있는 `SELECT` 문을 사용하여 뷰를 만듭니다. 조인 쿼리의 결과가 뷰를 채웁니다.  
  
```sql
CREATE VIEW view1  
AS 
SELECT fis.CustomerKey, fis.ProductKey, fis.OrderDateKey, 
  fis.SalesTerritoryKey, dst.SalesTerritoryRegion  
FROM FactInternetSales AS fis   
LEFT OUTER JOIN DimSalesTerritory AS dst   
ON (fis.SalesTerritoryKey=dst.SalesTerritoryKey);  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [DROP VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [저장 프로시저 만들기](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [sys.dm_sql_referenced_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_refreshview&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md)   
 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sys.views&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

