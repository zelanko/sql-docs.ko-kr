---
title: 찾기 및 바꾸기
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- match case [SQL Server]
- undo operations
- searches [SQL Server Management Studio]
- replacing text
- quick search and replaces [SQL Server Management Studio]
- Query Editor [SQL Server Management Studio], undo
- Query Editor [SQL Server Management Studio], searching
- regular expressions [SQL Server Management Studio]
- finding text [SQL Server Management Studio]
- text [SQL Server], search and replace operations
- finding [SQL Server Management Studio]
- locating text
- Query Editor [SQL Server Management Studio], replacing text
- Find and Replace dialog box
- wildcard options [SQL Server Management Studio]
- match whole word [SQL Server]
- searches [SQL Server Management Studio], replacing
ms.assetid: 3641c7b3-3e3e-4ddd-af82-c15b50004f94
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7fc7b5c7cb0fbd560dc2826af24029d2c7961d95
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75253686"
---
# <a name="search-and-replace"></a>찾기 및 바꾸기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  텍스트를 찾아서 바꾸는 방법에는 여러 가지가 있습니다. **편집** 메뉴에서 **찾기 및 바꾸기** 는 **빠른 찾기**, **빠른 바꾸기**, **파일에서 찾기**또는 **파일에서 바꾸기**의 네 가지 선택 사항을 제공합니다. 이러한 각 항목은 해당 버전의 **찾기 및 바꾸기** 대화 상자를 엽니다. 또한 증분 검색 바로 가기 키를 사용하여 대화 상자 없이 검색을 수행할 수 있습니다. 이러한 기술을 사용하면 찾기 및 바꾸기의 범위를 제어하고 검색 조건과 일치하는 항목 및 바꾼 항목을 검토하는 방법을 선택할 수 있습니다.  
  
 텍스트를 검색하고 바꿀 경우에는 다음 사항을 살펴 보십시오.  
  
-   **찾기 및 바꾸기** 대화 상자에 설정된 옵션은 모든 검색에 영향을 줍니다. 이러한 옵션에는 **대/소문자 구분**, **단어 단위로**, **위로 검색**, **숨겨진 텍스트 검색**, **와일드카드**, **정규식**, **찾는 위치: 모든 열린 문서**, **찾는 위치: 현재 문서**등이 있습니다. 모든 버전의 **찾기 및 바꾸기** 대화 상자에서 모든 옵션을 사용할 수 있는 것은 아닙니다.  
  
-   **실행 취소** 는 바꾸기 작업 이후에 열려 있는 문서에만 사용할 수 있습니다.  
  
-   여러 파일에 대해**모두 바꾸기** 작업의 **실행 취소** 를 수행하면 해당 작업은 영향을 받은 모든 파일에 적용되는 하나의 대량 동작으로 간주됩니다. 즉, 일부 파일에서만 변경 내용을 취소하고 다른 파일에서 변경 내용을 유지할 수는 없습니다.  
  
 일반적으로 그래픽 보기가 포함된 항목은 검색할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [활성 문서에서 입력하는 순서대로 검색](../../relational-databases/scripting/search-an-active-document-incrementally.md)   
 [대화형으로 문서 검색](../../relational-databases/scripting/search-documents-interactively.md)   
 [결과 목록을 사용하여 문서 검색](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [와일드카드로 텍스트 검색](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [정규식을 사용한 텍스트 검색](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
