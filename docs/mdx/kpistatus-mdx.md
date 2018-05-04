---
title: KPIStatus (MDX) | Microsoft Docs
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
dev_langs:
- kbMDX
helpviewer_keywords:
- KPIStatus function
ms.assetid: c563f3a9-5dd7-4586-9519-16a3ca58e2ec
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 2f00db6e9abf09d6ed4d02036fff11b23f9d7c42
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="kpistatus-mdx"></a>KPIStatus(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정된 KPI(핵심 성과 지표)의 상태 부분을 나타내는 정규화된 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
KPIStatus(KPI_Name)  
```  
  
## <a name="arguments"></a>인수  
 *KPI_Name*  
 KPI의 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>주의  
 상태 값은 일반적으로 -1에서 1 사이의 정규화된 값입니다.  
  
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
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
