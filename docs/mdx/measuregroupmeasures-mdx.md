---
title: MeasureGroupMeasures (MDX) | Microsoft Docs
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
dev_langs:
- kbMDX
helpviewer_keywords:
- MeasureGroupMeasures function
ms.assetid: 69d9b205-1ca7-4741-9ca9-c7926bc87ead
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: bad3fd8693c2d12cdf4a79801cc7d56ec050971a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 측정값 그룹에 속하는 측정값 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>인수  
 *MeasureGroupName*  
 측정값 집합을 검색할 측정값 그룹의 이름이 들어 있는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>주의  
 지정된 문자열은 측정값 그룹 이름과 정확히 일치해야 합니다. 측정값 그룹 이름에 공백이 포함되어 있어도 대괄호로 묶을 필요는 없습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Adventure Works 큐브에 있는 Internet Sales 측정값 그룹의 모든 측정값을 반환합니다.  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
