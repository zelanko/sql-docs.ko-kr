---
title: 분류 마법사 (데이터 마이닝 추가 기능 Excel 용) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- classification [data mining]
ms.assetid: 409c5076-c4c3-4f09-8f30-d3297df45f13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9109f47ba1173c115234f9040445fb110e3f0e3c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680884"
---
# <a name="classify-wizard-data-mining-add-ins-for-excel"></a>분류 마법사(Excel용 데이터 마이닝 추가 기능)
  ![데이터 마이닝 리본의 분류 마법사](media/dmc-classify.gif "데이터 마이닝 리본의 분류 마법사")  
  
 **분류** 마법사를 사용하면 Excel 테이블, Excel 범위 또는 외부 데이터 원본의 기존 데이터를 기반으로 분류 모델을 만들 수 있습니다.  
  
 분류 모델을 사용하면 유사성을 나타내는 데이터의 패턴을 추출하여 값 그룹에 따라 예측할 수 있습니다. 예를 들어 수입 또는 지출 패턴을 기반으로 위험을 예측하는 데 분류 모델을 사용할 수 있습니다.  
  
## <a name="using-the-classify-wizard"></a>분류 마법사 사용  
  
1.  에 **데이터 마이닝** 리본 메뉴 **분류**를 클릭 하 고 **다음**합니다.  
  
2.  에 **원본 데이터 선택** 페이지에서 분석할 데이터를 선택 합니다.  
  
     이 마법사는 여러 종류를의 데이터를 지원합니다. Excel 테이블, Excel 범위 및 외부 데이터 원본입니다. 외부 데이터의 경우 Excel에 추가하거나 Analysis Services 데이터 원본에서 테이블 또는 뷰 집합을 선택할 수 있습니다. 또한 테이블을 추가하고 열을 변경해서 임시 데이터 원본을 만들 수 있습니다.  
  
3.  에 **분류** 페이지에서 분류 하려는 열을 선택 합니다.  
  
     목록에서 열을 검토 **입력 열**, 고유 값을 갖고 있으므로 ID 번호, 고객 이름 등의 패턴을 만드는 데 유용 하지 않은 모든 열의 선택을 취소 하 고 등입니다. 또한 본질적으로 분류 가능한 열이 중복되게 만드는 열도 제거해야 합니다.  
  
     예를 들어 제품 범주 예측을 분류하는 경우, 알려진 비즈니스 규칙이 있으면 하위 범주 필드를 제외해야 합니다. 그렇지 않으면 해당 규칙의 강도로 인해 다른 상관 관계를 검색하는 데 방해가 될 수 있습니다.  
  
4.  필요에 따라 클릭 **매개 변수** 알고리즘 매개 변수를 변경 하 여 클러스터링 모델의 동작을 사용자 지정 합니다.  
  
5.  에 **데이터를 학습 집합과 테스트 집합으로 분할** 페이지에서 테스트용 데이터 양을 지정 합니다. 나머지는 항상 모델 학습에 사용됩니다.  
  
     기본 설정은 테스트 데이터 30%와 학습 데이터 70%입니다.  
  
6.  에 **완료** 페이지에서 데이터 집합 및 모델에 대해 설명 하는 이름을 제공 하 고 완성된 된 모델을 사용 하는 방법을 제어 하는 다음 옵션을 설정 합니다.  
  
    -   **모델을 찾으면**합니다. 이 옵션을 선택 하면 마법사 되 자 마자 모델 처리를 완료 함 열립니다는 **찾아보기** 창 결과 살펴볼 수 있도록 합니다. 뷰어 내용은 작성한 모델 유형에 따라 달라집니다. 자세한 내용은 참조 하세요. [의사 결정 트리 모델을 탐색](browsing-a-decision-trees-model.md) 하 고 [는 신경망 모델 찾아보기](browsing-a-neural-network-model.md)합니다.  
  
    -   **드릴스루**합니다. 완료된 모델에서 기본 데이터를 보려면 이 옵션을 선택합니다. 이 옵션은 의사 결정 트리 모델을 작성하는 경우에만 사용할 수 있습니다.  
  
    -   **임시 모델 사용**. 이 옵션을 선택하면 모델이 서버에 저장되지 않습니다. 임시 모델은 Excel을 닫을 때 삭제됩니다.  
  
## <a name="more-about-classification-models"></a>분류 모델에 대한 추가 정보  
 에 **알고리즘 매개 변수** 대화 상자에서 수도 있습니다 Analysis Services에서 제공 하는 이러한 알고리즘 중에서 분류 방법:  
  
-   Microsoft 의사 결정 트리  
  
-   Microsoft 로지스틱 회귀  
  
-   Microsoft Naïve Bayes  
  
-   Microsoft 신경망  
  
 각 알고리즘이 비슷한 결과를 생성할 수 있지만 데이터의 분석 방법이 다르기 때문에 여러 알고리즘을 시도해보고 결과를 비교하는 것이 좋습니다. 기본 방법은 Microsoft 의사 결정 트리입니다.  
  
 에 **매개 변수** 목록, 선택한 알고리즘 유형에 따라 고급 옵션을 변경할 수 있습니다. 각 알고리즘의 매개 변수에 대해서는 SQL Server 온라인 설명서에 보다 자세히 설명되어 있습니다.  
  
 [Microsoft 의사 결정 트리 알고리즘 기술 참조](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Microsoft 로지스틱 회귀 알고리즘 기술 참조](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Microsoft Naive Bayes 알고리즘 기술 참조](data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)  
  
 [Microsoft 신경망 알고리즘 기술 참조](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>요구 사항  
 사용 하는 **분류** 마법사를 연결 해야 하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스입니다. 연결을 만드는 방법에 대 한 자세한 내용은 [원본 데이터에 연결 &#40;Excel 용 데이터 마이닝 클라이언트&#41;](connect-to-source-data-data-mining-client-for-excel.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 모델 만들기](creating-a-data-mining-model.md)  
  
  
