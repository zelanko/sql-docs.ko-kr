---
title: 테이블 외의 항목 (Visual Database Tools)를 사용 하 여 쿼리 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], queries
- queries [SQL Server], creating
ms.assetid: 8e4a1f0a-8a42-4733-be8d-e21d6dbddb33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f6cd83135da7e5c9f4dac9e41ff562551d14ab20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63184327"
---
# <a name="create-queries-using-something-besides-a-table-visual-database-tools"></a>테이블 외의 항목을 사용하여 쿼리 만들기(Visual Database Tools)
  검색 쿼리를 작성할 때마다 원하는 열과 행, 쿼리 프로세서가 원래 데이터를 찾는 위치 등을 분명히 설정해야 합니다. 일반적으로 이 원래 데이터는 하나의 테이블 또는 함께 조인된 여러 테이블로 구성됩니다. 그러나 원래 데이터를 테이블 이외의 원본에서 가져올 수 있습니다. 실제로 테이블을 반환하는 사용자 정의 함수나 뷰, 쿼리 또는 동의어에서 가져올 수 있습니다.  
  
## <a name="using-a-view-in-place-of-a-table"></a>테이블 대신 뷰 사용  
 뷰에서 행을 선택할 수 있습니다. 예를 들어, 각 행에 가격이 $19.99가 넘는 책의 제목을 나타내는 "ExpensiveBooks"라는 뷰가 데이터베이스에 포함되어 있다고 가정하는 경우 뷰 정의는 다음과 같습니다.  
  
```  
SELECT *  
FROM titles  
WHERE price > 19.99  
  
```  
  
 ExpensiveBooks 뷰에서 심리학 책을 선택하면 가격이 비싼 심리학 책을 찾을 수 있습니다. 결과 SQL은 다음과 같습니다.  
  
```  
SELECT *  
FROM ExpensiveBooks  
WHERE type = 'psychology'  
  
```  
  
 이와 마찬가지로 뷰가 JOIN 연산에 참여할 수 있습니다. 예를 들어, ExpensiveBooks 뷰에 sales 테이블을 조인하면 판매되고 있는 비싼 책을 찾을 수 있습니다. 결과 SQL은 다음과 같습니다.  
  
```  
SELECT *  
FROM sales   
         INNER JOIN   
         ExpensiveBooks   
         ON sales.title_id   
         =  ExpensiveBooks.title_id  
  
```  
  
 쿼리에 뷰를 추가하는 방법에 대한 자세한 내용은 [쿼리에 테이블 추가&#40;Visual Database Tools&#41;](visual-database-tools.md)를 참조하세요.  
  
## <a name="using-a-query-in-place-of-a-table"></a>테이블 대신 쿼리 사용  
 쿼리에서 행을 선택할 수 있습니다. 예를 들어 공동으로 저술한 책(저자가 두 명 이상인 경우)의 제목과 ID를 검색하는 쿼리를 이미 작성했다고 가정하면 SQL은 다음과 같습니다.  
  
```  
SELECT   
     titles.title_id, title, type  
FROM   
     titleauthor   
         INNER JOIN  
         titles   
         ON titleauthor.title_id   
         =  titles.title_id   
GROUP BY   
     titles.title_id, title, type  
HAVING COUNT(*) > 1  
  
```  
  
 그런 다음 이 결과에 작성되는 다른 쿼리를 작성할 수 있습니다. 예를 들어, 공동으로 저술한 심리학 책을 검색하는 쿼리를 작성할 수 있습니다. 이 새 쿼리를 작성하기 위해 기존 쿼리를 새 쿼리 데이터의 원본으로 사용할 수 있습니다. 결과 SQL은 다음과 같습니다.  
  
```  
SELECT   
    title  
FROM   
    (  
    SELECT   
        titles.title_id,   
        title,   
        type  
    FROM   
        titleauthor   
            INNER JOIN  
            titles   
            ON titleauthor.title_id   
            =  titles.title_id   
    GROUP BY   
        titles.title_id,   
        title,   
        type  
    HAVING COUNT(*) > 1  
    )   
    co_authored_books  
WHERE     type = 'psychology'  
  
```  
  
 강조 표시한 텍스트는 새 쿼리 데이터의 원본으로 사용하는 기존 쿼리를 나타냅니다. 새 쿼리에서는 기존 쿼리의 별칭("co_authored_books")을 사용합니다. 별칭에 대한 자세한 내용은 [테이블 별칭 만들기&#40;Visual Database Tools&#41;](create-table-aliases-visual-database-tools.md) 및 [열 별칭 만들기&#40;Visual Database Tools&#41;](create-column-aliases-visual-database-tools.md)를 참조하세요.  
  
 마찬가지로 쿼리가 JOIN 연산에 참여할 수 있습니다. 예를 들어, ExpensiveBooks 뷰를 공동으로 저술한 책을 검색하는 쿼리에 조인하기만 하면 판매 중인 가격이 비싼 공동으로 저술한 책을 찾을 수 있습니다. 결과 SQL은 다음과 같습니다.  
  
```  
SELECT   
    ExpensiveBooks.title  
FROM   
    ExpensiveBooks   
        INNER JOIN  
        (  
        SELECT   
            titles.title_id,   
            title,   
            type  
        FROM   
            titleauthor   
                INNER JOIN  
                titles   
                ON titleauthor.title_id   
                =  titles.title_id   
        GROUP BY   
            titles.title_id,   
            title,   
            type  
        HAVING COUNT(*) > 1  
        )  
```  
  
 쿼리에 쿼리를 추가하는 방법에 대한 자세한 내용은 [쿼리에 테이블 추가&#40;Visual Database Tools&#41;](visual-database-tools.md)를 참조하세요.  
  
## <a name="using-a-user-defined-function-in-place-of-a-table"></a>테이블 대신 사용자 정의 함수 사용  
 SQL Server 2000 이상에서는 테이블을 반환하는 사용자 정의 함수를 만들 수 있습니다. 이러한 함수는 복잡하거나 절차적인 논리를 수행하는 데 유용합니다.  
  
 예를 들어, employee 테이블에 employee.manager_emp_id 추가 열이 있고 외래 키가 manager_emp_id 열에서 employee.emp_id 열까지 존재한다고 가정하면 employee 테이블의 각 행에서 manager_emp_id 열은 직원의 상사를 나타냅니다. 정확하게 말하자면 직원 상사의 emp_id를 나타냅니다. 높은 수준의 특정 관리자 조직 계층 내에서 작업하는 각 직원의 행을 포함하는 테이블을 반환하는 사용자 정의 함수를 만들 수 있습니다. 이 함수 이름을 fn_GetWholeTeam이라 하고 검색하려는 팀의 관리자의 emp_id, 즉 입력 변수를 가져오도록 디자인할 수 있습니다.  
  
 fn_GetWholeTeam 함수를 데이터 원본으로 사용하는 쿼리를 작성할 수 있습니다. 결과 SQL은 다음과 같습니다.  
  
```  
SELECT *   
FROM   
     fn_GetWholeTeam ('VPA30890F')  
  
```  
  
 "VPA30890F"는 검색하려는 조직의 관리자의 emp_id입니다. 쿼리에 사용자 정의 함수를 추가하는 방법에 대한 자세한 내용은 [쿼리에 테이블 추가&#40;Visual Database Tools&#41;](visual-database-tools.md)를 참조하세요. 사용자 정의 함수에 대한 자세한 내용은 [사용자 정의 함수](../../relational-databases/user-defined-functions/user-defined-functions.md)를 참조하세요.  
  
  
