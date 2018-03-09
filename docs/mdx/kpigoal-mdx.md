---
title: KPIGoal (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: KPIGoal function
ms.assetid: 0122c7d5-eefc-4819-b7a9-c80cd35505a8
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ab6781d7455572811d4bc1a596b9b1a3c017e25d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
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
  
## <a name="remarks"></a>주의  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
