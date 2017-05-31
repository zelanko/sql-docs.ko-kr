---
title: "MSSQLSERVER_207 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 207 (Database Engine error)
ms.assetid: d1ab00c7-0331-437a-84fe-bae53b82feec
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ba320288a06dd8498d9699712a6e53e34ae93c09
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver207"></a>MSSQLSERVER_207
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|207|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQ_BADCOL|  
|메시지 텍스트|열 이름 '%.*ls'이(가) 잘못되었습니다.|  
  
## <a name="explanation"></a>설명  
이 쿼리 오류는 다음과 같은 문제로 인해 발생할 수 있습니다.  
  
-   열 이름의 철자가 잘못되었거나 지정한 테이블 어디에도 해당 열이 없습니다.  
  
-   데이터베이스에서 데이터를 정렬하는 데 대/소문자를 구분하고 있으며 쿼리에 지정한 열 이름의 대/소문자가 테이블에 정의된 열의 대/소문자와 일치하지 않습니다. 예를 들어 테이블에서 열을 **LastName**으로 정의하고 데이터베이스에서 대/소문자 구분 데이터 정렬을 사용하는 경우 쿼리에 지정한 열이 **Lastname** 또는 **lastname**이면 열 이름이 일치하지 않으므로 207 오류가 반환됩니다.  
  
-   SELECT 절에 정의한 열 별칭을 WHERE 또는 GROUP BY 등의 다른 절에서 참조합니다. 예를 들어 다음 쿼리의 경우 SELECT 절에 열 별칭 `Year`를 정의하고 GROUP BY 절에서 이 별칭을 참조합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year, SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY Year;  
    ```  
  
    쿼리 절의 논리적인 처리 순서 때문에 이 예제에서는 207 오류가 반환됩니다. 처리 순서는 다음과 같습니다.  
  
    1.  FROM  
  
    2.  ON  
  
    3.  JOIN  
  
    4.  WHERE  
  
    5.  GROUP BY  
  
    6.  WITH CUBE 또는 WITH ROLLUP  
  
    7.  HAVING  
  
    8.  SELECT  
  
    9. DISTINCT  
  
    10. ORDER BY  
  
    11. 맨 위로 이동  
  
    SELECT 절을 처리할 때까지는 열 별칭이 정의되지 않은 상태이므로 GROUP BY 절을 처리하는 단계에서는 별칭 이름을 알 수 없습니다.  
  
-   *<merge_matched>* 절에서 원본 테이블의 열을 참조하고 있지만 WHEN NOT MATCHED BY SOURCE 절의 원본 테이블에서 아무 행도 반환하지 않는 경우 MERGE 문을 통해 이 오류가 발생합니다. 쿼리에 아무 행도 반환되지 않으면 원본 테이블의 열에 액세스할 수 없으므로 오류가 발생합니다. 예를 들어 원본 테이블의 `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1`에 액세스할 수 없는 경우 `Col1` 절을 지정하면 이 문이 실패할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
다음 정보를 확인하고 적절하게 문을 수정하십시오.  
  
-   열 이름이 테이블에 있는지 확인하고 이름의 철자가 올바른지 확인하십시오. 다음 예제에서는 **sys.columns** 카탈로그 뷰를 쿼리하여 지정된 테이블의 열 이름을 모두 반환합니다.  
  
    ```  
    SELECT name FROM sys.columns WHERE object_id = OBJECT_ID('schema_name.table_name');  
    ```  
  
-   데이터베이스 데이터 정렬의 대/소문자 구분. 다음 문은 지정된 데이터베이스의 데이터 정렬을 반환합니다.  
  
    ```  
    SELECT collation_name FROM sys.databases WHERE name = 'database_name';  
    ```  
  
    데이터 정렬 이름의 약어 CS는 해당 데이터 정렬에서 대/소문자를 구분한다는 의미입니다. 예를 들어 Latin1_General_CS_AS는 대/소문자와 악센트를 구분하는 데이터 정렬입니다. 열 이름의 대/소문자가 테이블에 정의된 것과 일치하도록 열 이름을 수정합니다.  
  
-   열 별칭을 올바르게 참조했는지 확인하십시오. 올바른 절에 별칭을 정의하는 식을 반복하거나 파생 테이블을 사용하여 문을 수정합니다. 다음 예에서는 GROUP BY 절에 `Year` 별칭을 정의하는 식을 반복합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year ,SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY DATEPART(yyyy,OrderDate);  
    ```  
  
    다음 예에서는 파생 테이블을 사용하여 별칭 이름을 쿼리의 다른 절에 사용할 수 있도록 만듭니다. 별칭 `Year`가 FROM 절에 정의되어 있고 이 절이 제일 먼저 처리되므로 쿼리의 다른 절에서도 이 별칭을 사용할 수 있습니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT d.Year, SUM(TotalDue) AS Total  
    FROM (SELECT DATEPART(yyyy,OrderDate) AS Year, TotalDue  
          FROM Sales.SalesOrderHeader)AS d  
    GROUP BY Year;  
    ```  
  
-   MERGE 문의 WHEN NOT MATCHED BY SOURCE 절이 참조하는 값에 액세스할 수 없습니다. WHEN NOT MATCHED BY SOURCE 절의 원본 테이블에서 하나 이상의 행을 반환하도록 MERGE 문을 수정합니다. 예를 들어 이 절에 지정된 검색 조건을 추가하거나 수정해야 할 수 있습니다. 또는 절을 수정하여 원본 테이블을 참조하지 않는 값을 지정할 수 있습니다. `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = <expression, or other available value>`)을 입력합니다.  
  
## <a name="see-also"></a>관련 항목:  
[MERGE&#40;Transact-SQL&#41;](~/t-sql/statements/merge-transact-sql.md)  
[FROM&#40;Transact-SQL&#41;](~/t-sql/queries/from-transact-sql.md)  
[SELECT&#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)  
[UPDATE&#40;Transact-SQL&#41;](~/t-sql/queries/update-transact-sql.md)  
  

