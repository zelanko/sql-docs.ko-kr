---
title: 차원 저장소 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], storage
- storing data [Analysis Services]
- storage [Analysis Services], dimensions
- relational OLAP
- multidimensional OLAP
- MOLAP
- storing data [Analysis Services], dimensions
- ROLAP
ms.assetid: 8d74b932-2174-4e1f-8414-636455880b6a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c452376162c901ce85158d3563526493d6d4934a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218873"
---
# <a name="dimension-storage"></a>차원 스토리지
  차원을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 두 저장소 모드를 지원 합니다.  
  
-   ROLAP(관계형 OLAP)  
  
-   MOLAP(다차원 OLAP)  
  
 저장소 모드에 따라 차원 데이터의 위치와 형식이 결정됩니다. MOLAP은 차원의 기본 저장소 모드입니다. **관련 항목:**[파티션 저장소 모드 및 처리](../multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
## <a name="molap"></a>MOLAP  
 MOLAP을 사용하는 차원의 데이터는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 다차원 구조에 저장됩니다. 이 다차원 구조는 차원이 처리될 때 생성되고 채워집니다. MOLAP 차원은 ROLAP 차원보다 우수한 쿼리 성능을 제공합니다.  
  
## <a name="rolap"></a>ROLAP  
 ROLAP을 사용하는 차원의 데이터는 실제로 차원 정의에 사용되는 테이블에 저장됩니다. ROLAP 저장소 모드를 사용하면 대량의 데이터를 복제하지 않고도 대규모 차원을 지원할 수 있는 대신 쿼리 성능이 저하됩니다. 차원은 해당 차원을 정의하는 데 사용한 데이터 원본 뷰의 테이블을 직접 사용하기 때문에 ROLAP 저장소 모드에서 실시간 OLAP도 지원합니다.  
  
> [!IMPORTANT]  
>  차원이 ROLAP 저장소 모드를 사용하며 MOLAP 저장소를 사용하는 큐브에 차원이 포함되어 있는 경우 해당 원본 테이블에 대한 스키마가 변경될 때마다 큐브를 바로 처리해야 합니다. 그렇지 않으면 큐브를 쿼리할 때 결과에 일관성이 없을 수 있습니다. **관련된 항목:**[자동화 Analysis Services Administrative Tasks with SSIS](../instances/automate-analysis-services-administrative-tasks-with-ssis.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [파티션 저장소 모드 및 처리](../multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
  
