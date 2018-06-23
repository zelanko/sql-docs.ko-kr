---
title: 인덱싱된 뷰 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-views
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- indexed views [SQL Server], creating
- clustered indexes, views
- CREATE INDEX statement
- large_value_types_out_of_row option
- indexed views [SQL Server]
- views [SQL Server], indexed views
ms.assetid: f86dd29f-52dd-44a9-91ac-1eb305c1ca8d
caps.latest.revision: 77
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5498cda83c3b33d0f6b3c6898954e1442e6e21cc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36171921"
---
# <a name="create-indexed-views"></a>인덱싱된 뷰 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 인덱싱된 뷰를 만드는 방법에 대해 설명합니다. 뷰에 만들어지는 첫 번째 인덱스는 고유 클러스터형 인덱스여야 합니다. 고유 클러스터형 인덱스가 만들어진 후에 비클러스터형 인덱스를 더 만들 수 있습니다. 뷰에 고유 클러스터형 인덱스를 만들면 클러스터형 인덱스가 있는 테이블의 저장 방식과 마찬가지로 데이터베이스에 뷰가 저장되므로 쿼리 성능이 향상됩니다. 쿼리 최적화 프로그램은 인덱싱된 뷰를 사용하여 쿼리 실행 속도를 높일 수 있습니다. 최적화 프로그램이 인덱싱된 뷰를 대신 사용하므로 쿼리에서 해당 뷰를 참조할 필요가 없습니다.  
  
  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 다음 단계는 인덱싱된 뷰를 만들고 성공적으로 구현하는 데 필요합니다.  
  
1.  뷰에 참조될 기존의 모든 테이블에 대해 SET 옵션이 올바른지 확인합니다.  
  
2.  테이블 및 뷰를 만들기 전에 세션에 SET 옵션이 올바르게 설정되어 있는지 확인합니다.  
  
3.  뷰 정의가 결정적인지 확인합니다.  
  
4.  WITH SCHEMABINDING 옵션을 사용하여 뷰를 만듭니다.  
  
5.  뷰에 고유 클러스터형 인덱스를 만듭니다.  
  
###  <a name="Restrictions"></a> 인덱싱된 뷰에 필요한 SET 옵션  
 쿼리가 실행될 때 다른 SET 옵션이 활성화되어 있으면 같은 식을 계산해도 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 다른 결과가 나올 수 있습니다. 예를 들어 SET 옵션 CONCAT_NULL_YIELDS_NULL이 ON으로 설정된 후 식 **'** abc **'** + NULL의 결과로 NULL 값이 반환됩니다. 그러나 CONCAT_NULL_YIEDS_NULL을 OFF로 설정한 후 같은 식의 결과는 **'** abc **'** 가 됩니다.  
  
 뷰를 올바르게 유지하고 일관된 결과를 반환하게 하려면 인덱싱된 뷰는 몇 가지 SET 옵션에 대해 고정 값이 필요합니다. 다음 표의 SET 옵션에 나와 있는 값으로 설정 해야 합니다는 **RequiredValue** 열은 다음 상황이 발생할 때마다:  
  
-   뷰와 뷰의 후속 인덱스가 생성됩니다.  
  
-   테이블을 만들 때 뷰에서 참조되는 기본 테이블입니다.  
  
-   인덱싱된 뷰에 참가하는 테이블에서 삽입, 업데이트 또는 삭제 작업이 수행됩니다. 이 요구 사항에는 대량 복사, 복제, 분산 쿼리 등의 작업이 포함됩니다.  
  
-   쿼리 최적화 프로그램에서 인덱싱된 뷰를 사용하여 쿼리 계획을 만듭니다.  
  
    |Set 옵션|필요한 값|기본 서버 값|Default<br /><br /> OLE DB 및 ODBC 값|Default<br /><br /> DB-Library 값|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|  
  
     *ANSI_WARNINGS를 ON으로 설정하면 암시적으로 ARITHABORT가 ON으로 설정됩니다.  
  
 OLE DB 또는 ODBC 서버 연결을 사용하는 경우 수정해야 하는 유일한 값은 ARITHABORT 설정입니다. 모든 DB-Library 값은 **sp_configure** 를 사용하여 서버 수준에서 또는 SET 명령을 사용하여 응용 프로그램에서 올바르게 설정해야 합니다.  
  
