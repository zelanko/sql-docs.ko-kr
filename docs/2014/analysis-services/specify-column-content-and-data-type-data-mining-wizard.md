---
title: 열 내용 및 데이터 형식 (데이터 마이닝 마법사)를 지정 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0634be64-4c38-4381-9b19-fe9a5889306c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d224a321ed78f89a798966bd28c0ff7f16d55134
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068464"
---
# <a name="specify-column-content-and-data-type-data-mining-wizard"></a>열 내용 및 데이터 형식 지정(데이터 마이닝 마법사)
  **열 내용 및 데이터 형식 지정** 페이지를 사용하여 마법사의 이전 페이지에서 선택한 각 열의 사용법 및 데이터 형식을 지정할 수 있습니다. 열을 무시하려면 **뒤로** 를 클릭하여 **학습 데이터 지정**페이지로 돌아간 다음 모든 확인란의 선택을 취소합니다.  
  
 열 사용법은 모델에서 데이터가 사용되는 방법을 나타냅니다. 열은 계열을 식별하는 키, 분석에서 사용할 입력 값 또는 예측할 값으로 사용할 수 있습니다. 열은 예측 및 입력에 모두 사용할 수 있습니다.  
  
 데이터 형식은 열에 포함되는 데이터 형식에 대한 추가 정보 및 학습 중에 데이터가 사용되는 방법을 지정합니다. 일부 내용 유형에는 특정 데이터 형식이 필요하고 특정 데이터 형식에는 일부 내용 유형이 필요합니다. 마이닝 모델을 만들 때 사용하는 알고리즘에 따라 특정 데이터 형식을 지정해야 할 수도 있습니다. 마이닝 모델과 구조의 콘텐츠 형식 및 데이터 형식에 대한 자세한 내용은 [콘텐츠 형식&#40;데이터 마이닝&#41;](data-mining/content-types-data-mining.md)을 참조하세요.  
  
 **참조 항목:** [마이닝 구조 &#40;Analysis Services-데이터 마이닝&#41;](data-mining/mining-structures-analysis-services-data-mining.md)를 [마이닝 모델 열](data-mining/mining-model-columns.md)합니다 [데이터 마이닝 마법사 &#40;&#40;analysis Services-데이터 마이닝&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md), [ 관계형 마이닝 구조 만들기](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>변수  
 **마이닝 모델 구조**  
 마법사의 이전 페이지에서 선택한 뷰 및 중첩 테이블의 열을 표시합니다.  
  
 **열**  
 열을 나열합니다.  
  
 **콘텐츠 형식**  
 열에 대한 내용 유형을 지정합니다. 마법사의 이전 페이지에서 열을 키로 지정한 경우 다음 값을 사용할 수 있습니다.  
  
|옵션|Description|  
|------------|-----------------|  
|Key|열에 사례 계열에 대한 고유 식별자가 포함되도록 지정합니다.|  
|키 시퀀스|열에 시퀀스 식별자가 포함되도록 지정합니다.|  
|Key Time|열에 데이터나 시계열을 식별하는 데 사용되는 데이터 또는 다른 고유 연속 숫자가 포함되도록 지정합니다.|  
  
 열을 키가 아닌 열로 선택한 경우 데이터 형식에 따라 다음 값을 사용할 수 있습니다.  
  
|옵션|Description|  
|------------|-----------------|  
|연속|열에 연속 숫자 값이 포함되도록 지정합니다.|  
|불연속화됨|열에 불연속화되거나 불연속 값으로 처리할 수 있는 숫자 값이 포함되도록 지정합니다.|  
|불연속|열에 텍스트 또는 숫자가 아닌 다른 값이 포함되도록 지정합니다.|  
  
 **Data type**  
 열에 대한 데이터 형식을 지정합니다.  
  
 사용할 수 있는 값은 다음과 같습니다.  
  
-   `Boolean`  
  
-   `Date`  
  
-   `Double`  
  
-   `Long`  
  
-   `Text`  
  
 **검색**  
 모든 숫자 열에 있는 데이터 예제를 분석합니다. 지정된 **내용 유형** 값을 권장 내용 유형으로 바꿉니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 마법사 F1 도움말 &#40;Analysis Services-데이터 마이닝&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [관련된 열 제안 &#40;데이터 마이닝 마법사&#41;](suggest-related-columns-data-mining-wizard.md)   
 [테이블 유형 지정 &#40;데이터 마이닝 마법사&#41;](specify-table-types-data-mining-wizard.md)   
 [열 내용 및 데이터 형식 지정 &#40;데이터 마이닝 마법사&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
