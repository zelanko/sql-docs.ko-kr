---
title: 예측 구조 수정 (중급 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1a6c138e-643b-4ae6-ad08-93631f149c20
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a86ddf0a715fc3a2313f555e898b3bd94cf66d8c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63301294"
---
# <a name="modifying-the-forecasting-structure-intermediate-data-mining-tutorial"></a>예측 구조 수정(중급 데이터 마이닝 자습서)
  이전 태스크에서 만든 마이닝 구조에는 단일 예측 모델이 포함되어 있습니다. 모델을 처리하고 탐색하기 전에 해당 구조를 약간 변경하고 속성 중 하나를 수정해야 합니다.  
  
## <a name="modifying-the-mining-structure"></a>마이닝 구조 수정  
 데이터 마이닝 디자이너의 **마이닝 구조** 탭을 사용 하 여 마이닝 구조를 변경할 수 있습니다. 데이터 마이닝 마법사로 모델을 만들 때에는 ReportingDate, ModelRegion 및 Quantity라는 3개의 열을 사용했습니다. 그러나 **예측** 테이블에는 판매 금액을 예측 하는 데 사용할 수 있는 amount 열도 포함 됩니다. **마이닝 구조** 탭을 사용 하 여 데이터 원본 뷰의이 열을 마이닝 구조에 추가할 수 있습니다.  
  
#### <a name="to-add-the-amount-column-to-the-forecasting-mining-structure"></a>Forecasting 마이닝 구조에 Amount 열을 추가하려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 구조** 탭에 있는 **데이터 원본 뷰** 창에서 vTimeSeries 테이블의 Amount 열을 선택 합니다.  
  
2.  **데이터 원본 뷰** 창에서 **예측** 구조의 열 목록으로 Amount 열을 끌어 옵니다.  
  
     이제 Amount 열이 **예측** 마이닝 구조에 포함 됩니다.  
  
## <a name="modifying-the-columns-in-the-mining-model"></a>마이닝 모델에서 열 수정  
 구조에 새 열을 추가했기 때문에 모델에서 열을 사용할 방법을 정의해야 합니다. 데이터 마이닝 디자이너의 **마이닝 모델** 탭에서 열이 사용 되는 방식을 지정할 수 있습니다.  
  
 마이닝 **모델** 탭에는 표의 **구조** 열에 마이닝 구조에 포함 된 열이 나열 되며 모델 이름이 있는 열 (이 경우 **예측**)에는 마이닝 모델에 포함 된 열이 나열 됩니다. 열의 이름을 클릭하여 수정합니다. **예측** 마이닝 모델에서 Amount 열은 입력 열로 사용 되 고 향후 판매를 예측 하는 데도 사용 됩니다. 따라서 열의 속성을 설정해야 입력 열과 예측 가능한 열 모두로 사용할 수 있습니다.  
  
> [!NOTE]  
>  **마이닝 모델** 탭에서는 동일한 구조를 기반으로 새 모델을 만들 수도 있으며 각 모델에 대 한 알고리즘 및 열 속성을 조정할 수도 있습니다. 그러나 해당 변경 내용을 적용하기 전에 모델을 처리해야 합니다.  
  
#### <a name="to-define-how-the-amount-column-will-be-used"></a>판매액 열을 사용할 방법을 정의하려면  
  
1.  **마이닝 모델** 탭에 있는 표의 **예측** 열에서 Amount 행의 셀을 클릭 합니다.  
  
2.  목록에서 **예측** 을 선택 합니다.  
  
     이제 Amount 열은 입력 열과 예측 가능한 열 모두로 사용됩니다.  
  
 열을 선택 하 고 **속성** 창을 열어 개별 열의 속성을 변경할 수도 있습니다. **속성** 창을 열려면 열 이름을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다. 개별 모델의 열 내에서 속성을 변경하면 해당 모델에 대해서만 속성을 변경할 수 있습니다. 그러나 **구조** 열 내에서 속성을 변경 하면 해당 구조와 연결 된 모든 모델에 변경 내용이 적용 됩니다. 모델 또는 구조를 변경할 때마다 효과를 확인하려면 다시 처리해야 합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [&#40;중급 데이터 마이닝 자습서를 통해 예측 모델 사용자 지정 및 처리&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [마이닝 구조 &#40;Analysis Services 데이터 마이닝&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [마이닝 모델 &#40;Analysis Services 데이터 마이닝&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
