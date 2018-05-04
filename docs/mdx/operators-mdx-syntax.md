---
title: (MDX syntax) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], operators
- operators [MDX]
- precedence [MDX]
- MDX [Analysis Services], operators
ms.assetid: 1ff5a529-88fd-4619-86e1-19fa214650d6
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 8b849cf1a9c87e91c2104217d8b435adfeef6efc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="operators-mdx-syntax"></a>연산자(MDX 구문)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  MDX에서 연산자를 이용해 다음 동작을 수행할 수 있습니다.  
  
-   영구적 또는 임시적으로 데이터를 변경합니다.  
  
-   지정한 조건을 만족하는 값 또는 개체를 검색합니다.  
  
-   값 또는 식 사이에서 결정할 사항을 구현합니다.  
  
-   트랜잭션을 시작하거나 커밋하기 전 또는 특정 문을 실행하기 전에 특정 조건을 테스트합니다.  
  
 MDX는 다음 테이블에 나열된 연산자를 지원합니다.  
  
|원하는 연산|찾기 옵션|  
|---------------------------------------|---------|  
|변수에 값을 할당하거나 결과 집합 열을 별칭과 연결합니다.|[대입 연산자](../mdx/assignment-operators.md)|  
|더하기, 빼기, 곱하기, 나누기 연산을 수행합니다.|[산술 연산자](../mdx/arithmetic-operators.md)|  
|AND, OR, NOT, XOR와 같은 조건에서 진리를 검사합니다.|[비트 연산자](../mdx/bitwise-operators.md)|  
|값을 다른 값이나 식에 대해 비교합니다.|[비교 연산자](../mdx/comparison-operators.md)|  
|두 문자열을 한 문자열로 영구 또는 임시적으로 결합합니다.|[연결 연산자](../mdx/concatenation-operators.md)|  
|두 집합 식을 한 집합으로 영구 또는 임시적으로 결합합니다.|[집합 연산자](../mdx/set-operators.md)|  
|한 피연산자에 대한 연산을 수행합니다.|[단항 연산자](../mdx/unary-operators.md)|  
  
> [!NOTE]  
>  쿼리에서 특정 유형의 연산자와 함께 사용될 큐브의 데이터를 볼 수 있는 사용자는 누구든 연산을 수행할 수 있습니다. 하지만 데이터를 변경하려면 적합한 권한이 필요합니다.  
  
 여러 연산자를 사용할 때는 MDX가 연산자를 계산하는 순서가 중요합니다. 마찬가지로 연산자 사용자가 해당 연산자로 계산하려면 먼저 데이터 형식을 다른 데이터 형식으로 변환해야 하도록 요구할 수도 있습니다.  
  
## <a name="evaluating-complex-expressions"></a>복잡한 식 계산  
 연산자를 사용하여 작은 식 여러 개를 결합한 식을 만들 수 있습니다. 이러한 복잡 한 식에 MDX 계산에서 사용 하는 연산자 우선 순위의 정의 기반으로 순서 대로 연산자 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]합니다. MDX는 높은 우선 순위의 연산자를 먼저 수행한 다음 낮은 우선 순위의 연산자를 수행합니다.  
  
### <a name="understanding-operator-precedence"></a>연산자 우선 순위의 이해  
 다음 목록은 내림차순으로 연산자 우선 순위를 표시한 것입니다. 같은 줄에 있는 연산자의 우선 순위는 같고 괄호로 묶인 경우가 아니라면 왼쪽에서 오른쪽으로 계산됩니다.  
  
-   IS  
  
-   AS  
  
-   DISTINCT  
  
-   :  
  
-   ^  
  
-   /, *  
  
-   +, -  
  
-   EXISTING  
  
-   <>, >=, =, \<=, >, <  
  
-   NOT  
  
-   및  
  
-   XOR  
  
-   OR  
  
 MDX의 연산자에에서 대 한 자세한 내용은 참조 하십시오. [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)합니다.  
  
### <a name="determining-results"></a>결과 확정  
 간단한 식들을 결합하여 복잡한 식을 구성하는 경우 연산자에 대한 규칙을 데이터 형식 우선 순위에 대한 규칙과 결합하면 결과 값의 데이터 형식이 결정됩니다.  
  
 결과가 문자 또는 유니코드 값인 경우에는 연산자에 대한 규칙을 데이터 정렬 우선 순위에 대한 규칙과 결합하면 결과의 데이터 정렬이 결정됩니다. 데이터 정렬에 대 한 자세한 내용은 참조 [언어 및 데이터 정렬 &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md)합니다.  
  
 간단한 식의 전체 자릿수, 소수 자릿수 및 길이를 기준으로 결과의 전체 자릿수, 소수 자릿수 및 길이를 결정하는 규칙도 있습니다.  
  
## <a name="converting-data-types"></a>데이터 형식 변환  
 MDX는 다른 형식이 필요한 식에서 개체를 사용할 때 그 개체를 암시적으로 다른 형식으로 변환합니다. 다음 테이블은 각 개체에 대한 변환 규칙을 정의한 것입니다.  
  
|원본 형식|필요한 형식|변환|  
|-------------------|-----------------|----------------|  
|Level|Set|\<수준 >.members|  
|계층|멤버|\<계층 구조 >.defaultmember|  
|멤버|Tuple|(\<멤버 >)|  
|Tuple|멤버|\<튜플 >.item(0)|  
|Tuple|스칼라|\<튜플 >.value|  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [MDX 구문 요소 &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
