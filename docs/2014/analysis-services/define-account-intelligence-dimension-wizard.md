---
title: 계정 인텔리전스 정의 (차원 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dimensionwizard.accountintelligencetypemapping.f1
ms.assetid: cbcff072-3a7e-4e98-858f-1b4265461561
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 27c0a8d48ae1a4a69ea96c4c87cc7cf8d0f1f1d3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080080"
---
# <a name="define-account-intelligence-dimension-wizard"></a>계정 인텔리전스 정의(차원 마법사)
  **계정 인텔리전스 정의** 페이지를 사용하여 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에서 정의한 계정 유형을 차원의 **계정 유형** 특성 유형과 연결된 차원 특성에서 정의한 계정 유형으로 매핑할 수 있습니다.  
  
> [!NOTE]  
>  **차원 유형 선택** 페이지에서 **표준 차원** 을 선택했으며 **차원 유형 지정** 페이지에서 차원 특성을 **계정 유형** 특성 유형에 매핑한 경우에만 이 페이지가 표시됩니다.  
  
## <a name="options"></a>변수  
 **원본 테이블 계정 유형**  
 **차원 키 및 유형 지정** 페이지의 **계정 유형** 특성 유형에 할당된 차원 특성에 포함된 값을 표시합니다.  
  
 **기본 제공 계정 유형**  
 원본 테이블의 계정 유형에 매핑되는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 정의된 계정 유형을 선택합니다.  
  
 다음 표에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 정의된 계정 유형을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**Asset**|특정 시간에 소유하고 있는 항목의 가치입니다.|  
|**Balance**|특정 시간의 항목 합계입니다.|  
|**Expense**|지출한 비용입니다.|  
|**Flow**|항목의 증분 합계입니다.|  
|**Income**|받은 항목의 가치입니다.|  
|**Liability**|특정 시간에 진 빚의 가치입니다.|  
|**통계**|항목의 계산된 비율 또는 집계되지 않는 항목의 합계입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [차원 마법사 F1 도움말](dimension-wizard-f1-help.md)   
 [차원 &#40;Analysis Services-다차원 데이터&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [다차원 모델의 차원](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  