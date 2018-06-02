---
title: KPIGoal (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4d7bfd5c6458e725692a0c0fcd8c7b3d03a1ca29
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580295"
---
# <a name="kpigoal-mdx"></a>KPIGoal(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 KPI(핵심 성과 지표)의 목표 부분 값을 계산하는 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
KPIGoal(KPI_Name)  
```  
  
## <a name="arguments"></a>인수  
 *KPI_Name*  
 KPI의 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="example"></a>예제  
 다음 예에서는 Fiscal Year 특성 계층 중 세 멤버의 하위 항목에 대한 채널 수익 측정값의 KPI 값, KPI 목표, KPI 상태 및 KPI 추세를 반환합니다.  
  
```  
SELECT  
   { KPIValue("Channel Revenue"),   
     KPIGoal("Channel Revenue"),  
     KPIStatus("Channel Revenue"),   
     KPITrend("Channel Revenue")  
   } ON Columns,  
Descendants  
   ( { [Date].[Fiscal].[Fiscal Year].&[2002],  
       [Date].[Fiscal].[Fiscal Year].&[2003],  
       [Date].[Fiscal].[Fiscal Year].&[2004]   
     }, [Date].[Fiscal].[Fiscal Quarter]  
   ) ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
