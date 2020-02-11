---
title: 데이터 마이닝 마법사 (Analysis Services 데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], data mining
- OLAP [Analysis Services], mining models
- Data Mining Wizard
- relational mining models [Analysis Services]
ms.assetid: d5fea90f-5f38-4639-8851-7707f6606a12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb853898d91533a61ae220ff2d73c032f2c65330
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084734"
---
# <a name="data-mining-wizard-analysis-services---data-mining"></a>데이터 마이닝 마법사(Analysis Services - 데이터 마이닝)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 마이닝 마법사는 데이터 마이닝 프로젝트에 새 마이닝 구조를 추가할 때마다 시작 됩니다. 이 마법사를 사용하면 데이터 원본을 선택하고, 분석에 사용할 데이터를 정의하는 데이터 원본 뷰를 설정한 다음 초기 모델을 만들 수 있습니다.  
  
 마법사의 마지막 단계에서는 원하는 경우 데이터를 학습 및 테스트 집합으로 나누고 드릴스루와 같은 기능을 사용하도록 설정할 수 있습니다.  
  
## <a name="what-to-know-before-you-start"></a>시작하기 전에 확인할 사항  
 마법사를 시작하기 전에 확인해야 하는 사항은 다음과 같습니다.  
  
-   데이터 마이닝 구조 및 모델을 관계형 데이터베이스에서 작성합니까 아니면 OLAP 데이터베이스의 기존 큐브에서 작성합니까?  
  
-   사례 레코드를 고유하게 식별하는 키가 들어 있는 열은 무엇입니까?  
  
-   예측에 사용할 열 또는 특성은 무엇입니까? 분석에 대한 입력으로 사용하기에 적합한 열 또는 특성은 무엇입니까?  
  
-   어떤 알고리즘을 사용해야 합니까? 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 제공 하는 알고리즘에는 서로 다른 특징이 있으며 다른 결과가 생성 됩니다. 각 데이터 집합에 대해 하나의 모델만 사용할 수 있는 것은 아니므로 원하는 대로 다양한 모델을 추가해 볼 수 있습니다.  
  
-   통합된 데이터 집합에서 모델을 테스트할 수 있어야 합니까? 그런 경우 일부 데이터를 테스트용으로 따로 떼어놓는 옵션을 사용하는 것이 좋습니다. 백분율을 선택할 수 있으며 원하는 경우 지정된 행 수로 상한을 정할 수 있습니다.  
  
##  <a name="BKMK_Using_DM_Wizard"></a>데이터 마이닝 마법사 시작  
 데이터 마이닝 마법사를 사용하려면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 데이터 마이닝 또는 OLAP 프로젝트가 하나 이상 포함된 솔루션을 열어야 합니다.  
  
-   솔루션이 데이터 마이닝을 사용할 준비가 되어 있는 경우 솔루션 탐색기에서 **마이닝 구조** 노드를 마우스 오른쪽 단추로 클릭하고 **새 마이닝 구조** 를 선택하면 마법사가 시작됩니다.  
  
-   솔루션에 기존 프로젝트가 포함되어 있지 않은 경우 새 데이터 마이닝 프로젝트를 추가할 수 있습니다. 
  **파일** 메뉴에서 **새로 만들기**를 선택한 다음 **프로젝트**를 선택합니다. 
  **Analysis Services 다차원 및 데이터 마이닝 프로젝트**템플릿을 선택합니다.  
  
-   Analysis Services 가져오기 마법사를 사용하여 기존 데이터 마이닝 솔루션의 메타데이터를 가져올 수도 있습니다. 하지만 개별 개체를 가져오도록 선택할 수는 없습니다. 모든 큐브, 데이터 원본 뷰 등이 포함된 전체 데이터베이스를 가져와야 합니다. 가져오기를 통해 만들어지는 새 솔루션은 자동으로 로컬 기본 데이터베이스를 사용하도록 구성됩니다. 개체를 처리하거나 찾아보기 전에 다른 인스턴스를 사용하도록 이 설정을 변경할 수 있습니다. 이전 버전의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 가져오는 경우 공급자에 대한 참조를 업데이트해야 합니다.  
  
 다음에는 마이닝 구조 및 이와 연결된 하나의 데이터 마이닝 모델을 만듭니다. 마이닝 구조만 만들고 모델은 나중에 추가할 수도 있지만 일반적으로 테스트 모델을 먼저 만드는 것이 더 편리합니다.  
  
