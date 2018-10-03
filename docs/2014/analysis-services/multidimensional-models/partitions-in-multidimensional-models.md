---
title: 다차원 모델의 파티션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 26e01dc7-fa49-4b1f-99eb-7799d1b4dcd2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8caec3620a5f7c0df1e3a5d0558272b1a2fb7bfa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164193"
---
# <a name="partitions-in-multidimensional-models"></a>다차원 모델의 파티션
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 *파티션* 은 로드된 팩트 데이터의 실제 저장소를 측정값 그룹에 제공합니다. 각 측정값 그룹에 대해 단일 파티션이 자동으로 만들어지지만 더욱 효율적으로 처리하고 쿼리 성능이 빨라지도록 데이터를 추가로 분할하는 추가 파티션을 만드는 것이 일반적입니다.  
  
 파티션을 하나 이상의 서버에서 독립적으로 병렬 처리할 수 있기 때문에 더 효율적으로 처리됩니다. 저장소 모드와 집계 최적화를 사용하여 응답 시간이 짧아지도록 각 파티션을 구성할 수 있기 때문에 쿼리가 더 빨리 실행됩니다. 예를 들어 최신 데이터를 포함하는 파티션에 대해 MOLAP 저장소를 선택하는 것이 ROLAP를 선택하는 경우보다 일반적으로 빠릅니다. 마찬가지로, 날짜별로 분할하는 경우 최신 데이터가 들어 있는 파티션의 최적화가 액세스 빈도가 낮은 오래된 데이터가 들어 있는 파티션의 최적화보다 더 많을 수 있습니다. 파티션을 통해 저장소 및 집계 디자인이 바뀌면 앞으로의 병합 작업에 부정적인 영향을 줍니다. 개별 파티션을 최적화하기 전에 병합이 파티션 관리 전략의 필수 구성 요소인지 여부를 고려해야 합니다.  
  
