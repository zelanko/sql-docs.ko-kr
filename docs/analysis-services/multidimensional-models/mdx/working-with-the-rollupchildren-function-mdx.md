---
title: "RollupChildren 함수 작업(MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "쿼리 [MDX], RollupChildren 함수"
  - "RollupChildren 함수"
  - "사용자 지정 멤버 속성 [MDX]"
  - "IIf 함수"
ms.assetid: 03c624d4-f277-451d-9995-623a07ea2f86
caps.latest.revision: 27
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# RollupChildren 함수 작업(MDX)
  MDX [RollupChildren](../../../mdx/rollupchildren-mdx.md) 함수는 멤버의 자식을 롤업하여 각각의 자식에 다른 단항 연산자를 적용하고 이 롤업 값을 멤버로 반환합니다. 자식 멤버와 관련된 멤버 속성에서 단항 연산자를 제공하거나 함수에 직접 제공되는 문자열 식이 단항 연산자가 될 수 있습니다.  
  
## RollupChildren 함수 예  
 MDX 문에서 **RollupChildren** 함수를 사용하는 방법을 설명하기는 쉽지만 MDX 쿼리에 미치는 이 함수의 효과는 매우 다양할 수 있습니다.  
  
 **RollupChildren** 함수의 효과는 기존의 큐브 데이터에 대한 선택적인 분석을 수행하도록 디자인된 MDX 쿼리에서 발생합니다. 예를 들어 다음 테이블에는 괄호로 표시된 단항 연산자(**UNARY_OPERATOR** 멤버 속성에 의해 표현됨)와 함께 Net Sales 부모 멤버에 대한 자식 멤버 목록이 들어 있습니다.  
  
|부모 멤버|자식 멤버|  
|-------------------|------------------|  
|순매출액|Domestic Sales (+)<br /><br /> Domestic Returns (-)<br /><br /> Foreign Sales (+)<br /><br /> Foreign Returns (-)|  
  
 Net Sales 부모 멤버는 현재 롤업의 일부로서 국내 및 해외 수입을 뺀 상태에서 순매출액 합계에서 국내 및 해외 총 판매액을 뺀 값을 제공합니다.  
  
 하지만 국내 및 해외 수입을 무시하고 국내 및 해외 총 판매액에 10%를 더한 값으로 빠르고 쉽게 전망치를 제공하려고 합니다. **RollupChildren** 함수를 사용하여 이 값을 계산할 수 있는 방법에는 사용자 지정 멤버 속성으로 계산하거나 **IIf** 함수로 계산하는 두 가지 방법이 있습니다.  
  
### 사용자 지정 멤버 속성 사용  
 롤업 계산이 자주 수행되는 연산인 경우에는 특정 함수에 대한 각 자식에 사용될 연산자를 저장하는 멤버 속성을 만드는 것이 한 가지 방법입니다. 다음 테이블에서는 유효한 단항 연산자를 표시하고 예상 결과를 설명합니다.  
  
|연산자|결과|  
|--------------|------------|  
|+|합계 = 합계 + 현재 자식 항목|  
|-|합계 = 합계 - 현재 자식 항목|  
|*|합계 = 합계 * 현재 자식 항목|  
|/|합계 = 합계 / 현재 자식 항목|  
|~|자식 항목을 롤업에 사용하지 않습니다. 자식 값을 무시합니다.|  
  
 예를 들어 **SALES_OPERATOR**라는 멤버 속성을 만들 수 있으며 다음 테이블에 표시된 것과 같이 그 멤버 속성에 다음의 단항 연산자가 할당됩니다.  
  
|부모 멤버|자식 멤버|  
|-------------------|------------------|  
|순매출액|Domestic Sales (+)<br /><br /> Domestic Returns (~)<br /><br /> Foreign Sales (+)<br /><br /> Foreign Returns (~)|  
  
 이 새 멤버 속성으로 다음 MDX 문은 총 판매액 추산 연산을 빠르고 효율적으로 수행하게 됩니다(해외 및 국내 수입은 무시).  
  
```  
RollupChildren([Net Sales], [Net Sales].CurrentMember.Properties("SALES_OPERATOR")) * 1.1  
```  
  
 이 함수를 호출하면 멤버 속성에 저장된 연산자를 사용하여 각 자식의 값을 합계에 적용합니다. 국내 및 해외 수입에 대한 멤버를 무시하고 **RollupChildren** 함수가 반환한 롤업 합계에 1.1을 곱합니다.  
  
### IIf 함수 사용  
 예로 든 연산이 일반적이지 않거나 연산이 한 MDX 쿼리에만 적용되는 경우 [IIf](../../../mdx/iif-mdx.md) 함수를 **RollupChildren** 함수와 함께 사용하면 같은 결과를 낼 수 있습니다. 다음 MDX 쿼리를 이용하면 사용자 지정 멤버 속성을 사용하지 않고도 앞선 예로 든 MDX와 같은 결과가 나옵니다.  
  
```  
RollupChildren([Net Sales], IIf([Net Sales].CurrentMember.Properties("UNARY_OPERATOR") = "-", "~", [Net Sales].CurrentMember.Properties("UNARY_OPERATOR))) * 1.1  
```  
  
 이 MDX 문은 자식 멤버의 단항 연산자를 검사합니다. 국내 및 해외 수입 멤버의 경우에서와 같이 단항 연산자를 빼기에 사용하는 경우 **IIf** 함수가 물결표(~) 단항 연산자를 대체합니다. 그렇지 않으면 **IIf** 함수는 자식 멤버의 단항 연산자를 사용합니다. 마지막으로 반환된 롤업 합계에 1.1을 곱하면 국내 및 해외 총 판매 예측 값이 됩니다.  
  
## 관련 항목:  
 [데이터 조작&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/manipulating-data-mdx.md)  
  
  