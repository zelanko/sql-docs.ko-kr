---
title: 값 삽입 쿼리 만들기(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- inserting values
- queries [SQL Server], types
- adding values
- row additions [SQL Server], Insert Values query
- inserting rows
- Insert Values query
- adding rows
- table values [SQL Server]
ms.assetid: 2d4b2f6d-cc09-434b-8a0e-ccce40628064
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fdca52b519f60fddbd1f42a9e44e08f85a5879b7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181480"
---
# <a name="create-insert-values-queries-visual-database-tools"></a>값 삽입 쿼리 만들기(Visual Database Tools)
  값 삽입 쿼리를 사용하여 현재 테이블에 새 행을 만들 수 있습니다. 값 삽입 쿼리를 만들려면 다음 항목을 지정합니다.  
  
-   행을 추가할 데이터베이스 테이블  
  
-   내용을 추가하려는 열  
  
-   개별 열에 삽입할 값이나 식  
  
 예를 들어, 다음 쿼리는 제목, 종류, 출판사 및 가격 값을 지정하는 행을 `titles` 테이블에 추가합니다.  
  
```  
INSERT INTO titles  
         (title_id, title, type, pub_id, price)  
VALUES   ('BU9876', 'Creating Web Pages', 'business', '1389', '29.99')  
```  
  
 값 삽입 쿼리를 만들면 삽입할 값과 열 이름 같이 새 행을 삽입하는 데 필요한 옵션만 반영하도록 조건 창이 변경됩니다.  
  
> [!CAUTION]  
>  값 삽입 쿼리의 실행 동작을 취소할 수는 없습니다. 문제가 발생할 경우에 대비하여 쿼리를 실행하기 전에 데이터를 백업하는 것이 좋습니다.  
  
### <a name="to-create-an-insert-values-query"></a>값 삽입 쿼리를 만들려면  
  
1.  업데이트하려는 테이블을 다이어그램 창에 추가합니다.  
  
2.  **쿼리 디자이너** 메뉴에서 **형식 변경**을 가리킨 다음 **값 삽입**을 클릭합니다.  
  
    > [!NOTE]  
    >  값 삽입 쿼리를 시작할 때 다이어그램 창에 두 개 이상의 테이블이 표시되어 있으면 업데이트할 테이블의 이름을 지정하라는 메시지가 쿼리 및 뷰 디자이너의 [값 삽입 대상 테이블 선택 대화 상자](visual-database-tools.md) 에 나타납니다.  
  
3.  다이어그램 창에서 새 값을 입력하려는 각 열의 확인란을 클릭합니다. 선택한 열이 조건 창에 표시됩니다. 열을 쿼리에 추가한 경우에만 열이 업데이트됩니다.  
  
4.  조건 창의 **새 값** 열에 열의 새 값을 입력합니다. 리터럴 값, 열 이름 또는 식을 입력할 수 있습니다. 이 값은 업데이트하려는 열의 데이터 형식과 일치하거나 호환되어야 합니다.  
  
    > [!CAUTION]  
    >  쿼리 및 뷰 디자이너에서는 사용자가 입력한 값이 삽입하려는 열의 길이에 맞는지 여부를 확인할 수 없습니다. 입력한 값이 너무 길면 아무런 경고 메시지 없이 값이 잘릴 수 있습니다. 예를 들어, 20자까지 허용되는 `name` 열에 길이가 25자인 삽입 값을 지정하면 마지막 5자가 잘릴 수 있습니다.  
  
 값 삽입 쿼리를 실행해도 [결과 창](results-pane-visual-database-tools.md)에는 결과가 보고되지 않습니다. 대신, 변경된 행의 수를 나타내는 메시지가 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [지원 되는 쿼리 유형 &#40;Visual Database Tools&#41;](supported-query-types-visual-database-tools.md)   
 [방법 도움말 항목 쿼리 및 뷰 디자인 &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [쿼리 관련 기본 작업 수행&#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  