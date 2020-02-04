---
title: 쿼리에 열 추가
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: b6638a8b5a749c833d2d50ca0dc6fba78d61038c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244194"
---
# <a name="add-columns-to-queries-visual-database-tools"></a>쿼리에 열 추가(Visual Database Tools)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
쿼리에서 열을 사용하려면 쿼리에 열을 추가해야 합니다. 열을 추가하여 쿼리 출력에 표시하거나, 정렬에 사용하거나, 열의 내용을 검색하거나, 해당 내용을 요약할 수 있습니다. 쿼리를 실행할 때 쿼리에 사용되는 열 중 어떠한 열을 결과 창에 포함할지 지정할 수 있습니다. 자세한 내용은 [쿼리 결과에서 열 제거&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md)를 참조하세요.  
  
> [!NOTE]  
> 쿼리 및 뷰 디자이너에서 열의 데이터 형식을 보려면 **다이어그램 창** 에서 테이블이나 테이블 반환 개체를 선택하고 속성 창에서 열 목록을 클릭합니다. 그런 다음, **줄임표(...)** 를 클릭하여 **열 목록** 대화 상자를 엽니다.  
  
쿼리에 열을 사용할 때 그 위치와 상관 없이 열, 리터럴, 연산자 및 함수의 조합으로 구성된 식을 사용할 수도 있습니다.  
  
### <a name="to-add-an-individual-column"></a>개별 열을 추가하려면  
  
-   **다이어그램 창**에서 포함하려는 열 옆에 있는 확인란을 선택합니다.  
  
    또는  
  
-   **조건 창**의 표에서 비어 있는 첫째 행으로 이동하여 **열** 열의 필드를 클릭한 다음 드롭다운 목록에서 열 이름을 선택합니다.  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>하나의 테이블 또는 테이블 반환 개체에 대한 열 전체를 추가하려면  
  
-   **다이어그램 창**에서 **&#42;(모든 열)** 옆에 있는 확인란을 선택합니다.  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>모든 테이블 및 테이블 구조 개체에 대한 열 전체를 추가하려면  
  
1.  **테이블 작업 창** 에 조인 선이 선택되어 있지 않아야 합니다.  
  
2.  디자인 창에서 빈 공간을 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **속성** 을 선택합니다.  
  
3.  속성 창에서 **모든 열 출력** 을 클릭하고 드롭다운 목록에서 **예** 또는 **아니요** 를 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 결과에서 열 제거&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md)  
[쿼리에서 열 제거&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-queries-visual-database-tools.md)  
[검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[쿼리 결과 요약&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[쿼리 관련 기본 작업 수행&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
