---
title: 경로 식의 구문을 약어를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- abbreviated syntax [XQuery]
ms.assetid: f83c2e41-5722-47c3-b5b8-bf0f8cbe05d3
caps.latest.revision: 23
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 30a856638a4210c964f3e10311e99f4ddf69fd91
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="path-expressions---using-abbreviated-syntax"></a>경로 식에서 축약형된 구문 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  모든 예 [xquery에서 경로 식 이해](../xquery/path-expressions-xquery.md) 경로 식에 대해 축약 하지 않은 구문을 사용 합니다. 경로 식의 축 단계에 대해 축약하지 않은 구문은 축 이름과 노드 테스트를 포함하고 두 개의 콜론으로 분리되며 뒤에 0개 이상의 단계 한정자가 옵니다.  
  
 예를 들어:  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 XQuery는 경로 식에 사용하기 위해 다음 축약을 지원합니다.  
  
-   **자식** 축이 기본 축입니다. 따라서는 **자식::** 축은 식의 단계에서 생략할 수 있습니다. 예를 들어 `/child::ProductDescription/child::Summary`를 `/ProductDescription/Summary`로 쓸 수 있습니다.  
  
-   **특성** 축으로 축약할 수 있습니다 @합니다. 예를 들어 `/child::ProductDescription[attribute::ProductModelID=10]`를 `/ProudctDescription[@ProductModelID=10]`로 쓸 수 있습니다.  
  
-   A **/descendant-or-self::node()/** 로 축약할 수 / /입니다. 예를 들어 `/descendant-or-self::node()/child::act:telephoneNumber`를 `//act:telephoneNumber`로 쓸 수 있습니다.  
  
     이전 쿼리는 Contact 테이블의 AdditionalContactInfo 열에 저장된 모든 전화 번호를 검색합니다. AdditionalContactInfo의 스키마는 방식으로 정의 하는 \<telephoneNumber > 요소 위치 문서에서 사용할 수 있습니다. 따라서 전화 번호를 모두 검색하려면 문서의 모든 노드를 검색해야 합니다. 검색은 문서의 루트에서 시작되어 모든 하위 노드로 진행됩니다.  
  
     다음 쿼리에서는 특정 고객 연락처에 대한 모든 전화 번호를 검색합니다.  
  
    ```  
    SELECT AdditionalContactInfo.query('             
                declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";             
                declare namespace crm="http://schemas.adventure-works.com/Contact/Record";             
                declare namespace ci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";             
                /descendant-or-self::node()/child::act:telephoneNumber             
                ') as result             
    FROM Person.Contact             
    WHERE ContactID=1             
    ```  
  
     경로 식 대신 축약형 구문인 `//act:telephoneNumber`를 사용하는 경우 같은 결과를 얻게 됩니다.  
  
-   **self:: node ()** 단계에서 단일 점 (.)으로 축약 될 수 있습니다. 그러나 점 없거나 해당 메서드와 호환는 **self:: node ()** 합니다.  
  
     예를 들어 다음 쿼리에서 점을 사용하는 것은 노드가 아닌 값을 나타냅니다.  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   **부모:: node ()** 단계에서 이중 점 (.)으로 축약 될 수 있습니다.  
  
  
