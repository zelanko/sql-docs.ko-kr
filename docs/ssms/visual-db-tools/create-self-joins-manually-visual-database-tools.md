---
title: 수동으로 자체 조인 만들기(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- self-joins
- manual joins [SQL Server]
- joins [SQL Server], self
ms.assetid: 910ed516-cb84-481b-95d0-cba3e89afdba
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ad4abd99364ec906cb61a37b8e7f47c7095e2081
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65090058"
---
# <a name="create-self-joins-manually-visual-database-tools"></a>수동으로 자체 조인 만들기(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
데이터베이스에서 테이블에 반사 관계가 없는 경우에도 테이블을 자체 조인할 수 있습니다. 예를 들어, 자체 조인을 사용하여 같은 도시에 살고 있는 만든 이 쌍을 찾을 수 있습니다.  
  
다른 조인과 마찬가지로 자체 조인에도 테이블이 두 개 이상 필요합니다. 차이점은 쿼리에 두 번째 테이블을 추가하지 않고 같은 테이블의 두 번째 인스턴스를 추가한다는 점입니다. 이런 방식으로 테이블의 첫 번째 인스턴스의 열을 두 번째 인스턴스의 같은 열과 비교하여 열의 값을 서로 비교할 수 있습니다. [쿼리 및 뷰 디자이너](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 는 테이블의 두 번째 인스턴스에 별칭을 할당합니다.  
  
예를 들어, Berkeley 에 살고 있는 모든 만든 이 쌍을 찾는 자체 조인을 만드는 중인 경우 테이블의 첫 번째 인스턴스의 `city` 열과 두 번째 인스턴스의 `city` 열을 비교합니다. 완성된 쿼리는 다음과 같습니다.  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
자체 조인을 만들 때 조인 조건이 여러 개 필요한 경우가 종종 있습니다. 이유를 알아보려면 이전 쿼리의 결과를 살펴보십시오.  
  
```  
Cheryl Carson       Cheryl Carson  
   Abraham Bennet      Abraham Bennet  
   Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
첫 번째 행은 Cheryl Carson이 Cheryl Carson과 같은 도시에 살고 있음을 나타내므로 필요하지 않습니다. 마찬가지로 두 번째 행도 필요하지 않습니다. 이런 필요 없는 데이터를 제거하려면 두 개의 만든 이 이름이 서로 다른 만든 이를 나타내는 결과 행만 보유하는 다른 조건을 추가합니다. 완성된 쿼리는 다음과 같습니다.  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                <> authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
결과 집합이 다음과 같이 향상되었습니다.  
  
```  
Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
하지만 두 결과 행이 중복됩니다. 첫 번째 행은 Carson이 Bennet과 같은 도시에 살고 있음을 나타내며 두 번째 행은 Bennet이 Carson과 같은 도시에 살고 있음을 나타냅니다. 이런 중복 결과를 제거하려면 두 번째 조인 조건을 "not equals"에서 "less than"으로 변경하면 됩니다. 완성된 쿼리는 다음과 같습니다.  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                < authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
결과 집합은 다음과 같습니다.  
  
```  
Cheryl Carson       Abraham Bennet  
```  
  
### <a name="to-create-a-self-join-manually"></a>자체 조인을 수동으로 만들려면  
  
1.  작업할 테이블 또는 테이블 반환 개체를 [다이어그램 창](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) 에 추가합니다.  
  
2.  다이어그램 창에 같은 테이블 또는 테이블 반환 개체가 두 번 표시되도록 같은 테이블을 다시 추가합니다.  
  
    쿼리 및 뷰 디자이너는 테이블 이름에 일련 번호를 추가하여 두 번째 인스턴스에 별칭을 할당합니다. 또한 쿼리 및 뷰 디자이너는 다이어그램 창 내에서 테이블 또는 테이블 반환 개체의 두 일치 항목 사이에 조인 선을 만듭니다.  
  
3.  조인 선을 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **속성** 을 선택합니다.  
  
4.  속성 창에서 **조인 조건 및 형식**을 클릭하고 속성의 오른쪽에 있는 **줄임표(...)** 를 클릭합니다.  
  
5.  필요한 경우 [조인 대화 상자](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md) 에서 기본 키 사이의 비교 연산자를 변경합니다. 예를 들어, 연산자를 (<)보다 작음으로 변경할 수 있습니다.  
  
6.  테이블 또는 테이블 반환 개체의 첫 번째 일치 항목에서 기본 조인 열의 이름을 끌어서 두 번째 일치 항목의 해당 열에 놓는 방법을 통해 추가 조인 조건(예: authors.zip = authors1.zip)을 만듭니다.  
  
7.  출력 열, 검색 조건, 정렬 순서 등의 기타 쿼리 옵션을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
[자체 조인 자동으로 만들기&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-self-joins-automatically-visual-database-tools.md)  
[조인을 사용한 쿼리&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