> [!IMPORTANT]  
>  서버의 데이터베이스에서 계산 열에 첫 번째로 인덱싱된 뷰 또는 인덱스가 만들어지면 바로 서버 차원에서 ARITHABORT 사용자 옵션을 ON으로 설정하는 것이 좋습니다.  
  
### <a name="deterministic-views"></a>결정적 뷰  
 인덱싱된 뷰의 정의는 결정적이어야 합니다. WHERE 및 GROUP BY 절뿐만 아니라 SELECT 목록의 모든 식이 결정적이면 뷰가 결정적입니다. 결정적 식은 특정 입력 값 집합을 사용하여 계산될 때마다 항상 같은 결과를 반환합니다. 결정적 함수만 결정적 식에 참여할 수 있습니다. 예를 들어 DATEADD 함수는 세 매개 변수에 지정된 인수 값 집합에 대해 항상 같은 결과를 반환하므로 결정적 함수입니다. GETDATE는 항상 같은 인수로 호출되지만 실행될 때마다 반환하는 값이 바뀌므로 비결정적 함수입니다.  
  
 뷰 열이 결정적인지 여부를 확인하려면 **COLUMNPROPERTY** 함수의 [IsDeterministic](/sql/t-sql/functions/columnproperty-transact-sql) 속성을 사용합니다. 스키마 바인딩되어 있는 뷰의 결정적 열이 정확한지 여부를 확인하려면 COLUMNPROPERTY 함수의 **IsPrecise** 속성을 사용합니다. COLUMNPROPERTY는 TRUE이면 1을 반환하고 FALSE이면 0을 반환하며 입력이 잘못되면 NULL을 반환합니다. 이는 해당 열이 비결정적이거나 정확하지 않음을 의미합니다.  
  
 식이 결정적인 경우에도 float 식이 포함되어 있으면 정확한 결과는 프로세서 아키텍처 또는 마이크로코드 버전에 따라 달라질 수 있습니다. 데이터 무결성을 보장하기 위해 이런 식은 인덱싱된 뷰의 키가 아닌 열로만 참여할 수 있습니다. float 식이 없는 결정적 식을 정확하다고 합니다. 정확한 결정적 식만 인덱싱된 뷰의 WHERE 또는 GROUP BY 절과 키 열에 참여할 수 있습니다.  
  
### <a name="additional-requirements"></a>추가 요구 사항  
 SET 옵션 및 결정적 함수 요구 사항 외에 다음 요구 사항을 충족해야 합니다.  
  
-   CREATE INDEX를 실행하는 사용자는 뷰의 소유자여야 합니다.  
  
-   인덱스를 만들 때 IGNORE_DUP_KEY 옵션은 OFF(기본 설정)로 설정되어야 합니다.  
  
-   테이블은 뷰 정의에서 *schema ***.*** tablename* 처럼 두 부분으로 구성된 이름으로 참조되어야 합니다.  
  
-   뷰에서 참조하는 사용자 정의 함수는 WITH SCHEMABINDING 옵션을 사용하여 만들어야 합니다.  
  
-   뷰에서 참조하는 사용자 정의 함수는 두 부분으로 구성된 이름인 *schema ***.*** function*으로 참조되어야 합니다.  
  
-   사용자 정의 함수의 데이터 액세스 속성은 NO SQL이어야 하고 외부 액세스 속성은 NO여야 합니다.  
  
-   CLR(공용 언어 런타임) 함수는 뷰의 SELECT 목록에 표시될 수 있지만 클러스터형 인덱스 키 정의의 일부일 수는 없습니다. CLR 함수는 뷰의 WHERE 절이나 뷰에서 JOIN 연산의 ON 절에 표시되지 않습니다.  
  
