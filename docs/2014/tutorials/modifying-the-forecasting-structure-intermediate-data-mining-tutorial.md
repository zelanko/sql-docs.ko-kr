---
title: 예측 (중급 데이터 마이닝 자습서) 구조 수정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 1a6c138e-643b-4ae6-ad08-93631f149c20
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 559f6aa6b31b8998703a93e84dc100ce375cbda8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48139533"
---
# <a name="modifying-the-forecasting-structure-intermediate-data-mining-tutorial"></a>예측 구조 수정(중급 데이터 마이닝 자습서)
  이전 태스크에서 만든 마이닝 구조에는 단일 예측 모델이 포함되어 있습니다. 모델을 처리하고 탐색하기 전에 해당 구조를 약간 변경하고 속성 중 하나를 수정해야 합니다.  
  
## <a name="modifying-the-mining-structure"></a>마이닝 구조 수정  
 사용 하 여 마이닝 구조를 변경할 수 있습니다 합니다 **마이닝 구조** 데이터 마이닝 디자이너의 탭 합니다. 데이터 마이닝 마법사로 모델을 만들 때에는 ReportingDate, ModelRegion 및 Quantity라는 3개의 열을 사용했습니다. 그러나 합니다 **Forecasting** 테이블 판매 금액을 예측 하는 데 사용할 수 있는 Amount 열도 포함 합니다. 사용 하 여 합니다 **마이닝 구조** 탭에서 마이닝 구조에 데이터 원본 뷰에서이 열을 추가할 수 있습니다.  
  
#### <a name="to-add-the-amount-column-to-the-forecasting-mining-structure"></a>Forecasting 마이닝 구조에 Amount 열을 추가하려면  
  
1.  에 **Mining Structure** 데이터 마이닝 디자이너의 탭에서를 **데이터 원본 뷰** 창 vTimeSeries 테이블의 Amount 열을 선택 합니다.  
  
2.  Amount 열을 끌어 합니다 **데이터 원본 뷰** 창에 대 한 열 목록에는 **Forecasting** 구조입니다.  
  
     이제 Amount 열에 포함 된 **Forecasting** 마이닝 구조입니다.  
  
## <a name="modifying-the-columns-in-the-mining-model"></a>마이닝 모델에서 열 수정  
 구조에 새 열을 추가했기 때문에 모델에서 열을 사용할 방법을 정의해야 합니다. 열에 사용할 방법을 지정할 수 있습니다 합니다 **마이닝 모델** 데이터 마이닝 디자이너의 탭 합니다.  
  
 **마이닝 모델** 탭에서 마이닝 구조에 포함 된 열을 나열 합니다 **구조** 열 표에서 및 마이닝 모델의 이름을 가진 열에 포함 된 열이 나열 합니다 이 경우 모델 **Forecasting**합니다. 열의 이름을 클릭하여 수정합니다. 에 **Forecasting** 마이닝 모델 Amount 열의 입력된 열으로 사용 되 고 향후 판매를 예측 하 때도 사용 됩니다. 따라서 열의 속성을 설정해야 입력 열과 예측 가능한 열 모두로 사용할 수 있습니다.  
  
> [!NOTE]  
>  에 **마이닝 모델** 탭 하면 동일한 구조를 기반으로 새 모델도 만들 수 있으며 각 모델의 알고리즘과 열 속성을 조정할 수 있습니다. 그러나 해당 변경 내용을 적용하기 전에 모델을 처리해야 합니다.  
  
#### <a name="to-define-how-the-amount-column-will-be-used"></a>판매액 열을 사용할 방법을 정의하려면  
  
1.  에 **Forecasting** 에 있는 표의 열을 **마이닝 모델** 탭에서 Amount 행의 셀을 클릭 합니다.  
  
2.  선택 **Predict** 목록에서.  
  
     이제 Amount 열은 입력 열과 예측 가능한 열 모두로 사용됩니다.  
  
 열 및 열을 선택 하 여 개별 열의 속성을 변경할 수도 있습니다는 **속성** 창입니다. 열려는 합니다 **속성** 창에서 열 이름을 마우스 오른쪽 단추로 클릭 **속성**합니다. 개별 모델의 열 내에서 속성을 변경하면 해당 모델에 대해서만 속성을 변경할 수 있습니다. 그러나 내에서 속성을 변경 하는 하는 **구조** 열 변경 내용이 적용 구조와 연결 된 모든 모델. 모델 또는 구조를 변경할 때마다 효과를 확인하려면 다시 처리해야 합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [사용자 지정 및 예측 모델을 처리 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 구조 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [마이닝 모델 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
