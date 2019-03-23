---
title: 파티션 처리 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partitionprocessingdest.f1
helpviewer_keywords:
- partitions [Analysis Services], processing
- Partition Processing destination [Integration Services]
- destinations [Integration Services], Partition Processing
ms.assetid: 36c592ff-3f78-4a58-b496-31c1c8eee131
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2d36d354aee299efdeefc38d6000c16f1d0fc6b9
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375031"
---
# <a name="partition-processing-destination"></a>파티션 처리 대상
  파티션 처리 대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 파티션을 로드하고 처리합니다. 파티션에 대한 자세한 내용은 [파티션&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)을 참조하세요.  
  
 파티션 처리 대상에는 다음 기능이 포함됩니다.  
  
-   증분, 전체 또는 업데이트 처리를 수행하기 위한 옵션  
  
-   처리 중에 오류를 무시하거나 지정된 오류 개수 이후에 프로세스가 중지되는지 여부를 지정하기 위한 오류 구성  
  
-   입력 열을 파티션 열에 매핑  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 처리하는 방법에 대한 자세한 내용은 [처리 옵션 및 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
> [!NOTE]  
>  여기에서 설명하는 태스크는 Analysis Services 테이블 형식 모델에 적용되지 않습니다.  테이블 형식 모델의 경우 입력 열을 파티션 열에 매핑할 수 없습니다. 대신 [Analysis Services Execute DDL Task](../control-flow/analysis-services-execute-ddl-task.md) 를 사용하여 파티션을 처리할 수 있습니다.  
  
## <a name="configuration-of-the-partition-processing-destination"></a>파티션 처리 대상 구성  
 파티션 처리 대상은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 연결하거나 대상에서 처리되는 큐브 및 파티션이 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결합니다. 자세한 내용은 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md)을(를) 참조하세요.  
  
 이 대상은 하나의 입력을 갖습니다. 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **파티션 처리 대상 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [파티션 처리 대상 편집기&#40;연결 관리자 페이지&#41;](../partition-processing-destination-editor-connection-manager-page.md)  
  
-   [파티션 처리 대상 편집기&#40;매핑 페이지&#41;](../partition-processing-destination-editor-mappings-page.md)  
  
-   [파티션 처리 대상 편집기&#40;고급 페이지&#41;](../partition-processing-destination-editor-advanced-page.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../common-properties.md)  
  
-   [파티션 처리 대상 사용자 지정 속성](partition-processing-destination-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
  
