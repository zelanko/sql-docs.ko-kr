---
title: DROP CELL CALCULATION 문 (MDX) | Microsoft Docs
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
- Calculation
- DROP
- DROP_CELL_CALCULATION
- CELL CALCULATION
- DROP CELL
- cell
- DROP CELL CALCULATION
dev_langs:
- kbMDX
helpviewer_keywords:
- deleting calculations
- dropping calculations
- removing calculations
- DROP CELL CALCULATION statement
- calculations [SQL Server]
- cubes [Analysis Services], calculations
ms.assetid: 77caedf4-dd96-4eac-a5e4-fd82148a44a7
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e84207fc0354c7599feb823f0b54b27fdc164619
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
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
  
## <a name="see-also"></a>관련 항목:  
 [CELL CALCULATION 문 &#40; 만들기 Mdx&#41;](../mdx/mdx-data-definition-create-cell-calculation.md)   
 [MDX 데이터 정의 문 &#40; Mdx&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
