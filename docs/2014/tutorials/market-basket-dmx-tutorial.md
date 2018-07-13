---
title: Market Basket DMX 자습서 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DMX [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- statements [DMX], tutorials
- Data Mining Extensions [Analysis Services], tutorials
- market basket analysis [Analysis Services]
- tutorials [Data Mining]
- tutorials [DMX]
ms.assetid: 6e262a1d-c89e-4033-8368-46cf25168ef5
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b73a618c5318d88ec6ee09751e09327687d865f4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220583"
---
# <a name="market-basket-dmx-tutorial"></a>Market Basket DMX 자습서
  이 자습서에서는 DMX(Data Mining Extensions) 쿼리 언어를 사용하여 마이닝 모델을 만들고 학습하며 탐색하는 방법을 설명합니다. 이러한 마이닝 모델을 사용하여 동시에 구입되는 경향이 있는 제품을 설명하는 예측을 만들 수 있습니다.  
  
 마이닝 모델은 가상 회사인 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]에 대한 데이터를 저장하는 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 예제 데이터베이스에 포함된 데이터에서 만들어집니다. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]는 규모가 큰 다국적 제조 회사입니다. 이 회사는 금속 및 합성 소재 자전거를 제조하여 북미, 유럽 및 아시아 시장에 판매합니다. 워싱턴 주 보셀에 위치한 본사에는 290명의 직원이 근무하고 있으며 각 지역 시장별로 영업 팀이 배치되어 있습니다.  
  
## <a name="tutorial-scenario"></a>자습서 시나리오  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]에서는 고객이 동시에 구입하는 경향이 있는 제품 유형을 예측하는 기능인 데이터 마이닝을 사용하는 사용자 지정 응용 프로그램을 만들기로 했습니다. 사용자 지정 응용 프로그램의 목표는 제품 집합을 지정하고 지정한 제품과 함께 구입할 가능성이 있는 추가 제품을 예측할 수 있게 하는 것입니다. 그러면 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]에서 이러한 정보를 사용하여 웹 사이트에 "제안" 기능을 추가하고 고객에게 정보를 제공하는 방식을 더 효과적으로 구성하게 됩니다.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 이 작업을 수행할 수 있는 여러 가지 도구를 제공 합니다.  
  
-   DMX 쿼리 언어  
  
-   [Microsoft 연결 알고리즘](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 쿼리 편집기  
  
 DMX(Data Mining Extensions)는 마이닝 모델을 만들고 작업할 때 사용할 수 있는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 제공하는 쿼리 언어입니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] 연결 알고리즘은 함께 구입할 가능성이 있는 제품을 예측할 수 있는 모델을 만듭니다.  
  
 이 자습서의 목표는 사용자 지정 응용 프로그램에서 사용할 DMX 쿼리를 제공하는 것입니다.  
  
 **자세한 내용은:** [데이터 마이닝 솔루션](../../2014/analysis-services/data-mining/data-mining-solutions.md)  
  
