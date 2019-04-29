---
title: 시간 시계열 예측 DMX 자습서 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 38ea7c03-4754-4e71-896a-f68cc2c98ce2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1623f824c062c270268323fd45ebf0e9533c8788
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63044191"
---
# <a name="time-series-prediction-dmx-tutorial"></a>시계열 예측 DMX 자습서
  이 자습서에서는 시계열 마이닝 구조 및 3개의 사용자 지정 시계열 마이닝 모델을 만든 다음 이러한 모델을 사용하여 예측을 수행하는 방법에 대해 설명합니다.  
  
 마이닝 모델은 가상 회사인  [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 에 대한 데이터를 저장하는 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]예제 데이터베이스에 포함된 데이터를 기반으로 합니다. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]는 규모가 큰 다국적 제조 회사입니다.  
  
## <a name="tutorial-scenario"></a>자습서 시나리오  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]는 예상 매출을 생성하는 데이터 마이닝을 사용하기로 결정했습니다. 이미 몇 가지 지역 예측 모델을 빌드 했는지 자세한 내용은 참조 하세요. [단원 2: 예측 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)합니다. 그러나 영업부는 정기적으로 데이터 마이닝 모델을 새 매출 데이터로 업데이트해야 합니다. 또한 다른 예상을 제공할 모델을 사용자 지정해야 합니다.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 이 작업을 수행할 수 있는 여러 가지 도구를 제공 합니다.  
  
-   DMX(Data Mining Extensions) 쿼리 언어  
  
-   Microsoft 시계열 알고리즘  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 쿼리 편집기  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시계열 알고리즘은 시간 관련 데이터 예측에 사용할 수 있는 모델을 만듭니다. DMX(Data Mining Extensions)는 마이닝 모델 및 예측 쿼리를 만들 때 사용할 수 있는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 제공하는 쿼리 언어입니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서에서는 사용자가 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 마이닝 모델을 만드는 데 사용하는 개체를 잘 알고 있다고 가정합니다. 이전에 DMX를 사용하여 마이닝 구조 또는 마이닝 모델을 만든 적이 없는 경우에는 [Bike Buyer DMX Tutorial](../../2014/tutorials/bike-buyer-dmx-tutorial.md)를 참조하십시오.  
  
 이 자습서는 다음 단원으로 이루어져 있습니다.  
  
 [1단원: 시계열 마이닝 모델 및 마이닝 구조 만들기](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)  
 이 단원에서는 `CREATE MINING MODEL` 문을 사용하여 새 예측 모델 및 이와 관련된 마이닝 모델을 추가하는 방법에 대해 설명합니다.  
  
 [2단원: 시계열 마이닝 구조에 마이닝 모델 추가](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
 이 단원에서는 ALTER MINING STRUCTURE 문을 사용하여 시계열 구조에 새 마이닝 모델을 추가하는 방법에 대해 설명합니다. 시계열 분석에 사용된 알고리즘을 사용자 지정하는 방법에 대해서도 설명합니다.  
  
 [3단원: 처리 된 시계열 구조 및 모델](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
 이 단원에서는 `INSERT INTO` 문을 사용하고 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터베이스의 데이터로 구조를 채워서 모델을 학습하는 방법에 대해 설명합니다.  
  
 [4단원: DMX를 사용 하 여 시계열 예측 만들기](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
 이 단원에서는 시계열 예측을 만드는 방법에 대해 설명합니다.  
  
 [5단원: 모델의 시계열을 확장](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
 이 단원에서는 `EXTEND_MODEL_CASES` 매개 변수를 사용하여 예측할 때 새 데이터로 모델을 업데이트하는 방법에 대해 설명합니다.  
  
## <a name="requirements"></a>요구 사항  
 이 자습서를 사용하려면 먼저 다음을 설치해야 합니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터베이스  
  
 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다. 공식 예제 데이터베이스를 설치 하려면 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 이동 하세요 [ http://www.CodePlex.com/MSFTDBProdSamples ](https://go.microsoft.com/fwlink/?LinkId=88417) 또는 Microsoft SQL Server Product Samples 섹션에서 Microsoft SQL Server Samples and Community Projects 홈 페이지입니다. **Databases**, **Releases** 탭을 차례로 클릭한 다음 원하는 데이터베이스를 선택합니다.  
  
> [!NOTE]  
>  자습서를 검토할 때는 문서 뷰어 도구 모음에 **다음 항목** 단추 및 **이전 항목** 단추를 추가하는 것이 좋습니다.  
  
## <a name="see-also"></a>관련 항목  
 [기본 데이터 마이닝 자습서](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [중급 데이터 마이닝 자습서 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
