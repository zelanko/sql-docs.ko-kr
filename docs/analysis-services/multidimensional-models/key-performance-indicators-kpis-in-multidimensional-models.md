---
title: "핵심 성과 지표 (Kpi) 다차원 모델의 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing Key Performance Indicators
- Key Performance Indicators [Analysis Services]
- KPIs [Analysis Services]
- OLAP objects [Analysis Services], performance indicators
- weights [Analysis Services]
- displaying Key Performance Indicators
- parent KPIs [Analysis Services]
- child KPIs
ms.assetid: 73aee2da-da30-44f1-829c-0a4c078a7768
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2fb3d1fa6ae92ba6dd23f9295428d696834ee8d4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="key-performance-indicators-kpis-in-multidimensional-models"></a>다차원 모델의 KPI(핵심 성과 지표)
  비즈니스 용어에서 KPI(핵심 성과 지표)는 비즈니스 성취도를 평가하기 위한 정량 측정값을 나타냅니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 KPI는 큐브의 비즈니스 성취도 평가에 사용되는 큐브의 측정값 그룹과 관련된 계산의 모음입니다. 일반적으로 이러한 계산은 MDX(Multidimensional Expression) 식 또는 계산 멤버의 조합입니다. 또한 KPI에는 클라이언트 응용 프로그램의 KPI 계산 결과 표시 방법에 대한 정보를 제공하는 추가적인 메타데이터가 포함됩니다.  
  
 KPI는 목표 집합에 대한 정보, 큐브에 기록된 성능의 실제 수식 및 성능의 추세와 상태를 보여 주는 측정값을 처리합니다. AMO는 KPI 값에 대한 수식 및 기타 정의를 정의하는 데 사용됩니다. ADOMD.NET과 같은 쿼리 인터페이스는 클라이언트 응용 프로그램에서 KPI 값을 검색하여 최종 사용자에게 노출하는 데 사용됩니다. 자세한 내용은 [ADOMD.NET을 사용하여 개발](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)을 참조하세요.  
  
 단순 <xref:Microsoft.AnalysisServices.Kpi> 개체는 기본 정보, 목표, 계산된 실제 값, 상태 값, 추세 값 및 KPI가 표시되는 폴더로 구성되어 있습니다. 기본 정보에는 KPI의 이름과 설명이 포함됩니다. 목표는 숫자로 계산되는 MDX 식입니다. 실제 값은 숫자로 계산되는 MDX 식입니다. 상태 및 추세 값은 숫자로 계산되는 MDX 식입니다. 폴더는 KPI를 클라이언트에 표시하기 위한 권장 위치입니다.  
  
 비즈니스 용어에서 KPI(핵심 성과 지표)는 비즈니스 성취도를 평가하기 위한 정량 측정값을 나타냅니다. KPI는 주로 시간에 따라 평가됩니다. 예를 들어 조직의 영업부에서는 월별 매출 총 이익을 KPI로 사용하고 인사부에서는 분기별 직원 전직률을 KPI로 사용할 수 있습니다. 각각은 KPI의 예에 해당합니다. 경영진은 비즈니스 성과표에 그룹화된 KPI를 사용하여 비즈니스 성취도에 대한 빠르고 정확한 요약 정보를 얻습니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 KPI는 큐브의 비즈니스 성취도 평가에 사용되는 큐브의 측정값 그룹과 관련된 계산의 모음입니다. 일반적으로 이러한 계산은 MDX(Multidimensional Expression) 식 및 계산 멤버의 조합입니다. 또한 KPI에는 클라이언트 응용 프로그램의 KPI 계산 결과 표시 방법에 대한 정보를 제공하는 추가적인 메타데이터가 포함됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 KPI는 여러 클라이언트 응용 프로그램에서 사용할 수 있는 서버 기반 KPI라는 주요 이점이 있습니다. 여러 클라이언트 응용 프로그램에서 생성되는 여러 사실 버전과 달리 서버 기반 KPI는 단일 사실 버전을 제공합니다. 또한 각 클라이언트 컴퓨터 대신 서버에서 복잡한 계산을 수행하므로 성능상의 이점이 있습니다.  
  
## <a name="common-kpi-terms"></a>일반적인 KPI 용어  
 다음 표에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 일반적인 KPI 용어에 대한 정의를 제공합니다.  
  
