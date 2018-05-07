---
title: UserName (MDX) | Microsoft Docs
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
f1_keywords:
- UserName
dev_langs:
- kbMDX
helpviewer_keywords:
- UserName function
ms.assetid: ecae549b-5c5e-4483-84e6-b713cd297d7e
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: c4b0624a26fe911f9b481a4a03370e65a1ab71a1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="username-mdx"></a>UserName(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  현재 연결의 도메인 이름과 사용자 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>주의  
 반환되는 값은 다음 형식의 문자열입니다.  
  
 *도메인 이름 \ 사용자 이름*  
  
## <a name="example"></a>예제  
 다음 예에서는 쿼리를 실행하는 사용자의 이름을 반환합니다.  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
