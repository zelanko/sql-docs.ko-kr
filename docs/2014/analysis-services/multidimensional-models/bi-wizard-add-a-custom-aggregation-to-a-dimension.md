---
title: 차원에 사용자 지정 집계 추가 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], Business Intelligence enhancements
- Business Intelligence enhancements [Analysis Services], custom aggregations
- aggregations [Analysis Services], custom
- unary operators
- custom aggregations [Analysis Services]
ms.assetid: 3199a6c2-a06d-47b9-bd1c-604dbb085318
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e647b32d8f94ebd545a9d8d85d066a25dde6e77c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66076905"
---
# <a name="add-a-custom-aggregation-to-a-dimension"></a>차원에 사용자 지정 집계 추가
  큐브나 차원에 향상된 사용자 지정 집계 기능을 추가하여 차원 멤버와 연결되는 기본 집계를 다른 단항 연산자로 바꿀 수 있습니다. 이 향상된 기능은 부모-자식 계층의 멤버에 대한 롤업을 정의하는 차원 테이블에 단항 연산자 열을 지정합니다. 단항 연산자는 부모-자식 계층의 부모 특성에 대해 실행됩니다.  
  
> [!NOTE]  
>  사용자 지정 집계는 기존 데이터 원본 기반의 차원에서만 사용할 수 있습니다. 데이터 원본을 사용하지 않고 만든 차원의 경우 스키마 생성 마법사를 실행하여 사용자 지정 집계를 추가하기 전에 데이터 원본 뷰를 만들어야 합니다.  
  
 사용자 지정 집계를 추가하기 전에 비즈니스 인텔리전스 마법사를 실행하여 **기능 선택** 페이지에서 **단항 연산자 지정** 옵션을 선택합니다. 그런 다음 마법사의 안내를 따라 사용자 지정 집계를 적용할 차원을 선택하고 사용자 지정 집계를 식별합니다.  
  
> [!NOTE]  
>  비즈니스 인텔리전스 마법사를 실행하여 사용자 지정 집계를 추가하기 전에 기능을 향상시킬 차원에 부모-자식 특성 계층이 있는지 확인하십시오. 자세한 내용은 [부모-자식 계층](parent-child-dimension.md)합니다.  
  
## <a name="selecting-a-dimension"></a>차원 선택  
 마법사의 첫 번째 **단항 연산자 지정** 페이지에서 사용자 지정 집계를 적용할 차원을 지정합니다. 이렇게 선택한 차원에 추가되는 사용자 지정 집계에 따라 차원이 변경됩니다. 이러한 변경 내용은 선택된 차원을 포함하는 모든 큐브에 상속됩니다.  
  
## <a name="adding-custom-aggregation-unary-operator"></a>사용자 지정 집계 추가(단항 연산자)  
 두 번째 **단항 연산자 지정** 페이지에서 사용자 지정 집계에 대한 부모 특성과 단항 연산자에 대한 차원 테이블의 원본 열을 지정합니다. **부모 특성** 된 특성이 나열 해당 `Usage` 속성으로 설정 `Parent`합니다. 부모 특성이 여러 개 있는 경우 사용할 부모-자식 관계에 해당하는 부모 특성을 선택합니다. 나열된 부모 특성이 없는 경우에는 차원에 유효한 부모-자식 계층이 없는 것입니다.  
  
 **원본 열**에서 단항 연산자가 있는 문자열 열을 선택합니다. (설정 하는이 옵션을이 선택 합니다 `UnaryOperatorColumn` 부모 특성의 속성입니다.) 차원 테이블에 단항 롤업 연산자를 지정하는 문자열 열도 있어야 합니다. 이 열의 문자열 값에는 올바른 집계 연산자가 포함되어야 합니다. 행이 비어 있으면 해당 멤버가 정상적으로 계산됩니다. 열의 수식이 유효하지 않으면 멤버를 사용하는 셀 값이 검색될 때마다 런타임 오류가 발생합니다. 자세한 내용은 [부모-자식 차원의 단항 연산자](parent-child-dimension-attributes-unary-operators.md)를 참조하세요.  
  
  
