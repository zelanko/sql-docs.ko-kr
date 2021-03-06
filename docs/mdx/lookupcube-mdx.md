---
description: LookupCube(MDX)
title: LookupCube (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d00f7cf0d657d2424b461ad95bc7f534cd2c33e8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341478"
---
# <a name="lookupcube-mdx"></a>LookupCube(MDX)


  같은 데이터베이스에서 지정된 또 다른 큐브에 대해 계산된 MDX 식의 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Numeric expression syntax  
LookupCube(Cube_Name, Numeric_Expression )  
  
String expression syntax  
LookupCube(Cube_Name, String_Expression )  
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브의 이름을 지정하는 유효한 문자열 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *String_Expression*  
 문자열을 반환하는 셀 좌표의 유효한 문자열 식으로서, 일반적으로 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 숫자 식이 지정 된 경우 **LookupCube** 함수는 지정 된 큐브에서 지정 된 숫자 식을 계산 하 고 결과 숫자 값을 반환 합니다.  
  
 문자열 식이 지정 된 경우 **LookupCube** 함수는 지정 된 큐브에서 지정 된 문자열 식을 계산 하 고 결과 문자열 값을 반환 합니다.  
  
 **LookupCube** 함수는 **LookupCube** 함수를 포함 하는 MDX 쿼리가 실행 중인 원본 큐브와 동일한 데이터베이스 내의 큐브에 대해 작동 합니다.  
  
> [!IMPORTANT]  
>  현재 쿼리의 컨텍스트는 쿼리되는 큐브에는 적용되지 않으므로 숫자 또는 문자열 식에 필요한 현재 멤버를 모두 지정해야 합니다.  
  
 **LookupCube** 함수를 사용 하는 계산은 성능이 저하 될 수 있습니다. 이 함수를 사용하는 대신 필요한 모든 데이터가 하나의 큐브에 있도록 솔루션을 다시 설계하는 것이 좋습니다.  
  
## <a name="examples"></a>예제  
 다음 쿼리에서는 LookupCube를 사용하는 방법을 보여 줍니다.  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
