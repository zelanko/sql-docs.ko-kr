---
title: Bike Buyer DMX 자습서 | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DMX [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- statements [DMX], tutorials
- Data Mining Extensions [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 4b634cc1-86dc-42ec-9804-a19292fe8448
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af20e220b4f1c2010606fec0d50e51025c73d31f
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53366725"
---
# <a name="bike-buyer-dmx-tutorial"></a>Bike Buyer DMX 자습서
  이 자습서에서는 DMX(Data Mining Extensions) 쿼리 언어를 사용하여 마이닝 모델을 만들고 학습하며 탐색하는 방법을 설명합니다. 이러한 마이닝 모델을 사용하여 고객이 자전거를 구입할 것인지 여부를 결정하는 예측을 만들 수 있습니다.  
  
 마이닝 모델은 가상 회사인 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 에 대한 데이터를 저장하는 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]예제 데이터베이스에 포함된 데이터에서 만들어집니다. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]는 규모가 큰 다국적 제조 회사입니다. 이 회사는 금속 및 합성 소재 자전거를 제조하여 북미, 유럽 및 아시아 시장에 판매합니다. 워싱턴 주 보셀에 위치한 본사에는 290명의 직원이 근무하고 있으며 각 지역 시장별로 영업 팀이 배치되어 있습니다.  
  
## <a name="tutorial-scenario"></a>자습서 시나리오  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]에서는 데이터 마이닝 기능을 사용하는 사용자 지정 응용 프로그램을 만들어 데이터 분석의 범위를 확장하기로 결정했습니다. 이 사용자 정의 애플리케이션을 만드는 목적은 다음과 같습니다.  
  
-   잠재 고객의 특정 특징을 입력으로 사용하여 해당 고객이 자전거를 구입할 것인지 여부 예측  
  
-   잠재 고객 목록뿐만 아니라 고객의 특징을 입력으로 사용하여 자전거를 구입할 고객 예측  
  
 첫 번째 경우 고객 등록 페이지에서 고객 데이터를 얻을 수 있으며 두 번째 경우 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 마케팅 부서에서 잠재 고객 목록을 얻을 수 있습니다.  
  
 또한 마케팅 부서에서는 거주지, 자녀 수 및 통근 거리와 같은 특징을 기반으로 기존 고객을 여러 범주로 그룹화하는 기능을 요청했습니다. 이 부서에서는 이러한 클러스터를 사용하여 마케팅 대상으로 삼을 특정 유형의 고객을 선택하는 데 도움이 되는지 알아보려고 합니다. 여기에는 추가 마이닝 모델이 필요합니다.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 이러한 작업을 수행할 수 있는 여러 가지 도구를 제공 합니다.  
  
-   DMX 쿼리 언어  
  
-   [Microsoft 의사 결정 트리 알고리즘](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md) 및 [Microsoft 클러스터링 알고리즘](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 쿼리 편집기  
  
 DMX(Data Mining Extensions)는 마이닝 모델을 만들고 작업할 때 사용할 수 있는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 제공하는 쿼리 언어입니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] 의사 결정 트리 알고리즘에서는 특정 고객이 자전거를 구입할 것인지 여부를 예측하는 데 사용할 수 있는 모델을 만듭니다. 결과 모델에서는 개인 고객이나 고객 테이블을 입력으로 사용할 수 있습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] 클러스터링 알고리즘에서는 공유 특징을 기반으로 고객을 그룹화할 수 있습니다. 이 자습서의 목표는 사용자 지정 애플리케이션에서 사용할 DMX 스크립트를 제공하는 것입니다.  
  
 **자세한 내용은 다음을 참조하세요.** [데이터 마이닝 솔루션](../../2014/analysis-services/data-mining/data-mining-solutions.md)  
  
