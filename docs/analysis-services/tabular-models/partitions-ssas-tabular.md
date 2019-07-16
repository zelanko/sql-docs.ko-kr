---
title: Analysis Services 테이블 형식 모델의 파티션에 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5d26b1b1558ca546fb47660488b15dc777c5ad87
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162727"
---
# <a name="partitions"></a>파티션
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  파티션은 테이블을 논리적 부분으로 나눕니다. 각 파티션은 다른 파티션과 별개로 처리(새로 고침)할 수 있습니다. 모델 제작 중 SSDT에서 파티션 대화 상자를 사용 하 여 만든 파티션은 모델 작업 영역 데이터베이스에 적용 됩니다. 모델을 배포하면 모델 작업 영역 데이터베이스에 대해 정의된 파티션이 배포된 model 데이터베이스에 복제됩니다. 수 더 만들고 SSMS에서 파티션 대화 상자를 사용 하 여 배포 된 model 데이터베이스에 대 한 파티션을 관리 합니다.  이 항목에서 제공 하는 정보에 SSDT에서 파티션 관리자 대화 상자를 사용 하 여 모델 제작 중에 만들어진 파티션을 설명 합니다. 배포 된 모델에 대 한 파티션을 만들고 관리 하는 방법에 대 한 내용은 [만들기 및 테이블 형식 모델 파티션 관리](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)합니다.  
  
##  <a name="bkmk_benefits"></a> 이점  
 테이블 형식 모델에서 파티션은 테이블을 논리적 파티션 개체로 나눕니다. 각 파티션은 다른 파티션과 별개로 처리할 수 있습니다. 예를 들어 한 테이블에 거의 변경되지 않는 데이터를 포함하는 행 집합과 자주 변경되는 데이터를 포함하는 행 집합이 들어 있을 수 있습니다. 이때 데이터의 일부만 처리하려고 할 경우 데이터를 모두 처리할 필요가 없습니다. 파티션을 사용하면 자주 처리해야 하는 데이터 부분을 자주 처리할 필요 없는 데이터와 분리할 수 있습니다.  
  
 효과적인 모델 디자인은 파티션을 이용하여 불필요한 처리 및 Analysis Services 서버에 대한 후속 프로세서 로드를 배제하는 동시에 데이터 원본의 최신 데이터를 반영하여 데이터를 자주 처리하고 새로 고칠 수 있습니다. 모델 제작 중에 파티션을 구현하고 이용하는 방법은 배포된 모델에 대해 파티션을 구현하고 이용하는 방법과 매우 다를 수 있습니다. 모델 제작 단계 중에는 최종적으로 배포된 모델에 포함될 데이터의 하위 집합에 대해서만 작업할 수 있다는 점에 유의해야 합니다.  
  
### <a name="processing-partitions"></a>파티션 처리  
 배포 된 모델에 대 한 처리 명령을 포함 하 고 처리 옵션 및 설정을 지정 하는 스크립트를 실행 하거나 SSMS를 사용 하 여 발생 합니다. SSDT를 사용 하 여 모델을 제작할 때는 모델 메뉴 또는 도구 모음에서 Process 명령을 사용 하 여 처리 작업을 실행할 수 있습니다. 파티션, 테이블 또는 모두에 대해 Process 작업을 지정할 수 있습니다.  
  
 처리 작업을 실행하면 데이터 연결을 사용하여 데이터 원본에 연결됩니다. 새 데이터를 모델 테이블에 가져오고, 각 테이블에 대해 관계 및 계층이 다시 작성되며, 계산된 열 및 측정값의 계산이 다시 계산됩니다.  
  
 테이블을 논리적 파티션으로 더 나눔으로써 각 파티션의 데이터가 처리되는 부분, 시간 및 방법을 선택적으로 정의할 수 있습니다. 모델을 배포 하는 경우 SSMS에서 파티션 대화 상자를 사용 하 여 수동으로 파티션의 처리를 완료할 수 있습니다 또는 스크립트를 사용 하 여 처리 명령을 실행 하는 합니다.  
  
### <a name="partitions-in-the-model-workspace-database"></a>모델 작업 영역 데이터베이스의 파티션  
 새 파티션을 만들거나 파티션을 편집 하거나 병합 파티션 관리자를 사용 하 여 SSDT에서 파티션을 삭제할 수 있습니다. 제작 하는 모델의 호환성 수준에 따라 파티션 관리자는 테이블, 행 및 파티션에 대 한 열을 선택 하기 위한 두 가지 모드를 제공: 테이블 형식 1400 모델에 대 한 M 쿼리를 사용 하 여 파티션이 정의 되지만 또는 디자인 모드를 사용 하 여 쿼리 편집기를 엽니다. 테이블 형식 1100, 1103, 1200 모델 사용 테이블 미리 보기 모드와 SQL 쿼리 모드입니다. 
  
### <a name="partitions-in-a-deployed-model-database"></a>배포된 model 데이터베이스의 파티션  
 모델을 배포할 때 배포 된 model 데이터베이스에 대 한 파티션을 SSMS에서 데이터베이스 개체로 나타납니다. 만들고, 편집, 병합 하 SSMS에서 파티션 대화 상자를 사용 하 여 배포 된 모델에 대 한 파티션을 삭제 합니다. SSMS에서 배포 된 모델에 대 한 파티션을 관리 하는 것은이 항목의 범위를 벗어납니다. SSMS에서 파티션을 관리 하는 방법에 대 한 자세한 참조 [만들기 및 테이블 형식 모델 파티션 관리](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)합니다.  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|항목|설명|  
|-----------|-----------------|  
|[작업 영역 데이터베이스에서 파티션 만들기 및 관리](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)|만들고 SSDT에서 파티션 관리자를 사용 하 여 모델 작업 영역 데이터베이스에서 파티션을 관리 하는 방법을 설명 합니다.|  
|[작업 영역 데이터베이스에서 파티션 처리](../../analysis-services/tabular-models/process-partitions-in-the-workspace-database-ssas-tabular.md)|모델 작업 영역 데이터베이스에서 파티션을 처리(새로 고침)하는 방법을 설명 합니다.|  
  
## <a name="see-also"></a>참조  
 [DirectQuery 모드](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [데이터 처리](../../analysis-services/tabular-models/process-data-ssas-tabular.md)  
  
  
