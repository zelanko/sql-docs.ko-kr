---
title: DirectQuery 배포 시나리오 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2aaf5cb8-294b-4031-94b3-fe605d7fc4c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a62a05c8908391b9ce925ecfe08ae30540b8fa29
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081647"
---
# <a name="directquery-deployment-scenarios-ssas-tabular"></a>DirectQuery 배포 시나리오(SSAS 테이블 형식)
  이 항목에서는 DirectQuery 모델에 대한 디자인 및 배포 프로세스를 연습할 수 있습니다. 관계형 데이터만 사용하도록 DirectQuery를 구성하거나(DirectQuery 전용) 전환을 통해 캐시된 데이터만 사용하거나 관계형 데이터만 사용하도록 모델을 구성할 수 있습니다(혼합 모드). 이 항목에서는 두 모드에 대한 구현 프로세스에 대해 설명하고 모드와 보안 구성에 따라 달라질 수 있는 쿼리 결과에 대해 살펴봅니다.  
  
 [디자인 및 배포 단계](#bkmk_DQProcedure)  
  
 [DirectQuery 구성 비교](#bkmk_Configurations)  
  
##  <a name="bkmk_DQProcedure"></a> 디자인 및 배포 단계  
 **1 단계입니다. 솔루션 만들기**  
  
 사용하는 모드에 관계없이 DirectQuery 모델에서 사용될 수 있는 데이터에 대한 제한 사항을 설명하는 정보를 검토해야 합니다. 예를 들어 모델 및 보고서에 사용되는 모든 데이터는 단일 SQL Server 데이터베이스에서 가져와야 합니다. 자세한 내용은 [DirectQuery 모드&#40;SSAS 테이블 형식&#41;](tabular-models/directquery-mode-ssas-tabular.md)를 참조하세요.  
  
 또한 측정값 및 계산 열에 대한 제한 사항을 검토하고 사용하려는 수식이 DirectQuery 모드와 호환되는지 여부를 확인합니다. 다음 요소를 제거하거나 수정해야 할 수 있습니다.  
  
-   계산 열이 지원되지 않습니다.  
  
-   복사하여 붙여 넣은 데이터를 사용할 수 없습니다. 이러한 데이터는 삭제할 수 없을 뿐만 아니라 DirectQuery 유효성 검사를 차단하므로 PowerPivot 모델을 가져와서 솔루션을 시작할 경우 솔루션을 가져오기 전에 연결된 테이블을 삭제해야 합니다.  
  
 **2 단계입니다. 모델 디자이너에서 DirectQuery 모드를 사용 하도록 설정**  
  
 기본적으로 DirectQuery는 사용하지 않도록 설정되어 있습니다. 따라서 DirectQuery 모드를 지원하도록 디자인 환경을 구성해야 합니다.  
  
 마우스 오른쪽 단추로 클릭 합니다 **Model.bim** 속성을 설정 하 고 솔루션 탐색기에서 노드 **DirectQuery 모드**를 `On`입니다.  
  
 언제든지 DirectQuery를 설정할 수 있지만, DirectQuery 모드와 호환되지 않는 수식이나 열을 만들지 않으려면 처음부터 DirectQuery 모드를 사용하도록 설정하는 것이 좋습니다.  
  
 처음에는 DirectQuery 모델이 항상 메모리에 생성됩니다. 또한 작업 영역 데이터베이스에 대한 기본 쿼리 모드는 **DirectQuery with In-Memory**로 설정됩니다. 이 혼합 작업 모드에서는 DirectQuery 요구 사항에 대한 모델의 유효성을 검사하는 동안 계속해서 가져온 데이터의 캐시를 사용할 수 있으므로 모델 디자인 프로세스 중 성능이 향상됩니다.  
  
 **3 단계: 유효성 검사 오류 해결**  
  
 DirectQuery를 설정할 때나 새 데이터 또는 수식을 추가할 때 유효성 검사 오류가 발생하는 경우 Visual Studio **오류 목록**을 연 다음 필요한 동작을 수행합니다.  
  
-   오류 메시지에 설명된 대로 DirectQuery 모드에 필요한 속성 설정을 변경합니다.  
  
-   계산 열을 제거합니다. 항상 사용 하 여 열 특정 측정값에 대 한 계산된 된 열에 필요한 경우 만들면 합니다 [관계형 쿼리 디자이너 &#40;SSAS&#41; ](relational-query-designer-ssas.md) 테이블 가져오기 마법사에서 제공 합니다.  
  
-   DirectQuery 모드와 호환되지 않는 수식을 수정하거나 제거합니다. 계산에 특정 함수가 필요한 경우에는 Transact-SQL을 사용하여 해당 함수를 제공할 수 있는 방법을 고려합니다.  
  
-   필요에 따라 데이터를 추가합니다.  모델에서 SQL Server가 아닌 공급자의 데이터나 복사하여 붙여 넣은 데이터를 사용한 적이 있는 경우 기존 연결 내에서 새 뷰와 파생 열을 만들거나 분산 쿼리를 사용할 수 있습니다.  DirectQuery 모델에서 사용되는 모든 데이터는 단일 SQL Server 데이터 원본을 통해 액세스할 수 있어야 합니다.  
  
 **4 단계입니다. 모델에 대 한 쿼리에 응답 하기 위한 기본 메서드를 설정 합니다.**  
  
|||  
|-|-|  
|**DirectQuery 전용**|속성을 **DirectQuery**로 설정합니다.|  
|**혼합 모드**|속성을 **In-Memory With DirectQuery** 또는 **DirectQuery With In-Memory**로 설정합니다.<br /><br /> 나중에 이 값을 변경하여 다른 기본 설정을 사용할 수 있습니다.<br /><br /> 클라이언트는 연결 문자열에서 기본적으로 사용되는 방법을 재정의할 수 있습니다.|  
  
 **5 단계입니다. DirectQuery 파티션 지정**  
  
|||  
|-|-|  
|**DirectQuery 전용**|(선택 사항) DirectQuery 전용 모델은 파티션이 필요하지 않습니다.<br /><br /> 그러나 디자인 단계 동안 모델에서 파티션을 만든 경우 파티션 중 하나만 데이터 원본으로 사용될 수 있습니다. 기본적으로 첫 번째로 만든 파티션이 DirectQuery 파티션으로 사용됩니다.<br /><br /> 모델에 필요한 모든 데이터를 DirectQuery 파티션에서 사용할 수 있도록 하려면 DirectQuery 파티션을 선택한 다음 전체 데이터 집합을 가져오도록 SQL 문을 편집합니다.|  
|**혼합 모드**|모델의 테이블에 파티션이 여러 개 있는 경우 파티션 중 하나를 *DirectQuery 파티션*으로 선택해야 합니다. 파티션을 할당하지 않을 경우 기본적으로 처음 만들어진 파티션이 DirectQuery 파티션으로 사용됩니다.<br /><br /> DirectQuery를 제외한 모든 파티션에 대한 처리 옵션을 설정합니다. 데이터가 관계형 원본에서 전달되므로 일반적으로 DirectQuery 파티션은 처리되지 않습니다.<br /><br /> 자세한 내용은 [파티션 및 DirectQuery 모드 &#40;&AMP;#40;SSAS 테이블 형식&#41;](tabular-models/define-partitions-in-directquery-models-ssas-tabular.md)합니다.|  
  
 **6 단계입니다. 가장 구성**  
  
 가장은 DirectQuery 모델에 대해서만 지원됩니다. 가장 옵션인 **가장 설정**은 지정된 SQL Server 데이터 원본에서 데이터를 볼 때 사용되는 자격 증명을 정의합니다.  
  
|||  
|-|-|  
|**DirectQuery 전용**|**가장 설정** 속성에서 SQL Server 데이터 원본에 연결하는 데 사용할 계정을 지정합니다.<br /><br /> **ImpersonateCurrentUser**값을 사용하면 모델을 호스팅하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스가 현재 모델 사용자의 자격 증명을 SQL Server 데이터베이스에 전달합니다.|  
|**혼합 모드**|**가장 설정** 속성에서 SQL Server 데이터 원본의 데이터에 액세스하는 데 사용할 계정을 지정합니다.<br /><br /> 이 설정은 모델에 사용된 캐시를 처리하는 데 사용되는 자격 증명에 영향을 주지 않습니다.|  
  
 **7 단계입니다. 모델 배포**  
  
 모델을 배포할 준비가 되었을 때 엽니다는 **프로젝트** 선택한 Visual Studio의 메뉴 **속성**합니다. **QueryMode** 속성을 다음 표에 설명된 값 중 하나로 설정합니다.  
  
 자세한 내용은 [배포에서 SQL Server Data Tools &#40;&AMP;#40;SSAS 테이블 형식&#41;](tabular-models/deploy-from-sql-server-data-tools-ssas-tabular.md)합니다.  
  
|||  
|-|-|  
|**DirectQuery 전용**|**DirectQueryOnly**<br /><br /> 직접 쿼리만 지정했으므로 모델의 메타데이터는 서버에 배포되지만 모델은 처리되지 않습니다.<br /><br /> 작업 영역 데이터베이스에서 사용한 캐시가 자동으로 삭제되지는 않습니다. 캐시된 데이터를 사용자가 볼 수 없도록 하려는 경우 디자인 타임 캐시의 선택을 취소할 수 있습니다. 자세한 내용은 [Analysis Services 캐시 지우기](instances/clear-the-analysis-services-caches.md)합니다.|  
|**혼합 모드**|**DirectQuery with In-memory**<br /><br /> **In-memory with DirectQuery**<br /><br /> 이 두 값을 사용하면 필요에 따라 캐시 또는 관계형 데이터 원본을 사용할 수 있습니다. 순서에 따라 모델에 대한 쿼리에 응답할 때 기본적으로 사용되는 데이터 원본이 정의됩니다.<br /><br /> 혼합 모드에서는 모델 메타데이터를 서버에 배포하는 동시에 캐시를 처리해야 합니다.<br /><br /> 배포 후 이 설정을 변경할 수 있습니다.|  
  
 **8 단계입니다. 배포 된 모델 확인**  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 모델을 배포한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스를 엽니다. 데이터베이스 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
-   **DirectQueryMode**속성은 배포 속성을 정의할 때 설정되었습니다.  
  
-   **데이터 원본 가장 정보**속성은 사용자 가장 옵션을 정의할 때 설정되었습니다. 자세한 내용은 [가장 옵션 설정&#40;SSAS - 다차원&#41;](multidimensional-models/set-impersonation-options-ssas-multidimensional.md)을 참조하세요.  
  
-   모델을 배포한 후 언제든지 이러한 속성을 변경할 수 있습니다.  
  
##  <a name="bkmk_Configurations"></a> DirectQuery 옵션 비교  
 **DirectQuery 전용**  
 단일 데이터 원본을 사용하려고 하거나 데이터가 너무 커서 메모리에 맞지 않는 경우 이 옵션을 사용하는 것이 좋습니다. 매우 큰 관계형 데이터 원본을 사용하는 경우 디자인 타임에 데이터의 일부 하위 집합을 사용하여 모델을 만들 수 있습니다. DirectQuery 전용 모드에서 모델을 배포하는 경우 필요한 데이터를 모두 포함하도록 데이터 원본 정의를 편집할 수 있습니다.  
  
 관계형 데이터 원본에서 제공하는 보안을 사용하여 데이터에 대한 사용자 액세스를 제어하려는 경우에도 이 옵션을 사용하는 것이 좋습니다. 캐시된 테이블 형식 모델을 사용하면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 역할을 사용하여 데이터 액세스를 제어할 수도 있지만 캐시에 저장된 데이터에 보안도 설정해야 합니다. 보안 컨텍스트를 위해 데이터를 캐시해서는 안 되는 경우에는 항상 이 옵션을 사용해야 합니다.  
  
 다음 표에서는 DirectQuery 전용 모드에서 가능한 배포 결과에 대해 설명합니다.  
  
|||  
|-|-|  
|**캐시가 없는 DirectQuery**|캐시에 로드되는 데이터가 없습니다. 모델을 처리할 수 없습니다.<br /><br /> 모델은 DAX 쿼리를 지원하는 클라이언트를 통해서만 쿼리할 수 있습니다. 쿼리 결과는 항상 원래 데이터 원본에서 반환됩니다.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **DirectQuery**|  
|**캐시에 대 한 쿼리를 사용 하 여 DirectQuery**|배포에 실패하며 이 구성은 지원되지 않습니다.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **In-Memory**|  
  
 **혼합 모드**  
 혼합 모드에서 모델을 배포하면 여러 가지 이점이 있습니다. 즉, 필요한 경우 SQL Server 데이터 원본에서 최신 데이터를 가져올 수 있지만 캐시를 유지하면 보고서를 디자인하거나 모델을 테스트하는 동안 성능을 높이도록 메모리에서 데이터를 사용할 수 있습니다.  
  
 DirectQuery 혼합 모드는 모델이 매우 큰 경우에도 유용합니다. 사용자로 하여금 유효하지 않은 데이터를 가져오게 하거나 캐시가 처리되는 동안 모델을 사용할 수 없게 하는 대신 처리가 진행되는 동안 모델을 DirectQuery 모드로 전환할 수 있습니다. 사용자는 성능이 조금 저하된다고 느낄 수 있지만 관계형 저장소에서 직접 데이터를 가져올 수 있으므로 최신 결과를 얻을 수 있습니다.  
  
 다음 표에서는 각각의 DirectQuery 옵션 조합에서 발생하는 배포 결과를 비교합니다.  
  
|||  
|-|-|  
|**캐시가 기본 설정 된 혼합 모드**|모델을 처리하고 캐시에 데이터를 로드할 수 있습니다. 쿼리는 기본적으로 캐시를 사용합니다.  클라이언트가 DirectQuery 원본을 사용하려는 경우 연결 문자열에 매개 변수를 삽입해야 합니다.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **In-Memory with DirectQuery**|  
|**DirectQuery가 기본 설정 된 혼합 모드**|모델을 처리하고 캐시에 데이터를 로드할 수 있습니다. 그러나 쿼리는 기본적으로 Directquery를 사용합니다. 클라이언트가 캐시된 데이터를 사용하려는 경우 연결 문자열에 매개 변수를 삽입해야 합니다. 모델에서 테이블이 분할되면 캐시의 주 파티션도 **In-Memory with DirectQuery**로 설정됩니다.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **DirectQuery with In-Memory**|  
  
## <a name="see-also"></a>관련 항목  
 [DirectQuery 모드&#40;SSAS 테이블 형식&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [테이블 형식 모델 데이터 액세스](tabular-models/tabular-model-data-access.md)  
  
  
