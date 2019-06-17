---
title: MeasureGroupMeasures (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 55e00420ad3f941d50d9179dcd4a87d678cc28a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267937"
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures(MDX)


  지정한 측정값 그룹에 속하는 측정값 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>인수  
 *MeasureGroupName*  
 측정값 집합을 검색할 측정값 그룹의 이름이 들어 있는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>Remarks  
 지정된 문자열은 측정값 그룹 이름과 정확히 일치해야 합니다. 측정값 그룹 이름에 공백이 포함되어 있어도 대괄호로 묶을 필요는 없습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Adventure Works 큐브에 있는 Internet Sales 측정값 그룹의 모든 측정값을 반환합니다.  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
