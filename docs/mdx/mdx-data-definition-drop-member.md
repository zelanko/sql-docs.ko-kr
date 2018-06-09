---
title: DROP MEMBER 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 78d5d27853922d7e7524d93ae2b8157e57166968
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741382"
---
# <a name="mdx-data-definition---drop-member"></a>MDX 데이터 정의-멤버 삭제


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
  
## <a name="see-also"></a>관련 항목  
 [CREATE MEMBER 문 &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [MDX 데이터 정의 문 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
