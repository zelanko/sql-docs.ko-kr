---
title: Data Mining Extensions (DMX) 구문 표기 규칙 | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cf80ef73ae3f55f58978d95b0d12b8c69b81dfff
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34843046"
---
# <a name="data-mining-extensions-dmx-syntax-conventions"></a>DMX(데이터 마이닝 확장) 구문 표기 규칙
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  확장 DMX (Data Mining) 참조 설명서를 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] DMX 언어를 설명 하기 위해 다음 규칙을 사용 합니다.  
  
|규칙|사용법|  
|----------------|-----------|  
|**굵게**|표시된 대로 입력해야 하는 DMX 키워드 및 텍스트|  
|*기울임꼴*|사용자가 제공하는 DMX 구문의 인수|  
|&#124;(세로 막대)|대괄호 또는 중괄호에서 구문 항목을 구분하는 데 사용합니다. 항목 중 하나만 선택할 수 있습니다.|  
|`[ ]`(대괄호)|옵션 구문 항목을 포함합니다. 대괄호는 입력하지 않습니다.|  
|{}(중괄호)|필수 구문 항목을 포함합니다. 중괄호는 입력하지 않습니다.|  
|, ...|쉼표 앞의 항목이 임의의 횟수만큼 반복될 수 있음을 나타냅니다. 각 항목은 쉼표로 구분됩니다.|  
|\<label> ::=|구문 블록의 이름입니다. 이 규칙은 문에서 한 번 이상 사용될 수 있는 긴 구문의 섹션 또는 구문 단위를 그룹화하고 레이블을 붙일 때 사용됩니다. 구문 블록이 사용 될 수 있는 각 위치 모양의 레이블로,와 같은 ֲ \<레이블 > 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 참조](../dmx/data-mining-extensions-dmx-reference.md)  
  
  

