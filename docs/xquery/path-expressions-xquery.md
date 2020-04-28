---
title: 경로 식 (XQuery) | Microsoft Docs
description: XQuery 경로 식이 문서에서 요소, 특성 및 텍스트 노드와 같은 노드를 찾는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- path expressions [XQuery]
- expressions [XQuery], path
ms.assetid: b93fa36c-bf69-46b9-b137-f597d66fd0c0
author: rothja
ms.author: jroth
ms.openlocfilehash: 0e4c87a0695c57461f444c8be4318bcd06cfdefe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81388061"
---
# <a name="path-expressions-xquery"></a>경로 식(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 경로 식은 문서에서 요소, 특성 및 텍스트 노드와 같은 노드를 찾습니다. 경로 식의 결과는 항상 결과 시퀀스에 중복 노드 없이 문서 순서에 따라 발생합니다. 경로를 지정할 때 비축약형 또는 축약형 구문을 사용할 수 있습니다. 다음은 비축약형 구문에 대한 내용입니다. 축약형 구문에 대해서는 이 항목의 뒷부분에서 설명합니다.  
  
> [!NOTE]  
>  이 항목의 예제 쿼리는 **제품 모델** 테이블의 **Xml** 유형 열 **CatalogDescription** 및 **지침**에 대해 지정 되므로 이러한 열에 저장 된 xml 문서의 내용과 구조에 대해 잘 알고 있어야 합니다.  
  
 경로 식은 상대 또는 절대일 수 있습니다. 다음은 이 두 경로 식에 대한 설명입니다.  
  
-   상대 경로 식은 한 개나 두 개의 슬래시 기호(/ 또는 //)로 구분되는 하나 이상의 단계로 구성됩니다. 예를 들어 `child::Features`는 상대 경로 식이며 여기서 `Child`는 컨텍스트 노드의 자식 노드만 참조합니다. 이 노드는 현재 처리 중인 노드입니다. 식은 컨텍스트 노드의 요소 \<노드 자식을> 기능을 검색 합니다.  
  
-   절대 경로 식은 한 개나 두 개의 슬래시 기호(/ 또는 //)로 시작되고 뒤에 선택적인 상대 경로가 옵니다. 예를 들어 `/child::ProductDescription`과 같이 슬래시 기호로 시작되는 식이 절대 경로 식입니다. 식의 시작 부분에 있는 슬래시 기호는 컨텍스트 노드의 문서 루트 노드를 반환 하기 때문에,이 식은 문서 루트의 \<모든 제품 설명> 요소 노드 자식을 반환 합니다.  
  
     절대 경로가 슬래시 기호 한 개로 시작되면 뒤에 상대 경로가 오거나 오지 않을 수 있습니다. 슬래시 기호를 한 개만 지정하면 식이 컨텍스트 노드의 루트 노드를 반환합니다. XML 데이터 유형의 경우 이 노드가 문서 노드입니다.  
  
 일반적인 경로 식은 단계로 구성됩니다. 예를 들어, 절대 경로 식 `/child::ProductDescription/child::Summary`에는 슬래시 기호로 구분 된 두 단계가 포함 됩니다.  
  
-   첫 번째 단계에서는 문서 \<루트의 제품 설명> 요소 노드 자식을 검색 합니다.  
  
-   두 번째 단계는 검색 \< \<된 각 제품 설명> 요소 노드에 대 한 요약> 요소 노드 자식을 검색 합니다 .이 노드는 컨텍스트 노드가 됩니다.  
  
 경로 식의 단계는 축 단계이거나 일반 단계일 수 있습니다.  
  
## <a name="axis-step"></a>축 단계  
 경로 식의 축 단계는 다음 부분으로 구성됩니다.  
  
 [축은](../xquery/path-expressions-specifying-axis.md)  
 이동 방향을 정의합니다. 컨텍스트 노드에서 시작하여 축이 지정하는 방향으로 도달할 수 있는 노드로 이동하는 경로 식의 축 단계입니다.  
  
 [노드 테스트](../xquery/path-expressions-specifying-node-test.md)  
 선택할 노드 유형이나 노드 이름을 지정합니다.  
  
 0개 이상의 선택적 조건자  
 일부는 선택하고 일부는 무시하여 노드를 필터링합니다.  
  
 다음 예에서는 경로 식에 **axisstep** 를 사용 합니다.  
  
-   절대 경로 식 `/child::ProductDescription`에는 단계가 하나만 있습니다. 이 단계는 축(`child`)과 노드 테스트(`ProductDescription`)를 지정합니다.  
  
-   상대 경로 식 `child::ProductDescription/child::Features`에는 슬래시 기호로 구분된 두 단계가 있습니다. 두 단계 모드 자식 축을 지정합니다. ProductDescription과 Features는 노드 테스트입니다.  
  
-   상대 경로 식 `child::root/child::Location[attribute::LocationID=10]`에는 슬래시 기호로 구분 된 두 단계가 포함 됩니다. 첫 번째 단계는 축(`child`)과 노드 테스트(`root`)를 지정합니다. 두 번째 단계는 축 단계의 세 구성 요소인 축(자식), 노드 테스트(`Location`) 및 조건자(`[attribute::LocationID=10]`)를 모두 지정합니다.  
  
 축 단계의 구성 요소에 대 한 자세한 내용은 경로 식 단계에서 [축 지정](../xquery/path-expressions-specifying-axis.md), 경로 [식 단계에서 노드 테스트 지정](../xquery/path-expressions-specifying-node-test.md)및 [경로 식 단계에서 조건자 지정](../xquery/path-expressions-specifying-predicates.md)을 참조 하세요.  
  
## <a name="general-step"></a>일반 단계  
 일반 단계는 노드 시퀀스로 계산해야 하는 식입니다.  
  
 SQL Server에서 XQuery를 구현하면 일반 단계가 경로 식의 첫 번째 단계로 지원됩니다. 다음은 일반 단계를 사용하는 경로 식의 예입니다.  
  
```  
(/a, /b)/c  
id(/a/b)  
```  
  
 Id 함수에 대 한 자세한 내용은 [Id 함수 &#40;XQuery&#41;](../xquery/functions-on-sequences-id.md)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [경로 식 단계에서 축 지정](../xquery/path-expressions-specifying-axis.md)  
 경로 식에서 축 단계를 사용하는 방법에 대해 설명합니다.  
  
 [경로 식 단계에서 노드 테스트 지정](../xquery/path-expressions-specifying-node-test.md)  
 경로 식에서 노드 테스트를 사용하는 방법에 대해 설명합니다.  
  
 [경로 식 단계에서 조건자 지정](../xquery/path-expressions-specifying-predicates.md)  
 경로 식에서 조건자를 사용하는 방법에 대해 설명합니다.  
  
 [경로 식에 축약형 구문 사용](../xquery/path-expressions-using-abbreviated-syntax.md)  
 경로 식에서 축약형 구문을 사용하는 방법에 대해 설명합니다.  
  
  
