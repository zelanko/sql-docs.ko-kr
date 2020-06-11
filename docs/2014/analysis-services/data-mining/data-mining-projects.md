---
title: 데이터 마이닝 프로젝트 | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 543d70fc-34d2-42dd-8d6d-0543109f94d0
author: minewiskan
ms.author: owend
ms.openlocfilehash: b5979ed2e4733609a504d852b5a0bcc8d7660b87
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84523181"
---
# <a name="data-mining-projects"></a>데이터 마이닝 프로젝트
  데이터 마이닝 프로젝트는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 솔루션의 일부입니다. 디자인 프로세스 중에 이 프로젝트에서 만든 개체를 작업 영역 데이터베이스의 일부로 테스트 및 쿼리할 수 있습니다. 사용자가 프로젝트에서 개체를 쿼리하거나 찾아볼 수 있도록 하려면 다차원 모드로 실행되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 프로젝트를 배포해야 합니다.  
  
 이 항목에서는 데이터 마이닝 프로젝트를 이해하고 만드는 데 필요한 기본 정보를 제공합니다.  
  
 
##  <a name="creating-data-mining-projects"></a><a name="bkmk_Overview"></a>데이터 마이닝 프로젝트 만들기  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 **OLAP 및 데이터 마이닝 프로젝트**템플릿을 사용하여 데이터 마이닝 프로젝트를 작성할 수 있습니다. 또한 AMO를 사용하여 프로그래밍 방식으로 데이터 마이닝 프로젝트를 만들 수 있습니다. ASSL(Analysis Services Scripting Language)을 사용하여 개별 데이터 마이닝 개체를 스크립팅할 수 있습니다. 자세한 내용은 [다차원 모델 데이터 액세스&#40;Analysis Services - 다차원 데이터&#41;](../multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)를 참조하세요.  
  
 기존 솔루션 내에 데이터 마이닝 개체를 만든 경우 해당 데이터 마이닝 개체는 기본적으로 솔루션 파일과 동일한 이름으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 배포됩니다. **보고서 속성** 대화 상자를 사용하여 이 이름 및 대상 서버를 변경할 수 있습니다. 자세한 내용은 [Analysis Services 프로젝트 속성 구성&#40;SSDT&#41;](../multidimensional-models/configure-analysis-services-project-properties-ssdt.md)인스턴스에 정의된 개체가 만들어집니다.  
  
> [!WARNING]  
>  프로젝트를 성공적으로 작성하고 배포하려면 OLAP/데이터 마이닝 모드로 실행되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 액세스 권한이 있어야 합니다. 테이블 형식 모델을 지원하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서는 데이터 마이닝 솔루션을 개발하거나 배포할 수 없으며, PowerPivot 통합 문서 또는 메모리 내 데이터 저장소를 사용하는 테이블 형식 모델에서 직접 데이터를 사용할 수 없습니다. 사용 중인 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 데이터 마이닝을 지원할 수 있는지 확인하려면 [Analysis Services 인스턴스의 서버 모드 확인](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)을 참조하세요.  
  
 만든 각 데이터 마이닝 프로젝트 내에서 다음 단계를 수행합니다.  
  
1.  큐브, 데이터베이스 또는 Excel/텍스트 파일 등 모델을 작성하는 데 사용할 원시 데이터가 포함된 *데이터 원본*을 선택합니다.  
  
2.  데이터 원본에서 분석에 사용할 데이터 하위 집합을 정의하고 이를 *데이터 원본 뷰*로 저장합니다.  
  
3.  모델링을 지원할 *마이닝 구조* 를 정의합니다.  
  
4.  *알고리즘* 을 선택하고 알고리즘에서 데이터를 처리하는 방법을 지정하여 마이닝 구조에 *마이닝 모델* 을 추가합니다.  
  
5.  모델을 선택한 데이터 또는 필터링된 데이터 하위 집합으로 채워 모델을 학습합니다.  
  
6.  모델을 탐색하고 테스트하고 다시 작성합니다.  
  
 프로젝트가 완료되면 사용자가 찾아보거나 쿼리하도록 프로젝트를 배포하거나 애플리케이션의 마이닝 모델에 대한 프로그래밍 방식의 액세스를 제공하여 예측 및 분석을 지원할 수 있습니다.  
  

  
##  <a name="objects-in-data-mining-projects"></a><a name="bkmk_Objects"></a> 데이터 마이닝 프로젝트의 개체  
 모든 데이터 마이닝 프로젝트는 다음 네 가지 유형의 개체를 포함합니다. 모든 유형의 개체를 여러 개 유지할 수 있습니다.  
  
-   데이터 원본  
  
-   데이터 원본 뷰  
  
-   마이닝 구조  
  
-   마이닝 모델  
  
 예를 들어 단일 데이터 마이닝 프로젝트에서 각각 여러 데이터 원본 뷰를 지원하는 여러 데이터 원본에 대한 참조를 포함할 수 있습니다. 또한 각 데이터 원본 뷰는 각각 여러 마이닝 모델과 관련된 여러 개의 마이닝 구조를 지원할 수 있습니다.  
  
 그 밖에도 프로젝트는 플러그 인 알고리즘, 사용자 지정 어셈블리 또는 사용자 지정 저장 프로시저를 포함할 수 있지만 여기에서는 이러한 개체에 대해 설명하지 않습니다. 자세한 내용은 [개발자 가이드 &#40;Analysis Services&#41;](../analysis-services-developer-documentation.md)를 참조 하세요.  
 
  
###  <a name="data-sources"></a><a name="bkmk_DataSources"></a>데이터 원본  
 데이터 원본은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에서 데이터 원본에 연결하는 데 사용할 연결 문자열 및 인증 정보를 정의합니다. 데이터 원본은 여러 개의 테이블 또는 뷰를 포함할 수 있으며, 단일 Excel 통합 문서 또는 텍스트 파일처럼 단순하거나 OLAP(온라인 분석 처리) 데이터베이스 또는 큰 관계형 데이터베이스처럼 복잡할 수 있습니다.  
  
 단일 데이터 마이닝 프로젝트에서 여러 데이터 원본을 참조할 수 있습니다. 마이닝 모델은 한 번에 하나의 데이터 원본만 사용할 수 있지만 프로젝트에는 데이터 원본이 서로 다른 여러 개의 모델 드로잉이 있을 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 많은 외부 공급자의 데이터를 지원하며, SQL Server 데이터 마이닝에서는 관계형 데이터와 큐브 데이터 둘 다를 데이터 원본으로 사용할 수 있습니다. 그러나 두 유형의 프로젝트 (관계형 원본 및 OLAP 큐브 기반 모델을 기반으로 하는 모델)를 모두 개발할 경우 별도의 프로젝트에서 개발 하 고 관리할 수 있습니다.  
  
-   일반적으로 OLAP 큐브를 기반으로 하는 모델은 OLAP 디자인 솔루션 내에서 개발해야 합니다. 그 이유 중 하나는 큐브를 기반으로 하는 모델은 큐브를 처리하여 데이터를 업데이트해야 하기 때문입니다. 일반적으로 큐브 데이터는 기본적인 데이터 스토리지 및 액세스 방법으로 사용되거나 다차원 프로젝트에서 만든 집계, 차원 및 특성이 필요한 경우에만 사용해야 합니다.  
  
-   프로젝트에서 관계형 데이터만 사용하는 경우에는 불필요하게 다른 개체를 다시 처리하지 않도록 별도의 프로젝트에서 관계형 모델을 만들어야 합니다. 대부분의 경우 큐브 만들기를 지원하는 데 사용되는 준비 데이터베이스 또는 데이터 웨어하우스에는 데이터 마이닝을 수행하는 데 필요한 뷰가 포함되어 있으므로 큐브의 집계 및 차원 대신 이러한 뷰를 데이터 마이닝에 사용할 수 있습니다.  
  
-   메모리 내 또는 PowerPivot 데이터를 직접 사용하여 데이터 마이닝 모델을 작성할 수 없습니다.  
  
 데이터 원본은 서버 또는 공급자와 일반적인 유형의 데이터만 식별합니다. 데이터 서식 및 집계를 변경하려면 데이터 원본 뷰 개체를 사용합니다.  
  
 데이터 원본의 데이터를 처리하는 방식을 제어하려면 파생 열 또는 계산을 추가하거나, 집계를 수정하거나, 데이터 원본 뷰의 데이터에 있는 열 이름을 바꾸면 됩니다. 마이닝 구조 열을 수정하거나 마이닝 모델 열의 수준에서 모델링 플래그 및 필터를 사용하여 데이터 다운스트림 작업을 수행할 수도 있습니다.  
  
 데이터 정리가 필요한 경우 또는 추가 변수를 만들거나 데이터 형식을 변경하거나 대체 집계를 만들기 위해 데이터 웨어하우스의 데이터를 수정해야 하는 경우 데이터 마이닝을 지원하는 추가 프로젝트 유형을 만들어야 할 수 있습니다. 관련 프로젝트에 대한 자세한 내용은 [데이터 마이닝 솔루션 관련 프로젝트](data-mining-solutions.md)를 참조하세요.  
  

  
###  <a name="data-source-views"></a><a name="bkmk_DSV"></a>데이터 원본 뷰  
 데이터 원본에 대한 연결을 정의한 후에는 모델과 관련된 특정 데이터를 식별하는 뷰를 만듭니다.  
  
 데이터 원본 뷰를 사용하면 데이터 원본의 데이터가 마이닝 모델에 제공되는 방식을 사용자 지정할 수도 있습니다. 데이터의 구조를 수정하여 프로젝트에 보다 적절하게 만들거나 특정 종류의 데이터만 선택할 수 있습니다.  
  
 예를 들어 데이터 원본 뷰 편집기를 사용하여 다음을 수행할 수 있습니다.  
  
-   날짜 부분, 부분 문자열 등의 파생 열 만들기  
  
-   GROUP BY와 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 값 집계  
  
-   일시적으로 데이터를 제한하거나 데이터 샘플링  
  
 데이터 원본 뷰 내에서 데이터를 수정하는 방법에 대한 자세한 내용은 [다차원 모델의 데이터 원본 뷰](../multidimensional-models/data-source-views-in-multidimensional-models.md)를 참조하세요.  
  
> [!WARNING]  
>  데이터를 필터링하려는 경우 데이터 원본 뷰에서 작업을 수행할 수 있지만 마이닝 모델 수준에서 데이터에 대한 필터를 만들 수도 있습니다. 필터 정의는 마이닝 모델과 함께 저장되므로 모델 필터를 사용하면 모델 학습에 사용된 데이터를 보다 쉽게 확인할 수 있습니다. 또한 여러 가지 필터 조건을 사용하여 여러 개의 관련 모델을 만들 수 있습니다. 자세한 내용은 [마이닝 모델에 대한 필터&#40;Analysis Services - 데이터 마이닝&#41;](mining-models-analysis-services-data-mining.md)를 참조하세요.  
  
 사용자가 만든 데이터 원본 뷰는 분석에 직접 사용되지 않는 추가 데이터를 포함할 수 있습니다. 예를 들어 테스트, 예측 또는 드릴스루에 사용되는 데이터 원본 뷰 데이터에 추가할 수 있습니다. 이러한 용도에 대한 자세한 내용은 [테스트 및 유효성 검사&#40;데이터 마이닝&#41;](testing-and-validation-data-mining.md) 및 [드릴스루](drillthrough-queries-data-mining.md)템플릿을 사용하여 데이터 마이닝 프로젝트를 작성할 수 있습니다.  
  

  
###  <a name="mining-structures"></a><a name="bkmk_Structures"></a>마이닝 구조  
 데이터 원본 및 데이터 원본 뷰를 만든 경우 프로젝트 내에서 *마이닝 구조* 를 정의하여 비즈니스 문제와 가장 관련이 있는 데이터 열을 선택해야 합니다. 마이닝 구조는 프로젝트에 실제로 모델링, 학습 및 테스트에 사용해야 하는 데이터 원본 뷰의 데이터 열을 알려 줍니다.  
  
 새 마이닝 구조를 추가하려면 데이터 마이닝 마법사를 시작합니다. 이 마법사는 마이닝 구조를 자동으로 정의하고 데이터 선택 과정을 안내하며 선택적으로 초기 마이닝 모델을 구조에 추가할 수 있도록 합니다. 마이닝 구조 내에서 데이터 원본 뷰 또는 OLAP 큐브의 테이블 및 열을 선택하고 테이블 간의 관계를 정의합니다(데이터에 중첩 테이블이 있는 경우).  
  
 선택한 데이터는 관계형 데이터 원본을 사용하는지 또는 OLAP(온라인 분석 처리) 데이터 원본을 사용하는지에 따라 데이터 마이닝 마법사에서 아주 다르게 표시됩니다.  
  
-   관계형 데이터 원본에서 데이터를 선택한 경우에는 마이닝 구조를 쉽게 설정할 수 있습니다. 데이터 원본 뷰의 데이터에서 열을 선택하고 별칭과 같은 추가 사용자 지정 항목을 설정하거나 열의 값을 그룹화 또는 범주화할 방법을 정의하면 됩니다. 자세한 내용은 [관계형 마이닝 구조 만들기](create-a-relational-mining-structure.md)를 참조하세요.  
  
-   OLAP 큐브의 데이터를 사용하려면 마이닝 구조가 OLAP 솔루션과 동일한 데이터베이스에 있어야 합니다.  마이닝 구조를 만들려면 OLAP 솔루션의 차원 및 관련 측정값에서 특성을 선택합니다. 일반적으로 숫자 값은 측정값에 있고 범주 변수는 차원에 있습니다. 자세한 내용은 [OLAP 마이닝 구조 만들기](create-an-olap-mining-structure.md)를 참조하세요.  
  
-   DMX를 사용하여 마이닝 구조를 정의할 수도 있습니다. 자세한 내용은 [DMX&#40;Data Mining Extensions&#41; 데이터 정의 문](/sql/dmx/dmx-statements-data-definition)을 참조하세요.  
  
 초기 마이닝 구조를 만든 후에는 구조 열을 복사하거나 수정하거나 별칭을 지정할 수 있습니다.  
  
 각 마이닝 구조는 여러 마이닝 모델을 포함할 수 있습니다. 따라서 작업을 완료한 후 마이닝 구조를 다시 열고 [Data Mining Designer](data-mining-designer.md) 를 사용하여 구조에 다른 마이닝 모델을 추가할 수 있습니다.  
  
 또한 데이터를 모델 작성에 사용되는 학습 데이터 집합과 마이닝 모델의 테스트 또는 유효성 검사에 사용할 홀드아웃 데이터 집합으로 구분할 수 있습니다.  
  
> [!WARNING]  
>  시계열 모델과 같은 일부 모델 유형은 학습에 연속된 일련의 데이터가 필요하기 때문에 홀드아웃 데이터 집합 만들기를 지원하지 않습니다. 자세한 내용은 [Training and Testing Data Sets](training-and-testing-data-sets.md)을 참조하세요.  
  
  
  
###  <a name="mining-models"></a><a name="bkmk_Models"></a>마이닝 모델  
 마이닝 모델은 데이터에 사용할 분석 방법이나 알고리즘을 정의합니다. 각 마이닝 구조에는 하나 이상의 마이닝 모델을 추가할 수 있습니다.  
  
 요구 사항에 따라 많은 모델을 단일 프로젝트에 통합하거나 각 유형의 모델 또는 분석 태스크에 대한 별도의 프로젝트를 만들 수 있습니다.  
  
 구조 및 모델을 만든 후에는 데이터 원본 뷰에서 데이터의 수학적 모델을 생성하는 알고리즘을 통해 데이터를 실행하여 각 모델을 *처리* 합니다. 이 프로세스를 *모델 학습*이라고도 합니다. 자세한 내용은 [처리 요구 사항 및 고려 사항&#40;데이터 마이닝&#41;](processing-requirements-and-considerations-data-mining.md)을 참조하세요.  
  
 모델을 처리한 후에는 마이닝 모델을 시각적으로 탐색하고 모델에 대한 예측 쿼리를 만들 수 있습니다. 학습 프로세스에서 데이터가 캐시된 경우 *드릴스루* 쿼리를 사용하여 모델에 사용된 사례에 대한 세부 정보를 반환할 수 있습니다.  
  
 프로덕션에 모델을 사용하려는 경우(예: 예측하는 데 사용하거나 일반 사용자의 탐색에 사용하려는 경우) 모델을 다른 서버에 배포할 수 있습니다. 나중에 모델을 다시 처리해야 하는 경우 기본 마이닝 구조의 정의와 데이터 원본 및 데이터 원본 뷰의 정의를 동시에 내보내야 합니다.  
  
 또한 모델을 배포할 때 구조 및 모델에 올바른 처리 옵션이 설정되었는지, 그리고 잠재적 사용자에게 쿼리를 수행하거나 모델을 보거나 구조 또는 모델 데이터로 드릴스루하는 데 필요한 권한이 있는지 확인해야 합니다. 자세한 내용은 [보안 개요&#40;데이터 마이닝&#41;](security-overview-data-mining.md)를 참조하세요.  
  
 
  
##  <a name="using-the-completed-data-mining-project"></a><a name="bkmk_Complete"></a>완성 된 데이터 마이닝 프로젝트 사용  
 이 섹션에서는 완료된 데이터 마이닝 프로젝트를 사용하는 방법을 요약하여 설명합니다. 정확도 차트를 만들고, 데이터에 대해 탐색 및 유효성 검사를 수행하고, 사용자가 데이터 마이닝 패턴을 사용할 수 있도록 할 수 있습니다.  
  
> [!WARNING]  
>  데이터 마이닝 모델에 사용하는 차트, 쿼리 및 시각화 요소는 데이터 마이닝 프로젝트의 일부로 저장되지 않으며 배포할 수 없습니다. 이러한 개체를 유지해야 하는 경우 제공된 콘텐츠를 저장하거나 각 개체에 대해 설명된 대로 스크립팅해야 합니다.  
  
 
  
###  <a name="view-and-explore-models"></a><a name="bkmk_ViewExplore"></a> View and Explore Models  
 모델을 만든 후에는 시각적 도구와 쿼리를 사용하여 모델에서 패턴을 탐색하고 기본 패턴 및 통계에 대한 자세한 정보를 확인할 수 있습니다. **의 데이터 마이닝 디자이너에 있는** 마이닝 모델 뷰어 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 탭에서는 각 마이닝 모델 유형에 대해 마이닝 모델을 탐색하는 데 사용할 수 있는 뷰어를 제공합니다.  
  
 이러한 시각화 요소는 일시적이므로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 세션을 종료할 때 저장하지 않고 닫힙니다. 따라서 이러한 시각화 요소를 프레젠테이션이나 이후의 분석에 사용하기 위해 다른 애플리케이션으로 내보내야 하는 경우 뷰어 인터페이스의 각 탭이나 창에 제공된 **복사** 명령을 사용합니다.  
  
 Excel용 데이터 마이닝 추가 기능에서도 모델을 Visio 다이어그램으로 표시하고 Visio 도구를 사용하여 주석을 달거나 다이어그램을 수정하는 데 사용할 수 있는 Visio 템플릿을 제공합니다. 자세한 내용은 [Microsoft Office 2007용 Microsoft SQL Server 2008 SP2 데이터 마이닝 추가 기능](https://www.microsoft.com/download/details.aspx?id=8569)을 참조하세요.
  
###  <a name="test-and-validate-models"></a><a name="bkmk_Validate"></a> Test and Validate Models  
 모델을 만든 후 결과를 조사하여 가장 적합한 모델을 결정할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 마이닝 모델을 직접 비교하고 가장 정확하거나 유용한 마이닝 모델을 선택하는 데 사용할 수 있는 도구를 제공하는 데 사용되는 여러 차트를 제공합니다. 이러한 도구에는 리프트 차트, 수익 차트 및 분류 행렬이 포함됩니다. 데이터 마이닝 디자이너의 **마이닝 정확도 차트** 를 사용하여 이 차트를 생성할 수 있습니다.  
  
 교차 유효성 검사 보고서를 통해 데이터를 반복적으로 서브샘플링하여 모델이 특정 데이터 집합에 편향되어 있는지 확인할 수도 있습니다. 또한 보고서에서 제공되는 통계를 사용하여 모델을 객관적으로 비교하고 학습 데이터의 품질을 평가할 수 있습니다.  
  
 이러한 보고서 및 차트는 프로젝트와 함께 저장되거나 ssASnoversion 데이터베이스에 저장되지 않으므로 결과를 유지하거나 복제하려면 결과를 저장하거나 DMX 또는 AMO를 사용하여 개체를 스크립팅해야 합니다. 교차 유효성 검사에 저장 프로시저를 사용할 수도 있습니다.  
  
 자세한 내용은 [테스트 및 유효성 검사&#40;데이터 마이닝&#41;](testing-and-validation-data-mining.md)템플릿을 사용하여 데이터 마이닝 프로젝트를 작성할 수 있습니다.  
  

  
###  <a name="create-predictions"></a><a name="bkmk_Predict"></a>예측 만들기  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 예측을 만드는 데 기본적으로 사용되고 쉽게 스크립팅할 수 있는 DMX(Data Mining Extensions)라는 쿼리 언어를 제공합니다. DMX 예측 쿼리를 쉽게 작성할 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 사용할 수 있는 쿼리 작성기를 제공합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에는 쿼리 편집기용 DMX 템플릿도 많이 있습니다. 예측 쿼리를 처음 사용하는 경우 데이터 마이닝 디자이너와 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 제공되는 쿼리 작성기를 사용하는 것이 좋습니다. 자세한 내용은 [Data Mining Tools](data-mining-tools.md)을 참조하세요.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 만든 예측은 유지되지 않으므로 쿼리가 복잡하거나 결과를 재현해야 하는 경우 예측 쿼리를 DMX 쿼리 파일에 저장하거나 예측 쿼리를 스크립팅하거나 쿼리를 Integration Services 패키지의 일부로 포함하는 것이 좋습니다.  
  
 
  
##  <a name="programmatic-access-to-data-mining-objects"></a><a name="bkmk_API"></a> 데이터 마이닝 개체에 대한 프로그래밍 방식 액세스  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 프로그래밍 방식으로 데이터 마이닝 프로젝트 및 개체 작업을 할 때 사용할 수 있는 여러 도구를 제공합니다. DMX 언어는 데이터 원본 및 데이터 원본 뷰를 만들고 데이터 마이닝 구조 및 모델을 생성, 학습 및 사용하는 데 사용할 수 있는 문을 제공합니다. 자세한 내용은 [DMX&#40;Data Mining Extensions&#41; 참조](/sql/dmx/data-mining-extensions-dmx-reference)를 참조하세요.  
  
 ASSL(Analysis Services Scripting Language) 또는 AMO(Analysis Management Objects)를 사용하여 이러한 태스크를 수행할 수도 있습니다. 자세한 내용은 [Analysis Services에서 XMLA를 사용하여 개발](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)을 참조하세요.  
  
  
  
## <a name="related-tasks"></a>관련 작업  
 다음 항목에서는 데이터 마이닝 마법사를 사용하여 데이터 마이닝 프로젝트와 관련 개체를 만드는 방법에 대해 설명합니다.  
  
|작업|토픽|  
|-----------|------------|  
|마이닝 구조 열로 작업하는 방법에 대해 설명합니다.|[관계형 마이닝 구조 만들기](create-a-relational-mining-structure.md)|  
|새 마이닝 모델을 추가하고 구조 및 모델을 처리하는 방법에 대해 자세히 설명합니다.|[구조에 마이닝 모델 추가&#40;Analysis Services - 데이터 마이닝&#41;](add-mining-models-to-a-structure-analysis-services-data-mining.md)|  
|마이닝 모델을 작성하는 알고리즘을 사용자 지정하는 데 도움이 되는 리소스에 대한 링크를 제공합니다.|[마이닝 모델 및 구조 사용자 지정](customize-mining-models-and-structure.md)|  
|각 마이닝 모델 뷰어 관련 정보에 대한 링크를 제공합니다.|[데이터 마이닝 모델 뷰어](data-mining-model-viewers.md)|  
|리프트 차트, 수익 차트 또는 분류표를 만들거나 마이닝 구조를 테스트하는 방법에 대해 설명합니다.|[테스트 및 유효성 검사&#40;데이터 마이닝&#41;](testing-and-validation-data-mining.md)|  
|처리 옵션 및 사용 권한에 대해 설명합니다.|[데이터 마이닝 개체 처리](processing-data-mining-objects.md)|  
|Analysis Services에 대한 자세한 정보를 제공합니다.|[다차원 model 데이터베이스&#40;SSAS&#41;](../multidimensional-models/multidimensional-model-databases-ssas.md)|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 디자이너](data-mining-designer.md)   
 [SQL Server Data Tools &#40;SSDT&#41;를 사용 하 여 다차원 모델 만들기](../multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [작업 영역 데이터베이스&#40;SSAS 테이블 형식&#41;](../tabular-models/workspace-database-ssas-tabular.md)  
  
  
