---
title: "여러 열에 여러 검색 조건 지정 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- search criteria [SQL Server], multiple conditions
- multiple search conditions
- search conditions [SQL Server], multiple
- OR operator
- AND, Criteria pane
ms.assetid: 06617729-0d0b-4da2-9890-b7e2f5cdbc7b
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 041d9a3c2a204d8413d755ec69946859195b5c0a
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="specify-multiple-search-conditions-for-multiple-columns-visual-database-tools"></a>여러 열에 여러 검색 조건 지정(Visual Database Tools)
여러 개의 데이터 열을 검색 조건의 일부로 포함하여 쿼리의 범위를 확장하거나 축소할 수 있습니다. 예를 들면 다음과 같습니다.  
  
-   근무 연수가 5년이 넘었거나 특정 작업을 담당하는 직원을 검색하는 경우  
  
-   특정 출판사에서 출판한 요리 관련 서적을 검색하는 경우  
  
둘 이상의 열 중 하나에 들어 있는 값을 검색하는 쿼리를 만들려면 OR 조건을 지정하고 둘 이상의 열에 있는 모든 조건을 만족해야 하는 쿼리를 만들려면 AND 조건을 지정합니다.  
  
## <a name="specifying-an-or-condition"></a>OR 조건 지정  
OR로 연결된 여러 개의 조건을 만들려면 조건 창에서 각 조건을 서로 다른 열에 지정합니다.  
  
#### <a name="to-specify-an-or-condition-for-two-different-columns"></a>두 개의 서로 다른 열에 OR 조건을 지정하려면  
  
1.  [조건 창](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)에서 검색할 열을 추가합니다.  
  
2.  검색할 첫 번째 열의 **필터** 열에서 첫째 조건을 지정합니다.  
  
3.  **필터** 열은 비워 두고 검색할 두 번째 데이터 열의 **또는...** 열에서 둘째 조건을 지정합니다.  
  
    쿼리 및 뷰 디자이너는 다음과 같이 OR 조건을 포함하는 WHERE 절을 만듭니다.  
  
    ```  
    SELECT job_lvl, hire_date  
    FROM employee  
    WHERE (job_lvl >= 200) OR   
      (hire_date < '01/01/1998')  
    ```  
  
4.  추가할 각 조건에 대하여 2단계와 3단계를 반복합니다. 각 새 조건에 서로 다른 **또는...** 열을 사용합니다.  
  
## <a name="specifying-an-and-condition"></a>AND 조건 지정  
AND로 연결된 조건을 사용하여 서로 다른 데이터 열을 검색하려면 표의 **필터** 열에 모든 조건을 지정합니다.  
  
#### <a name="to-specify-an-and-condition-for-two-different-columns"></a>두 개의 서로 다른 열에 AND 조건을 지정하려면  
  
1.  [조건 창](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)에서 검색할 열을 추가합니다.  
  
2.  검색할 첫 번째 데이터 열의 **필터** 열에서 첫째 조건을 지정합니다.  
  
3.  두 번째 데이터 열의 **필터** 열에서 둘째 조건을 지정합니다.  
  
    쿼리 및 뷰 디자이너는 다음과 같이 AND 조건을 포함하는 WHERE 절을 만듭니다.  
  
    ```  
    SELECT pub_id, title  
    FROM titles  
    WHERE (pub_id = '0877') AND (title LIKE '%Cook%')  
    ```  
  
4.  추가할 각 조건에 대하여 2단계와 3단계를 반복합니다.  
  
## <a name="see-also"></a>참고 항목  
[AND에 우선 순위가 있는 조건 조합(Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-and-has-precedence-visual-database-tools.md)  
[OR에 우선 순위가 있는 조건 조합(Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
[조건 창의 검색 조건 결합 규칙(Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[검색 조건 지정(Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  

