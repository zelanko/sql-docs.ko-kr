---
description: 연결 연산자
title: 연결 연산자 | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b53f5d79124a86e8748a473af5b371152932514e
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192558"
---
# <a name="concatenation-operators"></a>연결 연산자


  연결 연산자는 더하기 기호(+)입니다. 두 개 이상의 문자열을 하나의 문자열로 결합 또는 연결하거나 이진 문자열을 연결할 수 있습니다.  
  
 다음 코드는 제품 이름을 제품의 고유 이름과 결합하는 연결 연산자의 예입니다.  
  
```  
WITH MEMBER Measures.ProductName AS   
   Product.Product.CurrentMember.Name + " (" + Product.Product.CurrentMember.UniqueName + ")"  
SELECT   
   {Measures.ProductName} ON COLUMNS,  
   Product.Product.Members ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="language-considerations"></a>언어 관련 고려 사항  
 연결할 문자열이 모두 동일한 데이터 정렬을 사용하는 경우 연결된 결과 문자열은 입력과 같은 데이터 정렬을 사용합니다. 연결할 문자열의 데이터 정렬이 서로 다른 경우 데이터 정렬 선행 규칙에 따라 연결된 결과 문자열의 데이터 정렬이 결정됩니다. 자세한 내용은 [언어 및 데이터 정렬&#40;Analysis Services&#41;](/analysis-services/languages-and-collations-analysis-services)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [연산자 &#40;MDX 구문&#41;](../mdx/operators-mdx-syntax.md)  
  
