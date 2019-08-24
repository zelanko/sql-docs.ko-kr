---
title: 자동 관리 캐싱 (파티션) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- hybrid OLAP
- partitions [Analysis Services], proactive caching
- relational OLAP
- multidimensional OLAP
- MOLAP
- proactive caching [Analysis Services]
- ROLAP
- cache [Analysis Services]
ms.assetid: 422660b2-4d80-4165-b1c9-3963bcde556b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2c968cb8c75fc5f1fb8e77cc98d8c6a306a62115
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727277"
---
# <a name="proactive-caching-partitions"></a>자동 관리 캐싱(파티션)
  자동 관리 캐싱은 OLAP 개체에 자동 MOLAP 캐시 생성 및 관리 기능을 제공합니다. 큐브는 데이터베이스로부터 알림을 수신하는 즉시 데이터베이스에 있는 데이터의 변경 내용을 통합합니다. 자동 관리 캐싱의 목표는 ROLAP에서 제공하는 즉시성과 관리 용이성을 유지하면서 기존 MOLAP의 성능을 제공하는 것입니다.  
  
 단순 <xref:Microsoft.AnalysisServices.ProactiveCaching> 개체는 타이밍 사양과 테이블 알림으로 구성되어 있습니다. 타이밍 사양은 변경 알림을 수신한 후 캐시를 업데이트하는 시간을 정의합니다. 테이블 알림은 데이터 테이블과 <xref:Microsoft.AnalysisServices.ProactiveCaching> 개체 간의 알림 스키마를 정의합니다.  
  
 MOLAP(다차원 OLAP) 스토리지는 최상의 쿼리 응답을 제공하지만 약간의 데이터 대기 시간이 있다는 단점이 있습니다. ROLAP(실시간 관계형 OLAP) 스토리지를 사용하면 사용자가 데이터 원본의 최근 변경 내용을 직접 찾아볼 수 있지만 미리 계산된 데이터 요약이 없고 OLAP 스타일의 쿼리에 맞게 관계형 스토리지가 최적화되지 않았기 때문에 MOLAP보다 성능이 현저히 떨어지는 단점이 있습니다. MOLAP 스토리지의 성능상 이점을 활용하면서 애플리케이션에서 사용자가 최근 데이터를 확인할 수 있게 하려는 경우에는 특히 파티션과 함께 SQL Server Analysis Services의 자동 관리 캐싱 옵션을 사용하는 것이 좋습니다. 자동 관리 캐싱은 파티션과 차원 단위로 설정됩니다. 자동 관리 캐싱 옵션을 사용하면 MOLAP 스토리지의 뛰어난 성능과 ROLAP 스토리지의 즉시성을 균형 있게 조정할 수 있으며 기본 데이터 변경 시 또는 일정 설정에 따라 자동 파티션 처리가 가능합니다.  
  
## <a name="proactive-caching-configuration-options"></a>자동 관리 캐싱 구성 옵션  
 SQL Server Analysis Services에서 제공하는 여러 자동 관리 캐싱 구성 옵션을 사용하여 성능을 최대화하고 대기 시간을 최소화하며 처리를 예약할 수 있습니다. 자동 관리 캐싱 기능은 데이터 진부화(Data Obsolescence)를 관리하는 작업을 단순화합니다. 자동 관리 캐싱 설정에 따라 MOLAP 캐시라고도 하는 다차원 OLAP 구조를 다시 작성하는 빈도, 캐시를 다시 작성하는 동안 오래된 MOLAP 스토리지를 쿼리할지 또는 기본 ROLAP 데이터 원본을 쿼리할지 여부 및 데이터베이스의 변경 내용이나 일정에 따라 캐시를 다시 작성할지 여부가 결정됩니다.  
  
### <a name="minimizing-latency"></a>대기 시간 최소화  
 대기 시간을 최소화하도록 자동 관리 캐싱을 설정하면 데이터의 최근 변경 여부 및 자동 관리 캐싱의 구성 방법에 따라 ROLAP 스토리지나 MOLAP 스토리지에 대해 OLAP 개체에 대한 쿼리가 생성됩니다. 쿼리 엔진은 데이터 원본이 변경되기 전까지 MOLAP 스토리지의 원본 데이터로 쿼리를 전달합니다. 대기 시간을 최소화하기 위해 데이터 원본이 변경되면 캐시된 MOLAP 개체를 삭제할 수 있으며 캐시에서 MOLAP 개체가 다시 작성되는 동안 쿼리를 ROLAP 스토리지로 전달할 수 있습니다. MOLAP 개체가 다시 작성되고 처리되면 쿼리는 자동으로 MOLAP 스토리지로 전달됩니다. 현재 날짜만큼 작을 수 있는 현재 파티션과 같은 작은 파티션의 경우 캐시 새로 고침이 매우 빠르게 수행될 수 있습니다.  
  
### <a name="maximizing-performance"></a>성능 최대화  
 대기 시간을 줄이는 동시에 성능을 최대화하기 위해 현재 사용 중인 MOLAP 개체를 삭제하지 않고 캐싱을 사용할 수도 있습니다. 그러면 새 캐시로 데이터가 읽히고 처리되는 동안 쿼리는 계속 MOLAP 개체에 대해 수행됩니다. 이 방법을 사용하면 성능은 향상되지만 새 캐시를 다시 작성하는 동안 쿼리에서 오래된 데이터를 반환할 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [차원 저장소](../multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [파티션 저장소 설정&#40;Analysis Services - 다차원&#41;](../multidimensional-models/set-partition-storage-analysis-services-multidimensional.md)  
  
  
