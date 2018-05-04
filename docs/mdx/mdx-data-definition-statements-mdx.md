---
title: MDX 데이터 정의 문 (MDX) | Microsoft Docs
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
- MDX [Analysis Services], data manipulation
- data manipulation [MDX]
- data definition statements [MDX]
- Multidimensional Expressions [Analysis Services], data manipulation
ms.assetid: 1f975d7f-8875-43b6-a571-9d5cd7c70217
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 84a173a4e3496d61f8f1b1fc837908d2706af5b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition-statements-mdx"></a>MDX 데이터 정의 문(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  MDX에서 데이터 정의 문은 다차원 개체를 만들고 삭제하고 조작합니다. 다음 표에서는 사용할 수 있는 데이터 정의 문을 나열합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[ALTER CUBE 문 & #40; Mdx& #41;](../mdx/mdx-data-definition-alter-cube.md)|지정한 큐브의 구조를 변경합니다.|  
|[CREATE ACTION 문 &#40;MDX&#41;](../mdx/mdx-data-definition-create-action.md)|큐브, 차원, 계층 또는 종속 개체와 연관될 수 있는 동작을 만듭니다.|  
|[CELL CALCULATION 문 & #40; 만들기 Mdx& #41;](../mdx/mdx-data-definition-create-cell-calculation.md)|큐브 내의 지정된 튜플 집합에서 MDX 식을 계산하는 계산 식을 만듭니다.|  
|[CREATE GLOBAL CUBE 문 &#40;MDX&#41;](../mdx/mdx-data-definition-create-global-cube.md)|논리적 지속형 큐브를 서버에 있는 큐브의 하위 큐브에 따라 만들고 채웁니다. 논리적 지속형 큐브에 대한 연결 시에는 서버 연결이 필요하지 않습니다.|  
|[MEMBER 문 & #40; 만들기 Mdx& #41;](../mdx/mdx-data-definition-create-member.md)|계산 멤버를 만듭니다.|  
|[CREATE SESSION CUBE 문 &#40;MDX&#41;](../mdx/mdx-data-definition-create-session-cube.md)|서버에 있는 큐브를 기준으로 동일한 세션의 모든 쿼리에 사용할 수 있는 큐브를 만들어 채웁니다.|  
|[SET 문 & #40; 만들기 Mdx& #41;](../mdx/mdx-data-definition-create-set.md)|지정한 큐브에 대해 명명된 집합을 만듭니다.|  
|[CREATE SUBCUBE 문 &#40;MDX&#41;](../mdx/mdx-data-definition-create-subcube.md)|지정한 큐브 또는 하위 큐브의 큐브 공간을 지정한 하위 큐브로 다시 정의합니다.|  
|[DROP ACTION 문 &#40;MDX&#41;](../mdx/mdx-data-definition-drop-action.md)|지정한 큐브에서 특정 동작을 삭제합니다.|  
|[DROP CELL CALCULATION Statement &#40;MDX&#41;](../mdx/mdx-data-definition-drop-cell-calculation.md)|지정한 셀 계산을 제거합니다.|  
|[DROP MEMBER 문 &#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)|계산 멤버를 제거합니다.|  
|[DROP SET 문 &#40;MDX&#41;](../mdx/mdx-data-definition-drop-set.md)|명명된 집합을 제거합니다.|  
|[DROP SUBCUBE 문 &#40;MDX&#41;](../mdx/mdx-data-definition-drop-subcube.md)|지정한 하위 큐브를 삭제하고 이전에 정의한 큐브나 지정한 이름의 하위 큐브 정의로 돌아갑니다.|  
|[REFRESH CUBE 문은 &#40;MDX&#41;](../mdx/mdx-data-definition-refresh-cube.md)|큐브에 대한 클라이언트 캐시를 새로 고칩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 문 참조 &#40;MDX&#41;](../mdx/mdx-statement-reference-mdx.md)   
 [MDX 데이터 조작 문 &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [MDX 스크립팅 문 & #40; Mdx& #41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
