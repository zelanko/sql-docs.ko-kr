---
title: "런타임에 OData 원본 쿼리를 제공 합니다. | Microsoft Docs"
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
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 9da1f1be0a790d01f9403d6fc05a5c1498c0ee8b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/23/2017

---
# <a name="provide-an-odata-source-query-at-runtime"></a>런타임에 OData 원본 쿼리를 제공 합니다.
 추가 하 여 런타임에 OData 원본 쿼리를 수정할 수는 *식* 에 **[OData Source]. [ 쿼리]** 데이터 흐름 태스크의 속성입니다.  
  
 반환 되는 열; 디자인 타임에 반환 된 같은 열이 될 해야 합니다. 그렇지 않으면 패키지를 실행할 때 오류가 발생. $select 쿼리 옵션을 사용할 때 동일한 열을 같은 순서로 지정해야 합니다. $select 옵션을 사용하는 것보다 안전한 방법은 원본 구성 요소 UI에서 직접 원하지 않는 열의 선택을 취소하는 것입니다.  
  
 런타임에 쿼리 값을 동적으로 설정하는 몇 가지 다른 방법이 있습니다. 다음은 보다 일반적인 방법 중 일부입니다.  
  
## <a name="provide-the-query-as-a-parameter"></a>쿼리 매개 변수로 제공  
 다음 절차에는 OData 원본 구성 요소는 패키지의 매개 변수로 사용 하는 쿼리를 노출 하는 방법을 보여 줍니다.  
  
1.  **데이터 흐름 태스크** 를 마우스 오른쪽 단추로 클릭하고 **매개 변수화…**옵션을 선택합니다. 옵션에 로컬 컴퓨터 이름을 지정한 경우  
  
2.  에 **매개 변수화** 대화 상자에서 **[\<의 OData 원본 구성 요소 이름 >]. [ 쿼리]** 에 대 한 **속성**합니다.  
  
3.  **새 매개 변수 만들기** 또는 **기존 매개 변수 사용**중에서 하나를 선택합니다.  
  
4.  선택 하는 경우 **새 매개 변수 만들기**:  
  
    1.  매개 변수의 **이름** 및 **설명** 을 입력합니다.  
  
    2.  매개 변수의 기본 **값** 을 지정합니다.  
  
    3.  매개 변수의 **범위** (**패키지** 또는 **프로젝트**)를 지정합니다.  
  
    4.  매개 변수가 **필수** 인지 여부를 지정합니다.  
  
5.  **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
## <a name="provide-the-query-with-an-expression"></a>식으로 쿼리를 제공 합니다.
 이 방법은 런타임에 쿼리 문자열을 동적으로 생성 하려는 경우에 유용 합니다.
  
1.  선택은 **데이터 흐름 태스크** 를 포함 하 여 **OData 원본**합니다.  
  
2.  **속성** 창에서 **Expressions** 속성을 강조 표시합니다.  
  
3.  …(줄임표) 단추를 (줄임표) 단추를는 **속성 식 편집기**합니다.  
  
4.  **[OData Source].[Query]** 속성을 선택합니다.  
  
5.  …(줄임표) 단추를 에 대 한 (줄임표) 단추 **식**합니다.  
  
6.  **식**을 입력합니다.  
  
7.  **확인**을 클릭합니다.  
  
> [!NOTE]  
> 이 방법을 사용 하면 설정한 값은 URL로 인코딩된 제대로 확인 해야 합니다. 사용자 입력에서 값을 받을 때(예를 들어 매개 변수에서 개별 쿼리 옵션을 설정할 때) 잠재적인 SQL 삽입형 공격을 방지하기 위해 값의 유효성을 검사해야 합니다.  
  
  