-   뷰 정의에서 사용된 CLR 사용자 정의 형식의 메서드 및 CLR 함수의 속성을 다음 표와 같이 설정해야 합니다.  
  
    |속성|참고|  
    |--------------|----------|  
    |DETERMINISTIC = TRUE|Microsoft .NET Framework 메서드의 특성으로 명시적으로 선언되어야 합니다.|  
    |PRECISE = TRUE|.NET Framework 메서드의 특성으로 명시적으로 선언되어야 합니다.|  
    |DATA ACCESS = NO SQL|DataAccess 특성을 DataAccessKind.None으로 설정하고 SystemDataAccess 특성을 SystemDataAccessKind.None으로 설정함으로써 결정됩니다.|  
    |EXTERNAL ACCESS = NO|CLR 루틴의 경우 이 속성의 기본값은 NO입니다.|  
  
-   뷰는 WITH SCHEMABINDING 옵션을 사용하여 만들어야 합니다.  
  
-   뷰는 뷰와 동일한 데이터베이스의 기본 테이블만 참조해야 합니다. 뷰는 다른 뷰를 참조할 수 없습니다.  
  
-   뷰 정의의 SELECT 문에는 다음 Transact-SQL 요소가 포함되지 않아야 합니다.  
  
    ||||  
    |-|-|-|  
    |COUNT|ROWSET 함수(OPENDATASOURCE, OPENQUERY, OPENROWSET 및 OPENXML)|OUTER 조인(LEFT, RIGHT 또는 FULL)|  
    |파생 테이블(FROM 절에서 SELECT 문을 지정하여 정의)|자체 조인|SELECT \* 또는 SELECT *table_name*을 사용하여 열 지정*|  
    |DISTINCT|STDEV, STDEVP, VAR, VARP 또는 AVG|CTE(공통 테이블 식)|  
    |`float`\*`text`, `ntext`, `image`, `XML`, 또는 `filestream` 열|하위 쿼리|순위 함수 또는 집계 창 함수를 포함하는 OVER 절|  
    |전체 텍스트 조건자(CONTAIN, FREETEXT)|Null 허용 식을 참조하는 SUM 함수|ORDER BY|  
    |CLR 사용자 정의 집계 함수|맨 위로 이동|CUBE, ROLLUP 또는 GROUPING SETS 연산자|  
    |MIN, MAX|UNION, EXCEPT 또는 INTERSECT 연산자|TABLESAMPLE|  
    |테이블 변수|OUTER APPLY 또는 CROSS APPLY|PIVOT, UNPIVOT|  
    |스파스 열 집합|인라인 또는 다중 문 테이블 반환 함수|OFFSET|  
    |CHECKSUM_AGG|||  
  
     \*인덱싱된 뷰에 포함 될 수 있습니다 `float` 열; 그러나 클러스터형된 인덱스 키에 이러한 열을 포함할 수 없습니다.  
  
-   GROUP BY가 있는 경우 VIEW 정의는 COUNT_BIG(*)을 포함해야 하며 HAVING은 포함할 수 없습니다. 이러한 GROUP BY 제약 조건은 인덱싱된 뷰 정의에만 적용됩니다. 쿼리는 이러한 GROUP BY 제약 조건을 충족하지 않는 경우에도 실행 계획에 인덱싱된 뷰를 사용할 수 있습니다.  
  
-   뷰 정의에 GROUP BY 절이 들어 있으면 고유 클러스터형 인덱스의 키는 GROUP BY 절에 지정된 열만 참조할 수 있습니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
 인덱싱된 뷰의 `datetime` 및 `smalldatetime` 문자열 리터럴을 참조할 때 결정적 날짜 형식 스타일을 사용하여 리터럴을 원하는 날짜 유형으로 명시적으로 변환하는 것이 좋습니다. 결정적 날짜 형식 스타일 목록은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)를 참조하세요. 문자열을 암시적으로 변환 작업과 관련 된 식은 `datetime` 또는 `smalldatetime` 비 결정적인 것으로 간주 됩니다. 이는 서버 세션의 LANGUAGE 및 DATEFORMAT 설정에 따라 결과가 달라지기 때문입니다. 예를 들어 ' `CONVERT (datetime, '30 listopad 1996', 113)` ' 문자열이 다른 언어에서는 다른 월을 의미하므로`listopad`식의 결과는 LANGUAGE 설정에 따라 달라집니다. 마찬가지로 `DATEADD(mm,3,'2000-12-01')`식에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 DATEFORMAT 설정을 기준으로 `'2000-12-01'` 문자열을 해석합니다.  
  
 데이터 정렬 간의 비유니코드 문자 데이터를 암시적으로 변환하는 작업도 비결정적인 것으로 간주됩니다.  
  
