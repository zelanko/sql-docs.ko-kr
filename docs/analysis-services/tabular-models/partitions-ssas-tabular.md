---
title: "파티션 (SSAS 테이블 형식) | Microsoft Docs"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 708b9bdf-8c0b-4476-809a-8f616be23a58
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 729c24cf80e99f6f0e2596c51bfbc8bdf2490d0d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="partitions"></a>파티션
  파티션은 테이블을 논리적 부분으로 나눕니다. 각 파티션은 다른 파티션과 별개로 처리(새로 고침)할 수 있습니다. 모델 제작 중에 SSDT에서 파티션 대화 상자를 사용 하 여 만든 파티션은 모델 작업 영역 데이터베이스에 적용 됩니다. 모델을 배포하면 모델 작업 영역 데이터베이스에 대해 정의된 파티션이 배포된 model 데이터베이스에 복제됩니다. 있습니다 수 추가로 만들고 SSMS에서 파티션 대화 상자를 사용 하 여 배포 된 모델 데이터베이스에 대 한 파티션을 관리 합니다.  이 항목에서 제공 하는 정보는 SSDT에서 파티션 관리자 대화 상자를 사용 하 여 모델 제작 중에 만든 파티션을 설명 합니다. 배포 된 모델에 대 한 파티션을 만들고 관리 하는 방법에 대 한 내용은 [만들기 및 테이블 형식 모델 파티션 관리](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)합니다.  
  
##  <a name="bkmk_benefits"></a> 이점  
 테이블 형식 모델에서 파티션은 테이블을 논리적 파티션 개체로 나눕니다. 각 파티션은 다른 파티션과 별개로 처리할 수 있습니다. 예를 들어 한 테이블에 거의 변경되지 않는 데이터를 포함하는 행 집합과 자주 변경되는 데이터를 포함하는 행 집합이 들어 있을 수 있습니다. 이때 데이터의 일부만 처리하려고 할 경우 데이터를 모두 처리할 필요가 없습니다. 파티션을 사용하면 자주 처리해야 하는 데이터 부분을 자주 처리할 필요 없는 데이터와 분리할 수 있습니다.  
  
 효과적인 모델 디자인은 파티션을 이용하여 불필요한 처리 및 Analysis Services 서버에 대한 후속 프로세서 로드를 배제하는 동시에 데이터 원본의 최신 데이터를 반영하여 데이터를 자주 처리하고 새로 고칠 수 있습니다. 모델 제작 중에 파티션을 구현하고 이용하는 방법은 배포된 모델에 대해 파티션을 구현하고 이용하는 방법과 매우 다를 수 있습니다. 모델 제작 단계 중에는 최종적으로 배포된 모델에 포함될 데이터의 하위 집합에 대해서만 작업할 수 있다는 점에 유의해야 합니다.  
  
### <a name="processing-partitions"></a>파티션 처리  
 배포 된 모델에 대 한 처리 명령을 포함 하 고 처리 옵션 및 설정을 지정 하는 스크립트를 실행 하 여 또는 SSMS를 사용 하 여 발생 합니다. SSDT를 사용 하 여 모델을 제작할 때는 모델 메뉴 또는 도구 모음에서 Process 명령을 사용 하 여 처리 작업을 실행할 수 있습니다. 파티션, 테이블 또는 모두에 대해 Process 작업을 지정할 수 있습니다.  
  
 처리 작업을 실행하면 데이터 연결을 사용하여 데이터 원본에 연결됩니다. 새 데이터를 모델 테이블에 가져오고, 각 테이블에 대해 관계 및 계층이 다시 작성되며, 계산된 열 및 측정값의 계산이 다시 계산됩니다.  
  
 테이블을 논리적 파티션으로 더 나눔으로써 각 파티션의 데이터가 처리되는 부분, 시간 및 방법을 선택적으로 정의할 수 있습니다. 모델을 배포할 때 SSMS에서 파티션 대화 상자를 사용 하 여 수동으로 파티션의 처리를 완료할 수 있습니다 또는 처리 명령을 실행 하는 스크립트를 사용 하 여 합니다.  
  
### <a name="partitions-in-the-model-workspace-database"></a>모델 작업 영역 데이터베이스의 파티션  
 새 파티션을 만들거나 파티션을 편집 하거나 병합, SSDT에서 파티션 관리자를 사용 하 여 파티션을 삭제할 수 있습니다. 파티션 관리자 테이블, 행 및 파티션에 대 한 열을 선택 하기 위한 두 가지 모드 제공 제작 하는 모델의 호환성 수준에 따라: M 쿼리를 사용 하 여 테이블 형식 1400 모델에 파티션이 정의 되지만 또는 디자인 모드를 사용 하 여를 열려면 쿼리 편집기입니다. 테이블 형식 1100, 1103, 1200 모델에서는 사용 테이블 미리 보기 모드 및 SQL 쿼리 모드입니다. 
  
### <a name="partitions-in-a-deployed-model-database"></a>배포된 model 데이터베이스의 파티션  
 모델을 배포할 때 배포 된 모델 데이터베이스에 대 한 파티션을 SSMS에서 데이터베이스 개체로 나타납니다. 만들 편집 및 병합 하 고, SSMS에서 파티션 대화 상자를 사용 하 여 배포 된 모델에 대 한 파티션을 삭제할 수 있습니다. SSMS에서 배포 된 모델에 대 한 파티션 관리이 항목의 범위를 벗어납니다. SSMS에서 파티션을 관리 하는 방법에 대 한 자세한 내용은 [만들기 및 테이블 형식 모델 파티션 관리](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)합니다.  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|항목|Description|  
|-----------|-----------------|  
|[작업 영역 데이터베이스에서 파티션 만들기 및 관리](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)|만들고 SSDT에서 파티션 관리자를 사용 하 여 모델 작업 영역 데이터베이스에서 파티션을 관리 하는 방법을 설명 합니다.|  
|[작업 영역 데이터베이스에서 파티션 처리](../../analysis-services/tabular-models/process-partitions-in-the-workspace-databse-ssas-tabular.md)|모델 작업 영역 데이터베이스에서 파티션을 처리(새로 고침)하는 방법을 설명 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [DirectQuery 모드](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [데이터 처리](../../analysis-services/tabular-models/process-data-ssas-tabular.md)  
  
  

