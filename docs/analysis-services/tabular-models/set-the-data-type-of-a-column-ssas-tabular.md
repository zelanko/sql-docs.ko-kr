---
title: "데이터 형식의 열 (SSAS 테이블 형식)를 설정 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 34e2d508-7b64-4503-a4f0-c6c6ad5f8a44
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 8ff4bf9de4a232561d813ae304aa3ae660ff9041
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="set-the-data-type-of-a-column-ssas-tabular"></a>열 데이터 형식 설정(SSAS 테이블 형식)
  모델에 데이터를 가져오거나 붙여넣을 때 모델 디자이너에서 자동으로 데이터 형식을 감지하고 적용합니다. 모델에 데이터를 추가한 후 열의 데이터 형식을 수동으로 수정하여 데이터가 저장되는 방법을 변경할 수 있습니다. 원하는 경우 데이터 저장 방식은 변경하지 않고 데이터 표시 방식의 형식만 변경할 수도 있습니다.  
  
### <a name="to-change-the-data-type-or-display-format-for-a-column"></a>열의 데이터 형식 또는 표시 형식을 변경하려면  
  
1.  모델 디자이너에서 데이터 형식 또는 서식을 변경할 열을 선택합니다.  
  
2.  열 **속성** 창에서 다음 중 하나를 수행합니다.  
  
    -   **데이터 서식** 속성에서 다른 데이터 서식을 선택합니다.  
  
    -   **데이터 형식** 속성에서 다른 데이터 형식을 선택합니다.  
  
## <a name="considerations-when-changing-data-types"></a>데이터 형식을 변경할 때의 고려 사항  
 열의 데이터 형식을 변경하거나 데이터 변환을 선택할 때 다음 오류 중 하나가 발생할 수도 있습니다.  
  
-   데이터 형식을 변경하지 못했습니다.  
  
-   열 데이터 형식을 변경하지 못했습니다.  
  
 데이터 형식 드롭다운 목록에 데이터 형식이 옵션으로 표시되는 경우에도 이러한 오류가 발생할 수 있습니다. 이 섹션에서는 이러한 오류 메시지의 원인 및 이를 해결하는 방법에 대해 설명합니다.  
  
### <a name="understanding-automatically-determined-data-types"></a>자동으로 결정되는 데이터 형식 이해  
 모델에 데이터를 추가하면 모델 디자이너에서 데이터 열을 검사하여 각 열에 포함된 데이터 형식을 확인합니다. 해당 열의 데이터가 일치하면 가장 정확한 데이터 형식이 열에 할당됩니다.  
  
 그러나 Excel 또는 각 열에 단일 데이터 형식 사용을 적용하지 않는 기타 원본에서 데이터를 추가하는 경우 모델 디자이너에서 열의 모든 값을 수용하는 데이터 형식을 할당합니다. 따라서 정수, 긴 숫자, 통화 등의 여러 형식이 열에 포함되어 있으면 모델 디자이너에서 10진수 데이터 형식을 사용합니다. 또는 열에서 숫자와 텍스트를 함께 사용하는 경우 모델 디자이너에서 텍스트 데이터 형식을 사용합니다. 모델 디자이너는 Excel에서 사용 가능한 일반 데이터 형식과 비슷한 데이터 형식을 제공하지 않습니다.  
  
 따라서 열에 숫자와 텍스트 값이 모두 포함되어 있으면 열을 숫자 데이터 형식으로 변환할 수 없습니다.  
  
 모델비즈니스 인텔리전스 의미 체계 모델에서는 다음과 같은 데이터 형식을 사용할 수 있습니다.  
  
-   **텍스트**  
  
-   **10진수**  
  
-   **정수**  
  
-   **Currency**  
  
-   **TRUE/FALSE**  
  
-   **날짜**  
  
 데이터의 데이터 형식이 잘못되었거나 적어도 하나 이상의 데이터 형식이 원하는 형식과 다를 경우 다음과 같은 여러 가지 옵션 중에서 선택할 수 있습니다.  
  
-   데이터를 다시 가져올 수 있습니다. 이렇게 하려면 데이터 원본에 대한 기존 연결을 열고 열을 다시 가져옵니다. 데이터 원본 유형에 따라 가져오는 동안 필터를 적용하여 문제가 되는 값을 제거할 수도 있습니다.  
  
-   계산 열에 DAX 수식을 만들어 원하는 데이터 형식의 새 값을 만들 수 있습니다. 예를 들어 TRUNC 함수를 사용하여 10진수를 정수로 변경하거나 정보 함수와 논리 함수를 결합하여 값을 테스트하고 변환할 수 있습니다.  
  
### <a name="understanding-data-conversion"></a>데이터 변환 이해  
 데이터 변환 옵션을 선택할 때 오류가 발생하면 열의 현재 데이터 형식에서 지원하지 않는 변환을 선택했을 수 있습니다. 모든 데이터 형식에 모든 변환이 허용되는 것은 아닙니다. 예를 들어 열의 현재 데이터 형식이 숫자(정수 또는 10진수) 또는 텍스트일 경우 열을 부울 데이터 형식으로만 변경할 수 있습니다. 따라서 열의 데이터에 적합한 데이터 형식을 선택해야 합니다.  
  
 적절한 데이터 형식을 선택하면 모델 디자이너에서 정밀도 손실이나 잘림과 같은 데이터 변경이 발생할 수 있음을 알리는 경고 메시지를 표시합니다. 확인을 클릭하여 수락하고 데이터를 새 데이터 형식으로 변경합니다.  
  
 데이터 형식은 지원되지만 모델 디자이너에서 새 데이터 형식에 맞지 않는 값을 발견할 경우에는 다른 오류가 표시되며 계속하기 전에 데이터 값을 수정해야 합니다.  
  
 비즈니스 인텔리전스 의미 체계 모델에서 사용되는 데이터 형식, 이러한 데이터 형식이 암시적으로 변환되는 방법 및 수식에서 다양한 데이터 형식이 사용되는 방법에 대한 자세한 내용은 [지원되는 데이터 형식&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [지원되는 데이터 형식&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md)  
  
  
