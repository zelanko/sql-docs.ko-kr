---
title: 수익 차트 (Analysis Services 데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- accuracy, charting
- revenue, estimating
- benefits, estimating
- charts [Analysis Services]
- profit charts [Analysis Services]
ms.assetid: 760ee051-6fd8-48e3-8d2e-82db3ab45e45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a64eacb1219e239ad894d9922db5a5032ed525b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66083087"
---
# <a name="profit-chart-analysis-services---data-mining"></a>수익 차트(Analysis Services - 데이터 마이닝)
  수익 차트는 마이닝 모델 사용과 관련된 예상 수익성을 표시합니다. 예를 들어 비즈니스 시나리오에서 회사가 연락 해야 하는 고객을 모델에서 예측 하는 경우를 가정해 보겠습니다. 이 경우 수익 차트 정보에 타겟 메일링 캠페인 수행 비용을 추가합니다. 그런 다음 완성된 차트에서 고객에게 무작위로 연락하는 시나리오와 비교하여 고객을 올바르게 타게팅할 때 예상되는 수익을 확인할 수 있습니다.  
  
## <a name="build-a-profit-chart"></a>수익 차트 작성  
 수익 차트는 리프트 차트와 비슷합니다. 가장 먼저 리프트 차트를 만든 다음 비용 및 수익 정보를 추가합니다.  
  
 수익 차트를 추가하려면 기존 모델이 있어야 합니다.  
  
 이 예제에서는 타겟 메일링 의사 결정 트리 모델을 사용했습니다. 이 모델은 자전거를 구매할 가능성이 높은 고객을 식별합니다. 수익 극대화를 위해 몇 명의 고객을 타게팅해야 하는지 파악하기 위해 **수익 차트** 를 적용할 수 있습니다.  
  
 예제 모델이 없는 경우 [기본 데이터 마이닝 자습서](../../tutorials/basic-data-mining-tutorial.md)를 사용 하 여 만들 수 있습니다.  
  
1.  마이닝 정확도 차트 작성기를 엽니다.  
  
    -   SQL Server Management Studio에서 모델을 마우스 오른쪽 단추로 클릭하고 **리프트 차트 보기**를 선택합니다.  
  
    -   SQL Server Data Tools에서 모델을 만든 프로젝트를 열고 **마이닝 정확도 차트** 탭을 클릭합니다.  
  
2.  **입력 선택** 탭에서 모델을 선택하고 예측 가능한 특성 값을 선택합니다.  
  
     이 시나리오에서는 한 가지 값, 즉, [Bike Buyer] =1에 대한 정확한 예측 확률에만 관심이 있습니다.  
  
     하지만 다른 시나리오에서는 거짓 값도 정확하게 예측해야 할 수 있습니다. 예를 들어 의료 진단 테스트의 경우 거짓 긍정의 비용이 매우 크기 때문에 예측 확률에 거짓 긍정과 거짓 부정을 동등하게 고려해야 합니다. 이러한 시나리오에서는 모든 결과를 측정합니다.  
  
3.  테스트할 데이터 집합을 선택합니다. 이 예에서는 테스트 데이터베이스를 선택합니다.  
  
4.  이제 **리프트 차트** 탭을 클릭합니다.  
  
     리프트 차트가 자동으로 생성됩니다.  
  
5.  이 차트를 수익 차트로 변경하려면 **차트 종류** 목록에서 **수익 차트** 를 선택합니다.  
  
6.  차트 종류로 수익 차트로 선택하면 **수익 차트 설정** 대화 상자가 자동으로 열립니다.  
  
     이 대화 상자에서 타겟 메일링 캠페인과 연관된 비용 및 이익을 지정합니다. 이러한 예제의 차트에는 다음 값을 사용했습니다.  
  
    |설정|값|설명|  
    |-------------|-----------|--------------|  
    |**표본의**|20,000|총 대상 모집단에 대한 값 설정<br /><br /> 데이터베이스에 많은 고객이 있을 수 있지만 발송 비용을 절약하려면 응답할 가능성이 가장 높은 고객 20,000명만 타게팅해야 할 수 있습니다. 이 목록은 예측 쿼리를 실행하고 예측 모델별로 확률 결과를 정렬하여 얻을 수 있습니다.|  
    |**고정 비용**|500|20,000명의 고객들에게 타겟 메일링 캠페인을 한 번 제공할 때 드는 비용을 입력합니다. 여기에는 인쇄 또는 전자 메일 캠페인 설정 비용이 포함될 수 있습니다.|  
    |**개별 비용**|3|타겟 메일링 캠페인의 단위 비용을 입력합니다.<br /><br /> 모델에서 예측한 적절한 잠재 고객 수에 따라 20,000 이하의 숫자를 이 금액에 곱합니다.|  
    |**개인 당 수익**|400|성공적인 결과에서 예상할 수 있는 수익 또는 수입 금액을 나타내는 값을 입력합니다. 이 경우 카탈로그를 메일로 보내는 경우에는 액세서리 또는 자전거 $400 평균을 구입 하는 것으로 가정 합니다.<br /><br /> 이 금액은 높은 확률 사례와 관련된 총 수익을 산출하는 데 사용됩니다.|  
  
7.  필요한 매개 변수를 설정한 다음 **확인**을 클릭합니다.  
  
8.  차트가 업데이트되면서 수익 곡선이 표시됩니다.  
  
## <a name="understanding-the-profit-chart"></a>수익 차트 이해  
 다음 다이어그램에서는 이러한 매개 변수에 기반한 차트를 보여 줍니다. 차트의 Y축은 수익을 나타내고 X축은 회사에서 타겟 메일링 캠페인으로 연락한 고객의 백분율을 나타냅니다.  
  
 여기서 볼 수 있듯이, 수익 차트가 동일한 불연속 특성을 예측하는 경우 수익 차트를 사용하여 여러 모델을 비교할 수 있습니다.  
  
 ![3개의 모델을 비교하는 수익 차트](../media/dm14-profitchartupdated.gif "3개의 모델을 비교하는 수익 차트")  
  
 차트의 회색 수직선을 보십시오. 선을 클릭하고 끌면 도구 설명에 해당 지점에 포함된 타겟 모집단의 비율이 표시됩니다.  
  
 이 선을 끌면 **마이닝 범례** 가 업데이트되면서 세로 회색 선의 모집단 비율과 관련된 백분율 값, 수익 점수, 예측 확률이 표시됩니다.  
  
 예를 들어 이 모델을 사용하여 프로모션 자료를 발송할 대상을 결정하려는 경우 예측 확률을 기준으로 모집단의 25%만 타게팅할 것을 결정할 수 있습니다. 하지만 차트의 수익 곡선 아래의 영역이 40~70%에서 가장 높다는 것은 더 많은 사람들에게 발송할 경우 수익을 극대화할 수 있음을 나타내며, 전체 응답자 비율이 작을 경우에도 마찬가지입니다.  
  
## <a name="saving-charts"></a>차트 저장  
 정확도 차트 또는 수익 차트를 만들 경우 서버에 개체가 생성되지 않습니다. 대신, 기존 모델에 쿼리가 실행되고 뷰어에 결과가 렌더링됩니다. 결과를 저장해야 할 경우 차트 또는 결과를 Excel 또는 다른 파일로 복사해야 합니다.  
  
## <a name="related-content"></a>관련 내용  
 다음 항목에는 정확도 차트를 만들고 사용하는 방법에 대해 보다 자세한 내용이 나와 있습니다.  
  
|토픽|링크|  
|------------|-----------|  
|타겟 메일링 모델에 대한 리프트 차트를 만드는 방법을 보여 주는 연습을 제공합니다.|[기본 데이터 마이닝 자습서](../../tutorials/basic-data-mining-tutorial.md)<br /><br /> [리프트 차트를 사용하여 정확도 테스트&#40;기본 데이터 마이닝 자습서&#41;](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)|  
|관련 차트 종류에 대해 설명합니다.|[리프트 차트&#40;Analysis Services - 데이터 마이닝&#41;](lift-chart-analysis-services-data-mining.md)<br /><br /> [분류표&#40;Analysis Services - 데이터 마이닝&#41;](classification-matrix-analysis-services-data-mining.md)<br /><br /> [산점도&#40;Analysis Services - 데이터 마이닝&#41;](scatter-plot-analysis-services-data-mining.md)|  
|마이닝 모델 및 마이닝 구조에 대한 교차 유효성 검사를 설명합니다.|[교차 유효성 검사&#40;Analysis Services - 데이터 마이닝&#41;](cross-validation-analysis-services-data-mining.md)|  
|리프트 차트 및 기타 정확도 차트를 만드는 단계를 설명합니다.|[테스트 및 유효성 검사 태스크 및 방법&#40;데이터 마이닝&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝&#41;&#40;테스트 및 유효성 검사](testing-and-validation-data-mining.md)   
 [리프트 차트를 사용하여 정확도 테스트&#40;기본 데이터 마이닝 자습서&#41;](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
  
