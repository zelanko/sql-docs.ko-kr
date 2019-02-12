---
title: 데이터 접근자 함수 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- data-accessor functions [XQuery]
ms.assetid: 31bad04f-7c74-4773-9f83-612704fdd21c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1c28f61a39e45ea101f2e999d5787dfa23cb29c2
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031794"
---
# <a name="data-accessor-functions"></a>데이터 접근자 함수
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 섹션의 항목에서는 데이터 접근자 함수에 대해 설명하고 예제 코드를 제공합니다.  
  
## <a name="understanding-fndata-fnstring-and-text"></a>fn:data(), fn:string() 및 text() 이해  
 XQuery 함수를 포함 **fn:data()** 노드를 노드 테스트에서 형식화 된 스칼라 값을 추출 하 **text ()** 텍스트 노드 및 함수가 반환할 **fn: string** 반환 하는 합니다 노드의 문자열 값입니다. 이들 함수의 용도는 혼동될 수 있습니다. 다음은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 이러한 함수를 올바르게 사용하기 위한 지침입니다. XML 인스턴스에 \<age > 12\<age/>는 설명을 위해 사용 합니다.  
  
-   형식화되지 않은 XML: 경로 식 /age/text()는 텍스트 노드 "12"를 반환합니다. fn:data(/age) 함수는 문자열 값 "12"를 반환하고 fn:string(/age)도 "12"를 반환합니다.  
  
-   형식화된 XML: 모든 단순 형식에 대 한 정적 오류를 반환 하는 식 /age/text () \<age > 요소입니다. 반면에 fn:data(/age)는 정수 12를 반환하고 fn:string(/age)는 문자열 "12"를 반환합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [string 함수 &#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [data 함수 &#40;XQuery&#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>관련 항목  
 [경로 식 &#40;XQuery&#41;](../xquery/path-expressions-xquery.md)  
  
  
