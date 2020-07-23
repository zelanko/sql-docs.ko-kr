---
title: 슬래시 별 (주석) (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f09533b68ab6dc3c771a09b70faf71087ed69a62
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970429"
---
# <a name="slash-star-comment-dmx"></a>슬래시 별 (주석) (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 실행되지 않는 텍스트 문자열을 나타냅니다. 서버는 주석 문자/* 및/사이의 텍스트를 평가 하지 않습니다 \* . 주석을 DMX(Data Mining Extensions) 문 안에 중첩하거나 코드 줄 끝에 포함하거나 별도의 줄에 삽입할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
/* Comment_Text */  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Comment_Text*  
 주석 텍스트를 포함하는 문자열입니다.  
  
## <a name="remarks"></a>설명  
 여러 줄로 이루어진 주석은 /* 및 \*/로 표시되어야 합니다.  
  
 주석의 길이에는 제한이 없습니다.  
  
 DMX에서 다양 한 종류의 주석을 사용 하는 방법에 대 한 자세한 내용은 [dmx &#40;dmx&#41;](../dmx/comments-dmx.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [&#41; &#40;DMX &#40;주석&#41;](../dmx/double-slash-comment-dmx.md)   
 [--&#40;설명&#41; &#40;DMX&#41; 요약](../dmx/comment-dmx-summary.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
