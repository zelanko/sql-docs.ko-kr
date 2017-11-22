---
title: "MDX 구문 표기 규칙 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], syntax
- MDX [Analysis Services], syntax
ms.assetid: 50a6e723-91c4-407b-a0d5-87d0d4e4e0f6
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1ea6c7ecf3ecebf9fcb29e11ef89e554b2a343f0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-syntax-conventions-mdx"></a>MDX 구문 표기 규칙(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  MDX 언어 참조의 MDX 구문에 대한 다이어그램에서는 다음과 같은 표기 규칙을 사용합니다.  
  
|규칙|사용법|  
|----------------|-----------|  
|*기울임꼴*|사용자가 제공하는 MDX 구문의 인수를 나타냅니다.|  
|&#124;(세로 막대)|대괄호 또는 중괄호 내에서 구문 항목을 구분합니다. 항목 중 하나만 선택할 수 있습니다.|  
|`[ ]`(대괄호)|옵션 구문 항목을 나타냅니다. 대괄호는 입력하지 않습니다.|  
|[,] ...n|앞의 항목이 임의의 횟수만큼 반복될 수 있음을 나타냅니다. 각 항목은 쉼표로 구분되기도 합니다.|  
|\<레이블 >:: =|구문 블록의 이름을 나타냅니다. 이 규칙은 문에서 한번 이상 사용될 수 있는 긴 구문의 일부 또는 구문 단위를 그룹화하고 레이블을 붙일 때 사용됩니다. 구문 블록이 사용 될 수 있는 각 위치는 꺾쇠 괄호로 묶여 있는 레이블로 표시 됩니다: \<레이블 > 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 언어 참조 &#40; Mdx&#41;](../mdx/mdx-language-reference-mdx.md)  
  
  

