---
title: 셀 업데이트 (XMLA) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f0eab50aa7e70aedee93eef2cefee648e6ceb5c9
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81387893"
---
# <a name="updating-cells-xmla"></a>셀 업데이트(XMLA)
  [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) 명령을 사용하여 큐브 쓰기 에 사용하도록 설정된 큐브에서 하나 이상의 셀의 값을 변경할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트할 셀이 포함된 각 파티션에 대해 업데이트된 정보를 별도의 쓰기 저장 테이블에 저장합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
> [!NOTE]  
>  `UpdateCells` 명령은 큐브 쓰기 저장(writeback) 동안 할당을 지원하지 않습니다. 할당된 쓰기 백을 사용하려면 [문](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) 명령을 사용하여 다차원 식(MDX) UPDATE 문을 보내야 합니다. 자세한 내용은 [MDX &#40;큐브 문 업데이트&#41;. ](/sql/mdx/mdx-data-manipulation-update-cube)  
  
## <a name="specifying-cells"></a>셀 지정  
 명령의 Cell 속성에는 업데이트할 셀이 포함되어 있습니다. [Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) `UpdateCells` 해당 셀의 서수 번호를 사용하여 `Cell` 속성의 각 셀을 식별할 수 있습니다. 개념적으로 큐브의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 숫자 셀은 큐브가 *p-차원*배열인 것처럼, 여기서 *p는* 축 수입니다. 셀은 행 중심의 순서로 번호가 매겨집니다. 다음 그림에서는 셀의 서수 번호를 계산하는 수식을 보여 줍니다.  
  
 ![셀 서수 위치 계산 수식](../../analysis-services/dev-guide/media/cellordinalformula.gif "셀 서수 위치 계산 수식")  
  
 셀의 서수 번호를 알고 나면 [Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) 속성의 [Value](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla) 속성에서 셀의 의도된 값을 나타낼 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [XMLA&#41;&#40;요소 업데이트](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Analysis Services에서 XMLA를 사용하여 개발](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
