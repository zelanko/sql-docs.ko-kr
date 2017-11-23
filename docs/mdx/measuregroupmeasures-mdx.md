---
title: MeasureGroupMeasures (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: MeasureGroupMeasures function
ms.assetid: 69d9b205-1ca7-4741-9ca9-c7926bc87ead
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: baacb5ee83ecd45bc994cc462b04d35d6d3ca15a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
