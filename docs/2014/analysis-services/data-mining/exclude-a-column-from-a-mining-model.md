---
title: 마이닝 모델에서 열 제외 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- excluding mining model columns
- mining models [Analysis Services], columns
- columns [data mining], excluding
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 656e9dc84c2556cc4f5ea76858764ee9c1fbf556
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48068883"
---
# <a name="exclude-a-column-from-a-mining-model"></a>마이닝 모델에서 열 제외
  새 마이닝 모델을 만들 때 모델의 기반이 되는 마이닝 구조의 일부 열만 사용할 수도 있습니다. 예를 들어 드릴스루를 위해 추가한 고객 이름 열을 모델링에는 사용하지 않으려는 경우가 있습니다. 또는 여러 다른 불연속화가 있는 열의 여러 복사본을 만든 후 각 모델에 해당 복사본 중 하나만 사용하고 나머지는 무시할 수 있습니다. 여러 다른 모델에 입력 열을 선택적으로 추가하여 추가된 변수가 출력 열에 영향을 주는 방식을 확인할 수도 있습니다.  
  
 각 열 조합에 대해 새 마이닝 구조를 만들 필요가 없습니다. 대신, 특정 모델에서 사용되지 않도록 열에 플래그를 지정할 수 있습니다.  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>마이닝 모델에서 열을 제외하려면  
  
1.  **의 데이터 마이닝 디자이너에서** 마이닝 모델 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]탭을 선택하고 해당 마이닝 모델에서 제외할 열에 해당하는 셀을 선택합니다.  
  
2.  드롭다운 목록 상자에서 **무시** 를 선택합니다.  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 모델 태스크 및 방법](mining-model-tasks-and-how-tos.md)  
  
  
