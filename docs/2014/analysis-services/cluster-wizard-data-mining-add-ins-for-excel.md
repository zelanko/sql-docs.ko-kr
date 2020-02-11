---
title: 클러스터 마법사 (Excel 용 데이터 마이닝 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [data mining]
ms.assetid: 85b25625-a7ab-4960-9f9c-df22e8ecae37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d93f676aec67b5d791924cbbda8f71a966d5bbc2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087805"
---
# <a name="cluster-wizard-data-mining-add-ins-for-excel"></a>클러스터 마법사(Excel용 데이터 마이닝 추가 기능)
  ![데이터 마이닝 리본의 클러스터 마법사](media/dmc-cluster.gif "데이터 마이닝 리본의 클러스터 마법사")  
  
 클러스터 마법사에서는 비슷한 특성을 공유하는 행을 검색하고 이를 그룹화 하여 그룹 간의 거리를 최대화하는 모델을 작성할 수 있습니다. 이 마법사는 모든 종류의 데이터에서 패턴을 찾는 데 유용합니다.  
  
 클러스터 마법사는 Microsoft 클러스터링 알고리즘을 사용하며 다양한 방식으로 사용자 지정할 수 있습니다. 이 마법사에는 Excel 테이블, Excel 범위 또는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 쿼리의 기존 데이터가 사용됩니다. Excel 용 테이블 분석 도구에 제공 되는 [범주 검색](detect-categories-table-analysis-tools-for-excel.md) 도구에서 비슷한 기능을 제공 합니다. 하지만 범주 검색 도구는 사용자 지정할 수 없으며 Excel 테이블의 데이터를 사용해야 합니다.  
  
## <a name="using-the-cluster-wizard"></a>클러스터 마법사 사용  
  
1.  데이터 마이닝 리본에서 **클러스터**를 클릭 한 후 **다음**을 클릭 합니다.  
  
2.  **원본 데이터 선택** 페이지에서 Excel 테이블 또는 범위를 선택 합니다. 또는 외부 데이터 원본을 지정합니다.  
  
     외부 데이터 원본을 사용할 경우에는 사용자 지정 뷰를 만들거나 사용자 지정 쿼리 텍스트에 붙여 넣고 데이터 집합을 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터 원본으로 저장할 수 있습니다.  
  
3.  **클러스터링** 페이지에서 모델이 빌드되는 방식을 사용자 지정할 수 있습니다.  
  
    -   **세그먼트 수**의 경우 마법사에 고정 된 수의 범주를 만들도록 지시 하거나 최적의 그룹화 수를 자동으로 검색 하도록 할 수 있습니다.  
  
    -   **입력 열** 목록에서 열 목록을 검토 하 고 패턴을 만드는 데 유용 하지 않은 열을 선택 취소 합니다. 제외해야 하는 열에는 ID 번호, 고객 이름 등이 포함됩니다.  
  
4.  필요에 따라 **매개 변수** 를 클릭 하 여 알고리즘 매개 변수를 변경 하 고 클러스터링 모델의 동작을 사용자 지정 합니다.  
  
5.  **학습 및 테스트 집합으로 데이터 분할** 페이지에서 테스트를 위해 유지할 데이터 양을 지정 합니다. 나머지는 항상 모델 학습에 사용됩니다.  
  
     기본 설정은 테스트 데이터 30%와 학습 데이터 70%입니다.  
  
6.  **마침** 페이지에서 데이터 집합 및 모델에 대 한 설명이 포함 된 이름을 입력 하 고 완성 된 모델을 사용 하는 방법을 제어 하는 다음 옵션을 설정 합니다.  
  
    -   **모델 찾아보기**. 이 옵션을 선택 하면 마법사가 모델 처리를 완료 하는 즉시 결과를 탐색 하는 데 도움이 되는 **찾아보기** 창이 열립니다. 뷰어 내용은 작성한 모델 유형에 따라 달라집니다. 자세한 내용은 [클러스터링 모델 찾아보기](browsing-a-clustering-model.md)를 참조 하세요.  
  
    -   **드릴스루를 사용 하도록 설정**합니다. 완료된 모델에서 기본 데이터를 보려면 이 옵션을 선택합니다. 이 옵션은 의사 결정 트리 모델을 작성하는 경우에만 사용할 수 있습니다.  
  
    -   **임시 모델을 사용**합니다. 이 옵션을 선택하면 모델이 서버에 저장되지 않습니다. 임시 모델은 Excel을 닫을 때 삭제됩니다.  
  
## <a name="more-about-clustering-models"></a>클러스터링 모델에 대한 추가 정보  
 **고급** 을 클릭 하 고 **알고리즘 매개 변수** 대화 상자를 사용 하 여이 마법사에서 사용 하는 클러스터링 알고리즘을 변경할 수 있습니다.  
  
 Microsoft 클러스터링 알고리즘은 다음과 같은 클러스터링 방법을 제공합니다.  
  
-   Scalable 또는 Non-scalable K-Means  
  
-   Scalable 또는 Non-scalable EM(Expectation Maximization)  
  
 또한 CLUSTER_SEED 매개 변수를 사용하여 시작 값을 제어하고 동일한 데이터 집합을 사용하는 반복되는 모델의 결과가 동일하도록 만들 수 있습니다.  
  
### <a name="requirements"></a>요구 사항  
 클러스터 마법사를 사용하려면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에 연결해야 합니다. 자세한 내용은 [Excel 용 데이터 마이닝 클라이언트&#41;&#40;원본 데이터에 연결 ](connect-to-source-data-data-mining-client-for-excel.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 모델 만들기](creating-a-data-mining-model.md)   
 [Excel 용 테이블 분석 도구 &#40;범주 검색&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
  
