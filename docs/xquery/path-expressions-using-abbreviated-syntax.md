---
title: 경로 식의 구문을 사용 하 여 간략 한 형태로 | Microsoft Docs
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
ms.openlocfilehash: 8e75db08f283631cf9b5daf064790786a1abc10f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946411"
---
# <a name="path-expressions---using-abbreviated-syntax"></a>경로 식 - 축약형 구문 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  모든 예제 [xquery에서 경로 식 이해](../xquery/path-expressions-xquery.md) 경로 식에 대해 축약 하지 않은 구문을 사용 합니다. 경로 식의 축 단계에 대해 축약하지 않은 구문은 축 이름과 노드 테스트를 포함하고 두 개의 콜론으로 분리되며 뒤에 0개 이상의 단계 한정자가 옵니다.  
  
 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 XQuery는 경로 식에 사용하기 위해 다음 축약을 지원합니다.  
  
-   합니다 **자식** 축이 기본 축입니다. 따라서 합니다 **자식::** 축은 식의 단계에서 생략할 수 있습니다. 예를 들어 `/child::ProductDescription/child::Summary`를 `/ProductDescription/Summary`로 쓸 수 있습니다.  
  
-   **특성** 축으로 축약할 수 있습니다 @합니다. 예를 들어 `/child::ProductDescription[attribute::ProductModelID=10]`를 `/ProudctDescription[@ProductModelID=10]`로 쓸 수 있습니다.  
  
-   A **/descendant-or-self::node()** 로 축약할 수 있습니다 / /입니다. 예를 들어 `/descendant-or-self::node()/child::act:telephoneNumber`를 `//act:telephoneNumber`로 쓸 수 있습니다.  
  
     이전 쿼리는 Contact 테이블의 AdditionalContactInfo 열에 저장된 모든 전화 번호를 검색합니다. AdditionalContactInfo의 스키마는 방식으로 정의 하는 \<telephoneNumber > 요소가 문서의 아무 곳 이나 나타날 수 있습니다. 따라서 전화 번호를 모두 검색하려면 문서의 모든 노드를 검색해야 합니다. 검색은 문서의 루트에서 시작되어 모든 하위 노드로 진행됩니다.  
  
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
  
-   합니다 **self:: node ()** 단계에서 단일 점 (.)로 축약할 수 있습니다. 그러나 점 없거나 해당 메서드와 호환 합니다 **self:: node ()** 합니다.  
  
     예를 들어 다음 쿼리에서 점을 사용하는 것은 노드가 아닌 값을 나타냅니다.  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   합니다 **부모:: node ()** 단계에서 이중 점 (.)로 축약할 수 있습니다.  
  
  
