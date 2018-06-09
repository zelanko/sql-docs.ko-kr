---
title: DataMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98b10c951043416280c05fd6a0e5eeb5df92c104
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739492"
---
# <a name="datamember-mdx"></a>DataMember(MDX)


  차원의 리프가 아닌 멤버에 관련된 시스템 생성 데이터 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 이 함수는 계층의 리프가 아닌 멤버에 작동 하며에서 사용할 수는 [UPDATE CUBE 문 (MDX)](../mdx/mdx-data-manipulation-update-cube.md) 리프 멤버의 하위 항목 대신 리프가 아닌 멤버를 직접에 쓰기 저장 데이터에 명령 합니다.  
  
> [!NOTE]  
>  지정된 멤버가 리프 멤버인 경우나 리프가 아닌 멤버에 관련 데이터 멤버가 없는 경우에는 지정된 멤버를 반환합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 **DataMember** 각 개별 직원에 대 한 판매 할당량을 표시 하는 계산된 측정값에서 함수:  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [주요 개념 mdx에서 &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  
