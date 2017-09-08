---
title: "마이닝 모델 속성 | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], properties
- data mining [Analysis Services], properties
- columns [data mining], properties
- Data Mining Designer
- properties [data mining]
ms.assetid: c5194619-8b31-42be-a95f-585711462945
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1fa45b604df0a118936f903491e707bd09d58295
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="mining-model-properties"></a>마이닝 모델 속성
  마이닝 모델의 속성은 다음과 같습니다.  
  
-   마이닝 구조에서 상속되며, 모델에서 사용하는 데이터의 데이터 형식 및 내용 유형을 정의하는 속성  
  
-   마이닝 모델을 만드는 데 사용된 알고리즘과 관련된 속성(사용자 지정 매개 변수 포함)  
  
-   모델을 학습하는 데 사용된 모델의 필터를 정의하는 속성  
  
 마이닝 모델의 속성은 모델을 만들 때 초기에 정의됩니다. 그러나 알고리즘 매개 변수, 필터 및 열 사용법 속성을 포함하여 대부분의 속성을 나중에 변경할 수 있습니다. 데이터 마이닝 디자이너의 **마이닝 모델** 탭을 사용하거나 AMO 또는 XMLA를 사용하여 속성을 변경할 수 있습니다.  
  
 모델의 속성을 변경할 때마다 모델을 다시 처리해야 변경 내용이 모델에 반영됩니다. 열 별칭 또는 설명 추가와 같이 메타데이터만 변경한 경우에도 다시 처리해야 합니다.  
  
## <a name="properties-of-models"></a>모델의 속성  
 다음 표에서는 마이닝 모델에 특정한 속성에 대해 설명합니다. 또한 마이닝 시 개별 열에 대해 설정할 수 있는 속성도 나와 있습니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**알고리즘**|마이닝 모델에 대한 알고리즘 유형을 설정합니다.|  
|**AlgorithmParameters**|각 알고리즘 유형에 사용할 수 있는 알고리즘 매개 변수의 값을 설정합니다.|  
|**필터**|마이닝 모델을 학습하고 테스트할 때 사용하는 데이터에 적용되는 필터를 설정합니다. 필터 정의는 모델에 저장되며 예측 쿼리를 만들거나 모델의 정확도를 테스트할 때 선택적으로 사용할 수 있습니다.<br /><br /> 모델을 학습할 경우 모델 필터는 선택 사항이 아닙니다.|  
|**이름**|마이닝 모델의 이름을 설정합니다.|  
|**AllowDrillThrough**|드릴스루를 마이닝 모델에 설정할지 여부를 지정합니다.|  
  
## <a name="properties-of-model-columns"></a>모델 열의 속성  
 마이닝 모델의 각 열에 대해 다음 데이터 마이닝 속성을 설정할 수 있습니다. 마이닝 구조의 각 마이닝 모델에 대해 이러한 속성을 서로 다른 값으로 설정할 수 있습니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**Description**|마이닝 열의 목적을 설명합니다.|  
|**이름**|마이닝 모델 열의 이름을 설정합니다. 새 이름을 입력하여 마이닝 모델 열의 별칭을 제공할 수 있습니다.|  
|**ModelingFlags**|열에 대해 알고리즘별 플래그를 설정합니다.|  
|**SourceColumnID**|모델 열의 기반이 되는 마이닝 구조 열의 이름을 나타냅니다.<br /><br /> 이 속성은 읽기 전용입니다.|  
|**사용법**|마이닝 모델에서 열을 사용하는 방법을 설정합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 모델 열](../../analysis-services/data-mining/mining-model-columns.md)   
 [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [마이닝 모델 태스크 및 방법](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [마이닝 모델의 속성 변경](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)   
 [데이터 마이닝 도구](../../analysis-services/data-mining/data-mining-tools.md)   
 [관계형 마이닝 구조 만들기](../../analysis-services/data-mining/create-a-relational-mining-structure.md)   
 [모델 열의 별칭 만들기](../../analysis-services/data-mining/create-an-alias-for-a-model-column.md)  
  
  
