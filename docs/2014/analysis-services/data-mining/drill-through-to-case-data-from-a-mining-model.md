---
title: 마이닝 모델에서 사례 데이터로 드릴스루 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- drillthrough [Analysis Services]
ms.assetid: b4d3f350-e543-4ea9-b3a2-b4f7c0a9ae27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ed7750ac0f09fd90ffd846fa4257eb5aae25546
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48062629"
---
# <a name="drill-through-to-case-data-from-a-mining-model"></a>마이닝 모델에서 사례 데이터로 드릴스루
  모델 사례로 드릴스루할 수 있도록 마이닝 모델을 구성한 경우 모델을 찾을 때 모델을 만드는 데 사용된 사례에 대한 세부 정보를 검색할 수 있습니다. 또한 구조 사례로의 드릴스루를 허용하도록 기본 마이닝 구조를 구성했으며 적절한 권한이 있는 경우 마이닝 구조에서 정보를 반환할 수 있습니다. 여기에는 마이닝 모델에 포함되지 않은 열이 포함될 수 있습니다.  
  
 기본 데이터로의 드릴스루가 마이닝 구조에서는 허용되지 않지만 마이닝 모델에서는 허용되는 경우 마이닝 구조가 아닌 모델 사례에서 정보를 볼 수 있습니다.  
  
> [!NOTE]  
>  `AllowDrillthrough` 속성을 `True`로 설정하여 기존 마이닝 모델에 드릴스루 기능을 추가할 수 있습니다. 그러나 드릴스루를 사용하도록 설정한 후에는 모델을 다시 처리해야 사례 데이터를 볼 수 있습니다. 자세한 내용은 [마이닝 모델에 드릴스루 사용](enable-drillthrough-for-a-mining-model.md)을 참조하세요.  
  
 사용하는 뷰어 유형에 따라 다음과 같은 방법으로 드릴스루할 노드를 선택할 수 있습니다.  
  
|뷰어 이름|창 또는 탭 이름|노드 선택|  
|-----------------|----------------------|-----------------|  
|**Microsoft 트리 뷰어**|**의사 결정 트리** 탭|트리 노드를 클릭합니다.<br /><br /> **참고** 드릴스루를 사용 하지 않도록 합니다 `All` 노드, 결과 반환 하려면 시간이 오래 걸릴 수 있으므로 합니다.|  
|**Microsoft 클러스터 뷰어**|**클러스터 다이어그램**|클러스터 노드를 클릭합니다.|  
|**Microsoft 클러스터 뷰어**|**클러스터 프로필**|클러스터 열의 아무 곳이나 클릭합니다.|  
|**Microsoft 연결 뷰어**|**규칙** 탭|규칙 집합을 포함하는 행을 클릭합니다.|  
|**Microsoft 연결 뷰어**|**항목 집합** 탭|항목 집합을 포함하는 행을 클릭합니다.|  
|**Microsoft 시퀀스 클러스터링 뷰어**|**규칙** 탭|규칙 집합을 포함하는 행을 클릭합니다.|  
|**Microsoft 시퀀스 클러스터링 뷰어**|**항목 집합** 탭|항목 집합을 포함하는 행을 클릭합니다.|  
  
> [!NOTE]  
>  일부 모델에서는 드릴스루를 사용할 수 없습니다. 드릴스루를 사용할 수 있는지 여부는 모델을 만드는 데 사용된 알고리즘에 따라 달라집니다. 드릴스루를 지원하는 마이닝 모델 유형 목록은 [드릴스루 쿼리&#40;데이터 마이닝&#41;](drillthrough-queries-data-mining.md)를 참조하세요.  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>마이닝 모델에서 드릴스루 데이터를 보려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 마이닝 모델을 포함하는 마이닝 구조를 엽니다.  
  
2.  데이터 마이닝 디자이너에서 **마이닝 모델 뷰어** 탭을 클릭합니다.  
  
3.  **마이닝 모델** 드롭다운 목록에서 모델을 선택합니다.  
  
4.  **뷰어** 드롭다운 목록에서 뷰어를 선택하고 특정 노드를 마우스 오른쪽 단추로 클릭합니다.  
  
5.  **드릴스루**를 선택한 다음 **모델 열만**또는 **모델 및 구조 열** 을 선택하여 **드릴스루** 창을 엽니다.  
  
6.  데이터를 클립보드에 복사하려면 테이블에서 임의의 행을 마우스 오른쪽 단추로 클릭하고 **모두 복사**를 선택합니다.  
  
## <a name="see-also"></a>관련 항목  
 [드릴스루 쿼리 &#40;데이터 마이닝&#41;](drillthrough-queries-data-mining.md)  
  
  