## <a name="mining-structure-and-mining-models"></a>마이닝 구조 및 마이닝 모델  
 DMX 문을 만들려면 먼저 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 마이닝 모델 생성 시 사용하는 주요 개체를 이해하는 것이 중요합니다. 마이닝 구조는 마이닝 모델이 생성된 데이터 도메인을 정의하는 데이터 구조입니다. 단일 마이닝 구조에 같은 도메인을 공유하는 여러 개의 마이닝 모델이 포함될 수 있습니다. 마이닝 모델은 마이닝 구조로 나타나는 데이터에 마이닝 모델 알고리즘을 적용합니다.  
  
 마이닝 구조의 빌드 블록은 데이터 원본에 포함된 데이터를 설명하는 마이닝 구조 열입니다. 이러한 열에는 데이터 형식, 내용 유형, 데이터 배포 방법 등의 정보가 포함됩니다.  
  
 마이닝 모델에는 마이닝 구조에 설명된 키 열뿐만 아니라 나머지 열의 하위 집합도 포함되어야 합니다. 마이닝 모델은 각 열의 사용법을 정의하고 마이닝 모델을 만드는 데 사용되는 알고리즘을 정의합니다. 예를 들어 DMX에서 열을 Key 열이나 Predict 열로 지정할 수 있습니다. 열을 지정하지 않으면 Input 열로 간주됩니다.  
  
 DMX에서는 두 가지 방법으로 마이닝 모델을 만들 수 있습니다. CREATE MINING MODEL 문을 사용하여 마이닝 구조 및 연결 마이닝 모델을 함께 만들거나 CREATE MINING STRUCTURE 문을 사용하여 먼저 마이닝 구조를 만든 다음 ALTER STRUCTURE 문을 사용하여 구조에 마이닝 모델을 추가할 수 있습니다. 다음 표에서는 이러한 방법에 대해 설명합니다.  
  
 CREATE MINING MODEL  
 이 문을 사용하여 동일한 이름으로 마이닝 구조 및 연결 마이닝 모델을 함께 만들 수 있습니다. 이때 마이닝 모델 이름에 "Structure"가 추가되므로 마이닝 구조와 구분할 수 있습니다. 이 문은 단일 마이닝 모델을 포함하는 마이닝 구조를 만드는 경우 유용합니다.  
  
 자세한 내용은 [CREATE MINING MODEL&#40;DMX&#41;](/sql/dmx/create-mining-model-dmx)을 참조하세요.  
  
 ALTER MINING STRUCTURE  
 이 문을 사용하여 이미 서버에 있는 마이닝 구조에 마이닝 모델을 추가할 수 있습니다. 이 문은 여러 마이닝 모델을 포함하는 마이닝 구조를 만드는 경우 유용합니다. 단일 마이닝 구조에 마이닝 모델을 두 개 이상 추가하는 이유에는 여러 가지가 있습니다. 예를 들어 서로 다른 알고리즘을 사용하는 여러 마이닝 모델을 만들어 이 중 가장 적합한 알고리즘이 무엇인지 알아볼 수 있습니다. 또한 사용하는 알고리즘은 동일하지만 매개 변수 설정이 다른 마이닝 모델을 여러 개 만들어 최적의 매개 변수 설정을 찾을 수 있습니다.  
  
 자세한 내용은 [ALTER MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016)합니다.  
  
 이 자습서에서는 여러 마이닝 모델을 포함하는 마이닝 구조를 만들 것이므로 두 번째 방법을 사용합니다.  
  
 **자세한 내용은**  
  
 [Data Mining Extensions &#40;DMX&#41; 참조](/sql/dmx/data-mining-extensions-dmx-reference), [Select 문 이해 DMX](/sql/dmx/understanding-the-dmx-select-statement)합니다 [구조 및 사용법 DMX 예측 쿼리](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서는 다음 단원으로 이루어져 있습니다.  
  
 [1 단원: Bike Buyer 마이닝 구조 만들기](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md)  
 이 단원에서는 `CREATE` 문을 사용하여 마이닝 구조를 만드는 방법에 대해 설명합니다.  
  
 [2단원: Bike Buyer 마이닝 구조에 마이닝 모델 추가](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)  
 이 단원에서는 `ALTER` 문을 사용하여 마이닝 구조에 마이닝 모델을 추가하는 방법에 대해 설명합니다.  
  
 [3 단원: Bike Buyer 마이닝 구조 처리](../../2014/tutorials/lesson-3-processing-the-bike-buyer-mining-structure.md)  
 이 단원에서는 `INSERT INTO` 문을 사용하여 마이닝 구조 및 이에 연결된 마이닝 모델을 처리하는 방법에 대해 설명합니다.  
  
 [4 단원: Bike Buyer 마이닝 모델 찾아보기](../../2014/tutorials/lesson-4-browsing-the-bike-buyer-mining-models.md)  
 이 단원에서는 `SELECT` 문을 사용하여 마이닝 모델의 내용을 탐색하는 방법에 대해 설명합니다.  
  
 [5 단원: 예측 쿼리를 실행합니다.](../../2014/tutorials/lesson-5-executing-prediction-queries.md)  
 이 단원에서는 `PREDICTION JOIN` 문을 사용하여 마이닝 모델에 대한 예측을 만드는 방법에 대해 설명합니다.  
  
## <a name="requirements"></a>요구 사항  
 이 자습서를 사용하려면 먼저 다음을 설치해야 합니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]하십시오 [!INCLUDE[ssASversion10](../includes/ssasversion10-md.md)], [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터베이스. 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다.  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 공식 예제 데이터베이스를 설치하려면 [Microsoft SQL Sample Databases](https://go.microsoft.com/fwlink/?LinkId=88417) 페이지에서 설치할 데이터베이스를 선택합니다.  
  
> [!NOTE]  
>  자습서를 검토할 때는 문서 뷰어 도구 모음에 **다음 항목** 단추 및 **이전 항목** 단추를 추가하는 것이 좋습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Market Basket DMX 자습서](../../2014/tutorials/market-basket-dmx-tutorial.md)   
 [기본 데이터 마이닝 자습서](../../2014/tutorials/basic-data-mining-tutorial.md)  
  
  
