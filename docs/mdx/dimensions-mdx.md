---
title: Dimensions (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Dimensions
dev_langs:
- kbMDX
helpviewer_keywords:
- Dimensions function
ms.assetid: 64f63aa0-ef74-4415-a0c9-8acc6cd81739
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 2f0c3ea111eafd55f4fc1f0a0eacc0993ef0d713
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dimensions-mdx"></a>Dimensions(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  숫자 식 또는 문자열 식으로 지정된 계층을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Numeric expression syntax  
Dimensions(Hierarchy_Number)  
  
String expression syntax  
Dimensions(Hierarchy_Name)  
```  
  
## <a name="arguments"></a>인수  
 *Hierarchy_Number*  
 계층 번호를 지정하는 유효한 숫자 식입니다.  
  
 *Hierarchy_Name*  
 계층 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>주의  
 계층 번호가 지정 되는 **차원** 함수 큐브 내에서 0부터 시작 위치가 계층에 지정 된 계층 번호를 반환 합니다.  
  
 계층 이름이 지정 되는 **차원** 함수는 지정 된 계층을 반환 합니다. 이 문자열 버전을 사용 하는 일반적으로 **차원** 사용자 정의 함수는 함수입니다.  
  
> [!NOTE]  
>  **측정값** 차원은 항상으로 표시 됩니다 `Dimensions(0)`합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 사용는 **차원** 이름, 수준 수 및 숫자 식과 문자열 식을 모두 사용 하 여 지정된 된 계층의 멤버의 수를 반환 하는 함수입니다.  
  
```  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Levels.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Members.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