###  <a name="Considerations"></a> 고려 사항  
 인덱싱된 뷰의 열에 대한 **large_value_types_out_of_row** 옵션의 설정은 기본 테이블의 해당 열에 대한 설정에서 상속됩니다. 이 값은 [sp_tableoption](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql)을 통해 설정됩니다. 식으로부터 구성된 열의 기본 설정은 0으로서 큰 값 유형이 행 내부에 저장됨을 의미합니다.  
  
 인덱싱된 뷰는 분할된 테이블에서 만들 수 있으며 자신이 분할될 수 있습니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 인덱싱된 뷰를 사용하지 않게 하려면 쿼리에 OPTION (EXPAND VIEW) 힌트를 포함합니다. 또한 위에 표시된 옵션을 하나라도 잘못 설정하면 최적화 프로그램에서 뷰의 인덱스를 사용할 수 없게 됩니다. OPTION (EXPAND VIEW) 힌트에 대한 자세한 내용은 [SELECT&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)를 참조하세요.  
  
 뷰가 삭제되면 뷰에 있는 모든 인덱스도 삭제됩니다. 클러스터형 인덱스가 삭제되면 뷰의 모든 비클러스터형 인덱스 및 자동 생성된 통계가 삭제됩니다. 사용자가 만든 뷰의 통계는 유지됩니다. 비클러스터형 인덱스는 개별적으로 삭제될 수 있습니다. 뷰에서 클러스터형 인덱스를 삭제하면 저장된 결과 집합도 삭제되고 최적화 프로그램이 표준 뷰와 같은 뷰의 처리 단계로 되돌아갑니다.  
  
 테이블 및 뷰의 인덱스를 비활성화할 수 있습니다. 테이블의 클러스터형 인덱스가 비활성화되면 테이블과 관련된 뷰의 인덱스도 비활성화됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 데이터베이스에는 CREATE VIEW 권한이 필요하고 뷰를 만들 구성표에는 ALTER 권한이 필요합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-an-indexed-view"></a>인덱싱된 뷰를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 예에서는 뷰를 만들고 이 뷰에 인덱스를 만듭니다. 인덱싱된 뷰를 사용하는 두 개의 쿼리가 포함되어 있습니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Set the options to support indexed views.  
    SET NUMERIC_ROUNDABORT OFF;  
    SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,  
        QUOTED_IDENTIFIER, ANSI_NULLS ON;  
    GO  
    --Create view with schemabinding.  
    IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL  
    DROP VIEW Sales.vOrders ;  
    GO  
    CREATE VIEW Sales.vOrders  
    WITH SCHEMABINDING  
    AS  
        SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Revenue,  
            OrderDate, ProductID, COUNT_BIG(*) AS COUNT  
        FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o  
        WHERE od.SalesOrderID = o.SalesOrderID  
        GROUP BY OrderDate, ProductID;  
    GO  
    --Create an index on the view.  
    CREATE UNIQUE CLUSTERED INDEX IDX_V1   
        ON Sales.vOrders (OrderDate, ProductID);  
    GO  
    --This query can use the indexed view even though the view is   
    --not specified in the FROM clause.  
    SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev,   
        OrderDate, ProductID  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND ProductID BETWEEN 700 and 800  
            AND OrderDate >= CONVERT(datetime,'05/01/2002',101)  
    GROUP BY OrderDate, ProductID  
    ORDER BY Rev DESC;  
    GO  
    --This query can use the above indexed view.  
    SELECT  OrderDate, SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND DATEPART(mm,OrderDate)= 3  
            AND DATEPART(yy,OrderDate) = 2002  
    GROUP BY OrderDate  
    ORDER BY OrderDate ASC;  
    GO  
    ```  
  
 자세한 내용은 [CREATE VIEW&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [CREATE INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [SET ANSI_NULLS&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [SET ANSI_PADDING&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)   
 [SET ARITHABORT&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql)   
 [SET CONCAT_NULL_YIELDS_NULL&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql)   
 [SET NUMERIC_ROUNDABORT&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-numeric-roundabort-transact-sql)   
 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql)  
  
  
