---
title: Distinct (MDX) | Microsoft Docs
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
f1_keywords:
- DISTINCT
dev_langs:
- kbMDX
helpviewer_keywords:
- Distinct function
ms.assetid: d648f320-73dd-4a23-96e9-d72e93a64c0d
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 53c9822f3650f4c294505746f044700a67861abf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="distinct-mdx"></a>Distinct(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정된 집합을 계산하고 집합에서 중복 튜플을 제거하여 결과 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Distinct(Set_Expression)  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 경우는 **Distinct** 함수는 지정된 된 집합에서 중복 튜플의 찾을, 함수는 집합의 순서를 그대로 유지 하면서 중복 튜플의 첫 번째 인스턴스만 유지 합니다.  
  
## <a name="examples"></a>예  
 다음 예제 쿼리에서는 Distinct 함수를 명명된 집합과 함께 사용하는 방법과 이 함수를 Count 함수와 함께 사용하여 집합에서 중복 제외 튜플 수를 찾는 방법을 보여 줍니다.  
  
 `WITH SET MySet AS`  
  
 `{[Customer].[Customer Geography].[Country].&[Australia],[Customer].[Customer Geography].[Country].&[Australia],`  
  
 `[Customer].[Customer Geography].[Country].&[Canada],[Customer].[Customer Geography].[Country].&[France],`  
  
 `[Customer].[Customer Geography].[Country].&[United Kingdom],[Customer].[Customer Geography].[Country].&[United Kingdom]}`  
  
 `MEMBER MEASURES.SETCOUNT AS`  
  
 `COUNT(MySet)`  
  
 `MEMBER MEASURES.SETDISTINCTCOUNT AS`  
  
 `COUNT(DISTINCT(MySet))`  
  
 `SELECT {MEASURES.SETCOUNT, MEASURES.SETDISTINCTCOUNT} ON 0,`  
  
 `DISTINCT(MySet) ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
