---
title: "런타임에 OData 원본 쿼리를 수정 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e061fe6989d9629d655d9e0c08f2cd4c1d932540
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="modify-odata-source-query-at-runtime"></a>런타임에 OData 원본 쿼리 수정
  데이터 흐름 태스크의 **[OData Source].[Query]** 속성에 식을 추가하여 런타임에 OData 원본 쿼리를 수정할 수 있습니다.  
  
 열은 디자인 타임에 사용된 것과 동일하게 유지되어야 합니다. 그렇지 않으면 패키지가 실행될 때 오류가 발생합니다. $select 쿼리 옵션을 사용할 때 동일한 열을 같은 순서로 지정해야 합니다. $select 옵션을 사용하는 것보다 안전한 방법은 원본 구성 요소 UI에서 직접 원하지 않는 열의 선택을 취소하는 것입니다.  
  
 런타임에 쿼리 값을 동적으로 설정하는 몇 가지 다른 방법이 있습니다. 보다 일반적인 방법 중 몇 가지는 다음과 같습니다.  
  
## <a name="exposing-the-query-as-a-parameter"></a>쿼리를 매개 변수로 노출  
 다음 절차에는 OData 원본 구성 요소에서 패키지에 대한 매개 변수로 사용하는 쿼리를 노출하는 단계가 있습니다.  
  
1.  **데이터 흐름 태스크** 를 마우스 오른쪽 단추로 클릭하고 **매개 변수화…**옵션을 선택합니다. 옵션에 로컬 컴퓨터 이름을 지정한 경우  
  
2.  에 **매개 변수화** 대화 상자에서 **[\<의 OData 원본 구성 요소 이름 >]. [ 쿼리]** 에 대 한 **속성**합니다.  
  
3.  **새 매개 변수 만들기** 또는 **기존 매개 변수 사용**중에서 하나를 선택합니다.  
  
4.  **새 매개 변수 만들기**를 선택하는 경우 다음을 수행합니다.  
  
    1.  매개 변수의 **이름** 및 **설명** 을 입력합니다.  
  
    2.  매개 변수의 기본 **값** 을 지정합니다.  
  
    3.  매개 변수의 **범위** (**패키지** 또는 **프로젝트**)를 지정합니다.  
  
    4.  매개 변수가 **필수** 인지 여부를 지정합니다.  
  
5.  **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
## <a name="using-an-expression"></a>식 사용  
 이 방법은 런타임에 쿼리 문자열을 동적으로 생성하려는 경우에 유용합니다. 이 예에서 MaxRows 변수는 다른 수단(스크립트, 매개 변수 등)을 통해 설정됩니다.  
  
1.  **OData 원본** 이 포함된 **데이터 흐름 태스크**를 선택합니다.  
  
2.  **속성** 창에서 **Expressions** 속성을 강조 표시합니다.  
  
3.  …(줄임표) 단추를 클릭하여 **속성 식 편집기**를 엽니다.  
  
4.  **[OData Source].[Query]** 속성을 선택합니다.  
  
5.  …(줄임표) 단추를 **식**에 대해 클릭합니다.  
  
6.  **식**을 입력합니다.  
  
7.  **확인**을 클릭합니다.  
  
> [!WARNING]  
>  이 방법을 사용할 때는 설정된 값이 적절하게 URL로 인코딩되었는지 확인해야 합니다. 사용자 입력에서 값을 받을 때(예를 들어 매개 변수에서 개별 쿼리 옵션을 설정할 때) 잠재적인 SQL 삽입형 공격을 방지하기 위해 값의 유효성을 검사해야 합니다.  
  
  
