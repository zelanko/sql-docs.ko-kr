---
title: IsEmpty (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dbed0eba3fec73d7134b1ce21275c28dbd387fcd
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740172"
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
  
## <a name="remarks"></a>Remarks  
 **IsEmpty** 함수에서 반환 **true** 평가 식이 빈 셀 값이 있습니다. 그렇지 않으면이 함수가 반환 **false**합니다.  
  
> [!NOTE]  
>  멤버의 기본 속성은 멤버의 값입니다.  
  
 **IsEmpty** 함수는 빈 셀 값에서 특별 한 의미를 갖기 때문에 빈 셀에 대 한 안정적으로 테스트할 수 있는 유일한 방법은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]합니다.  
  
> [!IMPORTANT]  
>  경우 값 식의 평가 결과 오류가 반환 되는 함수는 반환 **false**합니다. 예를 들어 속성 참조가 잘못된 속성이나 존재하지 않는 속성을 참조하는 경우 값 식에서 오류가 반환될 수 있습니다.  
  
 빈 셀에 대한 자세한 내용은 OLE DB 설명서를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예에서는 Date 차원의 Fiscal 계층에 있는 현재 멤버에 대한 Internet Sales Amount가 빈 셀을 반환하는 경우 TRUE를 반환합니다.  
  
 `WITH MEMBER MEASURES.ISEMPTYDEMO AS`  
  
 `IsEmpty([Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.ISEMPTYDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [빈 값 작업](../mdx/working-with-empty-values.md)   
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
