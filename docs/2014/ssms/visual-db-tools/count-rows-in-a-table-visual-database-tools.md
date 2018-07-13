---
title: 테이블의 행 계산(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- totals [SQL Server], row counts
- row counts [SQL Server]
- column values [SQL Server]
- number of rows
- number of values
- counting rows
ms.assetid: dda4296a-1d16-4e77-8d6f-e295f6dd4e87
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d55f9112a4015ead999ca88f7b3b55555fabf324
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37269959"
---
# <a name="count-rows-in-a-table-visual-database-tools"></a>테이블의 행 계산(Visual Database Tools)
  테이블의 행을 계산하여 다음을 확인할 수 있습니다.  
  
-   테이블의 전체 행 수. 예를 들어, `titles` 테이블의 전체 책 수를 확인할 수 있습니다.  
  
-   테이블에서 특정 조건에 맞는 행의 수. 예를 들어, `titles` 테이블에서 한 출판사가 발행한 책 수를 확인할 수 있습니다.  
  
-   특정 열의 값 수  
  
 열의 값 수를 계산할 때 null 값은 포함되지 않습니다. 예를 들어, `titles` 열에 값이 있는 `advance` 테이블에서 책 수를 계산할 수 있습니다. 기본적으로 모든 값이 계산에 포함되며 여기에는 중복된 값도 포함됩니다.  
  
 이와 같은 세 가지 종류의 계산 절차는 모두 비슷합니다.  
  
### <a name="to-count-all-the-rows-in-a-table"></a>테이블의 전체 행 수를 계산하려면  
  
1.  요약하려는 테이블이 다이어그램 창에 표시되어 있어야 합니다.  
  
2.  다이어그램 창의 배경을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **그룹화 방법 추가** 를 선택합니다. [쿼리 및 뷰 디자이너](visual-database-tools.md) 에서 **그룹화 방법** 열이 조건 창의 표에 추가됩니다.  
  
3.  선택  **\* (모든 열)** 테이블 또는 테이블 반환 개체를 나타내는 사각형에서 합니다.  
  
     쿼리 및 뷰 디자이너의 조건 창에서 **그룹화 방법** 열에 **Count** 라는 단어가 자동으로 입력되고 요약하려는 열에 대한 열 별칭이 할당됩니다. 자동으로 생성된 이 별칭을 좀 더 의미 있는 별칭으로 바꿀 수 있습니다. 자세한 내용은 [열 별칭 만들기&#40;Visual Database Tools&#41;](create-column-aliases-visual-database-tools.md)를 참조하세요.  
  
4.  쿼리를 실행합니다.  
  
### <a name="to-count-all-the-rows-that-meet-a-condition"></a>조건을 충족하는 모든 행을 계산하려면  
  
1.  요약하려는 테이블이 다이어그램 창에 표시되어 있어야 합니다.  
  
2.  다이어그램 창의 배경을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **그룹화 방법 추가** 를 선택합니다. 쿼리 및 뷰 디자이너에서 **그룹화 방법** 열이 조건 창의 표에 추가됩니다.  
  
3.  선택  **\*(모든 열)** 테이블 또는 테이블 구조 개체를 나타내는 사각형에서 합니다.  
  
     쿼리 및 뷰 디자이너의 조건 창에서 **그룹화 방법** 열에 **Count** 라는 단어가 자동으로 입력되고 요약하려는 열에 대한 열 별칭이 할당됩니다. 쿼리 결과에 더 유용한 열 머리글을 만들려면 [열 별칭 만들기&#40;Visual Database Tools&#41;](create-column-aliases-visual-database-tools.md)를 참조하세요.  
  
4.  검색하려는 데이터 열을 추가한 다음 **출력** 열의 확인란 선택을 취소합니다.  
  
     쿼리 및 뷰 디자이너에서 표의 **그룹화 방법** 열에 **Group By** 라는 단어가 자동으로 입력됩니다.  
  
5.  **그룹화 방법** 열에서 **Group By** 를 **Where**로 변경합니다.  
  
6.  검색할 데이터 열의 **필터** 열에 검색 조건을 입력합니다.  
  
7.  쿼리를 실행합니다.  
  
### <a name="to-count-the-values-in-a-column"></a>열에 있는 값의 수를 계산하려면  
  
1.  요약하려는 테이블이 다이어그램 창에 표시되어 있어야 합니다.  
  
2.  다이어그램 창의 배경을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **그룹화 방법 추가** 를 선택합니다. 쿼리 및 뷰 디자이너에서 **그룹화 방법** 열이 조건 창의 표에 추가됩니다.  
  
3.  계산하려는 열을 조건 창에 추가합니다.  
  
     쿼리 및 뷰 디자이너에서 표의 **그룹화 방법** 열에 **Group By** 라는 단어가 자동으로 입력됩니다.  
  
4.  **그룹화 방법** 열에서 **Group By** 를 **Count**로 변경합니다.  
  
    > [!NOTE]  
    >  중복된 값은 모두 하나로 간주하여 계산하려면 **Count Distinct**를 선택합니다.  
  
5.  쿼리를 실행합니다.  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 결과 정렬 및 그룹화 &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [쿼리 결과 요약&#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)  
  
  
