---
title: "데이터 처리(SSAS 테이블 형식) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d88f2dc9-2933-4be5-9bf3-48ffbc2d0a1a
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 14
---
# 데이터 처리(SSAS 테이블 형식)
  데이터를 테이블 형식 모델로 가져올 경우 캐시된 모드에서 가져오는 시점에 해당 데이터의 스냅숏을 캡처하게 됩니다. 경우에 따라 이 데이터가 변경되지 않을 수 있으며 모델에서 데이터를 업데이트할 필요는 없습니다. 하지만 가져오는 데이터가 정기적으로 변경될 수 있으므로 모델이 데이터 원본의 최신 데이터를 반영하려면 데이터를 처리(새로 고침)하고 계산된 데이터를 다시 계산해야 합니다. 모델에서 데이터를 업데이트하려면 모든 테이블에 대해, 개별 테이블에 대해, 파티션별로 또는 데이터 원본 연결별로 처리 동작을 수행합니다.  
  
 모델 프로젝트를 제작할 때는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 처리 동작을 수동으로 시작해야 합니다. 모델을 배포한 후 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 처리 작업을 수행하거나 스크립트를 사용하여 처리 작업을 예약할 수 있습니다. 여기서 설명하는 태스크는 모두 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 모델 제작 중에 수행할 수 있는 처리 동작과 관련됩니다. 배포된 모델의 처리 동작에 대한 자세한 내용은 [데이터베이스, 테이블 또는 파티션 처리&#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)를 참조하세요.  
  
## 관련 작업  
  
|항목|Description|  
|-----------|-----------------|  
|[수동으로 데이터 처리&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/manually-process-data-ssas-tabular.md)|모델 작업 영역 데이터를 수동으로 처리하는 방법을 설명합니다.|  
|[데이터 처리 문제 해결&#40;SSAS 테이블 형식&#41;](../../analysis-services/troubleshoot-process-data-ssas-tabular.md)|처리 작업의 문제를 해결하는 방법을 설명합니다.|  
  
  