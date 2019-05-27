---
title: 예측 마법사 (데이터 마이닝 추가 기능 Excel 용) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- forecasting [data mining]
- time series [data mining]
ms.assetid: c5b33f75-42d4-4598-89e7-94815c142ce6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f0717d8a81cc89897de005144dd631d23da42137
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081028"
---
# <a name="forecast-wizard-data-mining-add-ins-for-excel"></a>예측 마법사(Excel용 데이터 마이닝 추가 기능)
  ![데이터 마이닝 리본의 연결 마법사](media/dmc-forecast.gif "연결 데이터 마이닝 리본의 마법사")  
  
 예측 마법사를 사용하면 시계열의 값을 예측할 수 있습니다. 예측 마법사는 제품 판매량과 같은 연속 열을 예측하기 위해 사용되는 회귀 알고리즘인 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시계열 알고리즘을 사용합니다.   
  
 각 예측 모델은 시퀀스의 요소를 구분하는 열인 사례 계열을 포함해야 합니다. 예를 들어 여러 달 동안의 판매량을 예측하기 위해 기록 데이터를 사용하는 경우 날짜 계열이 포함된 열을 사례 계열로 사용합니다.  
  
 새 입력 데이터를 제공하지 않아도 예측 모델로부터 예측을 만들 수 있습니다.  
  
 [예측 &#40;Excel 용 테이블 분석 도구&#41; ](forecast-table-analysis-tools-for-excel.md) 도구를 합니다 **분석** 예측 모델을 만들 리본, 수 있지만 사용자 지정 기능이 부족 하며 Excel 테이블에만 데이터를 사용할 수 있습니다.  
  
## <a name="using-the-forecast-wizard"></a>예측 마법사 사용  
  
1.  에 **데이터 마이닝** 리본 메뉴 **예측**합니다.  
  
2.  에 **원본 데이터 선택**, Excel 테이블, 범위 또는 입력으로 사용할 외부 데이터 원본을 선택 합니다.  
  
     외부 데이터 원본을 사용할 경우에는 사용자 지정 뷰 또는 쿼리를 정의하거나 데이터 원본을 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터 원본으로 저장할 수 있습니다.  
  
3.  에 **Forecasting** 페이지에 대 한 **타임 스탬프**을 사례 계열로 사용할 수 있는 고유 숫자 값 (날짜 및 시간 값 포함)이 포함 된 열을 선택 합니다. 데이터 원본은 이 열을 기준으로 오름차순으로 정렬되어야 합니다.  
  
     데이터에 이러한 열이 없으면 옵션을 사용할 수 있습니다 \<타임 스탬프 없음 >. 마법사는 입력 데이터에 대한 고유 순서 열을 추가합니다. 따라서 마법사를 실행하고 이 옵션을 선택하기 전에 데이터가 원하는 순서로 정렬되어 있는지 확인해야 합니다.  
  
4.  필요에 따라 눌러도 **매개 변수** 마이닝 모델의 동작을 사용자 지정 합니다.  
  
     예측 모델에는 여러 가지 알고리즘이 지원됩니다.  
  
    -   ARIMA  
  
    -   ARTXP(회귀 모델 유형)  
  
    -   ARTXP 및 ARIMA 조합  
  
     차이점에 대 한 자세한 내용은 [Microsoft Time Series Algorithm Technical Reference](data-mining/microsoft-time-series-algorithm-technical-reference.md)합니다.  
  
     또한 모델에 대해 주기 힌트를 추가하고, 다듬기(smoothing) 옵션을 지정하고, 회귀 옵션을 사용자 지정할 수도 있습니다.  
  
5.  에 **완료** 페이지에서 데이터 집합 및 모델에 대해 설명 하는 이름을 제공 하 고 완성된 된 모델을 사용 하는 방법을 제어 하는 다음 옵션을 설정 합니다.  
  
    -   **모델을 찾으면**합니다. 이 옵션을 선택 하면 마법사 되 자 마자 모델 처리를 완료 함 열립니다는 **찾아보기** 창 결과 살펴볼 수 있도록 합니다. 뷰어 내용은 작성한 모델 유형에 따라 달라집니다. 자세한 내용은 [예측 모델을 탐색](browsing-a-forecasting-model.md)합니다.  
  
    -   **드릴스루**합니다. 완료된 모델에서 기본 데이터를 보려면 이 옵션을 선택합니다. 이 옵션은 의사 결정 트리 모델을 작성하는 경우에만 사용할 수 있습니다.  
  
    -   **임시 모델 사용**. 이 옵션을 선택하면 모델이 서버에 저장되지 않습니다. 임시 모델은 Excel을 닫을 때 삭제됩니다.  
  
### <a name="requirements"></a>요구 사항  
 데이터에 시계열로 사용할 수 있는 열이 하나 이상 포함되어야 합니다. 이 열의 값은 고유 하 고 연속적 이어야 합니다-, 없어야 간격이 없어야 합니다. 마법사를 실행하기 전에 시계열 열을 기준으로 데이터를 오름차순으로 정렬합니다.  
  
 데이터에 시간 또는 날짜 열이 포함되지 않은 경우 임의 숫자 계열을 지정하거나 마법사에서 자동으로 만들 수 있습니다. 마법사에서 계열 순서 열을 자동으로 만들 경우, 마법사를 시작하기 전에 다른 열이 원하는 순서로 정렬되어 있는지 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 모델 만들기](creating-a-data-mining-model.md)   
 [예측 &#40;Excel 용 테이블 분석 도구&#41;](forecast-table-analysis-tools-for-excel.md)   
 [예측 모델 찾아보기](browsing-a-forecasting-model.md)  
  
  