## <a name="mining-structure-and-mining-models"></a>마이닝 구조 및 마이닝 모델  
 DMX 문을 만들려면 먼저 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 마이닝 모델 생성 시 사용하는 주요 개체를 이해하는 것이 중요합니다. 합니다 *마이닝 구조* 마이닝 모델이 생성 된 데이터 도메인을 정의 하는 데이터 구조입니다. 단일 마이닝 구조에는 여러 개 포함할 수 있습니다 *마이닝 모델* 는 같은 도메인을 공유 합니다. 마이닝 모델은 마이닝 구조로 나타나는 데이터에 마이닝 모델 알고리즘을 적용합니다.  
  
 마이닝 구조의 빌드 블록은 데이터 원본에 포함된 데이터를 설명하는 마이닝 구조 열입니다. 이러한 열에는 데이터 형식, 내용 유형, 데이터 배포 방법 등의 정보가 포함됩니다.  
  
 마이닝 모델에는 마이닝 구조에 설명된 키 열뿐만 아니라 나머지 열의 하위 집합도 포함되어야 합니다. 마이닝 모델은 각 열의 사용법을 정의하고 마이닝 모델을 만드는 데 사용되는 알고리즘을 정의합니다. 예를 들어 DMX에서 열을 Key 열이나 Predict 열로 지정할 수 있습니다. 열을 지정하지 않으면 Input 열로 간주됩니다.  
  
 DMX에서는 두 가지 방법으로 마이닝 모델을 만들 수 있습니다. `CREATE MINING MODEL` 문을 사용하여 마이닝 구조 및 연결된 마이닝 모델을 함께 만들거나 `CREATE MINING STRUCTURE` 문을 사용하여 먼저 마이닝 구조를 만든 다음 `ALTER STRUCTURE` 문을 사용하여 구조에 마이닝 모델을 추가할 수 있습니다. 이러한 방법은 아래에서 설명합니다.  
  
 `CREATE MINING MODEL`  
 이 문을 사용하여 동일한 이름으로 마이닝 구조 및 연결 마이닝 모델을 함께 만들 수 있습니다. 이때 마이닝 모델 이름에 "Structure"가 추가되므로 마이닝 구조와 구분할 수 있습니다.  
  
 이 문은 단일 마이닝 모델을 포함하는 마이닝 구조를 만드는 경우 유용합니다.  
  
 자세한 내용은 [CREATE MINING MODEL&#40;DMX&#41;](/sql/dmx/create-mining-model-dmx)을 참조하세요.  
  
 CREATE MINING STRUCTURE  
 이 문을 사용하여 모델이 없는 새 마이닝 구조를 만듭니다.  
  
 CREATE MINING STRUCTURE를 사용하는 경우 같은 마이닝 구조를 기반으로 한 모델을 테스트하는 데 사용할 수 있는 홀드아웃 데이터 집합을 만들 수도 있습니다.  
  
 자세한 내용은 [CREATE MINING STRUCTURE&#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx)를 참조하세요.  
  
 `ALTER MINING STRUCTURE`  
 이 문을 사용하여 이미 서버에 있는 마이닝 구조에 마이닝 모델을 추가할 수 있습니다.  
  
 단일 마이닝 구조에 마이닝 모델을 두 개 이상 추가하는 이유에는 여러 가지가 있습니다. 예를 들어 서로 다른 알고리즘을 사용하는 여러 마이닝 모델을 만들어 이 중 가장 적합한 모델이 무엇인지 알아볼 수 있습니다. 또는 사용하는 알고리즘은 동일하지만 매개 변수 설정이 다른 마이닝 모델을 여러 개 만들어 최적의 매개 변수 설정을 찾을 수 있습니다.  
  
 자세한 내용은 참조 하세요. [ALTER MINING STRUCTURE &#40;DMX&#41;] ((~/dmx/alter-mining-structure-dmx.md).  
  
 이 자습서에서는 여러 마이닝 모델을 포함하는 마이닝 구조를 만들 것이므로 두 번째 방법을 사용합니다.  
  
 **자세한 내용은**  
  
 [Data Mining Extensions &#40;DMX&#41; 참조](/sql/dmx/data-mining-extensions-dmx-reference), [Select 문 이해 DMX](/sql/dmx/understanding-the-dmx-select-statement)합니다 [구조 및 사용법 DMX 예측 쿼리](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서는 다음 단원으로 이루어져 있습니다.  
  
 [1단원: Market Basket 마이닝 구조 만들기](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)  
 이 단원에서는 `CREATE` 문을 사용하여 마이닝 구조를 만드는 방법에 대해 설명합니다.  
  
 [2단원: Market Basket 마이닝 구조에 마이닝 모델 추가](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)  
 이 단원에서는 `ALTER` 문을 사용하여 마이닝 구조에 마이닝 모델을 추가하는 방법에 대해 설명합니다.  
  
 [3단원: Market Basket 마이닝 구조 처리](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
 이 단원에서는 `INSERT INTO` 문을 사용하여 마이닝 구조 및 이에 연결된 마이닝 모델을 처리하는 방법에 대해 설명합니다.  
  
 [4단원: Market Basket 예측 실행](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
 이 단원에서는 `PREDICTION JOIN` 문을 사용하여 마이닝 모델에 대한 예측을 만드는 방법에 대해 설명합니다.  
  
## <a name="requirements"></a>요구 사항  
 이 자습서를 사용하려면 먼저 다음을 설치해야 합니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터베이스  
  
 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다. 공식 예제 데이터베이스를 설치 하려면 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 이동 하세요 [ http://www.CodePlex.com/MSFTDBProdSamples ](http://go.microsoft.com/fwlink/?LinkId=88417) 또는 Microsoft SQL Server Product Samples 섹션에서 Microsoft SQL Server Samples and Community Projects 홈 페이지입니다. **Databases**, **Releases** 탭을 차례로 클릭한 다음 원하는 데이터베이스를 선택합니다.  
  
> [!NOTE]  
>  자습서를 검토할 때는 문서 뷰어 도구 모음에 **다음 항목** 단추 및 **이전 항목** 단추를 추가하는 것이 좋습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Bike Buyer DMX 자습서](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [기본 데이터 마이닝 자습서](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [3 단원: 시장 바구니 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
  
