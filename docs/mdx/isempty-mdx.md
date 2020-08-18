---
description: IsEmpty(MDX)
title: IsEmpty (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 504df180a15673ecb0982d5a70c2eea1e9f71d11
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471865"
---
# <a name="isempty-mdx"></a>IsEmpty(MDX)


  평가 식이 빈 셀 값인지 여부를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsEmpty(Value_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Value_Expression*  
 일반적으로 멤버나 튜플의 셀 좌표를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **IsEmpty** 함수는 계산 된 식이 빈 셀 값인 경우 **true** 를 반환 합니다. 그렇지 않으면이 함수는 **false**를 반환 합니다.  
  
> [!NOTE]  
>  멤버의 기본 속성은 멤버의 값입니다.  
  
 **IsEmpty** 함수는 빈 셀 값이에서 특수 한 의미를 갖기 때문에 빈 셀을 안정적으로 테스트 하는 유일한 방법입니다 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  값 식의 계산에서 오류를 반환 하는 경우이 함수는 **false**를 반환 합니다. 예를 들어 속성 참조가 잘못된 속성이나 존재하지 않는 속성을 참조하는 경우 값 식에서 오류가 반환될 수 있습니다.  
  
 빈 셀에 대한 자세한 내용은 OLE DB 설명서를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예에서는 Date 차원의 Fiscal 계층에 있는 현재 멤버에 대한 Internet Sales Amount가 빈 셀을 반환하는 경우 TRUE를 반환합니다.  
  
 `WITH MEMBER MEASURES.ISEMPTYDEMO AS`  
  
 `IsEmpty([Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.ISEMPTYDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [빈 값 작업](../mdx/working-with-empty-values.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
