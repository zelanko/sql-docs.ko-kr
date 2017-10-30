---
title: "연결 연산자 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- concatenation operators [MDX]
ms.assetid: 9e4c181a-b71e-41ec-98a1-ec8b5b5103b1
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ae299577ece2c712504631fb85eeac4499c4d4c7
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="concatenation-operators"></a>연결 연산자
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 연결할 문자열이 모두 동일한 데이터 정렬을 사용하는 경우 연결된 결과 문자열은 입력과 같은 데이터 정렬을 사용합니다. 연결할 문자열의 데이터 정렬이 서로 다른 경우 데이터 정렬 선행 규칙에 따라 연결된 결과 문자열의 데이터 정렬이 결정됩니다. 자세한 내용은 [언어 및 데이터 정렬&#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 연산자 참조 &#40; Mdx&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [연산자 &#40; MDX 구문 &#41;](../mdx/operators-mdx-syntax.md)  
  
  

