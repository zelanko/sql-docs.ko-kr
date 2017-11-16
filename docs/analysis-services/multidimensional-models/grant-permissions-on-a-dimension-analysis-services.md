---
title: "차원 (Analysis Services)에 대 한 권한을 부여 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
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
f1_keywords:
- sql13.asvs.roledesignerdialog.dimensions.f1
helpviewer_keywords:
- dimensions [Analysis Services], security
- read/write permissions
- user access rights [Analysis Services], dimensions
- permissions [Analysis Services], dimensions
ms.assetid: be5b2746-0336-4b12-827e-131462bdf605
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 72ea5d3842b0fbf2f568606004b2de7a7e66825f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="grant-permissions-on-a-dimension-analysis-services"></a>차원에 대한 권한 부여(Analysis Services)
  차원 보안은 데이터가 아닌 차원 개체에 대한 권한을 설정하는 데 사용됩니다. 일반적으로, 차원에 대한 권한을 설정할 때 기본 목표는 처리 작업에 대한 액세스를 허용하거나 거부하는 것입니다.  
  
 그러나 실제 목표가 처리 작업을 제어하는 것이 아니라, 차원이나 차원이 포함하는 특성 또는 계층에 대한 데이터 액세스를 제어하는 것일 수 있습니다. 예를 들어 지방의 영업부를 둔 회사에서 영업부 외부 사람에게는 영업 성과 정보를 공개하지 않을 수 있습니다. 여러 구성 요소의 데이터 차원 일부에 대한 액세스를 허용하거나 거부하기 위해 차원 특성 및 차원 구성원에 대한 권한을 설정할 수 있습니다. 여기서 개별 차원 자체에 대한 액세스는 거부할 수 없으며 데이터에 대한 액세스만 거부할 수 있습니다. 우선적인 목표가 개별 특성 계층에 대한 액세스 권한을 비롯하여 차원 구성원에 대한 액세스 허용 또는 거부하는 것이라면 [차원 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) 에서 자세한 내용을 확인하세요.  
  
 이 항목의 나머지 부분에서는 다음을 비롯하여 차원 개체 자체에 대해 설정할 수 있는 권한을 다룹니다.  
  
-   읽기 또는 읽기/쓰기 권한(읽기 또는 읽기/쓰기 중에서만 선택 가능하며, "없음"은 옵션이 아님). 언급한 대로 차원 데이터에 대한 액세스를 제한하려면 [차원 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) 에서 자세한 내용을 참조하세요.  
  
-   처리 권한(개별 개체에 대한 사용자 지정 권한을 요구하는 처리 전략이 필요한 경우 이 권한 지정).  
  
-   정의 읽기 권한(일반적으로 특정 도구의 대화형 처리를 지원하기 위해 또는 모델로 시각화하기 위해 이 권한 지정, 정의 읽기를 통해 데이터에 대한 권한이나 정의를 수정하는 기능 없이도 차원의 구조를 볼 수 있음).  
  
 차원에 대한 역할을 정의할 때 사용 가능한 권한은 개체가 독립적인 데이터베이스 차원(데이터베이스의 내부이지만 큐브의 외부에 있음)인지 아니면 큐브인지 여부에 따라 다릅니다.  
  
> [!NOTE]  
>  기본적으로, 데이터베이스 차원에 대한 권한은 큐브 차원을 통해 상속됩니다. 예를 들어 고객 데이터베이스 차원에 대해 **읽기/쓰기** 를 사용하도록 설정하는 경우 고객 큐브 차원은 현재 컨텍스트에서 **읽기/쓰기** 를 상속합니다. 사용 권한 설정을 재정의하려는 경우 상속된 권한을 제거할 수 있습니다.  
  
## <a name="set-permissions-on-a-database-dimension"></a>데이터베이스 차원에 대한 권한 설정  
 데이터베이스 차원은 데이터베이스 내의 독립적인 개체로, 동일한 모델 내에서 차원 재사용이 가능합니다. 모델에서 여러 번 사용되는 DATE 데이터베이스 차원의 예로 주문일, 운송일 및 기한 큐브 차원을 생각해 볼 수 있습니다. 큐브 및 데이터베이스 차원은 데이터베이스의 피어 개체이므로, 각 개체에 대해 독립적으로 처리 권한을 설정할 수 있습니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하고 개체 탐색기에서 해당 데이터베이스에 대한 **역할** 을 확장한 다음 데이터베이스 역할을 클릭하거나 새 데이터베이스 역할을 만듭니다.  
  
2.  **차원** 창에서 차원 집합은 **모든 데이터베이스 차원**으로 설정해야 합니다.  
  
     기본적으로 권한은 **읽기**로 설정됩니다.  
  
     **읽기/쓰기** 가 사용 가능하지만 이 권한을 사용하지 않는 것이 좋습니다. **읽기/쓰기** 는 더 이상 사용되지 않는 차원 쓰기 저장 시나리오에 사용됩니다. [SQL Server 2016에서 사용되지 않는 Analysis Services 기능](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md)을 참조하세요.  
  
     선택적으로, **정의 읽기** 및 **처리** 권한이 아직 데이터베이스 수준으로 설정되지 않은 경우 개별 차원 개체에 대해 이러한 권한을 설정할 수 있습니다. 자세한 내용은 [처리 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) 및 [개체 메타데이터에 대한 정의 읽기 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)를 참조하세요.  
  
## <a name="set-permissions-on-a-cube-dimension"></a>큐브 차원에 대한 권한 설정  
 큐브 차원은 큐브에 추가된 데이터베이스 차원입니다. 따라서 연결된 측정값 그룹에 구조적으로 종속됩니다. 이러한 개체를 개별적으로 처리할 수 있지만 권한 부여의 측면에서 큐브 및 큐브 차원을 단일 개체로 처리하는 것이 좋습니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하고 개체 탐색기에서 해당 데이터베이스에 대한 **역할** 을 확장한 다음 데이터베이스 역할을 클릭하거나 새 데이터베이스 역할을 만듭니다.  
  
2.  에 **차원** 로 차원 설정 창에서 변경 \<큐브-이름 > **큐브 차원**합니다.  
  
     기본적으로 권한은 해당 데이터베이스 차원에서 상속됩니다. **상속** 확인란 선택을 취소하여 **읽기** 에서 **읽기/쓰기**로 사용 권한을 변경합니다. **읽기/쓰기**를 사용하기 전에 앞의 섹션에 나와 있는 참고 사항을 읽어보시기 바랍니다.  
  
> [!IMPORTANT]  
>  AMO(Analysis Management Object)를 사용하여 데이터베이스 역할의 사용 권한을 구성하면 큐브의 DimensionPermission 특성에 있는 큐브 차원에 대한 모든 참조가 데이터베이스의 DimensionPermission 특성으로부터 사용 권한 상속을 분리합니다. AMO에 대한 자세한 내용은 [AMO&#40;Analysis Management Objects&#41;를 사용하여 개발](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [역할 및 권한&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)   
 [큐브 또는 모델 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [데이터 마이닝 구조 및 모델 &#40;에 대 한 권한 부여 Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [데이터 &#40; 차원에 대 한 사용자 지정 액세스 부여 Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [셀 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
  

