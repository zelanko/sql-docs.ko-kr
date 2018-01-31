---
title: "런타임에 OData 원본 쿼리 제공 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 457e4f5b8d52be56aa82f854e5a87caae72ebd99
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="provide-an-odata-source-query-at-runtime"></a>런타임에 OData 원본 쿼리 제공
 데이터 흐름 태스크의 **[OData Source].[Query]** 속성에 *식*을 추가하여 런타임에 OData 원본 쿼리를 수정할 수 있습니다.  
  
 반환되는 열은 디자인 타임에서 반환된 열과 동일해야 합니다. 그렇지 않으면 패키지를 실행할 때 오류가 발생합니다. $select 쿼리 옵션을 사용할 때 동일한 열을 같은 순서로 지정해야 합니다. $select 옵션을 사용하는 것보다 안전한 방법은 원본 구성 요소 UI에서 직접 원하지 않는 열의 선택을 취소하는 것입니다.  
  
 런타임에 쿼리 값을 동적으로 설정하는 몇 가지 다른 방법이 있습니다. 보다 일반적인 방법 중 몇 가지는 다음과 같습니다.  
  
## <a name="provide-the-query-as-a-parameter"></a>쿼리를 매개 변수로 제공  
 다음 절차는 OData 원본 구성 요소에서 패키지의 매개 변수로 사용하는 쿼리를 노출하는 방법을 보여 줍니다.  
  
1.  **데이터 흐름 태스크** 를 마우스 오른쪽 단추로 클릭하고 **매개 변수화…**옵션을 선택합니다. 옵션에 로컬 컴퓨터 이름을 지정한 경우  
  
2.  **매개 변수화** 대화 상자에서 **속성**에 대한 **[\<OData 원본 구성 요소 이름>].[Query]**를 선택합니다.  
  
3.  **새 매개 변수 만들기** 또는 **기존 매개 변수 사용**중에서 하나를 선택합니다.  
  
4.  **새 매개 변수 만들기**를 선택하는 경우:  
  
    1.  매개 변수의 **이름** 및 **설명** 을 입력합니다.  
  
    2.  매개 변수의 기본 **값** 을 지정합니다.  
  
    3.  매개 변수의 **범위** (**패키지** 또는 **프로젝트**)를 지정합니다.  
  
    4.  매개 변수가 **필수** 인지 여부를 지정합니다.  
  
5.  **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
## <a name="provide-the-query-with-an-expression"></a>식으로 쿼리 제공
 이 방법은 런타임에 쿼리 문자열을 동적으로 생성하려는 경우에 유용합니다.
  
1.  **OData 원본**이 포함된 **데이터 흐름 태스크**를 선택합니다.  
  
2.  **속성** 창에서 **Expressions** 속성을 강조 표시합니다.  
  
3.  …(줄임표) 단추를 클릭하여 **속성 식 편집기**를 엽니다.  
  
4.  **[OData Source].[Query]** 속성을 선택합니다.  
  
5.  …(줄임표) 단추를 **식**에 대해 클릭합니다.  
  
6.  **식**을 입력합니다.  
  
7.  **확인**을 클릭합니다.  
  
> [!NOTE]  
> 이 방법을 사용할 때는 설정된 값이 적절하게 URL로 인코딩되었는지 확인해야 합니다. 사용자 입력에서 값을 받을 때(예를 들어 매개 변수에서 개별 쿼리 옵션을 설정할 때) 잠재적인 SQL 삽입형 공격을 방지하기 위해 값의 유효성을 검사해야 합니다.  
  
  
