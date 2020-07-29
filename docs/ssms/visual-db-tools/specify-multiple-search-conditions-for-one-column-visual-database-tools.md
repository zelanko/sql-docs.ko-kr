---
title: 한 열에 여러 검색 조건 지정
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], multiple conditions
- multiple search conditions
- search conditions [SQL Server], multiple
- OR operator
- AND, Criteria pane
ms.assetid: 2c006e36-56b1-4992-89b4-c6c0b19808f3
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 090d5376079546c461f3db9dc44572452c61f03d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999271"
---
# <a name="specify-multiple-search-conditions-for-one-column-visual-database-tools"></a>한 열에 여러 검색 조건 지정(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
동일한 데이터 열에 여러 개의 검색 조건을 적용해야 하는 경우가 있습니다. 예를 들면 다음과 같습니다.  
  
-   `employee` 테이블에서 여러 개의 다른 이름을 검색하는 경우 또는 급여가 서로 다른 직원을 검색하는 경우. 이런 형식의 검색에는 OR 조건이 필요합니다.  
  
-   "The"로 시작하며 "Cook"이라는 단어를 포함하는 책 제목을 검색하는 경우. 이런 형식의 검색에는 AND 조건이 필요합니다.  
  
> [!NOTE]  
> 이 항목의 정보는 쿼리에서 WHERE 절의 검색 조건과 HAVING 절의 검색 조건에 모두 적용됩니다. 이 예제는 WHERE 절 만들기를 중점적으로 설명하지만 이 원칙은 두 형식의 검색 조건 모두에 적용됩니다.  
  
동일한 데이터 열에서 하나의 조건만 만족해도 되는 값을 검색하려면 OR 조건을 지정하고 여러 조건을 모두 만족하는 값을 검색하려면 AND 조건을 지정합니다.  
  
## <a name="specifying-an-or-condition"></a>OR 조건 지정  
OR 조건을 사용하면 하나의 열에 검색할 조건 값을 여러 개 지정할 수 있습니다. 이 옵션은 검색 범위를 넓히므로 단일 값을 검색하는 것보다 많은 행을 반환할 수 있습니다.  
  
> [!TIP]  
> IN 연산자를 대신 사용하여 동일한 데이터 열에서 여러 개의 값을 검색할 수도 있습니다.  
  
#### <a name="to-specify-an-or-condition"></a>OR 조건을 지정하려면  
  
1.  [조건 창](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)에서 검색할 열을 추가합니다.  
  
2.  방금 추가한 데이터 열의 **필터** 열에 첫째 조건을 지정합니다.  
  
3.  동일한 데이터 열의 **또는...** 열에 둘째 조건을 지정합니다.  
  
쿼리 및 뷰 디자이너는 다음과 같이 OR 조건을 포함하는 WHERE 절을 만듭니다.  
  
```  
SELECT fname, lname  
FROM employees  
WHERE (salary < 30000) OR (salary > 100000)  
```  
  
## <a name="specifying-an-and-condition"></a>AND 조건 지정  
AND 조건을 사용하면 열에 있는 값 중 둘 이상의 조건을 모두 만족하는 행 값만 결과 집합에 포함되도록 지정할 수 있습니다. 이 옵션은 검색 범위를 좁히므로 일반적으로 단일 값을 검색하는 것보다 적은 수의 행을 반환합니다.  
  
> [!TIP]  
> 값 범위를 검색 중인 경우 AND를 사용하여 두 조건을 연결하는 대신 BETWEEN 연산자를 사용할 수도 있습니다.  
  
#### <a name="to-specify-an-and-condition"></a>AND 조건을 지정하려면  
  
1.  조건 창에서 검색할 열을 추가합니다.  
  
2.  방금 추가한 데이터 열의 **필터** 열에 첫째 조건을 지정합니다.  
  
3.  동일한 데이터 열을 조건 창에 다시 추가하여 표의 빈 행에 둡니다.  
  
4.  데이터 열의 두 번째 인스턴스에 대한 **필터** 열에 둘째 조건을 지정합니다.  
  
쿼리 디자이너는 다음과 같이 AND 조건을 포함하는 WHERE 절을 만듭니다.  
  
```  
SELECT title_id, title  
FROM titles  
WHERE (title LIKE '%Cook%') AND   
  (title LIKE '%Recipe%')  
```  
  
## <a name="see-also"></a>참고 항목  
[조건 창의 검색 조건 결합 규칙&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
