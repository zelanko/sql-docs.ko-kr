---
title: DROP ACTION 문 (MDX) | Microsoft Docs
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
- DROP
- DROP ACTION
- Action
- DROP_ACTION
dev_langs:
- kbMDX
helpviewer_keywords:
- DROP ACTION statement
- deleting actions
- removing actions
- actions [MDX]
- dropping actions
ms.assetid: 74b3cfee-dea8-4968-a54c-1754d52ee1bd
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: dd8e7776899331a089fb12157a072e4ade673655
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---drop-action"></a>MDX 데이터 정의-DROP 동작
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 큐브에서 특정 동작을 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP ACTION CURRENTCUBE | Cube_Name  
   .Action_Name   
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브 이름을 지정하는 유효한 문자열 식입니다.  
  
 *Action_Name*  
 삭제할 동작의 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE ACTION 문 &#40;MDX&#41;](../mdx/mdx-data-definition-create-action.md)   
 [MDX 데이터 정의 문 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
