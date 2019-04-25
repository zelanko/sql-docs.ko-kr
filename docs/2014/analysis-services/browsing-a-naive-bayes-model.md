---
title: Naive Bayes 모델 찾아보기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: f9160b48-3beb-439c-9694-f084e1afa625
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 91d39b174a0febed1aa6fd57140412828adc843b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62466195"
---
# <a name="browsing-a-naive-bayes-model"></a>Naive Bayes 모델 찾아보기
  사용 하 여 원시 Bayes 모델을 열면 **찾아보기**, 네 개의 다른 창을 사용 하 여 대화형 뷰어에서 모델이 표시 됩니다. 이 뷰어를 사용하여 상관 관계를 탐색하고 모델 및 기본 데이터에 대한 정보를 얻을 수 있습니다.  
  
-   [종속성 네트워크](#bkmk_DepNet)  
  
-   [특성 프로필](#bkmk_AttProf)  
  
-   [특성 특징](#bkmk_AttChar)  
  
-   [특성 판별](#bkmk_AttDisc)  
  
##  <a name="BKMK_Tabs"></a> 모델 탐색  
 뷰어는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 모델에서 발견된 입력 특성과 출력 특성(입력과 종속 변수) 간의 상호 작용을 탐색하는 데 유용합니다.  
  
 원시 Bayes 뷰어를 사용 하 여 실험 하려는 경우 사용 합니다 [분류 마법사 &#40;Excel 용 데이터 마이닝 추가 기능&#41; ](classify-wizard-data-mining-add-ins-for-excel.md) 데이터 마이닝 리본, 마법사를 클릭 합니다 **고급** 옵션을 변경 원시 Bayes 알고리즘을 사용 하는 알고리즘  
  
 이러한 예를 들어 샘플 통합 문서에 원본 데이터를 사용 하 고 열을 그룹화 **Yearly Income**, 5 가지 소득 그룹에에서 **매우 낮음** 하 **매우 높은**합니다. 그런 다음 Naïve Bayes 모델을 통해 각 소득 범주와 상관 관계가 있는 요인을 분석했습니다.  
  
###  <a name="bkmk_DepNet"></a> 종속성 네트워크  
 사용 하 여 첫 번째 창이 합니다 **종속성 네트워크**합니다. 이 창에서는 선택한 결과와 밀접한 상관 관계가 있는 입력을 한눈에 볼 수 있습니다.  
  
 ![Naive Bayes 뷰어의 종속성 네트워크](media/dm13-nb.gif "Naive Bayes 뷰어의 종속성 네트워크")  
  
##### <a name="explore-the-dependency-network"></a>종속성 네트워크 탐색  
  
1.  먼저 대상 결과 클릭 **Yearly Income**는 그래프의 노드로 표시 됩니다.  
  
     대상 변수 주위의 강조 표시된 노드는 이 결과와 통계적으로 상관 관계가 있습니다. 뷰어의 아래쪽에 있는 범례를 사용하여 관계의 특성을 이해할 수 있습니다.  
  
2.  뷰어 왼쪽에서 슬라이더를 클릭하여 아래로 끕니다.  
  
     이 컨트롤은 종속성 수준에 따라 독립 변수를 필터링합니다. 슬라이더를 아래로 끌면 가장 강력한 링크만 그래프에 남습니다.  
  
3.  그래프를 필터링 한 후 단추를 클릭 **그래프 뷰 복사**합니다. 그런 다음 Excel에서 워크시트를 선택하고 Ctrl+V를 누릅니다.  
  
     필터와 강조 표시를 비롯하여 선택한 뷰가 복사됩니다.  
  
 [맨 위로 이동](#BKMK_Tabs)  
  
###  <a name="bkmk_AttProf"></a> 특성 프로필  
 합니다 **특성 프로필** windows의 다른 모든 변수가 개별 결과 관련 된 시각적 표시를 제공 합니다.  
  
##### <a name="explore-the-profiles"></a>프로필 탐색  
  
1.  결과를 보다 쉽게 비교할 수 있도록 일부 값을 숨기려면 열 머리글을 클릭하고 다른 열 아래로 끕니다.  
  
     ![특성 프로필 Naive Bayes 뷰어의](media/dm13-nb-attprof.gif "프로필 Naive Bayes 뷰어의 특성")  
  
2.  값 분포를 보려면 아무 셀 이나 클릭 합니다 **마이닝 범례**합니다.  
  
     다른 결과와 연결된 특성이 시각적으로 표시되기 때문에 소득의 지역별 분포와 같은 흥미로운 상관 관계를 쉽게 확인할 수 있습니다.  
  
3.  이 뷰의 기본 데이터를 가져오려면 클릭 **Excel로 복사**합니다. 개별 특성 및 결과 간의 상관 관계를 보여 주는 테이블이 새 워크시트에 생성됩니다. 이 Excel 테이블에서 열을 쉽게 숨기거나 필터링할 수 있습니다.  
  
 [맨 위로 이동](#BKMK_Tabs)  
  
###  <a name="bkmk_AttChar"></a> 특성 특징  
 합니다 **특성 특징** 뷰는 특정 결과 변수와 영향을 주는 요인을 자세하게 데 유용 합니다.  
  
 ![Naive Bayes 뷰어의 특성 특성](media/dm13-nb-viewer.gif "Naive Bayes 뷰어의 특성 특성")  
  
##### <a name="explore-the-attribute-characteristics"></a>특성 특징 탐색  
  
1.  클릭 **값** 에서 항목을 선택 합니다 **값**합니다.  
  
     대상 결과를 선택하면 그래프가 업데이트되어 결과와 가장 밀접하게 관련된 요인이 중요도순으로 표시됩니다.  
  
     사용 하 여 모델을 만든 경우 합니다 [주요 영향 요인 분석 &#40;Excel 용 테이블 분석 도구&#41; ](analyze-key-influencers-table-analysis-tools-for-excel.md) 옵션을 둘 이상의 예측 가능한 특성이 있는 모델을 만들 수 있습니다. 그러나 데이터 마이닝 추가 기능의 다른 모든 마법사는 예측 가능한 특성을 하나로 제한합니다.  
  
2.  클릭 **Excel로 복사** 선택한 대상 결과 관련 된 모든 특성에 대 한 점수를 나열, 새 워크시트에는 테이블을 만듭니다.  
  
 [맨 위로 이동](#BKMK_Tabs)  
  
###  <a name="bkmk_AttDisc"></a> 특성 판별  
 합니다 **특성 판별** 뷰는 두 결과 나 기타 모든 결과 및 한 결과입니다.  
  
 ![특성 판별 Naive Bayes 뷰어의](media/dm13-nb-attdisc.gif "판별 Naive Bayes 뷰어의 특성")  
  
##### <a name="explore-attribute-discrimination"></a>특성 판별 탐색  
  
1.  컨트롤을 사용 하 여 **값 1** 하 고 **값 2**비교 하려는 결과 선택 합니다.  
  
     예를 들어,이 모델에서 몇 가지 흥미로운 특성이에 내용이 소득이 낮은 그룹 하므로 첫 번째 드롭다운 목록에서 가장 낮은 소득 그룹을 선택 하 고 선택한 **다른 모든 상태** 두 번째 드롭다운 목록에서입니다.  
  
     특성은 학습 데이터를 기반으로 계산된 중요도순으로 정렬됩니다. 따라서 직업은 소득과 가장 밀접한 상관 관계가 있는 요인입니다(적어도 이 대상 그룹의 경우).  
  
     정확한 수치를 보려면 색이 지정 된 가로 막대형 및 보기를 클릭 합니다 **마이닝 범례**합니다.  
  
2.  낮은 소득은 유럽 지역과도 상관 관계가 있습니다.  
  
     Naïve Bayes 모델은 드릴다운을 지원하지 않습니다. 이 결과 그룹과 관련된 사례를 조사하려면 쿼리를 사용할 수 있습니다. 이 유형의 모델 쿼리에 대 한 정보를 참조 하세요 [Naive Bayes 모델 쿼리 예제](data-mining/naive-bayes-model-query-examples.md)합니다.  
  
 [맨 위로 이동](#BKMK_Tabs)  
  
## <a name="see-also"></a>관련 항목  
 [Excel에서 모델 찾아보기 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
