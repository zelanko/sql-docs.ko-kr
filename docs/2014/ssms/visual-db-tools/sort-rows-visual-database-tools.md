---
title: 행 정렬(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sorting rows [SQL Server]
- sorting query results [SQL Server]
ms.assetid: 780ef467-f96e-4373-8235-6dacbedb05a2
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 611cae35eb3da42f1a9e5772ec6c4b2e148cb730
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43815859"
---
# <a name="sort-rows-visual-database-tools"></a>행 정렬(Visual Database Tools)
  쿼리 결과에서 행을 정렬할 수 있습니다. 즉, 해당 값이 결과 집합의 행 순서를 결정하는 특정 열 또는 열 집합의 이름을 지정할 수 있습니다.  
  
> [!NOTE]  
>  정렬 순서는 부분적으로 열의 배치 순서에 따라 결정됩니다. [데이터 정렬 대화 상자](visual-database-tools.md)에서 데이터 정렬 순서를 변경할 수 있습니다.  
  
 쿼리 결과를 정렬하는 데는 여러 가지 방법이 있습니다.  
  
-   **행을 오름차순 또는 내림차순으로 정렬할 수 있습니다.** 기본적으로 SQL에서는 열 정렬을 사용하여 오름차순으로 행을 정렬합니다. 예를 들어, 오름차순 가격으로 책 제목을 정렬하려면 price 열을 기준으로 행을 정렬하면 됩니다. 결과 SQL은 다음과 같습니다.  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price  
  
    ```  
  
     반면에 가격이 비싼 책의 제목부터 먼저 표시되도록 정렬하려면 내림차순으로 정렬하면 됩니다. 즉, 결과 행을 price 열 값의 내림차순으로 정렬하도록 지정합니다. 결과 SQL은 다음과 같습니다.  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price DESC  
  
    ```  
  
-   **여러 열을 기준으로 정렬할 수 있습니다.** 예를 들어, 각 저자별로 행이 하나씩 있는 결과 집합을 만들어 주별로 정렬한 다음 다시 도시별로 정렬할 수 있습니다. 결과 SQL은 다음과 같습니다.  
  
    ```  
    SELECT *  
    FROM authors   
    ORDER BY state, city  
  
    ```  
  
-   **결과 집합에 표시되지 않는 열을 기준으로 정렬할 수 있습니다.** 예를 들어, 가격이 결과 집합에 표시되지 않더라도 가장 비싼 책 제목을 먼저 표시하는 결과 집합을 만들 수 있습니다. 결과 SQL은 다음과 같습니다.  
  
    ```  
    SELECT title_id, title  
    FROM titles  
    ORDER BY price DESC  
  
    ```  
  
-   **파생 열을 기준으로 정렬할 수 있습니다.** 예를 들어, 각 행에 책 제목이 있는 결과 집합을 만들어 한 권당 가장 높은 인세를 지불하는 책이 먼저 표시되도록 할 수 있습니다. 결과 SQL은 다음과 같습니다.  
  
    ```  
    SELECT title, price * royalty / 100 as royalty_per_unit  
    FROM titles  
    ORDER BY royalty_per_unit DESC  
  
    ```  
  
     한 권 판매될 때마다 받는 인세를 계산하는 공식이 강조 표시됩니다.  
  
     파생 열을 계산하려면 위 예제에서와 같이 SQL 구문을 사용하거나 스칼라 값을 반환하는 사용자 정의 함수를 사용할 수 있습니다. 사용자 정의 함수에 대한 자세한 내용은 SQL Server 설명서를 참조하십시오.  
  
-   **그룹화된 행을 정렬할 수 있습니다.** 예를 들어, 각 행에 도시와 해당 도시에 있는 저자 수를 나타내는 결과 집합을 만들어 저자를 많이 포함하는 도시가 먼저 표시되도록 할 수 있습니다. 결과 SQL은 다음과 같습니다.  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    ORDER BY COUNT(*) DESC, state  
  
    ```  
  
     이 쿼리에서는 `state` 를 두 번째 정렬 열로 사용합니다. 따라서 두 개의 주에 같은 수의 저자가 있을 경우 해당 주들은 사전순으로 표시됩니다.  
  
-   **국가별 데이터를 사용하여 정렬할 수 있습니다.** 해당 열에 대한 기본 규칙과 다른 데이터 정렬 규칙을 사용하여 열을 정렬할 수 있습니다. 예를 들어, Jaime Patiño가 집필한 모든 책 제목을 검색하는 쿼리를 작성할 수 있습니다. 제목을 사전순으로 표시하려면 title 열에 스페인어 데이터 정렬 순서를 사용합니다. 결과 SQL은 다음과 같습니다.  
  
    ```  
    SELECT title  
    FROM   
        authors   
        INNER JOIN   
            titleauthor   
            ON authors.au_id   
            =  titleauthor.au_id   
            INNER JOIN  
                titles   
                ON titleauthor.title_id   
                =  titles.title_id   
    WHERE   
         au_fname = 'Jaime' AND   
         au_lname = 'Patiño'  
    ORDER BY   
         title COLLATE SQL_Spanish_Pref_CP1_CI_AS  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 결과 정렬 및 그룹화 &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
