---
title: 활성 문서에서 입력하는 순서대로 검색 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], incremental
- Query Editor [SQL Server Management Studio], incremental search
- incremental searches [SQL Server Management Studio]
ms.assetid: 490bb36c-dd43-4219-9e2a-ff27046b9395
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e491d415ec1bcb62c95366f2471ba6780ad3874f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65821963"
---
# <a name="search-an-active-document-incrementally"></a>활성 문서에서 입력하는 순서대로 검색
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  텍스트를 입력하여 하나의 문서나 창을 증분식으로 검색할 수 있습니다. 검색 작업은 문서나 창에서 증분 검색 중에 입력된 문자와 일치하는 첫 번째 문자 집합을 강조 표시합니다. 증분 검색은 숨겨진 텍스트를 제외하고 문서나 창에 있는 모든 텍스트를 자동으로 검색합니다.  
  
 **대/소문자 구분** 옵션의 경우 증분 검색은 이전 검색의 조건을 사용합니다. 예를 들어 **파일에서 찾기** 대화 상자를 사용하여 여러 파일을 검색했으며 **대/소문자 구분**을 선택한 경우 다음에 증분식으로 검색을 수행하면 검색에서 대/소문자를 구분합니다.  
  
### <a name="to-search-incrementally"></a>증분식으로 검색하려면  
  
1.  검색할 파일이나 창을 엽니다.  
  
2.  **편집** 메뉴에서 **고급**을 가리킨 다음 **증분 검색**을 클릭합니다.  
  
     커서 아이콘이 검색 방향을 나타나는 화살표가 있는 쌍안경 모양으로 바뀌고 상태 표시줄에 "증분 검색"이 표시됩니다.  
  
3.  텍스트 문자열 입력을 시작합니다.  
  
     입력하는 텍스트가 상태 표시줄에 표시되면서 텍스트와 일치하는 첫 번째 항목이 편집기에서 강조 표시됩니다. 입력을 계속하면 편집기는 일치하는 다음 항목으로 이동하여 해당 항목을 강조 표시합니다. 일치하는 항목이 없으면 상태 표시줄에 다음이 표시됩니다.  
  
    ```  
    Incremental Search: <text> (not found)  
    ```  
  
 증분 검색은 문서의 현재 위치에서 아래 방향으로 왼쪽에서 오른쪽으로 수행됩니다. 바로 가기 키를 사용하여 증분 검색을 수행할 수 있습니다.  
  
> [!NOTE]  
>  바로 가기 키의 전체 목록을 보려면 [SQL Server Management Studio 바로 가기 키](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [찾기 및 바꾸기](../../relational-databases/scripting/search-and-replace.md)   
 [대화형으로 문서 검색](../../relational-databases/scripting/search-documents-interactively.md)   
 [결과 목록을 사용하여 문서 검색](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [와일드카드로 텍스트 검색](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [정규식을 사용한 텍스트 검색](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
