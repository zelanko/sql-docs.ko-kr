---
title: 알고리즘 매개 변수 대화 상자 (마이닝 모델 뷰) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.models.algorithmparameters.f1
helpviewer_keywords:
- Algorithm Parameters dialog box
ms.assetid: 57f9f6f8-8ca4-4a6e-8f18-85f0571b7060
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dc3d863889f7e5cb8ca1e79f78e920aedd79f979
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62473495"
---
# <a name="algorithm-parameters-dialog-box-mining-models-view"></a>알고리즘 매개 변수 대화 상자(마이닝 모델 뷰)
  **알고리즘 매개 변수** 대화 상자를 사용하여 선택한 모델에 해당하는 알고리즘 매개 변수를 조정할 수 있습니다. 알고리즘 매개 변수를 변경하면 항상 마이닝 모델의 결과가 변경됩니다. 각 매개 변수가 결과에 영향을 미치는 방식은 사용 중인 알고리즘과 데이터에 따라 달라집니다. 자세한 내용은 [마이닝 모델 및 구조 사용자 지정](data-mining/customize-mining-models-and-structure.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **매개 변수**  
 선택한 마이닝 모델에 사용할 수 있는 매개 변수를 나열합니다.  
  
 다음 목록에서는 사용 가능한 열에 대해 설명합니다.  
  
|Column|Description|  
|------------|-----------------|  
|**매개 변수**|매개 변수의 이름을 나열합니다.|  
|**Value**|매개 변수의 기본값을 변경하려는 경우에만 값을 입력합니다.|  
|**Default**|**값** 열에 값을 입력하지 않은 경우 알고리즘에서 사용할 매개 변수의 기본값을 나열합니다.|  
|**범위**|**값** 열에 입력할 수 있는 값의 범위를 나열합니다. 범위는 다음 중 하나일 수 있습니다.<br /><br /> 1, 2, 3과 같은 불연속 목록<br /><br /> [0, 100]와 같은 포함 범위<br /><br /> (0,...)와 같은 배타적 범위<br /><br /> [0,...)와 같은 조합|  
  
 **설명**  
 **매개 변수** 목록에서 선택한 매개 변수에 대해 설명합니다.  
  
 **추가**  
 목록에 알고리즘 특정 매개 변수를 추가하려면 클릭합니다. 매개 변수를 추가한 다음에는 **매개 변수** 열에 올바른 이름을 입력하고 **값** 열에 값을 입력할 수 있습니다.  
  
 **제거**  
 목록에서 사용자 지정 매개 변수를 삭제하려면 클릭합니다.  
  
 목록에서 표준 Analysis Services 알고리즘 매개 변수 중 하나를 삭제하는 경우에도 매개 변수가 계속 모델에 사용되지만 해당 매개 변수의 기본값으로 사용됩니다. 매개 변수는 영구적으로 삭제되지 않으며 다음에 대화 상자를 열면 나타납니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰 &#40;데이터 마이닝 모델 디자이너&#41;](mining-models-view-data-mining-model-designer.md)   
 [데이터 마이닝 개체 이동](data-mining/moving-data-mining-objects.md)  
  
  
