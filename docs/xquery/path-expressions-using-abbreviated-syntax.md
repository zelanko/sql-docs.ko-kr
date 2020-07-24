---
title: 경로 식에 약식 구문 사용 | Microsoft Docs
description: XQuery 경로 식에서 약식 구문을 사용 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- abbreviated syntax [XQuery]
ms.assetid: f83c2e41-5722-47c3-b5b8-bf0f8cbe05d3
author: rothja
ms.author: jroth
ms.openlocfilehash: 4b8270babb8fe592c050a9352a7fd687660b178e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920099"
---
# <a name="path-expressions---using-abbreviated-syntax"></a>경로 식 - 축약형 구문 사용
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  [XQuery의 경로 식 이해](../xquery/path-expressions-xquery.md) 의 모든 예에서는 경로 식에 대해 축약 되지 않은 구문을 사용 합니다. 경로 식의 축 단계에 대해 축약하지 않은 구문은 축 이름과 노드 테스트를 포함하고 두 개의 콜론으로 분리되며 뒤에 0개 이상의 단계 한정자가 옵니다.  
  
 예를 들어:  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 XQuery는 경로 식에 사용하기 위해 다음 축약을 지원합니다.  
  
-   **자식** 축이 기본 축입니다. 따라서 식의 단계에서 **child::** axis를 생략할 수 있습니다. 예를 들어 `/child::ProductDescription/child::Summary`를 `/ProductDescription/Summary`로 쓸 수 있습니다.  
  
-   **특성** 축은로 약식으로 지정할 수 있습니다 @ . 예를 들어 `/child::ProductDescription[attribute::ProductModelID=10]`를 `/ProudctDescription[@ProductModelID=10]`로 쓸 수 있습니다.  
  
-   **/Descendant-or-self:: node ()/** 는//로 약식으로 지정할 수 있습니다. 예를 들어 `/descendant-or-self::node()/child::act:telephoneNumber`를 `//act:telephoneNumber`로 쓸 수 있습니다.  
  
     이전 쿼리는 Contact 테이블의 AdditionalContactInfo 열에 저장된 모든 전화 번호를 검색합니다. Additional된 정보에 대 한 스키마는 \<telephoneNumber> 요소가 문서 어디에 나 나타날 수 있는 방식으로 정의 됩니다. 따라서 전화 번호를 모두 검색하려면 문서의 모든 노드를 검색해야 합니다. 검색은 문서의 루트에서 시작되어 모든 하위 노드로 진행됩니다.  
  
     다음 쿼리에서는 특정 고객 연락처에 대한 모든 전화 번호를 검색합니다.  
  
    ```  
    SELECT AdditionalContactInfo.query('             
                declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";             
                declare namespace crm="https://schemas.adventure-works.com/Contact/Record";             
                declare namespace ci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";             
                /descendant-or-self::node()/child::act:telephoneNumber             
                ') as result             
    FROM Person.Contact             
    WHERE ContactID=1             
    ```  
  
     경로 식 대신 축약형 구문인 `//act:telephoneNumber`를 사용하는 경우 같은 결과를 얻게 됩니다.  
  
-   단계의 **self:: node ()** 는 단일 점 (.)으로 축약 될 수 있습니다. 그러나 점이 **self:: node ()** 와 동일 하거나 서로 교환할 수 없습니다.  
  
     예를 들어 다음 쿼리에서 점을 사용하는 것은 노드가 아닌 값을 나타냅니다.  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   단계의 **부모:: node ()** 는 이중 점 (..)으로 축약 될 수 있습니다.  
  
  
