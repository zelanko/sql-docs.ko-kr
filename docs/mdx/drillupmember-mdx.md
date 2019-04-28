---
title: DrillupMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 31981669d5d08e63a853b8daa530b886f9b7dfbe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62690763"
---
# <a name="drillupmember-mdx"></a>DrillupMember(MDX)


  지정된 두 번째 집합 멤버의 하위 항목이 아닌 지정된 집합 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DrillupMember(Set_Expression1, Set_Expression2)   
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression1*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Set_Expression2*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **DrillupMember** 함수에는 두 번째 집합에서 멤버의 하위 항목에는 첫 번째 집합에 지정 된 멤버를 기준으로 하는 멤버 집합을 반환 합니다. 첫 번째 집합은 어떠한 차원도 될 수 있지만 두 번째 집합은 1차원 집합을 포함해야 합니다. 첫 번째 집합의 원래 멤버 간 순서는 유지됩니다. 이 함수는 첫 번째 집합의 멤버 중 두 번째 집합에 있는 멤버의 직계 하위 항목에 해당하는 멤버만 포함하여 집합을 구성합니다. 첫 번째 집합에 있는 멤버의 직계 상위 항목이 두 번째 집합에 없으면 이 함수에서 반환된 집합에는 첫 번째 집합의 멤버가 포함됩니다. 첫 번째 집합의 하위 항목 중 두 번째 집합의 상위 멤버보다 앞에 있는 하위 항목도 포함됩니다.  
  
 첫 번째 집합에는 멤버 대신 튜플이 포함될 수 있습니다. 튜플 드릴다운은 멤버 대신 튜플 집합을 반환하는 OLE DB의 확장 기능입니다.  
  
> [!IMPORTANT]  
>  바로 다음에 자식 또는 하위 항목이 오는 멤버만 드릴업됩니다. 모두 드릴 다운에 대 한 집합에서 멤버의 순서가 중요\* 및 Drillup\* 함수 패밀리입니다. 사용을 고려 합니다 **Hierarchize** 적절 하 게 첫 번째 집합의 멤버를 정렬 하는 함수입니다.  
  
## <a name="example"></a>예제  
 다음 세 예제는 두 번째 집합을 제외하고는 동일합니다. 첫 번째 예제에서 두 번째 집합은 United States입니다. 따라서 Colorado는 결과 집합에서 제외되었습니다. Colorado는 United States의 하위 항목입니다.  
  
```  
SELECT DrillUpMember (   
  { [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[United States]}   
 ) ON 0   
FROM [Adventure Works]  
```  
  
 예제 2에서는 멤버 순서의 중요성을 보여 줍니다. 이후 **DrillupMember** 드릴업은 바로 뒤에 하위 항목 첫 번째 집합에는 해당 멤버를 해당 드릴업 하지 않습니다 Canada 멤버입니다. Canada는 해당 하위 항목이 United States 및 Colorado와 분리되어 있습니다. Canada가 Alberta 바로 위에 있도록 멤버를 다시 정렬하면 Alberta와 Brunswick이 둘 다 행 집합에서 제외됩니다.  
  
```  
SELECT DrillUpMember (   
 {  [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
```  
  
 예제 3 방법 사용 **Hierarchize** Canada 멤버의 멤버 순서 및 드릴업 영향을 줄일 수 있습니다.  
  
```  
SELECT DrillUpMember (   
 Hierarchize   
  (   
   { [Geography].[Geography].[Country].[Canada]   
    ,[Geography].[Geography].[Country].[United States]   
    ,[Geography].[Geography].[State-Province].[Colorado]   
    ,[Geography].[Geography].[State-Province].[Alberta]   
    ,[Geography].[Geography].[State-Province].[Brunswick]    
   }   
  ), {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
