---
title: DROP KPI 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 336eebbc8bcc98ec684faaaa1092b511cf95f100
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248234"
---
# <a name="mdx-data-definition---drop-kpi"></a>MDX 데이터 정의 - DROP KPI


  지정한 KPI(핵심 성과 지표)를 지정한 큐브에서 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP KPI CURRENTCUBE | Cube_Name.KPI_Name   
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브 이름을 지정하는 유효한 문자열입니다.  
  
 *KPI_Name*  
 삭제할 KPI의 이름을 지정하는 유효한 문자열입니다.  
  
## <a name="see-also"></a>관련 항목  
 [CREATE KPI 문 &#40;MDX&#41;](../mdx/mdx-data-definition-create-kpi.md)   
 [MDX 데이터 정의 문 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
