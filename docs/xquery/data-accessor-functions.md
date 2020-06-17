---
title: 데이터 접근자 함수 | Microsoft Docs
description: 'XQuery 데이터 접근자 함수 fn: data (), fn: string () 및 text ()를 사용 하는 방법에 대해 알아봅니다.'
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
ms.openlocfilehash: d25fa2236feb02ba8ed726dc56b946dc09350d1c
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84881879"
---
# <a name="data-accessor-functions"></a>데이터 접근자 함수
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 섹션의 항목에서는 데이터 접근자 함수에 대해 설명하고 예제 코드를 제공합니다.  
  
## <a name="understanding-fndata-fnstring-and-text"></a>fn:data(), fn:string() 및 text() 이해  
 XQuery에는 함수 **fn: data ()** 가 있습니다. 여기에는 스칼라, 형식화 된 값을 추출 하 고, 노드 테스트 **텍스트 ()** 는 텍스트 노드를 반환 하 고, **fn: string (** ) 함수는 노드의 문자열 값을 반환 합니다. 이들 함수의 용도는 혼동될 수 있습니다. 다음은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 이러한 함수를 올바르게 사용하기 위한 지침입니다. XML 인스턴스 \<age> 12는 \</age> 그림의 목적으로 사용 됩니다.  
  
-   형식화 되지 않은 XML: 경로 식/age/text ()는 텍스트 노드 "12"를 반환 합니다. fn:data(/age) 함수는 문자열 값 "12"를 반환하고 fn:string(/age)도 "12"를 반환합니다.  
  
-   형식화 된 XML: 식/age/text ()는 단순 형식화 된 요소에 대 한 정적 오류를 반환 합니다 \<age> . 반면에 fn:data(/age)는 정수 12를 반환하고 fn:string(/age)는 문자열 "12"를 반환합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [XQuery&#41;&#40;문자열 함수](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [데이터 함수 &#40;XQuery&#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>참고 항목  
 [XQuery의 경로 식 &#40;&#41;](../xquery/path-expressions-xquery.md)  
  
  
