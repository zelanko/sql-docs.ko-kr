---
title: "XML 열에 전체 텍스트 검색 사용 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- xml columns [full-text search]
- indexes [full-text search]
ms.assetid: 8096cfc6-1836-4ed5-a769-a5d63b137171
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5564331e341498a5c63550e08e466db859f5762b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="use-full-text-search-with-xml-columns"></a>XML 열에 전체 텍스트 검색 사용
  XML 값의 내용을 인덱싱하지만 XML 태그는 무시하는 전체 텍스트 인덱스를 XML 열에 만들 수 있습니다. 요소 태그는 토큰 경계로 사용됩니다. 다음 항목이 인덱싱됩니다.  
  
-   XML 요소의 내용입니다.  
  
-   그 값이 숫자 값이 아니면 최상위 요소의 XML 특성의 내용만 해당합니다.  
  
 가능한 경우 다음과 같은 방식으로 전체 텍스트 검색을 XML 인덱스와 조합할 수 있습니다.  
  
1.  먼저 SQL 전체 텍스트 검색을 사용하여 원하는 XML 값을 필터링합니다.  
  
2.  그런 다음 XML 열에서 XML 인덱스를 사용하는 해당 XML 값을 쿼리합니다.  
  
## <a name="example-combining-full-text-search-with-xml-querying"></a>예제: 전체 텍스트 검색을 XML 쿼리와 결합  
 XML 열에 전체 텍스트 인덱스를 만든 후 다음 쿼리는 XML 값에 책 제목 중 "custom"이라는 단어가 포함되어 있는지 확인합니다.  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'custom')   
AND    xCol.exist('/book/title/text()[contains(.,"custom")]') =1  
```  
  
 **contains()** 메서드는 전체 텍스트 인덱스를 사용하여 문서의 아무 곳에나 "custom"이 포함된 XML 값을 분류합니다. **exist()** 절은 "custom"이 책의 제목 부분에 있는지 확인합니다.  
  
 **contains()** 및 XQuery **contains()** 를 사용하는 전체 텍스트 검색은 서로 다른 의미를 가집니다. 후자는 하위 문자열 일치 검색이며 전자는 형태소 분석을 사용하는 토큰 일치 검색입니다. 따라서 검색이 제목에 "run"이 포함된 문자열을 찾는 경우, 전체 텍스트 **contains()** 및 Xquery **contains()** 가 모두 만족하기 때문에 일치 항목에는 "run", "runs" 및 "running"이 포함됩니다. 하지만 쿼리가 전체 텍스트 **contains()** 가 실패한 제목에서 "customizable"이라는 단어와 일치하지 않지만 Xquery **contains()** 는 만족합니다. 일반적으로 순수한 부분 문자열 비교를 위해 전체 텍스트 **contains()** 절을 제거해야 합니다.  
  
 또한 전체 텍스트 검색은 단어 형태소 분석을 사용하지만 XQuery **contains()** 는 리터럴 일치 검색입니다. 이러한 차이점은 다음 예에서 확인할 수 있습니다.  
  
## <a name="example-full-text-search-on-xml-values-using-stemming"></a>예제: 형태소 분석을 사용하여 XML 값에서 전체 텍스트 검색  
 이전 예에서 수행된 XQuery **contains()** 검사는 일반적으로 제거할 수 없습니다. 다음 쿼리를 살펴보십시오.  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'run')   
```  
  
 문서에 있는 "ran"이라는 단어는 형태소 분석으로 인해 검색 조건과 일치합니다. 또한 검색 컨텍스트는 XQuery를 사용하여 검사되지 않습니다.  
  
 전체 텍스트 인덱싱되는 AXSD를 사용하여 XML을 관계형 열로 분해하는 경우 XML 뷰에 대해 발생하는 XPath 쿼리는 기본 테이블에서 전체 텍스트 검색을 수행하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 인덱스&#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  
