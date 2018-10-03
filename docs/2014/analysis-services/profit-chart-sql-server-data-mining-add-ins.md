---
title: 수익 차트 (SQL Server 데이터 마이닝 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- accuracy chart
- profit chart
- mining models, charting
- mining models, testing
ms.assetid: 5c902543-4da9-4db3-99d5-4ce04c43d7ef
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 618388325ecc552bf38f20603ff9d3c4c432bd1d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191243"
---
# <a name="profit-chart-sql-server-data-mining-add-ins"></a>수익 차트(SQL Server 데이터 마이닝 추가 기능)
  ![데이터 마이닝 리본의 수익 차트 단추](media/dmc-profitchart.gif "데이터 마이닝 리본의 수익 차트 단추")  
  
 수익 차트는 비즈니스 시나리오에서 회사가 연락해야 하는 고객을 결정하는 데 마이닝 모델을 사용함으로써 얻을 수 있는 예상 수익 증가분을 표시합니다. 차트의 Y축은 수익을 나타내고 X축은 회사에서 연락한 모집단의 백분율을 나타냅니다. 일반적인 수익 차트에서는 특정 시점까지는 수익이 증가하고 이 시점 이후에는 연락하는 모집단이 증가할수록 수익이 줄어듭니다.  
  
## <a name="configuring-the-profit-chart"></a>수익 차트 구성  
 정확도 차트는 예측이 맞거나 틀릴 확률만 평가하는 반면 수익 차트는 예측에 대해 수행하는 조치의 영향에 대한 실제 지식을 통합합니다. 이 작업은 마법사를 실행할 때 지정하는 다음 요인을 고려하여 수행됩니다.  
  
-   **모집단**  
  
     리프트 차트를 만드는 데 사용된 데이터 집합의 사례 수입니다. 잠재적인 고객의 수가 여기에 포함됩니다.  
  
-   **고정 비용**  
  
     비즈니스상의 문제와 관련된 고정 비용입니다. 타겟 메일링 솔루션에 대한 문제인 경우 전화를 건 횟수 또는 홍보 메일을 전송한 횟수와 같은 변수에 따라 비용이 달라지지 않습니다.  
  
-   **개별 비용**  
  
     고정 비용 외에 각 고객에게 연락하는 데 드는 비용입니다. 홍보 메일을 전송하는 데 드는 비용이나 전화를 거는 데 드는 비용이 여기에 포함됩니다.  
  
-   **개인별 수익**  
  
     성공적인 각 판매와 관련된 수익입니다.  
  
## <a name="using-the-profit-chart-wizard"></a>수익 차트 마법사 사용  
 수익 차트를 만들려면 기존 데이터 마이닝 모델을 참조해야 합니다. 클릭 하 여 데이터를 일치 하는 모델을 찾는 모델을 찾아볼 수 있습니다 **모델 관리** 하거나 **찾아보기** 사용 된 알고리즘에 대 한 세부 정보 및 마이닝 모델의 열입니다.  
  
 자세한 내용은 [Excel에서 모델 찾아보기 &#40;SQL Server 데이터 마이닝 추가 기능&#41; ](browsing-models-in-excel-sql-server-data-mining-add-ins.md) 하 고 [모델 관리 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](manage-models-sql-server-data-mining-add-ins.md).  
  
#### <a name="to-create-a-profit-chart"></a>수익 차트를 만들려면  
  
1.  기존 모델을 선택합니다.  
  
2.  예측할 열 및 대상 값을 지정합니다(해당되는 경우).  
  
3.  예측을 만들기 위해 모델을 통해 전달할 데이터를 의미하는 원본 데이터를 선택합니다. 이 데이터는 모델을 만들 때 사용한 데이터와 달라야 합니다.  
  
4.  새 원본 데이터의 열을 데이터 마이닝 모델에 사용된 열에 매핑합니다. 열 이름이 비슷한 경우 마법사가 자동으로 매핑합니다.  
  
5.  마법사에 필요한 비용 정보를 입력 합니다: 고정된 비용, 개별 비용, 모집단 및 예상 수익입니다.  
  
6.  필요에 따라는 일련의 누진된 비용을 입력할 수 있습니다 (찾아보기 **(...)**  단추). 예를 들어 전송하는 항목 수가 증가함에 따라 우편 비용은 더 저렴해질 수 있으므로 항목 수에 따라 다른 비용을 입력할 수 있으며 마법사는 각 샘플 크기에 대해 자동으로 비용을 조정합니다.  
  
7.  마법사는 모델에 대한 비용 대비 이점 분석을 포함하는 차트를 만듭니다.  
  
### <a name="requirements"></a>요구 사항  
 불연속 숫자 값을 예측하는 경우 예측할 정확한 대상 값을 선택해야 합니다.  
  
## <a name="understanding-the-profit-chart"></a>수익 차트 이해  
 수익 차트에는 차트에서 위치를 클릭하여 이동할 수 있는 회색 세로줄이 포함되어 있습니다. 합니다 **마이닝 범례** 점수, 정확한 모집단 및 차트의 회색 선의 위치와 관련 된 예측 확률이 표시 됩니다. 회색 선을 사용하여 차트에서 최대 수익점을 선택하면 예측 확률 값을 사용하여 고객에게 연락할 확률 임계값을 결정할 수 있습니다.  
  
 예를 들어 수익 곡선의 최고점이 모집단의 55%이고 관련 예측 확률의 20%인 경우 최대 수익을 얻으려면 응답 가능성이 20% 이상으로 예측되는 고객에게만 연락을 해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [모델 유효성 검사 및 예측 용 모델 사용 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
