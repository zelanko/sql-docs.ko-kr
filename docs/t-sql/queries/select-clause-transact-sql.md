---
title: SELECT 절(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SELECT Clause
- SELECT_Clause_TSQL
- DISTINCT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- parentheses [SQL Server]
- identity columns [SQL Server], SELECT clause
- SELECT clause
- $IDENTITY keyword
- user-defined types [SQL Server], invoking methods and properties
- SELECT statement [SQL Server], processing orders
- clauses [SQL Server], SELECT
- $ROWGUID keyword
- queries [SQL Server], results
ms.assetid: 2616d800-4853-4cf1-af77-d32d68d8c2ef
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 47d4c1eea37f8c9edbba8bfdd9712a27cd0f0f0f
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554436"
---
# <a name="select-clause-transact-sql"></a>SELECT 절(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  쿼리에서 열을 반환하도록 지정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
SELECT [ ALL | DISTINCT ]  
[ TOP ( expression ) [ PERCENT ] [ WITH TIES ] ]   
<select_list>   
<select_list> ::=   
    {   
      *   
      | { table_name | view_name | table_alias }.*   
      | {  
          [ { table_name | view_name | table_alias }. ]  
               { column_name | $IDENTITY | $ROWGUID }   
          | udt_column_name [ { . | :: } { { property_name | field_name }   
            | method_name ( argument [ ,...n] ) } ]  
          | expression  
          [ [ AS ] column_alias ]   
         }  
      | column_alias = expression   
    } [ ,...n ]   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 **ALL**  
 결과 집합에 중복 행을 표시할 수 있도록 지정합니다. 기본값은 ALL입니다.  
  
 DISTINCT  
 결과 집합에 고유한 행만 표시하도록 지정합니다. Null 값은 용도 면에서 DISTINCT 키워드와 동등한 것으로 간주됩니다.  
  
 TOP (*expression* ) [ PERCENT ] [ WITH TIES ]  
 지정한 첫 번째 집합 또는 비율만큼의 행만 쿼리 결과 집합에서 반환될 것임을 나타냅니다. *expression* 은 행의 수 또는 비율일 수 있습니다.  
  
 이전 버전과의 호환성을 위해 SELECT 문에서 괄호 없이 TOP *expression*을 사용할 수 있지만 권장되지는 않습니다. 자세한 내용은 [TOP&#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)을 참조하세요.  
  
\< select_list > 결과 집합에 대해 선택할 열입니다. 선택 목록은 쉼표로 구분된 일련의 식입니다. 선택 목록에 지정할 수 있는 식의 최대 수는 4096개입니다.  
  
 \*  
 FROM 절에서 모든 테이블과 뷰에 있는 모든 열이 반환되도록 지정합니다. 열은 FROM 절에서 지정된 대로 테이블 또는 뷰에 존재하는 순서대로 테이블이나 뷰에서 반환됩니다.  
  
 *table_name* | *view_name* | *table*_*alias*.*  
 \*의 범위를 지정된 테이블 또는 뷰로 제한합니다.  
  
 *column_name*  
 반환할 열의 이름입니다. *column_name*을 한정하여 FROM 절의 두 테이블에 이름이 중복된 열이 있는 경우와 같이 모호한 참조가 발생하지 않도록 방지합니다. 예를 들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 SalesOrderHeader 및 SalesOrderDetail 테이블 모두에 ModifiedDate라는 열이 있습니다. 두 테이블이 한 쿼리에 조인된 경우 선택 목록에서 SalesOrderDetail 항목의 수정된 날짜를 SalesOrderDetail.ModifiedDate와 같이 지정할 수 있습니다.  
  
 *expression*  
 상수, 함수, 연산자로 연결된 열 이름, 상수 및 함수의 모든 조합 또는 하위 쿼리입니다.  
  
 $IDENTITY  
 ID 열을 반환합니다. 자세한 내용은 [IDENTITY&#40;속성&#41;&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md), [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) 및 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.  
  
 FROM 절에서 둘 이상의 테이블에 IDENTITY 속성을 포함한 열이 있는 경우 T1.$IDENTITY와 같은 특정 테이블 이름으로 $IDENTITY를 한정해야 합니다.  
  
 $ROWGUID  
 행 GUID 열을 반환합니다.  
  
 FROM 절에서 둘 이상의 테이블에 ROWGUIDCOL 속성이 있는 경우 T1.$ROWGUID와 같은 특정 테이블 이름으로 $ROWGUID를 한정해야 합니다.  
  
 *udt_column_name*  
 반환할 CLR(공용 언어 런타임) 사용자 정의 형식 열의 이름입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]는 사용자 정의 형식 값을 이진 표현으로 반환합니다. 사용자 정의 형식 값을 문자열 또는 XML 형식으로 반환하려면 [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) 또는 [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md)를 사용하세요.  
  
 { . | :: }  
 CLR 사용자 정의 형식의 메서드, 속성 또는 필드를 지정합니다. 인스턴스(비정적) 메서드, 속성 또는 필드에 대해 .를 사용하고, 정적 메서드, 속성 또는 필드에 대해서는 ::을 사용합니다. CLR 사용자 정의 형식의 메서드, 속성 또는 필드를 호출하려면 해당 형식에 대해 EXECUTE 권한이 있어야 합니다.  
  
 *property_name*  
 *udt_column_name*의 공용 속성입니다.  
  
 *field_name*  
 *udt_column_name*의 공용 데이터 멤버입니다.  
  
 *method_name*  
 하나 이상의 인수를 사용하는 *udt_column_name*의 공용 메서드입니다. *method_name*은 변경자(mutator) 메서드가 될 수 없습니다.  
  
 다음 예에서는 `Location`라는 메서드를 호출하여 `point` 테이블에서 `Cities` 형식으로 정의되는 `Distance` 열에 대한 값을 선택하는 방법을 보여 줍니다.  
  
```  
CREATE TABLE dbo.Cities (  
     Name varchar(20),  
     State varchar(20),  
     Location point );  
GO  
DECLARE @p point (32, 23), @distance float;  
GO  
SELECT Location.Distance (@p)  
FROM Cities;  
```  
  
 *column_ alias*  
 쿼리 결과 집합에서 열 이름을 대신하는 대체 이름입니다. 예를 들어 quantity라는 열에 Quantity, Quantity to Date 또는 Qty와 같은 별칭을 지정할 수 있습니다.  
  
 별칭은 식의 결과에 이름을 지정하는 데도 사용됩니다. 다음 예를 참조하세요.  
  
 ```sql
 USE AdventureWorks2012;  
 GO  
 SELECT AVG(UnitPrice) AS [Average Price]  
 FROM Sales.SalesOrderDetail;
 ```  
  
 *column_alias*는 ORDER BY 절에는 사용할 수 있지만, WHERE, GROUP BY 또는 HAVING 절에서는 사용할 수 없습니다. 쿼리 식이 DECLARE CURSOR 문의 일부인 경우 *column_alias*는 FOR UPDATE 절에서 사용할 수 없습니다.  
  
## <a name="remarks"></a>설명  
 SELECT 목록에 포함된 **text** 또는 **ntext** 열에 대해 반환되는 데이터의 길이는 **text** 열의 실제 크기, 기본 TEXTSIZE 세션 설정 또는 하드 코딩된 애플리케이션 제한 중에서 가장 작은 값으로 설정됩니다. 세션에 대해 반환되는 텍스트의 길이를 변경하려면 SET 문을 사용하세요. 기본적으로 하나의 SELECT 문이 반환하는 텍스트 데이터의 길이 제한은 4,000바이트입니다.  
  
 다음 동작 중 하나를 시도하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 예외 511을 발생시키고 현재 실행 중인 문을 롤백합니다.  
  
-   SELECT 문에서 8,060바이트를 넘는 결과 행이나 중간 작업 테이블 행을 생성합니다.  
  
-   DELETE, INSERT 또는 UPDATE 문에서 8,060바이트를 넘는 행에 동작을 시도합니다.  
  
 SELECT INTO 또는 CREATE VIEW 문으로 만든 열에 열 이름을 지정하지 않으면 오류가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SELECT 예제&#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
