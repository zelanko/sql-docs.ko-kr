---
title: "조건 창(Visual Database Tools) | Microsoft 문서"
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
- Query Designer [SQL Server], Criteria pane
- View Designer, Criteria pane
- entering query options into grid [SQL Server]
- Criteria pane
- inserting query options into grid
- grid showing query options [SQL Server]
- adding query options into grid
ms.assetid: 6291affe-580e-482f-a7ff-45ce3837956a
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 30bd3badd2ac11c7bd00125ed9ceedefbe1f1f7b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="criteria-pane-visual-database-tools"></a>조건 창(Visual Database Tools)
조건 창에서 스프레드시트 모양의 표 형태에 선택한 항목을 입력하여 표시할 데이터 열, 결과 정렬 방법, 선택할 행 등의 쿼리 옵션을 지정할 수 있습니다. 조건 창에서 지정할 수 있는 내용은 다음과 같습니다.  
  
-   표시할 열 및 열 이름 별칭  
  
-   열을 포함하는 테이블  
  
-   열 계산 식  
  
-   쿼리의 정렬 순서  
  
-   검색 조건  
  
-   요약 보고서에 사용할 집계 함수를 포함하는 그룹화 기준  
  
-   UPDATE  또는 INSERT INTO 쿼리의 새 값  
  
-   INSERT FROM 쿼리의 대상 열 이름  
  
조건 창에서 내용을 변경하면 다이어그램 창과 SQL 창의 내용도 자동으로 변경됩니다. 이와 마찬가지로 다른 창의 내용이 바뀌면 조건 창도 자동으로 업데이트됩니다.  
  
## <a name="about-the-criteria-pane"></a>조건 창 정보  
조건 창에서 행은 쿼리에 사용되는 데이터 열을 표시하고, 열은 쿼리 옵션을 표시합니다.  
  
조건 창에 나타나는 특정 정보는 만들고 있는 쿼리 형식에 따라 다릅니다.  
  
조건 창이 표시되지 않을 경우 디자이너를 마우스 오른쪽 단추로 클릭하고 **창**을 가리킨 다음 **조건**을 클릭합니다.  
  
## <a name="options"></a>옵션  
  
|**열**|**쿼리 유형**|**Description**|  
|--------------|------------------|-------------------|  
|열|모두|계산된 열의 쿼리 또는 식에 사용되는 데이터 열 이름을 표시합니다. 이 열은 가로로 스크롤할 때 항상 표시되도록 설정되어 있습니다.|  
|별칭|SELECT, INSERT FROM, UPDATE, MAKE TABLE|열의 대체 이름 또는 계산 열에 사용할 수 있는 이름을 지정합니다.|  
|테이블|SELECT, INSERT FROM, UPDATE, MAKE TABLE|관련 데이터 열에 대한 테이블 또는 테이블 구조 개체의 이름을 지정합니다. 계산된 열의 경우에는 이 열이 비어 있습니다.|  
|출력|SELECT, INSERT FROM, MAKE TABLE|쿼리 출력에 데이터 열을 나타낼지 여부를 지정합니다.<br /><br />참고: 데이터베이스에서 허용하면 결과 집합에 표시하지 않고 정렬 또는 검색 절에 데이터 열을 사용할 수 있습니다.|  
|정렬 형식|SELECT, INSERT FROM|관련 데이터 열을 쿼리 결과를 정렬하는 데 사용하고 오름차순으로 정렬할 것인지 또는 내림차순으로 정렬할 것인지 지정합니다.|  
|정렬 순서|SELECT, INSERT FROM|결과 집합을 정렬하는 데 사용되는 데이터 열에 정렬 우선 순위를 지정합니다. 데이터 열의 정렬 순서를 변경하면 다른 모든 열의 정렬 순서도 적절히 업데이트됩니다.|  
|그룹화 방법|SELECT, INSERT FROM, MAKE TABLE|관련 데이터 열을 사용하여 집계 쿼리를 만들도록 지정합니다. 이 표 형태 열은 **도구** 메뉴에서 **그룹화 방법** 을 선택하거나 SQL 창에 GROUP BY 절을 추가한 경우에만 나타납니다.<br /><br />기본적으로 이 열의 값은 **그룹화 방법**으로 설정되어 있으며 열은 GROUP BY 절의 일부가 됩니다.<br /><br />이 열의 한 셀로 이동하고 집계 함수를 선택하여 관련 데이터 열에 적용하면 기본적으로 결과 식이 결과 집합에 대한 출력 열로 추가됩니다.|  
|조건|모두|관련 데이터 열에 대한 검색 조건(필터)을 지정합니다. 연산자 및 검색할 값을 입력합니다. 이때 기본 연산자는 "="입니다. 텍스트 값은 작은따옴표로 묶어야 합니다.<br /><br />관련 데이터 열이 GROUP BY 절의 일부인 경우 입력한 식은 HAVING 절에 사용됩니다.<br /><br />**조건** 표 형태 열에서 두 개 이상의 셀에 값을 입력하는 경우 결과 검색 조건은 AND 논리로 자동으로 연결됩니다.<br /><br />예를 들어 (fname > 'A') AND (fname < 'M') 같은 단일 데이터베이스 열에 여러 검색 조건식을 지정하려면 조건 창에 데이터 열을 두 번 추가하고 데이터 열의 각 인스턴스에 대해 **조건** 표 형태 열에서 별도의 값을 입력합니다.|  
|또는...|모두|OR 논리를 사용한 이전 식에 연결된 데이터 열에 추가 검색 조건식을 지정합니다. 맨 오른쪽의 **또는...** 열에서 Tab 키를 눌러 표 형태의 **또는...** 열을 추가할 수 있습니다.|  
|추가|INSERT FROM|관련 데이터 열에 대상 데이터 열의 이름을 지정합니다. 삽입 원본 쿼리를 만들 때 쿼리 및 뷰 디자이너는 원본과 해당 대상 데이터 열을 일치시킵니다. 쿼리 및 뷰 디자이너가 일치하는 내용을 선택할 수 없는 경우 열 이름을 지정해야 합니다.|  
|새 값|UPDATE, INSERT INTO|관련 열에 넣을 값을 지정합니다. 리터럴 값 또는 식을 입력합니다.|  
  
## <a name="see-also"></a>참고 항목  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[다이어그램 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[검색 값 입력 규칙&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[쿼리 결과 정렬 및 그룹화&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[결과 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)  
[SQL 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)  
  

