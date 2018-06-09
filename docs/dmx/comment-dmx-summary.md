---
title: -(주석) (DMX) 요약 | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: be2fc3e82e1da18a12af4bc4756811225e85a280
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841186"
---
# <a name="---comment-dmx-summary"></a>-(주석) (DMX) 요약
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 실행되지 않는 텍스트 문자열을 나타냅니다. 주석을 DMX(Data Mining Extensions) 문 안에 중첩하거나 코드 줄 끝에 포함하거나 별도의 줄에 삽입할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>매개 변수  
 *Comment_Text*  
 주석 텍스트를 포함하는 문자열입니다.  
  
## <a name="remarks"></a>Remarks  
 이 연산자는 한 줄로 된 주석 또는 중첩된 주석에 사용합니다.  --를 사용하여 입력한 주석은 줄 바꿈 문자로 구분됩니다.  
  
 주석의 길이에는 제한이 없습니다.  
  
 DMX에서 다른 종류의 주석 사용 하는 방법에 대 한 자세한 내용은 참조 [주석 &#40;DMX&#41;](../dmx/comments-dmx.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [별 슬래시 &#40;주석&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)   
 [이중 슬래시 &#40;주석&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)   
 [Data Mining Extensions &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [연산자 &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
