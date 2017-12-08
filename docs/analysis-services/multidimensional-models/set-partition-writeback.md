---
title: "파티션 쓰기 설정 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], writeback
- partitions [Analysis Services], write-enabled
- writeback [Analysis Services], partitions
ms.assetid: 38bb09cc-2652-4971-8373-0cf468cdc7a6
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3f1f8ef13a4b05c5f5be5553b601e019b68aa100
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="set-partition-writeback"></a>파티션 쓰기 저장 설정
  측정값을 쓰기 가능하게 설정하면 최종 사용자가 큐브 데이터를 검색하는 동안 변경할 수 있으며, 변경 내용은 큐브 데이터 또는 원본 데이터가 아닌 쓰기 저장 테이블이라는 별도의 테이블에 저장됩니다. 쓰기 가능한 파티션을 검색하는 최종 사용자에게 해당 파티션에 대한 쓰기 저장 테이블의 모든 변경 내용에 대한 최종 결과가 표시됩니다.  
  
 쓰기 저장 데이터를 찾아보거나 삭제할 수 있으며 쓰기 저장 데이터를 파티션으로 변환할 수도 있습니다. 쓰기 가능한 파티션의 경우 큐브 역할을 사용하여 사용자 및 사용자 그룹에 읽기/쓰기 권한을 부여하고 파티션의 특정 셀 또는 셀 그룹에 대한 액세스를 제한할 수 있습니다.  
  
 쓰기 저장에 대한 간략한 비디오 지침은 [Analysis Services에 대한 Excel 2010 쓰기 저장](http://go.microsoft.com/fwlink/p/?LinkId=394951)을 참조하십시오. 이 기능에 대한 자세한 내용은 블로그 포스트 시리즈인 [Building a Writeback Application with Analysis Services (blog)](http://go.microsoft.com/fwlink/?LinkId=394977)(Analysis Services를 사용하여 쓰기 저장 응용 프로그램 빌드(블로그))를 참조하세요.  
  
> [!NOTE]  
>  쓰기 저장은 SQL Server 관계형 데이터베이스 및 데이터 마트, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 다차원 모델에 대해서만 지원됩니다.  
  
## <a name="how-to-write-enable-a-partition"></a>파티션을 쓰기 가능으로 설정하는 방법  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 큐브 디자이너에서 파티션 자체를 쓰기 가능으로 설정하여 파티션의 측정값 그룹을 쓰기 가능하게 할 수 있습니다.  
  
-   큐브 디자이너의 파티션 탭에서 파티션을 마우스 오른쪽 단추로 클릭하고 **쓰기 저장 설정**을 선택합니다.  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 데이터베이스 |큐브| 측정값 그룹을 확장한 다음 **쓰기 저장** 을 마우스 오른쪽 단추로 클릭하고 **쓰기 저장 사용**을 선택합니다.  
  
 쓰기 저장은 SUM 집계를 사용하는 측정값에서만 지원됩니다. AdventureWorks 샘플 데이터베이스에서 Sales Targets 측정값 그룹을 사용하여 쓰기 저장 동작을 테스트할 수 있습니다.  
  
 파티션을 쓰기 가능으로 설정할 때는 쓰기 저장 테이블 저장을 위한 테이블 이름 및 데이터 원본을 지정해야 합니다. 측정값 그룹에 대한 모든 후속 변경 내용은 이 테이블에 기록됩니다.  
  
## <a name="browse-writeback-data-in-a-partition"></a>파티션에서 쓰기 저장 데이터 찾아보기  
 큐브 디자이너의 **파티션** 탭에 있는 쓰기 가능한 파티션을 마우스 오른쪽 단추로 클릭하여 액세스할 수 있는 **데이터 찾아보기** 대화 상자에서 큐브의 쓰기 저장 테이블의 내용을 찾아볼 수 있습니다.  
  
## <a name="delete-writeback-data-or-disable-writeback"></a>쓰기 저장 데이터 삭제 또는 쓰기 저장 사용 안 함  
 쓰기 저장 데이터를 삭제하면 쓰기 저장 캐시가 지워지며 해당 데이터를 삭제한 직후부터 추가 쓰기 저장 작업은 백지 상태에서 수행됩니다. 큐브 파티션에 대해 쓰기 저장을 해제하면 해당 파티션에 대한 쓰기 저장이 해제됩니다.  
  
## <a name="convert-writeback-data-to-a-partition"></a>쓰기 저장 데이터를 파티션으로 변환  
 파티션의 쓰기 저장 테이블에 포함된 데이터를 파티션으로 변환할 수 있습니다. 이 절차로 인해 쓰기 저장 테이블이 새 파티션의 팩트 테이블이 됩니다.  
  
> [!CAUTION]  
>  파티션을 잘못 사용하면 정확하지 않은 큐브 데이터가 만들어질 수 있습니다. 자세한 내용은 [로컬 파티션 만들기 및 관리&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)를 참조하세요.  
  
 쓰기 저장 데이터 테이블을 파티션으로 변환하면 파티션이 쓰기 불가능으로 설정됩니다. 파티션의 셀에 대한 모든 제한 없는 읽기/쓰기 정책 및 읽기/쓰기 권한이 해제되며 최종 사용자는 표시된 큐브 데이터를 변경할 수 없게 됩니다. 제한 없는 읽기/쓰기 정책 또는 읽기/쓰기 권한이 해제된 최종 사용자도 큐브를 찾아볼 수는 있습니다. 읽기 권한 및 불확정 읽기 권한은 영향을 받지 않습니다.  
  
 쓰기 저장 데이터를 파티션으로 변환하려면 **파티션으로 변환** 대화 상자를 사용합니다. 이 대화 상자는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 쓰기 가능 파티션에 대한 쓰기 저장 테이블을 마우스 오른쪽 단추로 클릭하여 액세스할 수 있습니다. 대화 상자에서 파티션의 이름을 지정하고 파티션에 대한 집계를 파티션을 만들 때 디자인할지, 아니면 나중에 디자인할지를 지정합니다. 파티션을 선택할 때 집계를 만들려면 기존 파티션에서 집계 디자인을 복사하도록 선택해야 합니다. 기존 파티션은 반드시 그런 것은 아니지만 일반적으로 현재 쓰기 저장 파티션입니다. 파티션을 만들 때 해당 파티션을 처리하도록 선택할 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [쓰기 가능 파티션](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [Excel 2010의 셀 수준에서 OLAP 큐브 쓰기 저장을 사용 하도록 설정](http://go.microsoft.com/fwlink/p/?LinkId=394952)   
 [사용 및 Analysis Services 쓰기 저장 된 데이터 항목 보안 설정](http://go.microsoft.com/fwlink/p/?LinkId=394953)  
  
  
