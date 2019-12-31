---
title: 와일드카드로 텍스트 검색
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vswildcardsbuilder
helpviewer_keywords:
- searches [SQL Server Management Studio], wildcards
- Query Editor [SQL Server Management Studio], wildcard searches
- wildcard options [SQL Server Management Studio]
ms.assetid: 449600f8-cc87-4b3f-878a-59c158a88a40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caeda52d612f4df6672f686e06834de6fef0cc67
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243284"
---
# <a name="search-text-with-wildcards"></a>와일드카드로 텍스트 검색
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **찾기 및 바꾸기** 대화 상자의 **찾을 내용** 필드에서 다음 식은 문자나 숫자를 바꿀 수 있습니다.  
  
#### <a name="to-search-using-wildcards"></a>와일드카드를 사용하여 검색하려면  
  
1.  빠른 찾기, **파일에서 찾기** , **빠른 바꾸기**또는 **파일에서 바꾸기**작업 중에 **찾을 내용** 필드에서 와일드카드를 사용할 수 있게 하려면 **찾기 옵션** 아래에서 **사용** 옵션을 선택한 다음 **와일드카드**를 선택합니다.  
  
2.  그러면 **찾을 내용** 필드 옆에 있는 삼각형 **참조 목록** 단추를 사용할 수 있습니다. 이 단추를 클릭하여 사용할 수 있는 와일드카드 목록을 표시합니다. 
  **참조 목록**에서 임의의 항목을 선택하면 해당 항목이 **찾을 대상** 문자열에 삽입됩니다.  
  
 다음 표에서는 **참조 목록**에서 사용할 수 있는 와일드카드를 설명합니다.  
  
|식|구문|설명|  
|----------------|------------|-----------------|  
|임의의 단일 문자|?|임의의 문자 하나에 대응합니다.|  
|임의의 단일 숫자|#|임의의 숫자 하나와 대응합니다. 예를 들어 7#은 7 다음에 다른 숫자 하나가 표시되는 숫자와 일치합니다(즉, 71과는 일치하지만 17과는 일치하지 않음).|  
|집합에 없는 문자|[! ]|집합에 지정되지 않는 임의의 문자 하나와 대응합니다.|  
|하나 이상의 문자|*|하나 이상의 임의의 문자와 대응합니다. 예를 들어 new*는 "new"를 포함하는 임의의 텍스트(예: newfile.txt)와 대응합니다.|  
|문자 집합|[ ]|집합에 지정된 문자 중 하나와 대응합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [검색 및 바꾸기](search-and-replace.md)   
 [정규식을 사용 하 여 텍스트 검색](search-text-with-regular-expressions.md)  
