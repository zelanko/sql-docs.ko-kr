---
title: 추정 마법사 (데이터 마이닝 추가 기능 Excel 용) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- estimation
ms.assetid: 7f2b1d5f-c9b3-4939-b35a-34ae099af15f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b7ffc1b77d90946a119dc462da2057cf3fe4988
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081249"
---
# <a name="estimate-wizard-data-mining-add-ins-for-excel"></a>추정 마법사(Excel용 데이터 마이닝 추가 기능)
  ![데이터 마이닝 리본의 추정 마법사](media/dmc-estimate.gif "데이터 마이닝 리본의 추정 마법사")  
  
 **추정** 마법사로 추정 모델을 만들 수 있습니다. 추정 모델은 데이터에서 패턴을 추출하고 패턴을 사용하여 결과에 영향을 주는 요인을 예측합니다.  
  
 추정은 숫자 결과를 예측하는 데 사용됩니다. 예를 들어 대상 열에 백분율로 표현된 학교 졸업률이 포함되어 있는 경우 학교별 학생 수, 학생과 교사 비율, 교사 수 등 졸업률을 높이거나 낮출 수 있는 요인을 분석할 수 있습니다.  
  
## <a name="using-the-estimate-data-wizard"></a>데이터 추정 마법사 사용  
  
1.  **데이터 마이닝** 리본에서 **추정**을 클릭합니다.  
  
2.  **원본 데이터 선택** 대화 상자에서 사용할 원본 데이터를 선택합니다. Excel **테이블**, Excel **데이터 범위**또는 **외부 데이터 원본**의 데이터를 사용할 수 있습니다.  
  
     외부 데이터 원본을 사용할 경우에는 사용자 지정 뷰 또는 쿼리를 만들고 이를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터 원본으로 저장할 수 있습니다.  
  
3.  **추정** 대화 상자에서 **분석할 열**을 선택합니다.  
  
     대상 열에는 연속 숫자 데이터가 있어야 합니다.  
  
4.  **입력 열** 확인란을 선택하여 입력으로 사용할 열을 선택합니다.  
  
     이러한 열은 패턴을 만드는 데 사용됩니다. ID 번호 또는 관련이 없는 데이터가 포함된 열과 같이 필요하지 않은 열은 분석에서 제외해야 합니다.  
  
5.  **추정** 마법사는 데이터 집합에 가장 적합한 알고리즘을 선택합니다. 그러나 **매개 변수** 를 클릭하여 **알고리즘 매개 변수** 대화 상자를 열고 고급 옵션을 설정할 수 있습니다.  
  
6.  데이터가 숫자이고 Microsoft 선형 회귀 방법을 사용할 수 있으면 **회귀 변수** 상자에서 예측 가능한 값과 상관될 수 있는 것으로 알려진(또는 그러한 가능성이 매우 높은) 숫자 열을 확인할 수 있습니다.  
  
     이 알고리즘은 그런 다음 해당 열의 값을 테스트해서 결과에 영향을 주는지 여부를 확인합니다. 확실하지 않으면 **제안** 을 클릭합니다. 그러면 알고리즘이 모든 열을 테스트하고 회귀 변수로 사용하기에 가장 적합한 값을 자동으로 검색합니다.  
  
    > [!NOTE]  
    >  추정을 만들려면 회귀 변수가 필요합니다. 데이터 초기 패스를 기반으로 마법사가 항상 최상의 회귀 변수를 제안합니다. 따라서 잘 모르는 경우에는 제안된 선택 항목을 받아들이는 것이 좋습니다.  
  
7.  **학습 및 테스트 집합으로 데이터 분할** 페이지에서 테스트용 데이터 하위 집합을 만들지 여부를 지정합니다.  
  
8.  **마침** 페이지에서 새 마이닝 구조 및 마이닝 모델의 이름을 지정하거나 기본으로 제공되는 이름을 사용합니다.  
  
9. 모델 사용 옵션을 설정합니다.  
  
    -   모델을 뷰어에서 바로 열려면 **찾아보기** 를 선택합니다.  
  
         이 그래픽 뷰어에는 종속성 네트워크 그래프 및 알고리즘에서 생성된 의사 결정 트리가 표시됩니다. 이 정보를 검토하면 추정 값에 영향을 주는 요인을 더 잘 이해할 수 있습니다.  
  
    -   분석 사용자가 기본 데이터를 볼 수 있도록 하려면 **드릴스루 사용** 을 선택합니다.  
  
         이 옵션은 의사 결정 트리 또는 선형 회귀 알고리즘을 사용하는 경우에만 사용할 수 있습니다.  
  
    -   **임시 모델 사용**. 이 옵션을 선택하면 모델이 서버에 저장되지 않습니다. 임시 모델은 Excel을 닫을 때 삭제됩니다.  
  
## <a name="more-about-estimation-models"></a>추정 모델에 대한 추가 정보  
 **추정** 마법사는 다음 알고리즘의 사용을 지원합니다.  
  
-   Microsoft 의사 결정 트리 알고리즘  
  
-   Microsoft 선형 회귀 알고리즘  
  
-   Microsoft 로지스틱 회귀 알고리즘  
  
-   Microsoft 신경망 알고리즘  
  
 **알고리즘 매개 변수** 대화 상자에서는 선택한 알고리즘에 따라 고급 옵션을 추가로 설정할 수 있습니다. 각 알고리즘의 옵션에 대한 자세한 내용은 SQL Server 온라인 설명서에서 다음 항목들을 참조하십시오.  
  
 [Microsoft 의사 결정 트리 알고리즘 기술 참조](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Microsoft 선형 회귀 알고리즘 기술 참조](data-mining/microsoft-linear-regression-algorithm-technical-reference.md)  
  
 [Microsoft 로지스틱 회귀 알고리즘 기술 참조](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Microsoft 신경망 알고리즘 기술 참조](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>요구 사항  
 데이터 추정 마법사를 사용하려면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에 연결되어 있어야 합니다.  
  
 연결을 만드는 방법에 대 한 자세한 내용은 [원본 데이터에 연결 &#40;Excel 용 데이터 마이닝 클라이언트&#41;](connect-to-source-data-data-mining-client-for-excel.md)합니다.  
  
 추정 알고리즘을 사용하려면 예측하려는 결과가 통화, 판매 금액, 날짜 또는 시간과 같은 숫자 값으로 표시되어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 모델 만들기](creating-a-data-mining-model.md)   
 [트리 다이어그램 연습 의사 결정 &#40;데이터 마이닝 추가 기능&#41;](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
  
