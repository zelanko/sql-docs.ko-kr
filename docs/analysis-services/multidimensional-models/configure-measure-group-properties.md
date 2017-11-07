---
title: "측정값 그룹 속성 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
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
- properties [Analysis Services], measure groups
ms.assetid: fa66bdb6-60b8-413c-ac2a-00e4d09f60a2
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 16613e83f5632864fd86ff46067a72ed9dc88539
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="configure-measure-group-properties"></a>측정값 그룹 속성 구성
  측정값 그룹에는 측정값 그룹의 작동 방법을 정의할 수 있는 속성이 있습니다.  
  
## <a name="measure-group-properties"></a>측정값 그룹 속성  
 측정값 그룹 속성은 전체 측정값 그룹의 동작을 결정하고 측정값 그룹에 있는 측정값의 특정 속성에 대한 기본 동작을 설정합니다.  
  
|속성|정의|  
|--------------|----------------|  
|**AggregationPrefix**|ROLAP 저장소에 적용됩니다. SQL Server에서 이 측정값 그룹과 연관된 파티션에 대한 집계를 저장하는 데 사용되는 인덱싱된 뷰에 공통 접두사를 할당합니다.|  
|**DataAggregation**|이 속성은 나중에 사용하도록 예약되어 있으며 현재 영향을 주지 않습니다. 따라서 이 설정을 수정하지 않는 것이 좋습니다.|  
|**Description**|이 속성을 사용하여 측정값 그룹을 문서화할 수 있습니다.|  
|**ErrorConfiguration**|중복 키, 알 수 없는 키, Null 키, 오류 제한, 오류 감지 시 수행 동작 및 오류 로그 파일을 처리할 때 구성 가능한 오류 처리 설정을 제공합니다. [큐브, 파티션 및 차원 처리에 대한 오류 구성&#40;SSAS - 다차원&#41;](../../analysis-services/multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)을 참조하세요.|  
|**EstimatedRows**|팩트 테이블의 예상 행 수를 지정합니다.|  
|**EstimatedSize**|측정값 그룹의 예상 크기(바이트)를 지정합니다.|  
|**ID**|개체의 식별자를 지정합니다.|  
|**IgnoreUnrelatedDimensions**|측정값 그룹과 관련이 없는 차원의 멤버가 쿼리에 포함될 때 관련이 없는 차원이 최상위로 강제되는지 결정합니다. 기본 설정은 **True**입니다.|  
|**이름**|측정값의 이름입니다. 이 속성은 읽기 전용입니다.|  
|**ProactiveCaching**|중복 키, 알 수 없는 키, Null 키, 오류 제한, 오류 감지 시 수행 동작 및 오류 로그 파일을 처리할 때 구성 가능한 오류 처리 설정을 제공합니다.|  
|**ProcessingMode**|인덱싱 및 집계를 처리 중에 수행할지 아니면 처리 후에 수행할지를 나타냅니다. 사용할 수 있는 옵션은 Regular와 LazyAggregations입니다. LazyAggregations를 사용하여 집계를 백그라운드 작업으로 실행할 수 있습니다.|  
|**ProcessingPriority**|지연 집계 및 지연 인덱싱과 같이 백그라운드 작업 중의 큐브 처리 우선 순위를 결정합니다. 기본값은 **0**입니다.|  
|**StorageLocation**|측정값 그룹의 파일 시스템 저장소 위치입니다. 지정하지 않으면 측정값 그룹을 포함하는 큐브에서 위치가 상속됩니다.|  
|**StorageMode**|측정값 그룹에 대한 저장소 모드입니다. 사용 가능한 값은 MOLAP, ROLAP 또는 HOLAP입니다.|  
|**형식**|측정값 그룹의 유형을 지정합니다.|  
  
  

