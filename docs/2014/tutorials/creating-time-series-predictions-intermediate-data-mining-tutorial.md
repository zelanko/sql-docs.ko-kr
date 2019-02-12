---
title: 시계열 예측 (중급 데이터 마이닝 자습서) 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: fb22cffa-ac99-4d34-ac4a-9c93068e33e8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ca1aa4022931c78f6139a8058c05adc707af5e77
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027994"
---
# <a name="creating-time-series-predictions-intermediate-data-mining-tutorial"></a>시계열 예측 만들기(중급 데이터 마이닝 자습서)
  이 단원의 이전 태스크에서는 시계열 모델을 만들고 결과를 살펴보았습니다. 기본적으로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 항상 시계열 모델에 대한 5개의 예측으로 구성된 집합을 만들고 예측 값을 예측 차트의 일부분으로 표시합니다. 그러나 DMX(Data Mining Extensions) 예측 쿼리를 작성하여 예측을 만들 수도 있습니다.  
  
 이 태스크에서는 뷰어에서 본 것과 같은 예측을 생성하는 예측 쿼리를 만듭니다. 이 태스크에서는 사용자가 이미 기본 데이터 마이닝 자습서의 단원을 마쳤으며 예측 쿼리 작성기를 사용하는 방법에 익숙하다고 가정합니다. 이제 시계열 모델과 관련된 쿼리를 만드는 방법을 배웁니다.  
  
## <a name="creating-time-series-predictions"></a>시계열 예측 만들기  
 일반적으로 예측 쿼리를 만드는 첫 번째 단계는 마이닝 모델과 입력 테이블을 선택하는 것입니다. 그러나 시계열 모델에는 일반 예측을 위해 추가 입력이 필요하지 않습니다. 따라서 모델에 데이터를 추가하거나 데이터를 바꾸지 않는 한 예측을 만들 때 새로운 데이터 원본을 지정할 필요가 없습니다.  
  
 이 단원에서는 예측 단계 수를 지정해야 합니다. 특정 제품 및 지역 조합에 대한 예측을 얻기 위해 계열 이름을 지정할 수 있습니다.  
  
#### <a name="to-select-a-model-and-input-table"></a>모델과 입력 테이블을 선택하려면  
  
1.  에 **마이닝 모델 예측** 데이터 마이닝 디자이너의 탭에서 합니다 **마이닝 모델** 상자를 클릭 합니다 **모델 선택**합니다.  
  
2.  에 **마이닝 모델 선택** 대화 상자에서 Forecasting 구조를 확장을 선택 합니다 **Forecasting** 목록에서 모델 및 클릭 **확인**합니다.  
  
3.  무시 된 **입력 테이블 선택** 상자입니다.  
  
    > [!NOTE]  
    >  시계열 모델의 경우 교차 예측을 수행하지 않는 한 별도의 입력을 지정할 필요가 없습니다.  
  
4.  에 **원본** 그리드에서 열을 **마이닝 모델 예측** 탭, 첫 번째 빈 행의 셀을 클릭 한 다음 선택 **Forecasting 마이닝 모델**합니다.  
  
5.  에 **필드** 열 선택 **Model Region**합니다.  
  
     이렇게 하면 예측이 적용되는 모델 및 지역 조합을 나타내기 위해 예측 쿼리에 계열 식별자가 추가됩니다.  
  
6.  다음 빈 행을 클릭 합니다 **소스** 열을 선택한 후 **예측 함수**합니다.  
  
7.  에 **필드** 열 선택 **PredictTimeSeries**합니다.  
  
    > [!NOTE]  
    >  `Predict` 함수도 시계열 모델에 사용할 수 있습니다. 그러나 기본적으로 Predict 함수는 각 계열에 대해 하나의 예측만 만듭니다. 따라서 여러 예측 단계를 지정 하려면 사용 해야 합니다 **PredictTimeSeries** 함수입니다.  
  
8.  에 **마이닝 모델** 창, 마이닝 모델 열 선택 **크기.** 끌어 크기를 **조건/인수** 상자에 **PredictTimeSeries** 이전에 추가한 함수를 합니다.  
  
9. 클릭 합니다 **조건/인수** 뒤에 쉼표를 입력 **5**, 필드 이름 뒤에 오는 합니다.  
  
     텍스트를 **조건/인수** 상자에는 다음 이제 표시 됩니다.  
  
     `[Forecasting].[Amount],5`  
  
10. 에 **별칭** 열, 형식 `PredictAmount`합니다.  
  
11. 다음 빈 행을 클릭 합니다 **소스** 열을 선택한 후 **예측 함수** 다시 합니다.  
  
12. 에 **필드** 열 선택 **PredictTimeSeries**합니다.  
  
13. 에 **마이닝 모델** 창, Quantity 열을 선택한 다음으로 끌어 놓습니다 합니다 **조건/인수** 두 번째 상자 **PredictTimeSeries** 함수입니다.  
  
14. 클릭 합니다 **조건/인수** 뒤에 쉼표를 입력 **5**, 필드 이름 뒤에 오는 합니다.  
  
     텍스트를 **조건/인수** 상자에는 다음 이제 표시 됩니다.  
  
     `[Forecasting].[ Quantity],5`  
  
15. 에 **별칭** 열, 형식 `PredictQuantity`합니다.  
  
