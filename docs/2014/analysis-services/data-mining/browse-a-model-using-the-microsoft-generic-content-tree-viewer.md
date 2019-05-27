---
title: Microsoft 일반 콘텐츠 트리 뷰어를 사용 하 여 모델 찾아보기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining model content, viewing
ms.assetid: 4a5f7c51-c704-4214-b05d-21cf735e6d96
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bb080721ccb3e5b5aef190eda3d1088df09762c0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086065"
---
# <a name="browse-a-model-using-the-microsoft-generic-content-tree-viewer"></a>Microsoft 일반 콘텐츠 트리 뷰어를 사용하여 모델 찾아보기
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 일반 마이닝 모델 콘텐츠 뷰어는 마이닝 알고리즘을 통해 발견된 패턴에 대한 자세한 정보를 제공하며, 분석 프로세스 중에 생성된 다양한 통계에 대한 액세스도 제공합니다. 정보의 양과 유형은 사용된 알고리즘에 따라 다르지만 다음과 같은 범주가 있습니다.  
  
-   데이터 세그먼트 및 특징  
  
-   각 그룹 또는 전체 데이터 집합에 대한 기술 통계  
  
-   트리의 분기 또는 자식 노드 수  
  
-   클러스터 또는 전체 데이터 집합에 대한 계산(예: 분산 또는 평균)  
  
 이러한 정보를 보면 분석 결과를 보다 잘 이해하는 데 도움이 됩니다. 또한 모델을 미세 조정한 다음 다시 학습하는 방법도 확인할 수 있습니다. 또는 다른 알고리즘을 사용하여 다시 학습하도록 결정할 수도 있습니다.  
  
## <a name="viewing-mining-model-content"></a>마이닝 모델 콘텐츠 보기  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 일반 콘텐츠 뷰어에는 마이닝 모델 *콘텐츠 스키마 행 집합* 의 열, 규칙, 속성, 특성, 노드 및 기타 콘텐츠가 표시됩니다. 콘텐츠 스키마 행 집합은 데이터 마이닝 모델의 콘텐츠에 대한 세부 정보를 나타내는 일반 프레임워크입니다.  
  
 이 자세한 정보는 모델의 패턴, 클러스터 또는 트리를 노드로 나타내는 HTML 테이블에 포함되어 있습니다. 각 노드를 클릭하고 확장하여 숫자 특성의 고유 값 개수 또는 수식과 같은 자세한 세부 정보를 볼 수 있습니다. 노드 간의 자식-부모 관계를 탐색할 수도 있습니다.  
  
 마이닝 모델 콘텐츠에 사용된 용어의 일반적인 의미에 대한 자세한 내용은 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-analysis-services-data-mining.md)를 참조하세요. 항목에는 특정 모델 유형의 마이닝 모델 콘텐츠에 대한 정보를 볼 수 있는 링크도 포함되어 있습니다. 각 마이닝 모델 유형에 데이터에서 찾은 알고리즘 및 패턴과 관련성이 매우 높은 정보가 포함되어 있으므로 각 모델 유형을 완전히 이해하기 위해 각 모델 유형에 대해 기술 참조 항목을 검토하는 것이 좋습니다.  
  
## <a name="querying-mining-model-content"></a>마이닝 모델 내용 쿼리  
 마이닝 모델을 쿼리하면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 일반 콘텐츠 트리 뷰어에서 제공하는 것과 동일한 정보를 볼 수 있습니다. 마이닝 모델 콘텐츠에 대한 쿼리는 DMX(Data Mining Extensions) 문을 사용하여 만들 수 있습니다. 예를 들어 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 다음 DMX 문을 실행하여 내용 쿼리를 실행할 수 있습니다.  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 자세한 내용은 [데이터 마이닝 쿼리](data-mining-queries.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 일반 콘텐츠 트리 뷰어&#40;데이터 마이닝&#41;](../microsoft-generic-content-tree-viewer-data-mining.md)   
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
  