###  <a name="BKMK_Relational"></a>관계형 마이닝 모델과 OLAP 마이닝 모델 비교  
 다음으로는 관계형 데이터 원본을 사용할지 아니면 다차원(OLAP) 데이터를 기반으로 모델을 만들지 선택해야 합니다.  
  
 이 시점에서 데이터 원본이 관계형인지, 아니면 큐브에 있는지에 따라 데이터 마이닝 마법사는 두 경로로 나뉩니다. 데이터 선택 프로세스를 제외 하 고 다른 모든 항목은 알고리즘 선택, 홀드 아웃 데이터 집합을 추가 하는 기능 등의 모든 기능을 제공 합니다. 하지만 큐브 데이터를 선택 하는 것은 관계형 데이터를 사용 하는 것 보다 약간 더 복잡 합니다. 큐브를 기반으로 모델을 만드는 경우 마지막에 몇 가지 옵션을 더 선택해야 합니다.  
  
 각 옵션에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
 [관계형 마이닝 구조 만들기](create-a-relational-mining-structure.md)  
 관계형 데이터 마이닝 모델을 작성할 때 결정하는 사항을 살펴봅니다.  
  
 [OLAP 마이닝 구조 만들기](create-an-olap-mining-structure.md)  
 OLAP 큐브에서 데이터를 선택하는 경우의 추가 옵션과 선택 사항에 대해 설명합니다.  
  
> [!NOTE]  
>  데이터 마이닝을 위해 큐브 또는 OLAP 데이터베이스가 반드시 필요한 것은 아닙니다. 데이터가 큐브에 이미 저장되어 있거나 OLAP 차원 또는 OLAP 집계/계산 결과를 마이닝하려는 경우가 아니면 데이터 마이닝에 관계형 테이블 또는 데이터 원본을 사용하는 것이 좋습니다.  
  
