---
title: 집계 및 집계 디자인 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- aggregations [Analysis Services], about aggregations
- storage [Analysis Services], aggregations
- Storage Design Wizard
- data summary [Analysis Services]
- data storage [Analysis Services]
- storing data [Analysis Services], aggregations
- aggregations [Analysis Services]
ms.assetid: 35bd8589-39fa-4e0b-b28f-5a07d70da0a2
author: minewiskan
ms.author: owend
ms.openlocfilehash: c56e80482ef71e8041f8518ae9901691a1809990
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545335"
---
# <a name="aggregations-and-aggregation-designs"></a>Aggregations and Aggregation Designs
  <xref:Microsoft.AnalysisServices.AggregationDesign>개체는 여러 파티션에서 공유할 수 있는 집계 정의의 집합을 정의합니다.  
  
 <xref:Microsoft.AnalysisServices.Aggregation> 개체는 차원의 특정 세분성으로 측정값 그룹의 요약을 나타냅니다.  
  
 단순 <xref:Microsoft.AnalysisServices.Aggregation> 개체는 기본 정보와 차원으로 구성되어 있습니다. 기본 정보에는 집계의 이름, ID, 주석 및 설명이 포함됩니다. 차원은 차원 세분성 특성 목록을 포함하는 <xref:Microsoft.AnalysisServices.AggregationDimension> 개체의 컬렉션입니다.  
  
 집계는 리프 셀의 데이터로 미리 계산된 요약입니다. 집계는 질문이 있기 전에 응답을 준비하여 쿼리 응답 시간을 단축시켜 줍니다. 예를 들어 수많은 행을 포함하는 데이터 웨어하우스 팩트 테이블에서 특정 제품 라인에 대한 주간 판매 합계를 요청하는 쿼리의 경우 응답을 컴퓨팅하기 위해 쿼리 시 팩트 테이블의 모든 행을 검색하고 합산해야 한다면 응답 시간이 매우 길어질 수 있습니다. 그러나 이 쿼리에 응답하기 위한 요약 데이터가 미리 계산되어 있다면 응답이 거의 즉시 이루어질 수 있습니다. 이러한 요약 데이터 미리 계산은 신속한 응답 시간을 위한 OLAP 기술의 기본이며 처리 과정에서 수행됩니다.  
  
 큐브는 OLAP 기술에서 요약 데이터를 다차원 구조로 구성하는 방법입니다. 차원과 그 특성의 계층에는 큐브에 질문할 수 있는 쿼리가 반영됩니다. 집계는 차원으로 지정된 좌표에 있는 셀에 다차원 구조로 저장됩니다. 예를 들어, “1998년 제품 X의 북서부 지역 판매량은?” 질문에는 3차원(제품, 시간 및 지역)과 단일 측정값(판매)이 포함됩니다. 큐브에서 지정한 좌표(제품 X, 1998, 북서부)에 있는 셀 값은 단일 숫자 값이며 질문에 대한 답이 됩니다.  
  
 "1998년의 분기별 및 지역별 하드웨어 제품 판매량은 얼마입니까?"와 같이 여러 값을 반환할 수 있는 질문도 있습니다. 이러한 쿼리는 지정한 조건에 맞는 좌표로부터 셀 집합을 반환합니다. 쿼리에서 반환하는 셀 개수는 제품 차원의 하드웨어 수준에 포함된 항목 수, 1998년의 네 분기 및 지리 차원의 지역 수에 따라 달라집니다. 모든 요약 데이터가 집계로 미리 계산된 경우에는 지정한 셀을 추출하는 데 필요한 시간에 따라서만 쿼리의 응답 시간이 달라집니다. 팩트 테이블의 데이터를 계산하거나 읽을 필요는 없습니다.  
  
 큐브에서 가능한 집계를 모두 미리 계산하면 모든 쿼리의 응답 시간을 최대한 단축시킬 수 있지만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 미리 계산된 다른 집계에서 일부 집계 값을 쉽게 계산할 수 있습니다. 또한 가능한 집계를 모두 계산하려면 처리 시간과 스토리지가 많이 소요됩니다. 그러므로 스토리지 요구 사항과 미리 계산할 수 있는 집계 비율 간에는 상호 균형이 필요합니다. 집계를 전혀 미리 계산하지 않으면(0%) 큐브에 필요한 처리 시간과 스토리지 공간이 최소화되지만 먼저 각 쿼리에 응답하는 데 필요한 데이터를 리프 셀에서 검색한 후 쿼리 시에 각 쿼리에 대한 응답을 위해 집계를 수행해야 하므로 쿼리 응답 시간이 연장될 수 있습니다. 예를 들어 앞의 질문 "1998년 북서부 지역의 제품 X 판매량은 얼마입니까?"에 대한 응답으로 단일 숫자를 반환하기 위해 수많은 데이터 행을 읽어야 하며 각 행에서 판매 측정값을 제공하는 데 사용되는 열 값을 추출하여 합계를 계산해야 합니다. 또한 데이터를 검색 하는 데 필요한 시간은 데이터에 대해 선택한 저장소 모드 (MOLAP, HOLAP 또는 ROLAP)에 따라 크게 달라 집니다.  
  
## <a name="designing-aggregations"></a>집계 디자인  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 미리 계산 된 값에서 다른 집계를 신속 하 게 계산할 수 있도록 미리 계산할 집계를 선택 하기 위한 정교한 알고리즘을 통합 합니다. 예를 들어 시간 계층의 월 수준에 대해 집계를 미리 계산하면 사분기 수준에 대한 계산에는 요청 시 신속하게 계산할 수 있는 3가지 숫자의 요약만 필요합니다. 이 기술을 통해 쿼리 응답 시간에 주는 영향을 최소화하면서 처리 시간을 절약하고 스토리지 요구 사항을 줄일 수 있습니다.  
  
 집계 디자인 마법사는 쿼리 응답 시간과 스토리지 요구 사항 간의 적절한 균형을 이루기 위한 알고리즘에 대해 스토리지 및 비율 제약 조건을 지정할 수 있는 옵션을 제공합니다. 그러나 집계 디자인 마법사의 알고리즘은 가능한 쿼리가 모두 균일하다고 가정합니다. 사용 빈도 기반 최적화 마법사를 사용하면 클라이언트 애플리케이션에서 제출한 쿼리를 분석하여 측정값 그룹에 대한 집계 디자인을 조정할 수 있습니다. 또한 이 마법사를 통해 큐브의 집계를 튜닝하여 큐브에 필요한 스토리지에 큰 영향을 주지 않으면서 빈번히 발생하는 쿼리에 대해서는 응답 능력을 향상시키고 빈번히 발생하지 않는 쿼리에 대해서는 응답 능력을 감소시킬 수 있습니다.  
  
 집계는 마법사를 사용하여 디자인되지만 집계가 디자인되는 파티션을 처리한 다음에만 실제로 계산됩니다. 집계가 생성된 다음 큐브 구조가 변경되는 경우 또는 큐브의 원본 테이블에서 데이터가 추가되거나 변경되는 경우에는 일반적으로 큐브의 집계를 검토하고 큐브를 다시 처리해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [파티션 스토리지 모드 및 처리](partitions-partition-storage-modes-and-processing.md)  
  
  