> [!NOTE]  
>  여러 파티션에 대한 지원은 비즈니스 인텔리전스 버전 및 엔터프라이즈 버전에서 제공됩니다. 스탠더드 버전에서는 여러 파티션을 지원하지 않습니다. 자세한 내용은 [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조하세요.  
  
## <a name="important-considerations-when-designing-a-partitioning-strategy"></a>분할 전략을 디자인할 때 중요한 고려 사항  
 큐브 데이터의 무결성이 보장되려면 파티션 사이에 중복된 데이터가 없도록 큐브의 파티션에 데이터가 분산되어야 합니다. 파티션에서 데이터가 요약되는 경우 둘 이상의 파티션에 있는 모든 데이터 요소는 서로 다른 데이터 요소인 것처럼 요약됩니다. 따라서 이런 경우 최종 사용자에게 잘못된 요약과 오류가 있는 데이터가 제공될 수 있습니다. 예를 들어 제품 X의 판매 트랜잭션이 두 파티션의 팩트 테이블에서 중복될 경우 제품 X 판매 요약에 중복된 트랜잭션이 이중으로 계산될 수 있습니다.  
  
 파티션은 병합할 수 있으므로 전체적인 저장소 및 데이터 업데이트 전략에서 이 기능을 사용할 수 있습니다. 파티션은 저장소 모드와 집계 디자인이 동일한 경우에만 병합할 수 있습니다. 나중에 병합할 파티션을 만들려면 파티션을 만들 때 다른 파티션의 집계 디자인을 복사합니다. 파티션을 만든 후 이를 편집하여 다른 파티션의 집계 디자인을 복사할 수도 있습니다. 파티션 병합은 결과 파티션에 데이터가 중복되지 않도록 주의해서 수행해야 합니다. 데이터가 중복될 경우 정확하지 않은 큐브 데이터가 만들어질 수 있습니다.  
  
## <a name="local-partitions"></a>로컬 파티션  
 로컬 파티션은 한 서버에서 정의되어 처리되고 저장되는 파티션입니다. 큐브에 큰 측정값 그룹이 있는 경우 파티션 전체에서 병렬 처리되도록 해당 측정값 그룹을 분할할 수 있습니다. 병렬 처리를 수행하면 실행 속도가 빨라집니다. 작업을 처리 중인 파티션을 다른 파티션이 시작되기 전에 종료할 필요가 없기 때문에 두 파티션이 병렬로 실행될 수 있습니다. 자세한 내용은 [로컬 파티션 만들기 및 관리&#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)를 참조하세요.  
  
## <a name="remote-partitions"></a>원격 파티션  
 원격 파티션은 한 서버에서 정의되어 다른 서버에서 처리되고 저장되는 파티션입니다. 데이터 및 메타데이터의 저장소를 여러 서버로 분산시키려는 경우 원격 파티션을 사용합니다. 일반적으로 개발에서 프로덕션으로 전환하면 분석 중인 데이터의 크기가 몇 배 이상 증가합니다. 이렇게 큰 데이터 청크의 경우 해당 데이터를 여러 컴퓨터로 분산할 수 있습니다. 이는 한 컴퓨터가 모든 데이터를 보유할 수 없기 때문이기도 하지만 두 개 이상의 컴퓨터에서 데이터를 병렬로 처리할 수 있기 때문이기도 합니다. 자세한 내용은 [원격 파티션 만들기 및 관리 &#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md)합니다.  
  
## <a name="aggregations"></a>Aggregations  
 집계는 큐브 데이터의 미리 계산된 요약으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 신속한 쿼리 응답을 제공할 수 있도록 도와 줍니다. 저장소 성능 향상에 대한 제한을 설정하거나 집계 빌드 프로세스가 얼마 동안 실행된 후 이를 임의로 중지하여 측정값 그룹에 대해 만들어지는 집계 수를 제어할 수 있습니다. 집계 수가 많을수록 더 좋은 것은 아닙니다. 모든 새로운 집계는 디스크 공간과 처리 시간 모두에서 비용을 초래합니다. 30% 성능 향상이 되도록 집계를 만든 다음 테스트 또는 환경에서 보장하는 경우에만 집계 수를 늘리는 것이 좋습니다. 자세한 내용은 [집계 디자인&#40;Analysis Services - 다차원&#41;](designing-aggregations-analysis-services-multidimensional.md)을 참조하세요.  
  
## <a name="partition-merging-and-editing"></a>파티션 병합 및 편집  
 두 개의 파티션이 동일한 집계 디자인을 사용하는 경우 이러한 두 파티션을 하나로 병합할 수 있습니다. 예를 들어 월별로 분할된 재고 차원이 있는 경우 월말마다 해당 월 파티션을 기존 연간 파티션에 병합할 수 있습니다. 이렇게 하면 현재 월 파티션을 신속하게 처리 및 분석할 수 있으며 해당 연도의 나머지 달은 병합될 때만 다시 처리해도 됩니다. 이러한 다시 처리 작업은 시간이 오래 걸리며 낮은 빈도로 실행할 수 있습니다. 파티션 병합 프로세스를 관리 하는 방법에 대 한 자세한 내용은 참조 하세요. [Analysis Services의 파티션 병합 &#40;&AMP;#40;SSAS-다차원&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)합니다. 사용 하 여 큐브 파티션을 편집 하려면 합니다 **파티션을** 큐브 디자이너의 탭을 참조 하십시오 [편집 또는 파티션이 삭제 &#40;&#40;analysis Services-다차원&#41;](edit-or-delete-partitions-analyisis-services-multidimensional.md).  
  
## <a name="related-topics"></a>관련 항목  
  
|항목|Description|  
|-----------|-----------------|  
|[로컬 파티션 만들기 및 관리 &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)|필터 또는 다른 팩트 테이블을 사용하여 데이터가 중복되지 않도록 데이터를 분할하는 방법에 대한 정보가 포함되어 있습니다.|  
|[파티션 저장소 설정 &#40;Analysis Services-다차원&#41;](set-partition-storage-analysis-services-multidimensional.md)|파티션 저장소를 구성하는 방법에 대해 설명합니다.|  
|[파티션 편집 또는 삭제 &#40;Analysis Services-다차원&#41;](edit-or-delete-partitions-analyisis-services-multidimensional.md)|파티션을 보고 편집하는 방법에 대해 설명합니다.|  
|[Analysis Services의 파티션 병합 &#40;&AMP;#40;SSAS-다차원&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)|데이터가 중복되지 않도록 서로 다른 팩트 테이블 또는 서로 다른 데이터 조각이 있는 파티션을 병합하는 방법에 대한 정보가 포함되어 있습니다.|  
|[파티션 쓰기 저장(writeback) 설정](set-partition-writeback.md)|파티션을 쓰기가 가능하도록 설정하는 방법을 제공합니다.|  
|[원격 파티션 만들기 및 관리 &#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md)|원격 파티션을 만들고 관리하는 방법에 대해 설명합니다.|  
  
  
