---
title: 원격 파티션을 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- archiving remote partitions [Analysis Services]
- partitions [Analysis Services], remote
- restoring remote partitions [Analysis Services]
- backing up remote partitions [Analysis Services]
- partitions [Analysis Services], storage
- storing data [Analysis Services], partitions
- MasterDataSourceID property
- remote partitions [Analysis Services]
ms.assetid: 63f5d9f5-c6b6-4ceb-94fe-7b6c396d10bb
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 31629125aacd20b4d8d5ea69b68372abf4f5599b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090268"
---
# <a name="remote-partitions"></a>원격 파티션
  원격 파티션의 데이터는 Microsoft의 다른 인스턴스로에 저장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 파티션과 부모 큐브가 정의 (메타 데이터)를 포함 하는 인스턴스와 합니다. 원격 파티션은 파티션과 해당 부모 큐브가 정의된 것과 동일한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 관리됩니다.  
  
> [!NOTE]  
>  원격 파티션을 저장 하려면 컴퓨터의 인스턴스로 있어야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 설치 하 고 파티션이 정의 된 인스턴스와 동일한 수준의 서비스 팩을 실행 합니다. 이전 버전의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서는 원격 파티션이 지원되지 않습니다.  
  
 측정값 그룹에 원격 파티션이 포함되어 있는 경우 큐브의 메모리 및 CPU 사용률이 측정값 그룹의 모든 파티션에 분산됩니다. 예를 들어 원격 파티션을 단독으로 또는 부모 큐브 처리의 일부로 처리하는 경우 해당 파티션의 메모리와 CPU가 대부분 원격 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 사용됩니다.  
  
> [!NOTE]  
>  원격 파티션을 포함하는 큐브는 쓰기 가능 차원을 포함할 수 있지만 이로 인해 큐브 성능이 저하될 수 있습니다. 쓰기 가능 차원에 대 한 자세한 내용은 참조 [쓰기 가능한 차원](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)합니다.  
  
## <a name="storage-modes-for-remote-partitions"></a>원격 파티션에 대한 저장소 모드  
 원격 파티션에서는 로컬 파티션에 사용되는 MOLAP(다차원 OLAP), HOLAP(하이브리드 OLAP) 또는 ROLAP(관계형 OLAP) 등의 저장소 유형을 모두 사용할 수 있습니다. 원격 파티션에서 자동 관리 캐싱을 사용할 수도 있습니다. 원격 파티션의 저장소 모드에 따라 원격 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 저장되는 데이터가 다음과 같이 달라집니다.  
  
|||  
|-|-|  
|저장소 유형|data|  
|MOLAP|파티션의 집계 및 파티션의 원본 데이터에 대한 복사본|  
|HOLAP|파티션 집계|  
|ROLAP|파티션 데이터가 저장되지 않음|  
  
 측정값 그룹에 여러 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 저장된 MOLAP 또는 HOLAP 파티션이 여러 개 포함되어 있으면 큐브가 측정값 그룹의 데이터를 해당 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 간에 분산합니다.  
  
## <a name="merging-remote-partitions"></a>원격 파티션 병합  
 원격 파티션은 동일한 원격 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 저장된 다른 원격 파티션과만 병합될 수 있습니다. 파티션을 병합 하는 방법에 대 한 자세한 내용은 참조 [Analysis Services의 파티션 병합 &#40;SSAS-다차원 데이터&#41;](../multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)합니다.  
  
## <a name="archiving-and-restoring-remote-partitions"></a>원격 파티션 보관 및 복원  
 원격 파티션을 저장하는 데이터베이스를 보관하거나 복원하는 경우 원격 파티션의 데이터를 보관하거나 복원할 수 있습니다. 원격 파티션을 복원하지 않고 데이터베이스를 복원하는 경우에는 먼저 원격 파티션을 처리해야 파티션에서 데이터를 사용할 수 있습니다. 데이터베이스 보관 및 복원 하는 방법에 대 한 자세한 내용은 참조 [백업 및 복원의 Analysis Services 데이터베이스](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [원격 파티션 만들기 및 관리 &#40;Analysis Services&#41;](../multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)   
 [Analysis Services 개체 처리](../multidimensional-models/processing-analysis-services-objects.md)  
  
  