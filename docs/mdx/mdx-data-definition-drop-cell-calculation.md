---
title: DROP CELL CALCULATION 문 (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ac37584d12f2efa68084ada626ba57ab9fb28155
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579315"
---
# <a name="mdx-data-definition---drop-cell-calculation"></a>MDX 데이터 정의-DROP CELL CALCULATION
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 셀 계산을 제거합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP [ SESSION ] CELL CALCULATION CURRENTCUBE | Cube_Name.CellCalc_Name  
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브 식의 이름을 지정하는 유효한 문자열 식입니다.  
  
 *CellCalc_Name*  
 삭제할 셀 계산의 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="see-also"></a>관련 항목  
 [CREATE CELL CALCULATION 문 &#40;MDX&#41;](../mdx/mdx-data-definition-create-cell-calculation.md)   
 [MDX 데이터 정의 문 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
