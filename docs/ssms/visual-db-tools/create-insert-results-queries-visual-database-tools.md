---
title: 결과 삽입 쿼리 만들기(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- result sets [SQL Server], queries
- results [SQL Server], query
- Insert Results query
- queries [SQL Server], results
ms.assetid: 8770d630-09cc-47ec-a0e9-e9de2d7bbc89
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 850d64df71644c5010cfda9a2c2624ab4bfd49cf
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264957"
---
# <a name="create-insert-results-queries-visual-database-tools"></a>결과 삽입 쿼리 만들기(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
결과 삽입 쿼리를 사용하여 테이블 내에서 또는 한 테이블에서 다른 테이블로 행을 복사할 수 있습니다. 예를 들어 `titles` 테이블에서 결과 삽입 쿼리를 사용하여 한 출판사의 모든 도서 제목에 대한 정보를 두 번째 테이블로 복사하고 이 테이블을 해당 출판사에서 사용하도록 만들 수 있습니다. 결과 삽입 쿼리는 테이블 만들기 쿼리와 비슷하지만 행을 기존 테이블에 복사한다는 점에서 차이가 있습니다.  
  
> [!TIP]  
> 잘라내기와 붙여넣기를 사용하여 한 테이블에서 다른 테이블로 행을 복사할 수도 있습니다. 각 테이블에 대한 쿼리를 만들고 쿼리를 실행합니다. 한 결과 표에서 다른 결과 표로 행을 복사합니다.  
  
결과 삽입 쿼리를 만들려면 다음 항목을 지정합니다.  
  
-   행을 복사해 넣을 데이터베이스 테이블(대상 테이블)  
  
-   행을 복사할 하나 이상의 원본 테이블. 원본 테이블은 하위 쿼리의 일부가 됩니다. 테이블 내에서 복사하는 경우 원본 테이블은 대상 테이블과 같습니다.  
  
-   해당 내용을 복사하려는 원본 테이블의 열  
  
-   데이터를 복사해 넣을 대상 테이블의 대상 열  
  
-   복사할 행을 정의하는 검색 조건  
  
-   행을 특정 순서에 따라 복사하려는 경우 정렬 순서  
  
-   요약 정보만 복사하려는 경우 그룹화 방법 옵션  
  
예를 들어, 다음 쿼리는 `titles` 테이블의 제목 정보를 `archivetitles`라는 보관 테이블로 복사합니다. 이 쿼리는 특정 출판사에서 발행한 모든 도서 제목의 네 가지 열에 들어 있는 내용을 복사합니다.  
  
```  
INSERT INTO archivetitles   
   (title_id, title, type, pub_id)  
SELECT title_id, title, type, pub_id  
FROM titles  
WHERE (pub_id = '0766')  
```  
  
> [!NOTE]  
> 새 행에 값을 삽입하려면 값 삽입 쿼리를 사용합니다.  
  
행의 열 전체 또는 선택한 열의 내용을 복사할 수 있습니다. 두 경우 모두 복사하는 데이터는 복사 대상 위치인 행의 열과 호환되어야 합니다. 예를 들어, `price`같은 열의 내용을 복사하는 경우 이 데이터를 복사해 넣을 행의 열에서 소수점이 포함된 숫자 데이터를 사용할 수 있어야 합니다. 행 전체를 복사하는 경우 대상 테이블에는 원본 테이블과 동일한 실제 위치에 원본 행과 호환되는 열이 있어야 합니다.  
  
결과 삽입 쿼리를 만들면 데이터를 복사하는 데 사용할 수 있는 옵션이 반영되도록 조건 창이 변경됩니다. 데이터를 복사해 넣을 대상 열을 지정하는 데 사용할 수 있는 추가 열이 나타납니다.  
  
> [!CAUTION]  
> 결과 삽입 쿼리의 실행 동작을 취소할 수는 없습니다. 문제가 발생할 경우에 대비하여 쿼리를 실행하기 전에 데이터를 백업하는 것이 좋습니다.  
  
### <a name="to-create-an-insert-results-query"></a>결과 삽입 쿼리를 만들려면  
  
1.  새 쿼리를 만들고 행을 복사할 원본 테이블을 추가합니다. 테이블 내에서 행을 복사하는 경우 원본 테이블을 대상 테이블로 추가할 수 있습니다.  
  
2.  **쿼리 디자이너** 메뉴에서 **형식 변경**을 가리킨 다음 **결과 삽입**을 클릭합니다.  
  
3.  [결과 삽입의 대상 테이블 선택 대화 상자](../../ssms/visual-db-tools/choose-target-table-for-insert-results-dialog-box-visual-database-tools.md)에서 행을 복사해 넣을 대상 테이블을 선택합니다.  
  
    > [!NOTE]  
    > 쿼리 및 뷰 디자이너에서는 업데이트 가능한 테이블과 뷰를 미리 확인할 수 없습니다. 따라서 **결과 삽입의 대상 테이블 선택** 대화 상자의 **테이블 이름** 목록에는 쿼리하려는 데이터 연결에 사용 가능한 모든 테이블과 뷰가 표시됩니다. 여기에는 행을 복사해 넣을 수 없는 테이블이나 뷰도 포함됩니다.  
  
4.  테이블이나 테이블 반환 개체를 나타내는 사각형에서 복사하려는 내용이 들어 있는 열의 이름을 선택합니다. 행 전체를 복사하려면 **&#42;(모든 열)** 를 선택합니다.  
  
    사용자가 선택한 열이 쿼리 및 뷰 디자이너에서 조건 창의 **열** 열에 추가됩니다.  
  
5.  조건 창의 **추가** 열에서 복사하려는 각 열에 대한 대상 테이블의 대상 열을 선택합니다. 행 전체를 복사하는 경우 *tablename.&#42;* 를 선택합니다. 대상 테이블 열의 데이터 형식은 원본 테이블 열의 데이터 형식과 동일하거나 호환되어야 합니다.  
  
6.  행을 특정 순서에 따라 복사하려면 정렬 순서를 지정합니다. 자세한 내용은 [쿼리 결과 정렬 및 그룹화&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)를 참조하세요.  
  
7.  **필터** 열에 검색 조건을 입력하여 복사할 행을 지정합니다. 자세한 내용은 [검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)을 참조하세요.  
  
    검색 조건을 지정하지 않으면 원본 테이블의 행 전체가 대상 테이블에 복사됩니다.  
  
    > [!NOTE]  
    > 검색할 열을 조건 창에 추가하면 쿼리 및 뷰 디자이너의 복사할 열 목록에도 이 열이 추가됩니다. 열을 검색만 하고 복사는 하지 않으려면 테이블 또는 테이블 반환 개체를 나타내는 사각형에서 열 이름 옆에 있는 확인란의 선택을 취소합니다.  
  
8.  요약 정보를 복사하려면 그룹화 방법 옵션을 지정합니다. 자세한 내용은 [쿼리 결과 요약&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)을 참조하세요.  
  
결과 삽입 쿼리를 실행해도 [결과 창](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)에는 결과가 보고되지 않습니다. 대신, 복사한 행의 수를 나타내는 메시지가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 형식&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
