---
title: 모델 뷰어에서 드릴스루 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e5e065ad-c688-4c2c-8c82-7f3038e04915
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3c1cea79210cd5b8e90be2228cba31c714dbf9dc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="use-drillthrough-from-the-model-viewers"></a>모델 뷰어에서 드릴스루 사용
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  모델 유형에 따라 데이터 마이닝 디자이너의 **마이닝 모델 뷰어** 탭에 있는 브라우저 뷰어에서 드릴스루를 사용하여 마이닝 모델에 사용된 사례를 탐색하거나 마이닝 구조의 추가 열을 볼 수 있습니다. 모델의 패턴은 특정 사례에 직접 연결할 수 없으므로 대부분의 모델 유형에서 드릴스루를 지원하지 않지만 다음 모델 유형에서는 드릴스루를 지원합니다.  
  
 모델에 드릴스루가 사용하도록 설정되어 있고 사용자에게 적절한 사용 권한이 있어야 합니다. 또한 모델이 현재 처리되지 않은 상태인 경우에는 모델이 이전에 처리되었고 모델에 내용이 있는지 여부에 관계없이 드릴스루 옵션이 사용하지 않도록 설정될 수도 있습니다. 드릴스루를 사용하여 모델 사례 데이터를 검색하려면 구조 및 모델의 캐시가 최신 상태여야 합니다.  
  
### <a name="use-drillthrough-in-the-microsoft-tree-viewer"></a>Microsoft 트리 뷰어에서 드릴스루 사용  
  
1.  데이터 마이닝 디자이너에서 의사 결정 트리 모델을 선택하고 **모델 찾아보기** 를 선택하여 **Microsoft 트리 뷰어**에서 모델을 엽니다. SQL Server Management Studio에서 모델을 마우스 오른쪽 단추로 클릭하고 **찾아보기**를 선택합니다.  
  
2.  트리 그래프에서 노드를 마우스 오른쪽 단추로 클릭하고 **드릴스루**를 선택합니다.  
  
3.  **모델 열만** 또는 **모델 및 구조 열**옵션 중 하나를 선택합니다. 사용 권한이 없는 경우 옵션을 사용하지 못할 수 있습니다.  
  
4.  **드릴스루** 대화 상자가 열리고 사례 데이터 및/또는 구조 데이터가 표시됩니다. 또한 대화 상자의 제목 표시줄에 드릴스루 쿼리가 실행된 노드를 식별하는 설명이 포함됩니다.  
  
5.  결과의 아무 곳이나 마우스 오른쪽 단추로 클릭하고 **모두 복사** 를 선택하여 결과를 클립보드에 저장합니다.  
  
### <a name="use-drillthrough-in-the-microsoft-cluster-viewer"></a>Microsoft 클러스터 뷰어에서 드릴스루 사용  
  
1.  데이터 마이닝 디자이너에서 클러스터링 모델을 선택하고 **모델 찾아보기** 를 선택하여 **Microsoft 클러스터 뷰어**에서 모델을 엽니다. SQL Server Management Studio에서 모델을 마우스 오른쪽 단추로 클릭하고 **찾아보기**를 선택합니다.  
  
2.  **클러스터** 탭에서 노드를 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **드릴스루**를 선택하고 **모델 열만** 또는 **모델 및 구조 열**옵션 중 하나를 선택합니다. 사용 권한이 없는 경우 옵션을 사용하지 못할 수 있습니다.  
  
4.  **드릴스루** 대화 상자가 열리고 사례 데이터 및/또는 구조 데이터가 표시됩니다. 또한 대화 상자의 제목 표시줄에 사례에 대한 클러스터를 식별하는 설명이 포함됩니다.  
  
5.  결과의 아무 곳이나 마우스 오른쪽 단추로 클릭하고 **모두 복사** 를 선택하여 결과를 클립보드에 저장합니다.  
  
### <a name="use-drillthrough-in-the-microsoft-association-rules-viewer"></a>Microsoft 연결 규칙 뷰어에서 드릴스루 사용  
  
1.  데이터 마이닝 디자이너에서 연결 모델을 선택하고 **모델 찾아보기** 를 선택하여 **Microsoft 연결 규칙 뷰어**에서 모델을 엽니다. SQL Server Management Studio에서 모델을 마우스 오른쪽 단추로 클릭하고 **찾아보기**를 선택합니다.  
  
2.  **규칙** 탭에서 규칙을 나타내는 행을 마우스 오른쪽 단추로 클릭합니다. **항목 집합** 탭에서 항목 집합이 포함된 행을 클릭합니다.  
  
3.  **드릴스루**를 선택하고 **모델 열만** 또는 **모델 및 구조 열**옵션 중 하나를 선택합니다. 사용 권한이 없는 경우 옵션을 사용하지 못할 수 있습니다.  
  
4.  **드릴스루** 대화 상자가 열리고 사례 데이터 및/또는 구조 데이터가 표시됩니다. 또한 대화 상자의 제목 표시줄에 규칙 이름을 식별하는 설명이 포함됩니다.  
  
5.  결과의 아무 곳이나 마우스 오른쪽 단추로 클릭하고 **모두 복사** 를 선택하여 전체 사례 결과를 클립보드에 저장합니다. **복사** 를 선택하여 선택한 사례만 복사할 수도 있습니다. 모델에 중첩 테이블 열이 포함되어 있는 경우 중첩 테이블 열의 이름만 붙여넣어지므로 각 사례의 중첩 테이블 열 내에 있는 데이터 값을 검색하려면 모델 콘텐츠에 대한 쿼리를 만들어야 합니다  
  
### <a name="use-drillthrough-in-the-microsoft-sequence-cluster-viewer"></a>Microsoft 시퀀스 클러스터 뷰어에서 드릴스루 사용  
  
1.  데이터 마이닝 디자이너에서 클러스터링 모델을 선택하고 **모델 찾아보기** 를 선택하여 **Microsoft 클러스터 뷰어**에서 모델을 엽니다. SQL Server Management Studio에서 모델을 마우스 오른쪽 단추로 클릭하고 **찾아보기**를 선택합니다.  
  
2.  **클러스터 다이어그램**탭에서 클러스터를 나타내는 노드를 마우스 오른쪽 단추로 클릭합니다. **클러스터 프로필** 탭에서 클러스터 프로필 또는 전체 모델 모집단을 나타내는 클러스터의 아무 곳이나 클릭합니다.  
  
3.  **드릴스루**를 선택하고 **모델 열만** 또는 **모델 및 구조 열**옵션 중 하나를 선택합니다. 사용 권한이 없는 경우 옵션을 사용하지 못할 수 있습니다.  
  
4.  **드릴스루** 대화 상자가 열리고 사례 데이터 및/또는 구조 데이터가 표시됩니다. 또한 대화 상자의 제목 표시줄에 사례에 대한 클러스터를 식별하는 설명이 포함됩니다.  
  
5.  결과의 아무 곳이나 마우스 오른쪽 단추로 클릭하고 **모두 복사** 를 선택하여 결과를 클립보드에 저장합니다. 모델에 중첩 테이블 열이 포함되어 있는 경우 중첩 테이블 열의 이름만 붙여넣어지므로 각 사례의 중첩 테이블 열 내에 있는 데이터 값을 검색하려면 모델 콘텐츠에 대한 쿼리를 만들어야 합니다  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 모델 뷰어 태스크 및 방법](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [마이닝 모델에서의 드릴스루](../../analysis-services/data-mining/drillthrough-on-mining-models.md)   
 [마이닝 구조에서 드릴스루](../../analysis-services/data-mining/drillthrough-on-mining-structures.md)  
  
  
