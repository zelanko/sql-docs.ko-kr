---
title: Visio (데이터 마이닝 추가 기능)에서 데이터 마이닝 모델 보기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagram, modifying
- templates [Visio]
- shapes, data mining
- diagram
ms.assetid: 5841adea-6650-4fae-8526-26af33edbede
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9dbb4e78685982dc3b7cd981fc6df6db9bf40a13
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37259359"
---
# <a name="viewing-data-mining-models-in-visio-data-mining-add-ins"></a>Visio에서 데이터 마이닝 모델 보기(데이터 마이닝 추가 기능)
  데이터 마이닝용 Visio 셰이프를 사용하여 서버에 연결하고 기존 데이터 마이닝 모델을 나타내는 다이어그램을 만들 수 있습니다. 그런 다음 Visio 컨트롤을 사용하여 다이어그램을 사용자 지정할 수 있지만, 데이터로 드릴다운하고, 일부 기본 통계를 노출하고, 기본 모델을 사용할 수도 있습니다.  
  
## <a name="building-a-model-diagram"></a>모델 다이어그램 작성  
 데이터 마이닝용 Visio 셰이프를 포함 하는 파일을 열면 합니다 **셰이프** 창에는 다음 셰이프가 표시 됩니다.  
  
 Visio를 열 때 데이터 마이닝 셰이프가 표시되지 않으면 설치 폴더에서 템플릿 파일을 엽니다.  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 셰이프를 사용하려면 셰이프를 페이지로 끌어서 놓습니다. 각 셰이프에 대해 원본 데이터 선택, 특정 다이어그램 유형에 대한 옵션 설정, 음영 및 다른 표시 옵션 지정을 돕는 다른 마법사가 열립니다.  
  
 다음 표에는 각 다이어그램 유형에 사용할 수 있는 모델 유형이 나열되어 있습니다.  
  
|Visio 셰이프|지원되는 모델|  
|-----------------|----------------------|  
|의사 결정 트리|의사 결정 트리 또는 선형 회귀 알고리즘을 기반으로 하는 모델에 이 셰이프를 사용합니다.|  
|종속성 네트워크|이 셰이프를 사용 하 여 다음과 같은 알고리즘 중 하나에 따라 모델에 대 한: Naive Bayes, 의사 결정 트리 또는 연결 규칙입니다.|  
|클러스터|클러스터링 알고리즘을 기반으로 하는 모델에 이 셰이프를 사용합니다.|  
  
 마이닝 모델의 데이터 형식에 따라 마법사에서 제공하는 옵션이 다를 수 있습니다. 예를 들어, 연속 숫자를 포함하는 열은 범주 변수를 포함하는 열과 다르게 시각화됩니다.  
  
## <a name="working-with-completed-shapes"></a>완성된 셰이프 사용  
 다이어그램이 완료되면 이 다이어그램을 사용하여 데이터 마이닝 모델을 탐색하거나 프레젠테이션에 맞게 다이어그램을 향상시킬 수 있습니다.  
  
### <a name="visio-menus"></a>Visio 메뉴  
 Visio는 다이어그램 향상을 위한 다양한 렌더링 컨트롤, 테마 및 바로 가기 메뉴를 제공합니다.  
  
-   Visio 테마를 사용하여 다이어그램 색을 변경합니다.  
  
-   커넥터 또는 다이어그램 레이아웃을 변경합니다.  
  
### <a name="data-mining-menus"></a>데이터 마이닝 메뉴  
 이들 도구 모음과 메뉴 항목은 각 셰이프나 모델 형식과 관련된 추가 기능에서 제공합니다.  
  
-   각 다이어그램 유형에는 특수 옵션에 액세스할 수 있도록 지원하는 셰이프에 대한 바로 가기 메뉴가 포함되어 있습니다. 이 메뉴의 많은 옵션이 모든 Visio 셰이프에 공통적인 것이지만 일부 옵션은 데이터 마이닝 템플릿에 고유합니다.  
  
     예를 들어 의사 결정 트리 다이어그램에서 개별 노드를 클릭하고 자식 노드를 축소하여 다이어그램을 더 단순하게 만들거나 자식 노드를 별도 페이지로 옮길 수 있습니다.  
  
-   모델 데이터에 셰이프가 바인딩되기 때문에 다이어그램을 통한 탐색도 어느 정도 가능합니다.  
  
     표시되는 노드를 필터링하거나 트리 수준 또는 그래프 깊이를 변경합니다.  
  
     특정 섹션을 확대하고 특정 특성이 포함된 노드를 검색하거나 가장자리별로 종속성 그래프를 필터링합니다(확률).  
  
## <a name="walkthroughs"></a>연습  
 완료된 다이어그램에서 작업하거나 해석하는 방법에 대한 예는 다음 항목을 참조하십시오.  
  
 [클러스터 다이어그램 연습](cluster-diagram-walkthrough-data-mining-add-ins.md)  
  
 [종속성 네트워크 다이어그램 연습](dependency-network-diagram-walkthrough-data-mining-add-ins.md)  
  
 [의사 결정 트리 다이어그램 연습](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
## <a name="see-also"></a>관련 항목  
 [Excel에서 모델 찾아보기 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