|용어|정의|  
|----------|----------------|  
|목표|KPI의 목표 값을 반환하는 MDX 숫자 식 또는 계산입니다.|  
|Value|KPI의 실제 값을 반환하는 MDX 숫자 식입니다.|  
|상태|지정된 기간의 KPI 상태를 나타내는 MDX 식입니다.<br /><br /> 상태 MDX 식은 -1과 1 사이의 정규화된 값을 반환해야 합니다. 값이 -1 이하이면 "불량"이나 "낮음"으로 해석됩니다. 값 영(0)은 "허용됨"이나 "보통"으로 해석됩니다. 1 이상의 값은 "양호"나 "높음"으로 해석됩니다.<br /><br /> 중간 값을 제한 없이 선택적으로 반환할 수 있으며 클라이언트 응용 프로그램에서 지원하는 경우 이러한 값을 사용하여 추가 상태를 원하는 만큼 표시할 수 있습니다.|  
|추세|시간에 따라 KPI 값을 평가하는 MDX 식입니다. 추세는 특정 비즈니스 컨텍스트에서 유용한 시간 기반 조건입니다.<br /><br /> 추세 MDX 식을 사용하여 비즈니스 사용자는 KPI가 시간에 따라 향상되는지 또는 저하되는지 여부를 확인할 수 있습니다.|  
|상태 표시|KPI의 상태를 빠르게 보여 주는 시각적 요소입니다. 요소 표시 방법은 상태를 평가하는 MDX 식의 값에 의해 결정됩니다.|  
|추세 표시|KPI의 추세를 빠르게 보여 주는 시각적 요소입니다. 요소 표시 방법은 추세를 평가하는 MDX 식의 값에 의해 결정됩니다.|  
|표시 폴더|사용자가 큐브를 검색할 때 KPI가 나타나는 폴더입니다.|  
|부모 KPI|부모 KPI 계산의 일부로 자식 KPI의 값을 사용하는 기존 KPI를 가리킵니다. 때에 따라서는 다른 KPI에 대한 값으로 구성되는 계산으로 KPI가 지정될 수 있습니다. 이 속성을 통해 클라이언트 응용 프로그램에서 부모 KPI 아래에 자식 KPI를 정확히 표시할 수 있습니다.|  
|현재 시간 멤버|KPI의 임시 컨텍스트를 식별하는 멤버를 반환하는 MDX 식입니다.|  
|Weight|KPI에 상대적 중요도를 할당하는 MDX 숫자 식입니다. 부모 KPI에 특정 KPI가 할당된 경우 부모 KPI의 값 계산 시 가중치에 따라 자식 KPI 값의 결과가 알맞게 조정됩니다.|  
  
## <a name="parent-kpis"></a>부모 KPI  
 조직의 여러 비즈니스 메트릭을 다양한 수준에서 추적할 수 있습니다. 예를 들어 2-3개의 KPI만으로 회사 전체의 비즈니스 성공 여부를 평가하되 이러한 회사 차원 KPI의 기반으로 회사 전체의 비즈니스 단위에서 추적하는 3-4개의 다른 KPI를 사용할 수 있습니다. 또한 회사의 비즈니스 단위에서 동일한 KPI를 계산하는 데 여러 다른 통계를 사용할 수 있습니다. 계산된 KPI의 결과는 회사 차원 KPI로 롤업됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 KPI 간에 부모-자식 관계를 정의할 수 있습니다. 이러한 부모-자식 관계를 통해 자식 KPI의 결과를 사용하여 부모 KPI의 결과를 계산할 수 있습니다. 또한 클라이언트 응용 프로그램에서 이 관계를 사용하여 부모 및 자식 KPI를 적절히 표시할 수 있습니다.  
  
## <a name="weights"></a>가중치  
 자식 KPI에 가중치를 할당할 수도 있습니다. 가중치를 사용하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 부모 KPI의 값을 계산할 때 자식 KPI의 결과가 그에 따라 조정됩니다.  
  
## <a name="retrieving-and-displaying-kpis"></a>KPI 검색 및 표시  
 KPI의 표시 방법은 전적으로 클라이언트 응용 프로그램의 구현에 따라 달라집니다. 예를 들어 큐브 디자이너의 **KPI** 탭에 있는 도구 모음에서 **브라우저 보기** 를 선택하면 가능한 하나의 클라이언트 구현과 함께 상태 및 추세 표시를 보여 주는 그래픽, KPI 그룹화에 사용되는 폴더를 보여 주는 그래픽 및 부모 KPI 아래에 자식 KPI가 표시된 그래픽이 나타납니다.  
  
 MDX 함수를 사용하여 MDX 식, 문 및 스크립트에 사용할 값이나 목표와 같은 KPI의 개별 섹션을 검색할 수 있습니다.  
  
  

