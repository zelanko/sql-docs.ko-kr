---
title: 마이닝 모델에서 열 제외 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 56ecdc39a08e9fa862d942ab21e08b107af1a339
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="exclude-a-column-from-a-mining-model"></a>마이닝 모델에서 열 제외
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  새 마이닝 모델을 만들 때 모델의 기반이 되는 마이닝 구조의 일부 열만 사용할 수도 있습니다. 예를 들어 드릴스루를 위해 추가한 고객 이름 열을 모델링에는 사용하지 않으려는 경우가 있습니다. 또는 여러 다른 불연속화가 있는 열의 여러 복사본을 만든 후 각 모델에 해당 복사본 중 하나만 사용하고 나머지는 무시할 수 있습니다. 여러 다른 모델에 입력 열을 선택적으로 추가하여 추가된 변수가 출력 열에 영향을 주는 방식을 확인할 수도 있습니다.  
  
 각 열 조합에 대해 새 마이닝 구조를 만들 필요가 없습니다. 대신, 특정 모델에서 사용되지 않도록 열에 플래그를 지정할 수 있습니다.  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>마이닝 모델에서 열을 제외하려면  
  
1.  **의 데이터 마이닝 디자이너에서** 마이닝 모델 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]탭을 선택하고 해당 마이닝 모델에서 제외할 열에 해당하는 셀을 선택합니다.  
  
2.  드롭다운 목록 상자에서 **무시** 를 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 모델 태스크 및 방법](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
