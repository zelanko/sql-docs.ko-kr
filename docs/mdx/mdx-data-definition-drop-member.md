---
description: MDX 데이터 정의 - DROP MEMBER
title: DROP MEMBER 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f71232997c24a1bdca9a1294a804e8b30660d704
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483856"
---
# <a name="mdx-data-definition---drop-member"></a>MDX 데이터 정의 - DROP MEMBER


  계산 멤버를 제거합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP MEMBER   
   CURRENTCUBE | Cube_Name  
      .Member_Name   
               [,CURRENTCUBE | Cube_Name.Member_Name ...n]  
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브 이름을 지정하는 유효한 문자열 식입니다.  
  
 *Member_Identifier*  
 멤버 이름이나 멤버 키를 지정하는 유효한 문자열 식입니다.  
  
## <a name="see-also"></a>참고 항목  
 [CREATE MEMBER 문 &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [Mdx 데이터 정의 문은 MDX를 &#40;&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
