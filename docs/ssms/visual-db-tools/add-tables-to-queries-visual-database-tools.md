---
title: "쿼리에 테이블 추가(Visual Database Tools) | Microsoft 문서"
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
- inserting tables
- adding tables
- queries [SQL Server], tables
ms.assetid: 6551aa7e-31a1-4636-852a-819bc53d658b
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ffa0dc48650d116f76df704ceae1d10f96b2b5be
ms.lasthandoff: 04/11/2017

---
# <a name="add-tables-to-queries-visual-database-tools"></a>쿼리에 테이블 추가(Visual Database Tools)
쿼리를 만들 때는 뷰와 특정 사용자 정의 함수 같은 테이블 구조의 다른 개체나 테이블에서 데이터를 검색합니다. 쿼리에서 이러한 개체를 사용하여 작업하려면 필요한 개체를 **다이어그램 창**에 추가합니다.  
  
### <a name="to-add-a-table-or-table-valued-object-to-a-query"></a>테이블 또는 테이블 반환 개체를 쿼리에 추가하려면  
  
1.  쿼리 및 뷰 디자이너의 **다이어그램 창** 에서 배경을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **테이블 추가** 를 선택합니다.  
  
2.  **테이블 추가** 대화 상자에서 쿼리에 추가할 개체 형식에 대한 탭을 선택합니다.  
  
3.  항목의 목록에서 추가하려는 항목을 두 번 클릭합니다.  
  
4.  항목 추가를 마치면 **닫기**를 클릭합니다.  
  
    쿼리 및 뷰 디자이너는 **다이어그램 창**, **조건 창**및 **SQL 창** 을 적절하게 업데이트합니다.  
  
SQL 창에서 테이블이나 뷰를 문에 참조하면 참조된 테이블과 뷰가 쿼리에 자동으로 추가됩니다.  
  
테이블 또는 테이블 구조 개체에 대한 충분한 액세스 권한이 없거나 드라이버가 이에 대한 정보를 반환하지 않으면 쿼리 및 뷰 디자이너에 데이터 열이 표시되지 않습니다. 이러한 경우에는 테이블이나 테이블 반환 개체에 대해 제목 표시줄과 * (모든 열) 확인란만 표시됩니다.  
  
### <a name="to-add-an-existing-query-to-a-new-query"></a>새 쿼리에 기존 쿼리를 추가하려면  
  
1.  만들려는 새 쿼리에 **SQL 창** 이 표시되어 있어야 합니다.  
  
2.  **SQL 창**에서 FROM이라는 단어 뒤에 여는 괄호와 닫는 괄호 ()를 입력합니다.  
  
3.  기존 쿼리에 대해 쿼리 디자이너를 엽니다. 이제 두 개의 쿼리 디자이너가 열려 있는 상태입니다.  
  
4.  새로운 외부 쿼리에 포함하려는 기존의 내부 쿼리에 대해 **SQL 창** 을 표시합니다.  
  
5.  **SQL 창**에서 텍스트 전체를 선택하여 클립보드에 복사합니다.  
  
6.  새 쿼리의 **SQL 창** 을 클릭하고 앞서 추가했던 괄호 사이에 커서를 놓은 다음 클립보드 내용을 붙여 넣습니다.  
  
7.  **SQL 창**에서 닫는 괄호 뒤에 별칭을 추가합니다.  
  
## <a name="see-also"></a>관련 항목:  
[테이블 별칭 만들기&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[쿼리에서 테이블 제거&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/remove-tables-from-queries-visual-database-tools.md)  
[검색 조건 지정&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[쿼리 결과 요약&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[쿼리 관련 기본 작업 수행&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  

