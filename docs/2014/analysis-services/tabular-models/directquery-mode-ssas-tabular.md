---
title: DirectQuery 모드 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.realtime.f1
ms.assetid: 45ad2965-05ec-4fb1-a164-d8060b562ea5
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b0badf00027259bb2203828e075a8d009deb8d5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37149834"
---
# <a name="directquery-mode-ssas-tabular"></a>DirectQuery 모드(SSAS 테이블 형식)
  Analysis Services를 사용하면 *DirectQuery 모드*를 통해 관계형 데이터베이스 시스템에서 직접 데이터 및 집계를 검색하여 테이블 형식 모델에서 데이터를 검색하고 보고서를 만들 수 있습니다. 이 항목에서는 메모리에만 있는 표준 테이블 형식 모델과 관계형 데이터 원본을 쿼리할 수 있는 테이블 형식 모델 간의 차이점을 소개하고 DirectQuery 모드에서 사용할 모델을 제작하고 배포하는 방법에 대해 설명합니다.  
  
 이 항목의 섹션:  
  
-   [DirectQuery 모드의 이점](#bkmk_Benefits)  
  
-   [DirectQuery 모드를 사용 하 여 사용할 모델 제작](#bkmk_Design)  
  
    -   [DirectQuery 모델에 대 한 데이터 원본](directquery-mode-ssas-tabular.md#bkmk_datasources)  
  
    -   [유효성 검사 및 DirectQuery 모드에 대 한 디자인 제한 사항](#bkmk_Validation)  
  
    -   [DirectQuery 모델에 대 한 수식 호환성](#bkmk_FormulaCompat)  
  
    -   [DirectQuery 모드의 보안](#bkmk_Security)  
  
    -   [DirectQuery 모드의 보안](#bkmk_Security)  
  
-   [DirectQuery 속성](#bkmk_PropertyList)  
  
-   [관련된 항목 및 작업](#bkmk_related_tasks)  
  
##  <a name="bkmk_Benefits"></a> DirectQuery 모드의 이점  
 기본적으로 테이블 형식 모델은 메모리 내 캐시를 사용하여 데이터를 저장하고 쿼리합니다. 테이블 형식 모델은 메모리에 있는 데이터를 사용하기 때문에 복잡한 쿼리도 아주 빨리 처리할 수 있습니다. 그러나 캐시된 데이터를 사용하는 경우 다음과 같은 몇 가지 단점이 있습니다.  
  
-   원본 데이터를 변경해도 데이터가 새로 고쳐지지 않습니다. 데이터를 업데이트하려면 모델을 처리해야 합니다.  
  
-   모델을 호스팅하는 컴퓨터를 끄면 캐시가 디스크에 저장되며, 모델을 로드하거나 PowerPivot 파일을 열 때 캐시를 다시 열어야 합니다. 따라서 저장 및 로드 작업 시간이 많이 걸릴 수 있습니다.  
  
 이와 달리 DirectQuery 모드는 SQLServer 데이터베이스에 저장된 데이터를 사용합니다.  일반적으로 모델을 제작하는 동안 데이터의 모든 예제 또는 일부 예제를 가져오고, 모델을 배포할 때 모델에 대한 쿼리의 데이터 원본이 캐시된 데이터가 아닌 SQL Server여야 한다고 지정합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 데이터에 대한 DAX 쿼리를 지정된 관계형 데이터 원본에 대해 해당하는 SQL 문으로 변환합니다.  
  
 DirectQuery 모드를 사용하여 모델을 배포하는 경우 많은 이점이 있습니다.  
  
-   데이터 집합에 대한 모델이 너무 커서 Analysis Services 서버의 메모리에 맞지 않을 수 있습니다.  
  
-   데이터가 최신 데이터이며, 데이터에 대한 별도의 복사본을 유지 관리해야 하는 추가적인 관리 오버헤드가 없습니다. 기본 원본 데이터를 변경하면 데이터 모델에 대한 쿼리에 바로 반영될 수 있습니다.  
  
-   DirectQuery는 xVelocity 메모리 최적화 열 인덱스에서 제공하는 것과 같은 공급자 측 쿼리 가속 기능을 활용할 수 있습니다.  
  
-   백 엔드 데이터베이스에 의해 적용된 모든 보안은 행 수준 보안을 사용하여 적용됩니다. 이와 달리, 캐시된 데이터를 사용하는 경우에는 서버에서 캐시 보안을 정확하게 설정하기 어려울 수 있습니다.  
  
-   모델에 포함되어 있는 복합 수식에 여러 쿼리가 필요할 수 있는 경우 Analysis Services에서는 최적화를 수행하여 벡 엔드 데이터베이스에 대해 실행된 쿼리의 쿼리 계획 효율성을 극대화할 수 있습니다.  
  
##  <a name="bkmk_Design"></a> DirectQuery 모드를 사용 하 여 사용할 모델 제작  
 테이블 형식 모델은 모델 디자이너 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 사용하여 만듭니다. 모델 디자이너가 메모리에 모든 모델을 만듭니다. 이는 모델링할 때 데이터가 너무 커서 메모리에 맞지 않는 경우 작업 영역 데이터베이스에 사용된 캐시에 데이터의 하위 집합만을 가져와야 함을 의미합니다.  
  
 DirectQuery 모드로 전환할 준비가 되었으면 DirectQuery 모드를 사용하도록 설정하는 속성을 변경할 수 있습니다. 자세한 내용은 [DirectQuery 디자인 모드를 사용 하도록 설정 &#40;&AMP;#40;SSAS 테이블 형식&#41;](enable-directquery-mode-in-ssdt.md)합니다.  
  
 이렇게 하면 모델 디자이너가 혼합 모드에서 실행되도록 자동으로 작업 영역 데이터베이스를 구성하므로 캐시된 데이터를 계속해서 사용할 수 있습니다. 또한 모델 디자이너는 모델에서 DirectQuery 모드와 호환되지 않는 모든 기능을 알려 줍니다. 다음 목록에는 유의해야 할 주요 사항이 요약되어 있습니다.  
  
-   **데이터 원본:** DirectQuery 모델은 단일 SQL Server 데이터 원본의 데이터만 사용할 수 있습니다. 모델에서 DirectQuery 모드를 사용하도록 설정했으면 모델 디자이너에서 복사/붙여넣기 작업으로 추가한 테이블을 비롯한 다른 형식의 데이터를 사용할 수 없습니다. 또한 모든 가져오기 옵션도 사용할 수 없습니다. 쿼리에 포함된 모든 테이블은 SQL Server 데이터 원본의 일부여야 합니다. 참조 [Data Sources for DirectQuery Models](directquery-mode-ssas-tabular.md#bkmk_datasources)자세한 내용은 합니다.  
  
-   **계산 열에 대한 지원:** DirectQuery 모델에 대해서는 계산 열이 지원되지 않습니다. 그러나 데이터 집합에 대해 작동하는 측정값 및 KPI를 만들 수는 있습니다. 자세한 내용은 [유효성 검사](#bkmk_Validation) 섹션을 참조하십시오.  
  
-   **DAX 함수의 제한된 사용:** 일부 DAX 함수는 DirectQuery 모드에서 사용할 수 없으므로 해당 함수를 다른 함수로 바꾸거나 데이터 원본에서 파생 열을 사용하여 값을 만들어야 합니다. 모델 디자이너에서는 DirectQuery 모드와 호환되지 않는 수식을 만들 때 발생하는 모든 오류에 대한 디자인 타임 유효성 검사 기능을 제공합니다. 자세한 내용은 [유효성 검사](#bkmk_Validation)섹션을 참조하십시오.  
  
-   **수식 호환성:** 알려진 특정 경우에 동일한 수식에서 관계형 데이터 저장소만 사용하는 DirectQuery 모델과 비교했을 때 혼합 모델이나 캐시된 모델의 경우 다른 결과를 반환할 수 있습니다. xVelocity 메모리 내 분석(VertiPaq) 엔진과 SQL Server 간의 의미 체계 차이점 때문에 이러한 차이가 발생합니다. 이러한 차이점에 대한 자세한 내용은 [수식 호환성](#bkmk_FormulaCompat)섹션을 참조하십시오.  
  
-   **보안:** 모델의 배포 방법에 따라 모델 보안을 설정하는 데 사용하는 방법이 다릅니다. 테이블 형식 모델의 캐시된 데이터에는 Analysis Services 인스턴스의 보안 모델을 사용하여 보안이 설정됩니다. 역할을 사용하여 DirectQuery 모델 보안을 설정할 수 있지만 관계형 데이터 저장소에 정의된 보안을 사용할 수도 있습니다. 즉, DirectQuery 전용 모델을 기반으로 보고서를 여는 사용자가 SQL Server에서 해당 사용자의 사용 권한에 허용되는 데이터만 볼 수 있도록 모델을 구성할 수 있습니다. 자세한 내용은 다음 섹션을 참조하십시오. [보안](#bkmk_Security).  
  
-   **클라이언트 제한 사항:** DirectQuery 모드에 있는 모델은 DAX를 사용해서만 쿼리할 수 있습니다. MDX를 사용하여 쿼리를 만들 수는 없습니다. 즉, Excel에서는 MDX를 사용하기 때문에 Excel 피벗 클라이언트를 사용할 수 없습니다.  
  
     그러나 DirectQuery 모델에 대 한 쿼리를 만들 수 있습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] DAX 테이블 쿼리를 XMLA Execute 문의 일부로 자세한를 사용 하면 참조 [DAX 쿼리 구문 참조](https://msdn.microsoft.com/library/ee634217.aspx)합니다.  
  
 모든 디자인 문제를 해결하고 모델을 테스트했으면 배포할 준비가 된 것입니다. 이때 모델에 대한 쿼리에 응답하는 데 기본적으로 사용되는 방법을 설정할 수 있습니다. 사용자가 캐시에 액세스할 수 있는 권한을 가지도록 할지 항상 관계형 데이터 원본만 사용하도록 할지 결정하셨습니까?  
  
 *혼합 모드*에서 모델을 배포하면 계속해서 캐시를 사용할 수 있으며 쿼리에 캐시를 사용할 수 있습니다. 혼합 모드에서는 여러 가지 옵션이 제공됩니다.  
  
-   캐시와 관계형 데이터 원본 모두 사용할 수 있는 경우 기본적으로 사용되는 연결 방법을 설정할 수 있지만 궁극적으로는 클라이언트가 DirectQueryMode 연결 문자열 속성을 사용하여 사용되는 원본을 제어합니다.  
  
-   DirectQuery 모드에 사용된 기본 파티션이 절대 처리되지 않는 방식으로 캐시에 파티션을 구성할 수도 있으며 항상 관계형 원본을 참조해야 합니다. 여러 가지 방법으로 파티션을 사용하여 모델 디자인 및 보고 환경을 최적화할 수 있습니다. 자세한 내용은 [파티션 및 DirectQuery 모드 &#40;&AMP;#40;SSAS 테이블 형식&#41;](define-partitions-in-directquery-models-ssas-tabular.md)합니다.  
  
-   모델을 배포한 후 기본적으로 사용되는 연결 방법을 변경할 수 있습니다. 예를 들어 모델을 사용하는 보고서나 쿼리를 모두 철저히 테스트한 후에만 테스트에 혼합 모드를 사용하고 모델을 **DirectQuery 전용** 모드로 전환할 수 있습니다. 자세한 내용은 [DirectQuery의 기본 연결 방법 설정 또는 변경](../set-or-change-the-preferred-connection-method-for-directquery.md)을 참조하세요.  
  
###  <a name="bkmk_DataSources"></a> DirectQuery 모델에 대 한 데이터 원본  
 DirectQuery 모드를 사용하도록 디자인 환경을 변경하는 즉시 작업 영역 데이터베이스의 데이터 원본을 단일 SQL Server 데이터 원본에서 가져온 것인지 확인하기 위해 유효성이 검사됩니다. 복사하여 붙여 넣은 데이터를 비롯하여 다른 원본에서 가져온 데이터는 DirectQuery 모델에서 사용할 수 없습니다.  
  
 DirectQuery 모드에서 모델을 사용하려는 경우 보고하는 데 필요한 모든 데이터가 지정한 SQL Server 데이터베이스에 저장되도록 해야 합니다. 해당 원본에서 모델링에 필요한 데이터를 사용할 수 없는 경우에는 Integration Services 또는 다른 데이터 웨어하우징 도구를 사용하여 DirectQuery 데이터 원본으로 사용할 SQL Server 데이터베이스로 데이터를 가져오십시오.  
  
###  <a name="bkmk_Validation"></a> 유효성 검사 및 DirectQuery 모드에 대 한 디자인 제한 사항  
 DirectQuery 모드에서 사용할 모델을 만들 때는 처음에 데이터의 일부분을 캐시에 로드해야 합니다. 사용 하 여 최종적으로 데이터가 너무 커서 메모리에 맞지 않는 경우 사용할 수는 **미리 보기 및 필터** 원하는 데이터를 가져올 데이터의 하위 집합을 선택 하거나 SQL 스크립트를 작성 하려면 테이블 가져오기 마법사의 옵션입니다.  
  
> [!WARNING]  
>  DirectQuery 모드는 계산 열의 사용을 지원하지 않으므로 결합하거나 다른 작업을 수행하려는 열이 있는 경우 미리 계획하고 열 정의를 데이터 가져오기 쿼리 또는 스크립트의 일부로 만들어야 합니다.  
  
 열기를 보고 하려면 유효성 검사 오류를 해결 합니다 **오류 목록** 에서 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]합니다. DirectQuery 모드를 차단하는 심각한 오류는 **오류** 탭에 표시됩니다. DirectQuery 모드로 변경하기 전에 이러한 오류를 수정해야 합니다. 일반적으로 더 해결하기 어려운 유효성 검사 오류는 DirectQuery 모드에서 지원되지 않는 수식과 관련이 있습니다. 수식 및 계산 열과 관련된 오류에 대한 개요를 보려면 [수식 호환성](#bkmk_FormulaCompat)섹션을 참조하십시오.  
  
 다음 목록에서는 DirectQuery 액세스를 위한 모델을 제작할 때 유의해야 할 기타 고려 사항에 대해 설명합니다.  
  
-   *DirectQuery 전용* 모드에서는 결과를 보는 사용자의 보안 컨텍스트에 따라 보고서 결과가 달라질 수 있습니다. 사용자가 예상 결과를 얻을 수 있도록 하려면 여러 다른 자격 증명을 사용하여 모델을 테스트해야 합니다.  
  
-   SQL Server의 데이터 또는 캐시를 사용할 수 있도록 혼합 모드에서 작동하는 모델을 구성하는 경우 연결 문자열에 지정된 모드에 따라 각 원본에 연결하는 클라이언트에게 서로 다른 결과를 표시될 수도 있음을 알고 있어야 합니다. 보고서 사용자에게 SQL Server의 데이터만 표시되어야 하는 경우에는 캐시를 지우거나 모델을 DirectQueryOnly로 변경해야 합니다.  
  
###  <a name="bkmk_FormulaCompat"></a> DirectQuery 모델에 대 한 수식 호환성  
 일부 모델에는 DirectQuery 모드에서 지원되지 않는 수식이 포함될 수 있으며, 유효성 검사 오류가 발생하지 않도록 해당 모델을 다시 디자인해야 합니다. DirectQuery 모드에서 지원되는 수식에 대한 제한 사항은 다음과 같습니다.  
  
-   계산 열은 DirectQuery 모드를 사용하도록 설정된 테이블 형식 모델에서 지원되지 않으며, 혼합 모델에서도 지원되지 않습니다. 모델에 계산 열이 필요한 경우 가져오기 정의에 Transact-SQL을 사용하여 해당 열을 파생 열로 변환하십시오.  
  
-   DirectQuery 모델은 측정값에 DAX 수식을 사용할 수 있도록 지원합니다. 이 수식은 관계형 데이터 저장소에 대한 집합 기반 연산으로 변환됩니다. 암시적 측정값을 사용하여 만드는 측정값은 모두 지원됩니다.  
  
-   일부 함수는 지원되지 않습니다. DirectQuery 모델을 쿼리할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 모든 DAX 수식과 측정값 정의를 SQL 문으로 변환하기 때문에 Transact-SQL로 변환할 수 없는 요소가 들어 있는 수식에서는 모두 모델에 대한 유효성 검사 오류가 발생합니다. 예를 들어 시간 인텔리전스 함수는 지원되지 않습니다. 통계 함수와 같은 지원되는 함수도 다르게 동작할 수 있습니다. 호환성 문제의 전체 목록은 참조 하세요 [DirectQuery 모드에서의 수식 호환성](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)합니다.  
  
-   모델을 DirectQuery 모드로 전환하는 경우 모델의 일부 수식이 유효성 검사를 수행할 수 있지만 캐시와 관계형 데이터 저장소에 대해 실행될 때는 다른 결과를 반환합니다. 캐시에 대한 계산은 Excel 동작을 에뮬레이트하는 여러 기능이 포함된 xVelocity 메모리 내 분석(VertiPaq) 엔진의 의미 체계를 사용하는 반면 관계형 데이터 저장소에 저장된 데이터에 대한 쿼리는 반드시 SQL Server의 의미 체계를 사용하기 때문에 이러한 결과가 발생합니다. 목록을 반환할 수 있는 다른 결과 모델을 배포할 때 실시간으로 DAX 함수 참조 [DirectQuery 모드에서의 수식 호환성](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)합니다.  
  
###  <a name="bkmk_Connecting"></a> DirectQuery 모델에 연결  
 DMX를 쿼리 언어로 사용하는 클라이언트는 DirectQuery 모드를 사용하는 모델에 연결할 수 없습니다. 예를 들어 DirectQuery 모델에 대해 MDX 쿼리를 만들려고 하면 큐브를 찾을 수 없거나 큐브가 처리되지 않았다는 오류가 발생합니다. [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], DMX 수식 또는 XMLA 쿼리를 사용하여 DirectQuery 모델에 대한 쿼리를 만들 수 있습니다. 테이블 형식 모델에 대 한 임시 쿼리를 수행 하는 방법에 대 한 자세한 내용은 참조 하십시오 [Tabular Model Data Access](tabular-model-data-access.md)합니다.  
  
 혼합 모델을 사용하는 경우 DirectQueryMode 연결 문자열 속성을 지정하여 사용자가 캐시에 연결하는지 아니면 DirectQuery 데이터를 사용하는지 지정할 수 있습니다.  
  
###  <a name="bkmk_Security"></a> DirectQuery 모드의 보안  
 모델 제작 중에 원본 데이터를 검색하는 데 사용되는 사용 권한을 지정합니다. 주로 사용자 자격 증명 또는 개발에 사용되는 계정입니다. 그러나 DirectQuery 모드를 사용하도록 모델을 전환하면 보안 컨텍스트가 더 복잡해집니다.  
  
-   사용자가 관계형 데이터 저장소의 데이터에 대해 필요한 수준의 액세스 권한을 가지고 있는지 여부를 고려합니다.  
  
-   사용자의 보안 컨텍스트에 따라 동일한 모델 또는 보고서를 보는 사용자가 서로 다른 데이터를 볼 수 있습니다.  
  
-   모델 캐시가 유지된 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 보안 모델(역할)을 사용하여 캐시에 보안이 설정됩니다. 캐시에 사용자는 볼 수 없고 모델 디자이너는 볼 수 있는 권한을 가진 데이터가 있을 수 있습니다. 모델 및 보고서 디자이너는 역할을 통해 액세스를 제어하여 이 데이터 보안을 설정하거나 캐시를 지워야 합니다.  
  
-   캐시의 쿼리에 대답하는 모델은 데이터 원본에 연결할 때 현재 사용자를 가장할 수 없습니다. 데이터 원본에 연결할 때 현재 사용자를 가장하려면 DirectQuery 모드를 사용해야 합니다.  
  
-   보고서 모델에 보안이 필요한 경우 두 가지 옵션이 있습니다: 사용 하거나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 역할을 하거나 데이터 원본에서 행 수준 권한을 설정할 수 있습니다. 관계형 데이터 원본의 보안을 사용하여 테이블에 대한 액세스를 제어할 수 있으며 열 수준 보안은 지원되지 않습니다. 따라서 특정 지역의 사용자가 다른 지역의 판매 수치를 볼 수 있는 권한을 가지고 있지 않은 경우 Sales 테이블 기반 측정값이 포함된 보고서에서 공백 또는 오류를 반환합니다.  
  
 가장 설정 속성은 DirectQuery 전용 모델 또는 DirectQuery를 사용하여 쿼리에 대답하는 혼합 모델에 대해 DirectQuery를 사용하여 모델에 연결할 때 사용되는 자격 증명을 지정합니다. 속성 값은 다음과 같습니다.  
  
 **Default**  
 가져오기 마법사에서 지정한 자격 증명을 사용하여 데이터 원본에 연결합니다. 이 자격 증명은 특정 Windows 사용자 또는 서비스 계정일 수 있습니다.  
  
 `ImpersonateCurrentUser`  
 현재 사용자의 자격 증명을 사용하여 데이터 원본에 연결합니다.  
  
 이러한 속성을 설정 하는 방법에 대 한 자세한 내용은 [DirectQuery 배포 시나리오 &#40;&AMP;#40;SSAS 테이블 형식&#41;](../directquery-deployment-scenarios-ssas-tabular.md)합니다.  
  
##  <a name="bkmk_PropertyList"></a> DirectQuery 속성  
 다음 표에서는 모델에 대한 쿼리에 사용되는 데이터 원본을 제어하고 DirectQuery를 사용하도록 설정하기 위해 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 설정할 수 있는 속성을 보여 줍니다.  
  
|속성 이름|Description|  
|-------------------|-----------------|  
|**DirectQueryMode 속성**|이 속성은 모델 디자이너에서 DirectQuery 모드를 사용하도록 설정합니다. 다른 DirectQuery 속성을 변경하려면 이 속성을 `On`으로 설정해야 합니다.<br /><br /> 자세한 내용은 [DirectQuery 디자인 모드를 사용 하도록 설정 &#40;&AMP;#40;SSAS 테이블 형식&#41;](enable-directquery-mode-in-ssdt.md)합니다.|  
|**QueryMode 속성**|이 속성은 DirectQuery 모델에 대한 기본 쿼리 메서드를 지정합니다. 이 속성은 모델을 배포할 때 모델 디자이너에서 설정하지만 나중에 재정의할 수 있습니다. 속성 값은 다음과 같습니다.<br /><br /> **DirectQuery** – 이 설정은 모델에 대한 모든 쿼리에서 관계형 데이터 원본만 사용하도록 지정합니다.<br /><br /> **DirectQuery with In-Memory** - 이 설정은 클라이언트의 연결 문자열에 다르게 지정되어 있지 않으면 기본적으로 관계형 원본을 사용하여 쿼리에 응답하도록 지정합니다.<br /><br /> **In-Memory** - 이 설정은 캐시만 사용하여 쿼리에 응답하도록 지정합니다.<br /><br /> **In-Memory with DirectQuery** - 이 설정은 기본적으로 클라이언트에서 연결 문자열에 다르게 지정되어 있지 않으면 캐시를 사용하여 쿼리에 응답하도록 지정합니다.<br /><br /> <br /><br /> 자세한 내용은 [DirectQuery의 기본 연결 방법 설정 또는 변경](../set-or-change-the-preferred-connection-method-for-directquery.md)을 참조하세요.|  
|**DirectQueryMode 속성**|모델을 배포한 후 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 이 속성을 변경하여 DirectQuery 모델에 대해 기본적으로 사용되는 쿼리 데이터 원본을 변경할 수 있습니다.<br /><br /> 이전 속성과 마찬가지로 이 속성은 모델의 기본 데이터 원본을 지정하며 속성 값은 다음과 같습니다.<br /><br /> **InMemory**: 쿼리에서 캐시만 사용할 수 있습니다.<br /><br /> **DirectQuerywithInMemory**: 클라이언트에서 연결 문자열에 다르게 지정되어 있지 않으면 기본적으로 쿼리에서 관계형 데이터 원본을 사용합니다.<br /><br /> **InMemorywithDirectQuery**: 클라이언트에서 연결 문자열에 다르게 지정되어 있지 않으면 기본적으로 쿼리에서 캐시를 사용합니다.<br /><br /> (**DirectQuery**: 쿼리에서 관계형 데이터 원본만 사용합니다.<br /><br /> <br /><br /> 자세한 내용은 [DirectQuery의 기본 연결 방법 설정 또는 변경](../set-or-change-the-preferred-connection-method-for-directquery.md)을 참조하세요.|  
|**가장 설정 속성**|이 속성은 쿼리 시 SQL Server 데이터 원본에 연결하는 데 사용되는 자격 증명을 정의합니다. 모델 디자이너에서 이 속성을 설정할 수 있으며 모델을 배포한 후 나중에 값을 변경할 수도 있습니다.<br /><br /> 이러한 자격 증명은 관계형 데이터 저장소에 대한 쿼리 응답에만 사용되며, 혼합 모델의 캐시를 처리하는 데 사용되는 자격 증명과는 다릅니다.<br /><br /> 모델을 메모리에 내에서만 사용하는 경우에는 가장을 사용할 수 없습니다. 모델에서 DirectQuery 모드를 사용하지 않는 경우에는 `ImpersonateCurrentUser` 설정이 유효하지 않습니다.|  
  
 또한 모델에 파티션이 포함되어 있는 경우 DirectQuery 모드에서 쿼리의 원본으로 사용할 하나의 파티션을 선택해야 합니다. 자세한 내용은 [파티션 및 DirectQuery 모드 &#40;&AMP;#40;SSAS 테이블 형식&#41;](define-partitions-in-directquery-models-ssas-tabular.md)합니다.  
  
##  <a name="bkmk_related_tasks"></a> 관련된 항목 및 작업  
  
|항목|Description|  
|-----------|-----------------|  
|[파티션 및 DirectQuery 모드 &#40;&AMP;#40;SSAS 테이블 형식&#41;](define-partitions-in-directquery-models-ssas-tabular.md)|DirectQuery 모드에 대해 구성된 모델에서 파티션을 사용하는 방법에 대해 설명합니다.|  
|[DirectQuery 모드에서의 DAX 수식 호환성](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)|DirectQuery 모드에 대해 구성된 모델에서 사용할 수 있는 수식에 대한 제한 사항과 호환성 요구 사항을 설명합니다.|  
|[DirectQuery 디자인 모드를 사용 하도록 설정 &#40;&AMP;#40;SSAS 테이블 형식&#41;](enable-directquery-mode-in-ssdt.md)|DirectQuery 모드를 사용하여 지원하도록 디자인 타임 환경을 변경하는 방법에 대해 설명합니다.|  
|[DirectQuery 파티션 변경 &#40;&AMP;#40;SSAS 테이블 형식&#41;](../change-the-directquery-partition-ssas-tabular.md)|DirectQuery 파티션을 변경하는 방법을 설명합니다.|  
|[DirectQuery의 기본 연결 방법 설정 또는 변경](../set-or-change-the-preferred-connection-method-for-directquery.md)|DirectQuery에 대해 구성된 모델에 대한 연결 방법을 설정하거나 변경하는 방법을 설명합니다.|  
|[DirectQuery 배포 시나리오 &#40;&AMP;#40;SSAS 테이블 형식&#41;](../directquery-deployment-scenarios-ssas-tabular.md)|DirectQuery 배포 시나리오를 설명합니다.|  
|[테이블 형식 모델 데이터베이스에 대해 메모리 내 또는 DirectQuery 액세스 구성](enable-directquery-mode-in-ssms.md)|DirectQuery 구성 이해|  
|[Analysis Services 캐시 지우기](../instances/clear-the-analysis-services-caches.md)|테이블 형식 모델의 캐시 지우기|  
  
## <a name="see-also"></a>관련 항목  
 [파티션 &#40;&AMP;#40;SSAS 테이블 형식&#41;](partitions-ssas-tabular.md)   
 [테이블 형식 모델 프로젝트 &#40;&AMP;#40;SSAS 테이블 형식&#41;](tabular-model-projects-ssas-tabular.md)   
 [Excel에서 분석 &#40;&AMP;#40;SSAS 테이블 형식&#41;](analyze-in-excel-ssas-tabular.md)  
  
  
