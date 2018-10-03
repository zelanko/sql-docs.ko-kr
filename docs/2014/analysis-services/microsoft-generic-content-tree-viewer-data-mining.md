---
title: Microsoft 일반 콘텐츠 트리 뷰어 (데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.contentviewer.f1
ms.assetid: 751b4393-f6fd-48c1-bcef-bdca589ce34c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dff4254252523096b187bb2894782fe9eea523be
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48066960"
---
# <a name="microsoft-generic-content-tree-viewer-data-mining"></a>Microsoft 일반 콘텐츠 트리 뷰어(데이터 마이닝)
  **Microsoft 일반 콘텐츠 트리 뷰어** 에는 표준화된 HTML 테이블 형식으로 데이터 마이닝 모드의 콘텐츠에 대한 세부 정보가 표시됩니다. 이 뷰는 모델의 기본 구조뿐만 아니라 계수, 값 분포 등에 대한 세부 정보를 표시하기 때문에 유용합니다.  
  
 이 테이블에 표시되는 실제 콘텐츠는 사용된 알고리즘에 따라 달라지며 열, 규칙, 속성, 특성, 노드 및 수식을 포함할 수 있습니다. 모델 콘텐츠 및 각 모델 유형에 대한 정보를 해석하는 방법에 대한 자세한 내용은 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/mining-model-content-analysis-services-data-mining.md)를 참조하세요.  
  
 뷰어에 표시되는 정보는 마이닝 모델의 콘텐츠 스키마 행 집합을 기반으로 하는 공용 구조를 사용합니다. 콘텐츠 스키마 행 집합은 데이터 마이닝 모델의 기타 콘텐츠, 통계 및 패턴 저장에 대한 일반 프레임워크입니다. 마이닝 모델에 대한 데이터 마이닝 스키마 행 집합의 열 목록은 [DMSCHEMA_MINING_MODEL_CONTENT 행 집합](schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **노드 캡션 (고유 ID)**  
 이 창에는 선택한 마이닝 모델에 있는 모든 노드 목록이 표시됩니다. 노드가 트리에 정렬되는 방식은 보고 있는 모델의 유형에 따라 다릅니다.  
  
 각 노드를 클릭하여 **노드 자세히 보기** 창에 노드에 대한 세부 정보를 표시할 수 있습니다.  
  
 **노드 자세히 보기**  
 선택한 노드의 콘텐츠에 대한 세부 정보를 표시합니다. 각 노드는 표준화된 형식으로 정보를 저장하지만 테이블에 있는 각 줄의 콘텐츠과 의미는 보고 있는 노드의 유형이나 모델의 유형에 따라 다릅니다. 예를 들어 연결 모델의 규칙을 나타내는 노드에 대해 저장된 정보에는 의사 결정 트리 모델의 트리를 나타내는 노드와 다른 정보가 포함됩니다.  
  
 특정 모델 유형에 대한 노드 정보를 해석하는 방법에 대한 자세한 내용은 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/mining-model-content-analysis-services-data-mining.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘 &#40;Analysis Services-데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어 &#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 쿼리](data-mining/data-mining-queries.md)  
  
  
