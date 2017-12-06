---
title: "데이터 접근자 함수 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords: data-accessor functions [XQuery]
ms.assetid: 31bad04f-7c74-4773-9f83-612704fdd21c
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed2c535c046fe7d2fc9d830eb2c3f9e3cfd9a7bf
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="data-accessor-functions"></a>데이터 접근자 함수
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 섹션의 항목에서는 데이터 접근자 함수에 대해 설명하고 예제 코드를 제공합니다.  
  
## <a name="understanding-fndata-fnstring-and-text"></a>fn:data(), fn:string() 및 text() 이해  
 에 함수는 XQuery **fn:data()** 노드를 노드 테스트에서 형식화 된 스칼라 값을 추출 하 **text ()** 텍스트 노드 및 함수 반환을 **fn: string** 반환 하는 노드의 문자열 값입니다. 이들 함수의 용도는 혼동될 수 있습니다. 다음은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 이러한 함수를 올바르게 사용하기 위한 지침입니다. XML 인스턴스 \<age > 12 \< /a g e >는 설명을 위해 사용 합니다.  
  
-   형식화 되지 않은 XML: 경로 식 /age/text () 텍스트 노드 "12"를 반환합니다. fn:data(/age) 함수는 문자열 값 "12"를 반환하고 fn:string(/age)도 "12"를 반환합니다.  
  
-   형식화 된 XML: 식 /age/text ()에 대 한 모든 단순 유형의 정적 오류를 반환 합니다 \<age > 요소입니다. 반면에 fn:data(/age)는 정수 12를 반환하고 fn:string(/age)는 문자열 "12"를 반환합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [문자열 함수 &#40; XQuery &#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [데이터 함수 &#40; XQuery &#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>관련 항목:  
 [경로 식 &#40; XQuery &#41;](../xquery/path-expressions-xquery.md)  
  
  
