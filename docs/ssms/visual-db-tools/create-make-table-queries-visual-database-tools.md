---
title: 테이블 만들기 쿼리 만들기(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- table creation [SQL Server], Make Table query
- inserting tables
- Make Table query
- adding tables
ms.assetid: 4493cffa-7b2d-4c24-8ef0-d49329198972
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 456834ab7682ec013a1f8fb7fe120a13b3591862
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65105909"
---
# <a name="create-make-table-queries-visual-database-tools"></a>테이블 만들기 쿼리 만들기(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
테이블 만들기 쿼리를 사용하여 행을 새 테이블에 복사할 수 있습니다. 이 방법은 작업에 사용할 데이터의 하위 집합을 만들거나 한 데이터베이스에서 다른 데이터베이스로 테이블 내용을 복사하는 데 유용합니다. 테이블 만들기 쿼리는 결과 삽입 쿼리와 비슷하지만 행을 복사해 넣을 새 테이블을 만든다는 점에서 차이가 있습니다.  
  
테이블 만들기 쿼리를 만들려면 다음 항목을 지정합니다.  
  
-   새 데이터베이스 테이블(대상 테이블)의 이름  
  
-   행을 복사할 하나 이상의 원본 테이블. 단일 테이블이나 조인된 테이블에서 복사할 수 있습니다.  
  
-   해당 내용을 복사하려는 원본 테이블의 열  
  
-   행을 특정 순서에 따라 복사하려는 경우 정렬 순서  
  
-   복사할 행을 정의하는 검색 조건  
  
-   요약 정보만 복사하려는 경우 그룹화 방법 옵션  
  
예를 들어, 다음 쿼리에서는 `uk_customers`라는 새 테이블을 만들고 `customers` 테이블에서 이 테이블로 정보를 복사합니다.  
  
```  
SELECT *   
INTO uk_customers  
FROM customers  
WHERE country = 'UK'  
```  
  
테이블 만들기 쿼리를 성공적으로 사용하려면  
  
-   데이터베이스에서 SELECT...INTO 구문을 지원해야 합니다.  
  
-   대상 데이터베이스에 테이블을 만들 수 있는 권한이 있어야 합니다.  
  
### <a name="to-create-a-make-table-query"></a>테이블 만들기 쿼리를 만들려면  
  
1.  하나 이상의 원본 테이블을 다이어그램 창에 추가합니다.  
  
2.  **쿼리 디자이너** 메뉴에서 **형식 변경**을 가리킨 다음 **테이블 만들기**를 클릭합니다.  
  
3.  **테이블 만들기** 대화 상자에서 대상 테이블의 이름을 입력합니다. 쿼리 및 뷰 디자이너는 이 이름이 이미 사용되고 있는지와 사용자에게 테이블을 만들 수 있는 권한이 있는지를 확인하지 않습니다.  
  
    다른 데이터베이스에 대상 테이블을 만들려면 대상 데이터베이스의 이름, 소유자(필요한 경우) 및 테이블의 이름을 포함하는 정규화된 테이블 이름을 지정합니다.  
  
4.  쿼리에 열을 추가하여 복사할 열을 지정합니다. 자세한 내용은 [쿼리에 열 추가(Visual Database Tools)](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)를 참조하세요. 열을 쿼리에 추가한 경우에만 열이 복사됩니다. 행 전체를 복사하려면 **&#42;(모든 열)** 를 선택합니다.  
  
    사용자가 선택한 열이 쿼리 및 뷰 디자이너에서 조건 창의 **열** 열에 추가됩니다.  
  
5.  행을 특정 순서에 따라 복사하려면 정렬 순서를 지정합니다. 자세한 내용은 **쿼리 결과 정렬 및 그룹화**를 참조하세요.  
  
6.  검색 조건을 입력하여 복사할 행을 지정합니다. 자세한 내용은 [검색 조건 지정(Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)을 참조하세요.  
  
    검색 조건을 지정하지 않으면 원본 테이블의 행 전체가 대상 테이블에 복사됩니다.  
  
    > [!NOTE]  
    > 검색할 열을 조건 창에 추가하면 쿼리 및 뷰 디자이너의 복사할 열 목록에도 이 열이 추가됩니다. 열을 검색만 하고 복사는 하지 않으려면 테이블 또는 테이블 구조 개체를 나타내는 사각형에서 열 이름 옆에 있는 확인란의 선택을 취소합니다.  
  
7.  요약 정보를 복사하려면 그룹화 방법 옵션을 지정합니다. 자세한 내용은 [쿼리 결과 요약(Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)을 참조하세요.  
  
테이블 만들기 쿼리를 실행해도 [결과 창](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)에는 결과가 보고되지 않습니다. 대신, 복사한 행의 수를 나타내는 메시지가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 및 뷰 디자인 방법 도움말 항목(Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[쿼리 형식(Visual Database Tools)](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
  
