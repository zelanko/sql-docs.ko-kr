---
title: 파티션 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 708b9bdf-8c0b-4476-809a-8f616be23a58
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d0797d22b66a40c0cf13fcd9c394d0072827b8e9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37239703"
---
# <a name="partitions-ssas-tabular"></a>파티션(SSAS 테이블 형식)
  파티션은 테이블을 논리적 부분으로 나눕니다. 각 파티션은 다른 파티션과 별개로 처리(새로 고침)할 수 있습니다. 모델 제작 중 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 파티션 대화 상자를 사용하여 만든 파티션은 모델 작업 영역 데이터베이스에 적용됩니다. 모델을 배포하면 모델 작업 영역 데이터베이스에 대해 정의된 파티션이 배포된 model 데이터베이스에 복제됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 파티션 대화 상자를 사용하여 배포된 model 데이터베이스에 대해 파티션을 추가로 만들고 관리할 수 있습니다.  이 항목에서는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 파티션 관리자 대화 상자를 사용하여 모델 제작 중에 만든 파티션을 설명합니다. 배포된 모델의 파티션을 만들고 관리하는 방법에 대한 자세한 내용은 [테이블 형식 모델 파티션 만들기 및 관리&#40;SSAS 테이블 형식&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md)를 참조하세요.  
  
 이 항목의 섹션:  
  
-   [이점](#bkmk_benefits)  
  
-   [관련 작업](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> 이점  
 테이블 형식 모델에서 파티션은 테이블을 논리적 파티션 개체로 나눕니다. 각 파티션은 다른 파티션과 별개로 처리할 수 있습니다. 예를 들어 한 테이블에 거의 변경되지 않는 데이터를 포함하는 행 집합과 자주 변경되는 데이터를 포함하는 행 집합이 들어 있을 수 있습니다. 이때 데이터의 일부만 처리하려고 할 경우 데이터를 모두 처리할 필요가 없습니다. 파티션을 사용하면 자주 처리해야 하는 데이터 부분을 자주 처리할 필요 없는 데이터와 분리할 수 있습니다.  
  
 효과적인 모델 디자인은 파티션을 이용하여 불필요한 처리 및 Analysis Services 서버에 대한 후속 프로세서 로드를 배제하는 동시에 데이터 원본의 최신 데이터를 반영하여 데이터를 자주 처리하고 새로 고칠 수 있습니다. 모델 제작 중에 파티션을 구현하고 이용하는 방법은 배포된 모델에 대해 파티션을 구현하고 이용하는 방법과 매우 다를 수 있습니다. 모델 제작 단계 중에는 최종적으로 배포된 모델에 포함될 데이터의 하위 집합에 대해서만 작업할 수 있다는 점에 유의해야 합니다.  
  
### <a name="processing-partitions"></a>파티션 처리  
 배포된 모델의 경우 처리는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하거나, 처리 명령을 포함하고 처리 옵션 및 설정을 지정하는 스크립트를 실행하여 수행됩니다. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]를 사용하여 모델을 제작할 때는 모델 메뉴 또는 도구 모음에서 Process 명령을 사용하여 처리 작업을 실행할 수 있습니다. 파티션, 테이블 또는 모두에 대해 Process 작업을 지정할 수 있습니다.  
  
 처리 작업을 실행하면 데이터 연결을 사용하여 데이터 원본에 연결됩니다. 새 데이터를 모델 테이블에 가져오고, 각 테이블에 대해 관계 및 계층이 다시 작성되며, 계산된 열 및 측정값의 계산이 다시 계산됩니다.  
  
 테이블을 논리적 파티션으로 더 나눔으로써 각 파티션의 데이터가 처리되는 부분, 시간 및 방법을 선택적으로 정의할 수 있습니다. 모델을 배포할 때 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 파티션 대화 상자를 사용하거나 처리 명령을 실행하는 스크립트를 사용하여 파티션의 처리를 수동으로 완료할 수 있습니다.  
  
### <a name="partitions-in-the-model-workspace-database"></a>모델 작업 영역 데이터베이스의 파티션  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 파티션 관리자를 사용하여 새 파티션을 만들거나 파티션을 편집, 병합 또는 삭제할 수 있습니다. 파티션 관리자는 파티션에 대해 테이블, 행 및 열을 선택하는 두 가지 모드, 즉 테이블 미리 보기 모드 및 SQL 쿼리 모드를 제공합니다. SQL 쿼리를 사용하여 모든 파티션이 정의되지만, 테이블 미리 보기 모드를 사용하여 파티션에 포함할 데이터를 미리 보고 선택할 수 있습니다. SQL 쿼리가 자동으로 만들어지고 유효성이 검사됩니다. 테이블 미리 보기 모드는 테이블 속성 편집 대화 상자 및 테이블 가져오기 마법사의 테이블 미리 보기 페이지에 있는 것과 동일한 테이블 미리 보기이므로 미리 보기의 최대 행 수는 50입니다.  
  
### <a name="partitions-in-a-deployed-model-database"></a>배포된 model 데이터베이스의 파티션  
 모델을 배포하면 배포된 model 데이터베이스에 대한 파티션은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 데이터베이스 개체로 나타납니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 파티션 대화 상자를 사용하여 배포된 모델에 대해 파티션을 만들고 편집, 병합 및 삭제할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 배포된 모델에 대한 파티션 관리는 이 항목에서 다루지 않습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 파티션을 관리하는 방법에 대한 자세한 내용은 [테이블 형식 모델 파티션 만들기 및 관리&#40;SSAS 테이블 형식&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md)를 참조하세요.  
  
##  <a name="bkmk_related_tasks"></a> 관련 태스크  
  
|항목|Description|  
|-----------|-----------------|  
|[작업 영역 데이터베이스에서 파티션 만들기 및 관리 &#40;&AMP;#40;SSAS 테이블 형식&#41;](workspace-database-ssas-tabular.md)|[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 파티션 관리자를 사용하여 모델 작업 영역 데이터베이스에서 파티션을 만들고 관리하는 방법에 대해 설명합니다.|  
|[작업 영역 데이터베이스에서 파티션 처리 &#40;&AMP;#40;SSAS 테이블 형식&#41;](process-partitions-in-the-workspace-databse-ssas-tabular.md)|모델 작업 영역 데이터베이스에서 파티션을 처리(새로 고침)하는 방법을 설명 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [DirectQuery 모드&#40;SSAS 테이블 형식&#41;](directquery-mode-ssas-tabular.md)   
 [데이터 처리 &#40;&AMP;#40;SSAS 테이블 형식&#41;](../process-data-ssas-tabular.md)  
  
  
