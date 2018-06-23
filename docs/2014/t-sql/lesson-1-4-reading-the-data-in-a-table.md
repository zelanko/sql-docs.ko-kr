---
title: 테이블의 데이터 읽기(자습서) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- reading data in a table
ms.assetid: 532232c9-3d41-45cd-9150-de67a1cbfcf5
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7eb28bcefab604d070b2d3599accb4045faae8aa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079884"
---
# <a name="reading-the-data-in-a-table-tutorial"></a>테이블의 데이터 읽기(자습서)
  SELECT 문을 사용하여 테이블의 데이터를 읽을 수 있습니다. SELECT 문은 가장 중요한 [!INCLUDE[tsql](../includes/tsql-md.md)] 문 중 하나이며 구문은 다양하게 변형되어 사용됩니다. 이 자습서에서는 5개의 간단한 버전을 사용합니다.  
  
### <a name="to-read-the-data-in-a-table"></a>테이블의 데이터를 읽으려면  
  
1.  다음 문을 입력하고 실행하여 `Products` 테이블의 데이터를 읽습니다.  
  
    ```  
    -- The basic syntax for reading data from a single table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
    GO  
  
    ```  
  
2.  별표를 사용하여 테이블의 모든 열을 선택할 수 있습니다. 이 방법은 임시 쿼리에서 사용되는 경우가 많습니다. 나중에 새 열이 테이블에 추가되는 경우에도 문에서 예측된 열을 반환하도록 영구 코드로 열 목록을 제공해야 합니다.  
  
    ```  
    -- Returns all columns in the table  
    -- Does not use the optional schema, dbo  
    SELECT * FROM Products  
    GO  
  
    ```  
  
3.  반환하지 않으려는 열은 생략할 수 있습니다. 열은 나열된 순서대로 반환됩니다.  
  
    ```  
    -- Returns only two of the columns from the table  
    SELECT ProductName, Price  
        FROM dbo.Products  
    GO  
  
    ```  
  
4.  `WHERE` 절을 사용하여 사용자에게 반환되는 행을 제한할 수 있습니다.  
  
    ```  
    -- Returns only two of the records in the table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
        WHERE ProductID < 60  
    GO  
  
    ```  
  
5.  열이 반환되면 열의 값에 대한 작업을 수행할 수 있습니다. 다음 예는 `Price` 열에서 수치 연산을 수행합니다. `AS` 키워드를 사용하여 이름을 제공하지 않은 경우 이 방법으로 변경된 열에는 이름이 없습니다.  
  
    ```  
    -- Returns ProductName and the Price including a 7% tax  
    -- Provides the name CustomerPays for the calculated column  
    SELECT ProductName, Price * 1.07 AS CustomerPays  
        FROM dbo.Products  
    GO  
    ```  
  
## <a name="functions-that-are-useful-in-a-select-statement"></a>SELECT 문에 유용한 함수  
 SELECT 문에서 데이터 작업을 수행하는 데 사용할 수 있는 일부 함수에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
|||  
|-|-|  
|[문자열 함수&#40;Transact-SQL&#41;](/sql/t-sql/functions/string-functions-transact-sql)|[날짜 및 시간 데이터 형식 및 함수 &#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)|  
|[수치 연산 함수&#40;Transact-SQL&#41;](/sql/t-sql/functions/mathematical-functions-transact-sql)|[텍스트 및 이미지 함수 &#40;Transact SQL&#41;](/sql/t-sql/functions/text-and-image-functions-textptr-transact-sql)|  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [요약: 데이터베이스 개체 만들기](lesson-1-5-summary-creating-database-objects.md)  
  
## <a name="see-also"></a>관련 항목  
 [SELECT&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)  
  
  
