---
title: "대화형으로 문서 검색 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interactive searches [SQL Server Management Studio]
- searches [SQL Server Management Studio], interactive
- Query Editor [SQL Server Management Studio], interactive search
ms.assetid: dae65ac5-67af-45c6-a6e0-952fea26d680
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a87a33ea63725ae2db48d61d557ff4bf91704490
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="search-documents-interactively"></a>대화형으로 문서 검색
  **찾기 및 바꾸기** 대화 상자를 사용하면 하나 이상의 열려 있는 파일이나 창을 검색하고 검색 조건과 일치하는 항목을 하나씩 이동할 수 있습니다. 이 기술을 사용하면 일치하는 항목 주위의 텍스트 컨텍스트에서 일치하는 개별 항목을 검토할 수 있습니다. 또한 **찾기 및 바꾸기** 대화 상자를 사용하여 대량 찾기 작업을 수행하고 검색 조건과 일치하는 항목을 보고서 형식으로 검토할 수 있습니다.  
  
### <a name="to-search-all-open-documents"></a>열린 모든 문서를 검색하려면  
  
1.  검색할 항목을 엽니다.  
  
2.  **편집** 메뉴에서 **찾기 및 바꾸기** 를 가리킨 다음 **빠른 찾기**를 클릭합니다.  
  
3.  **찾기 및 바꾸기** 입력란에 검색할 텍스트를 입력합니다.  
  
4.  **찾는 위치** 목록에서 **모든 열린 문서**를 선택합니다.  
  
    > [!NOTE]  
    >  **모든 열린 문서** 를 선택한 경우 열려 있는 특정 파일이 검색되지 않을 수 있습니다. 텍스트 뷰(예: 코드 뷰)에서 현재 열려 있는 파일만 검색에 포함됩니다. 디자이너 뷰의 파일은 검색에 포함되지 않습니다.  
  
5.  검색의 정확도를 높이려면 추가 검색 옵션을 선택합니다.  
  
6.  **다음 찾기** 를 클릭하여 검색을 시작하고 마지막 파일이 검색될 때까지 계속해서 **다음 찾기** 를 클릭합니다.  
  
 문서의 시작 또는 끝을 검색이 통과하면 상태 표시줄에 메시지가 표시됩니다. 검색의 시작 지점에 검색이 도달하면 메시지 상자가 나타납니다.  
  
#### <a name="to-replace-in-all-active-files-interactively"></a>모든 활성 파일에서 대화형으로 바꾸려면  
  
1.  **편집** 메뉴에서 **찾기 및 바꾸기**를 가리킨 다음 **빠른 바꾸기**를 클릭합니다.  
  
2.  **찾을 내용** 상자에 검색할 텍스트를 입력합니다.  
  
3.  **바꿀 내용** 상자에 검색 텍스트를 바꿀 텍스트를 입력합니다.  
  
4.  **찾는 위치** 목록에서 **모든 열린 문서**를 선택합니다.  
  
5.  **바꾸기**를 클릭하고 마지막 파일의 마지막 항목이 바뀔 때까지 계속해서 **바꾸기** 를 클릭합니다. 바꾸지 않을 항목을 건너뛰려면 **다음 찾기** 를 클릭합니다.  
  
     -또는-  
  
     **모두 바꾸기** 를 선택하여 일치하는 모든 항목을 바꿉니다. 바뀐 항목의 총 개수가 표시되는 메시지 상자가 나타납니다.  
  
 **모두 바꾸기** 명령은 **다음 찾기** 단추로 건너뛴 항목을 비롯하여 일치하는 모든 항목을 바꿉니다. **모두 바꾸기**를 취소하려면 파일을 닫기 전에 **편집** 메뉴에서 **실행 취소** 를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [활성 문서에서 입력하는 순서대로 검색](../../relational-databases/scripting/search-an-active-document-incrementally.md)   
 [찾기 및 바꾸기](../../relational-databases/scripting/search-and-replace.md)   
 [결과 목록을 사용하여 문서 검색](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [와일드카드로 텍스트 검색](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [정규식을 사용한 텍스트 검색](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
