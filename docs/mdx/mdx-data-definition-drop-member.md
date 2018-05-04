---
title: DROP MEMBER 문 (MDX) | Microsoft Docs
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
- Member
- DROP_MEMBER
- DROP MEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- deleting calculated members
- calculated members [MDX]
- DROP MEMBER statement
- dropping calculated members
- removing calculated members
ms.assetid: e9819976-a9ec-4c48-b0b5-3f6938e200f5
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: a49ce890fb3a98e26f67f1b1e648decd4372c7ac
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---drop-member"></a>MDX 데이터 정의-멤버 삭제
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="see-also"></a>관련 항목:  
 [MEMBER 문 & #40; 만들기 Mdx& #41;](../mdx/mdx-data-definition-create-member.md)   
 [MDX 데이터 정의 문 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