### <a name="choosing-an-algorithm"></a>알고리즘 선택  
 다음에는 데이터를 처리할 때 사용할 알고리즘을 결정해야 합니다. 이 결정은 내리기 어려운 결정일 수 있습니다. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 제공하는 각 알고리즘은 기능이 서로 다르며 서로 다른 결과를 생성하므로 사용자의 데이터와 비즈니스 문제에 가장 적합한 알고리즘을 결정하려면 여러 모델을 실험해 보는 것이 좋습니다. 알고리즘별로 가장 적합한 태스크에 대한 설명을 보려면 다음 항목을 참조하십시오.  
  
 [데이터 마이닝 알고리즘 &#40;Analysis Services 데이터 마이닝&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
 다양한 알고리즘을 사용하여 여러 모델을 만들거나 알고리즘의 매개 변수를 변경하여 다양한 모델을 만들 수 있습니다. 선택한 알고리즘으로만 제한되는 것이 아니므로 하나의 데이터에 대해 여러 가지 다른 모델을 만드는 것이 좋습니다.  
  
### <a name="define-the-data-used-for-modeling"></a>모델링에 사용되는 데이터 정의  
 원본에서 데이터를 선택하는 것 외에도 데이터 원본 뷰에서 *사례 데이터*를 포함하는 테이블을 지정해야 합니다. 사례 테이블은 데이터 마이닝 모델을 학습하는 데 사용되므로 고객 및 고객의 인구 통계 정보와 같이 분석할 엔터티를 포함해야 합니다. 각 사례는 고유해야 하며 *사례 키*로 식별할 수 있어야 합니다.  
  
 사례 테이블 지정 외에도 데이터에 *중첩 테이블* 을 포함할 수 있습니다. 중첩 테이블에는 일반적으로 고객이 수행한 트랜잭션 또는 엔터티와 다 대 일 관계에 있는 특성과 같은 사례 테이블의 엔터티에 대한 추가 정보가 포함되어 있습니다. 예를 들어 **Customers** 사례 테이블에 조인된 중첩 테이블에는 각 고객이 구매한 제품 목록이 포함될 수 있습니다. 웹 사이트에 대한 트래픽을 분석하는 모델에서 중첩 테이블은 사용자가 방문한 페이지 시퀀스를 포함할 수 있습니다. 자세한 내용은 [중첩 테이블&#40;Analysis Services - 데이터 마이닝&#41;](nested-tables-analysis-services-data-mining.md)을 참조하세요.  
  
### <a name="additional-features"></a>추가 기능  
 적절한 데이터를 선택하고 데이터 원본을 올바르게 구성할 수 있도록 데이터 마이닝 마법사는 다음과 같은 추가 기능을 제공합니다.  
  
-   **데이터 형식 자동 검색**: 마법사는 열 값의 고유성 및 분포를 검사 한 다음 최적의 데이터 형식을 권장 하 고 데이터의 사용 유형을 제안 합니다. 목록에서 값을 선택하여 이러한 제안을 무시할 수 있습니다.  
  
-   **변수 제안**: 대화 상자를 클릭 하 여 모델에 포함 된 열에서 상관 관계를 계산 하는 분석기를 시작 하 고, 지금 까지의 모델 구성을 고려 하 여 열이 결과 특성을 예측 변수 수 있는지 여부를 확인 합니다. 다른 값을 입력하여 이러한 제안을 무시할 수 있습니다.  
  
-   **기능 선택**: 대부분의 알고리즘은 적절 한 예측 변수 열을 자동으로 검색 하 여 해당 하는 것을 사용 합니다. 값이 너무 많이 포함된 열의 경우 데이터 카디널리티를 줄이고 의미 있는 패턴을 찾는 기회를 늘리기 위해 *기능 선택* 이 적용됩니다. 모델 매개 변수를 사용하여 기능 선택 동작을 조정할 수 있습니다.  
  
-   **자동 큐브 조각화**: 마이닝 모델이 OLAP 데이터 원본을 기반으로 하는 경우 큐브 특성을 사용 하 여 모델을 조각화 하는 기능이 자동으로 제공 됩니다. 이 기능은 큐브 데이터의 하위 집합을 기반으로 모델을 만드는 데 유용합니다.  
  
### <a name="completing-the-wizard"></a>마법사 완료  
 마법사의 마지막 단계는 마이닝 구조 및 관련 마이닝 모델의 이름을 지정하는 것입니다. 만들어진 모델의 유형에 따라 다음과 같은 옵션을 선택할 수도 있습니다.  
  
-   
  **드릴스루 허용**을 선택하는 경우 모델에 *드릴스루* 기능이 설정됩니다. 적절한 권한이 있는 사용자는 드릴스루 기능을 통해 모델을 작성하는 데 사용된 원본 데이터를 탐색할 수 있습니다.  
  
-   OLAP 모델을 작성하는 경우 **새 마이닝 모델 큐브 만들기**또는 **데이터 마이닝 차원 만들기**옵션을 선택할 수 있습니다. 이러한 옵션을 사용하면 더 쉽게 완성된 모델을 검색하고 기본 데이터로 드릴스루할 수 있습니다.  
  
 데이터 마이닝 마법사를 완료한 후에는 데이터 마이닝 디자이너를 사용하여 마이닝 구조 및 모델을 수정하거나, 모델의 정확도를 보거나, 구조 및 모델의 특징을 보거나, 모델을 사용하여 예측을 수행합니다.  
  
 [맨 위로 이동](#BKMK_Using_DM_Wizard)  
  
## <a name="related-content"></a>관련 내용  
 데이터 마이닝 모델을 만들 때 결정해야 하는 사항에 대해 더 자세히 알아보려면 다음 링크를 참조하십시오.  
  
 [데이터 마이닝 알고리즘 &#40;Analysis Services 데이터 마이닝&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
 [데이터 마이닝&#41;&#40;내용 유형](content-types-data-mining.md)  
  
 [데이터 마이닝 &#40;데이터 형식&#41;](data-types-data-mining.md)  
  
 [데이터 마이닝&#41;&#40;기능 선택](feature-selection-data-mining.md)  
  
 [누락 값 &#40;Analysis Services 데이터 마이닝&#41;](missing-values-analysis-services-data-mining.md)  
  
 [마이닝 모델에서의 드릴스루](drillthrough-on-mining-models.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 도구](data-mining-tools.md)   
 [데이터 마이닝 솔루션](data-mining-solutions.md)  
  
  