16. 클릭 **쿼리 결과 뷰로 전환**합니다.  
  
     쿼리 결과가 테이블 형식으로 표시됩니다.  
  
 열 값을 사용하는 결과 하나와 예측 함수에서 예측 값을 가져오는 결과 두 개를 합쳐 세 가지 유형의 결과를 쿼리 작성기에서 만들었습니다. 따라서 쿼리 결과에 세 개의 다른 열이 포함됩니다. 첫 번째 열에는 제품 및 지역 조합 목록이 포함됩니다. 두 번째 및 세 번째 열에는 각각 예측 결과의 중첩 테이블이 포함됩니다. 각 중첩 테이블에는 다음 표와 같은 시간 단계 및 예측 값이 포함됩니다.  
  
 결과 예(금액은 소수점 두 자리로 잘림):  
  
 **M200 Europe PredictAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|7/25/2008|99978.00|  
|8/25/2008|145575.07|  
|9/25/2008|116835.19|  
|10/25/2008|116537.38|  
|11/25/2008|107760.55|  
  
 **M200 Europe PredictQuantity**  
  
|$TIME|수량|  
|-----------|--------------|  
|7/25/2008|52|  
|8/25/2008|67|  
|9/25/2008|58|  
|10/25/2008|57|  
|11/25/2008|54|  
  
 **M200 North America - PredictAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|7/25/2008|348533.93|  
|8/25/2008|340097.98|  
|9/25/2008|257986.19|  
|10/25/2008|374658.24|  
|11/25/2008|379241.44|  
  
 **M200 North America-PredictQuantity**  
  
|$TIME|수량|  
|-----------|--------------|  
|7/25/2008|272|  
|8/25/2008|152|  
|9/25/2008|250|  
|10/25/2008|181|  
|11/25/2008|290|  
  
> [!WARNING]  
>  예제 데이터베이스에 사용된 날짜가 이 릴리스에 맞게 변경되었습니다. 이전 버전의 예제 데이터를 사용하는 경우에는 결과가 다르게 나타날 수 있습니다.  
  
## <a name="saving-the-prediction-results"></a>예측 결과 저장  
 예측 결과를 사용하기 위한 여러 다른 옵션이 있습니다. 결과를 일반화하고 결과 뷰에서 데이터를 복사하여 Excel 워크시트 또는 다른 파일에 붙여 넣을 수 있습니다.  
  
 결과 저장 프로세스를 간소화하기 위해 데이터 마이닝 디자이너에서도 데이터를 데이터 원본 뷰에 저장할 수 있는 기능이 제공됩니다. 데이터 원본 뷰에 결과를 저장하는 기능은 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서만 사용할 수 있습니다. 결과는 일반 형식으로만 저장할 수 있습니다.  
  
#### <a name="to-flatten-the-results-in-the-results-pane"></a>결과 창에서 결과를 평면화하려면  
  
1.  예측 쿼리 작성기에서 클릭 **쿼리 디자인 뷰로 전환**합니다.  
  
     DMX 쿼리 텍스트를 수동으로 편집할 수 있도록 뷰가 변경됩니다.  
  
2.  `FLATTENED` 키워드 다음에 `SELECT` 키워드를 입력합니다. 전체 쿼리 텍스트가 다음과 같이 됩니다.  
  
    ```  
    SELECT FLATTENED  
      [Forecasting].[Model Region],  
      (PredictTimeSeries([Forecasting].[Amount],5)) as [PredictAmount],  
      (PredictTimeSeries([Forecasting].[Quantity],5)) as [PredictQuantity]  
    FROM  
      [Forecasting]  
    ```  
  
3.  필요에 따라 다음 예와 같이 결과를 제한하는 절을 입력할 수도 있습니다.  
  
    ```  
    SELECT FLATTENED  
      [Forecasting].[Model Region],  
      (PredictTimeSeries([Forecasting].[Amount],5)) as [PredictAmount],  
      (PredictTimeSeries([Forecasting].[Quantity],5)) as [PredictQuantity]  
    FROM  
      [Forecasting]  
    WHERE [Forecasting].[Model Region] = 'M200 North America'   
    OR [Forecasting].[Model Region] = 'M200 Europe'  
  
    ```  
  
4.  클릭 **쿼리 결과 뷰로 전환**합니다.  
  
#### <a name="to-export-prediction-query-results"></a>예측 쿼리 결과를 내보내려면  
  
1.  클릭 **쿼리 결과 저장**합니다.  
  
2.  에 **데이터 마이닝 쿼리 결과 저장** 대화 상자에 대 한 **데이터 원본**선택, [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]합니다. 데이터를 다른 관계형 데이터베이스에 저장하려는 경우 데이터 원본을 만들 수도 있습니다.  
  
3.  에 **테이블 이름** 와 같은 새 임시 테이블 이름, 형식, 열 **Test Predictions**합니다.  
  
4.  **저장**을 클릭합니다.  
  
    > [!NOTE]  
    >  만든 테이블을 보려면 데이터를 저장한 인스턴스의 데이터베이스 엔진에 대한 연결을 만들고 쿼리를 만드십시오.  
  
## <a name="conclusion"></a>결론  
 기본 시계열 모델을 작성하고 예측을 해석 및 생성하는 방법을 배웠습니다.  
  
 이 자습서의 나머지 태스크는 선택 사항이며 고급 시계열 예측에 대해 설명합니다. 계속하기로 결정한 경우 새 데이터를 모델에 추가하고 확장된 계열에 대해 예측을 생성하는 방법을 배우게 됩니다. 또한 모델의 추세를 사용하되 데이터는 새 데이터 계열로 교체하여 교차 예측을 수행하는 방법도 배웁니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [고급 시계열 예측 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [시계열 모델 쿼리 예제](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)  
  
  
