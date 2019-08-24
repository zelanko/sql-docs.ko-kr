---
title: 차원 유형 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cbe1c8932c082ce537cd5dc3f2b12d98c05c3811
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62728559"
---
# <a name="dimension-types"></a>차원 유형
  `Type` 속성 설정은 서버 및 클라이언트 애플리케이션에 차원 내용에 대한 정보를 제공합니다. 일부 경우에 `Type` 설정은 클라이언트 애플리케이션에 대한 지침만 제공하며 선택적입니다. `Accounts` 또는 `Time` 차원의 경우처럼 차원 및 해당 특성에 대한 `Type` 속성 설정에 따라 특정 서버 기반 동작이 결정되는 경우도 있고 큐브의 특정 동작을 구현하는 데 이러한 속성 설정이 필요할 수도 있습니다. 예를 들어 차원의 `Type` 속성을 `Accounts`로 설정하여 표준 차원에 계정 특성이 포함되어 있다는 것을 클라이언트 애플리케이션에 나타낼 수 있습니다. 시간, 계정 및 통화 차원에 대 한 자세한 내용은 참조 하세요. [날짜 유형 차원 만들기](../multidimensional-models/database-dimensions-create-a-date-type-dimension.md)를 [부모-자식 유형 차원의 재무 계정 만들기](../multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md), 및 [통화 만들기 차원 입력](../multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)합니다.  
  
 차원 유형의 기본 설정은 차원 내용에 대해 어떠한 가정도 하지 않는 `Regular`입니다. 이 설정은 차원 마법사를 사용하여 차원을 정의할 때 `Time`을 지정하지 않은 한 차원을 처음 정의할 때 모든 차원에 대한 기본 설정이 됩니다. 차원 마법사가 차원 유형에 대한 적절한 유형을 나열하지 않는 경우 `Regular`를 차원 유형으로 유지해야 합니다.  
  
## <a name="available-dimension-types"></a>사용 가능한 차원 유형  
 다음 표에에서 사용할 수 있는 차원 유형에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다.  
  
|차원 유형|Description|  
|--------------------|-----------------|  
|Regular|해당 유형이 특별한 차원 유형으로 설정되지 않은 차원입니다.|  
|Time|해당 특성이 연도, 반기, 분기, 월 및 일과 같은 기간을 나타내는 차원입니다.|  
|조직|해당 특성이 직원이나 자회사와 같은 조직 정보를 나타내는 차원입니다.|  
|지리|해당 특성이 도시 또는 우편 번호와 같은 지리적 정보를 나타내는 차원입니다.|  
|제품 구성 정보|해당 특성이 제품의 부품 목록 같은 재고 또는 제조 정보를 나타내는 차원입니다.|  
|계정|해당 특성이 재무 보고용 계정 차트를 나타내는 차원입니다.|  
|고객|해당 특성이 고객 또는 연락처 정보를 나타내는 차원입니다.|  
|제품|해당 특성이 제품 정보를 나타내는 차원입니다.|  
|시나리오|해당 특성이 기획 또는 전략 분석 정보를 나타내는 차원입니다.|  
|정량|해당 특성이 정량 정보를 나타내는 차원입니다.|  
|유틸리티|해당 특성이 기타 정보를 나타내는 차원입니다.|  
|Currency|이 차원 유형에는 통화 데이터 및 메타데이터가 포함됩니다.|  
|요율|해당 특성이 환율 정보를 나타내는 차원입니다.|  
|채널|해당 특성이 채널 정보를 나타내는 차원입니다.|  
|홍보 행사|해당 특성이 마케팅 홍보 행사 정보를 나타내는 차원입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [기존 테이블을 사용 하 여 차원 만들기](../multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [차원 & #40; Analysis Services-다차원 데이터 & #41;](dimensions-analysis-services-multidimensional-data.md)  
  
  
