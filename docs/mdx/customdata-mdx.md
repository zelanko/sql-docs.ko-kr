---
title: CustomData (MDX) | Microsoft Docs
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
- EXISTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Exists function
ms.assetid: 61d9f5a2-6f56-4179-a39b-317c8e0a2cdd
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5fb7c745ac65b41095c3d4dfb41b62b081d83c1d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="customdata-mdx"></a>CustomData(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  값을 반환 된 **CustomData** 연결 문자열 속성이 정의 되지 않으면 **null**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>반환 값  
 **CustomData** 함수를 검색할 수는 **CustomData** 연결 문자열 속성 및 구성 설정을 같은 MDX (Multidimensional Expressions) 함수 및 문에서 사용할 전달할 [UserName (MDX)](../mdx/username-mdx.md) 및 [CALL 문 (MDX)](../mdx/mdx-data-manipulation-call.md)합니다. 예를 들어이 함수 사용할 수는 동적 보안 식에서 문자열 값에 대 한 허용/거부 집합 멤버를 선택 하 고 **CustomData** 연결 문자열 속성입니다.  
  
## <a name="example"></a>예제  
 반환 된 값을 표시 하는 다음 쿼리는 **CustomData** 계산된 측정값에서 함수:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
