---
title: "차원 유형 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- time dimensions [Analysis Services]
- quantitative dimensions [Analysis Services]
- BillOfMaterials dimension [Analysis Services]
- geography dimensions
- utility dimensions [Analysis Services]
- channel dimensions
- dimensions [Analysis Services], types
- products dimensions [Analysis Services]
- account dimensions [Analysis Services]
- organization dimensions
- currency dimensions [Analysis Services]
- rates dimensions
- promotion dimensions
- scenario dimensions [Analysis Services]
- customers dimensions [Analysis Services]
- Type property
ms.assetid: bd3195da-e762-4c98-b643-34c76e842343
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7e870e18ae05b3daddf9e8230079bec87bb29e2d
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="database-dimension-properties---types"></a>데이터베이스 차원 속성 형식
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
**형식** 속성 설정은 서버 및 클라이언트 응용 프로그램에 차원 내용에 대 한 정보를 제공 합니다. 일부 경우에는 **형식** 설정은 클라이언트 응용 프로그램에 대 한 지침을 제공 하며 선택적입니다. 다른 경우에서와 같은 **계정** 또는 **시간** 차원은 **형식** 차원과 차원의 특성에 대 한 속성 설정이 특정 서버 기반 동작을 결정 및 큐브의 특정 동작을 구현 해야 할 수 있습니다. 예를 들어는 **형식** 차원의 속성 설정할 수 있습니다 **계정** 표준 차원에 계정 특성이 포함 되어는 클라이언트 응용 프로그램에 알립니다. 시간, 계정 및 통화 차원에 대 한 자세한 내용은 참조 [날짜 유형 차원 만들기](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md), [부모-자식 유형 차원의 재무 계정 만들기](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md), 및 [통화 만들기 차원 입력](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)합니다.  
  
 기본 설정은 차원 유형은 **일반**, 차원의 내용에 대해 정확히 수 있게 해줍니다. 이 모든 차원에 대 한 기본 설정을 지정 하지 않는 한 차원을 처음 정의할 때 **시간** 차원 마법사를 사용 하 여 차원을 정의할 때. 유지 해야 **일반** 차원 마법사가 차원 유형에 대 한 적절 한 유형을 나열 하지 않는 경우 차원 유형으로 합니다.  
  
## <a name="available-dimension-types"></a>사용 가능한 차원 유형  
 다음 표에에서 사용할 수 있는 차원 유형에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다.  
  
|차원 유형|Description|  
|--------------------|-----------------|  
|일반|해당 유형이 특별한 차원 유형으로 설정되지 않은 차원입니다.|  
|Time|해당 특성이 연도, 반기, 분기, 월 및 일과 같은 기간을 나타내는 차원입니다.|  
|조직|해당 특성이 직원이나 자회사와 같은 조직 정보를 나타내는 차원입니다.|  
|지리|해당 특성이 도시 또는 우편 번호와 같은 지리적 정보를 나타내는 차원입니다.|  
|제품 구성 정보|해당 특성이 제품의 부품 목록 같은 재고 또는 제조 정보를 나타내는 차원입니다.|  
|계정|해당 특성이 재무 보고용 계정 차트를 나타내는 차원입니다.|  
|Customers|해당 특성이 고객 또는 연락처 정보를 나타내는 차원입니다.|  
|제품|해당 특성이 제품 정보를 나타내는 차원입니다.|  
|시나리오|해당 특성이 기획 또는 전략 분석 정보를 나타내는 차원입니다.|  
|정량|해당 특성이 정량 정보를 나타내는 차원입니다.|  
|유틸리티|해당 특성이 기타 정보를 나타내는 차원입니다.|  
|Currency|이 차원 유형에는 통화 데이터 및 메타데이터가 포함됩니다.|  
|요율|해당 특성이 환율 정보를 나타내는 차원입니다.|  
|채널|해당 특성이 채널 정보를 나타내는 차원입니다.|  
|Promotion|해당 특성이 마케팅 홍보 행사 정보를 나타내는 차원입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [기존 테이블을 사용 하 여 차원 만들기](../../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [차원 &#40; Analysis Services-다차원 데이터 &#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
