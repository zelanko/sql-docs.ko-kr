---
title: 차원 순서 정의 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2306e5d8c7414967e82c79e89449930c389cb4ba
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="bi-wizard---define-the-ordering-for-a-dimension"></a>BI 마법사-차원 순서 정의
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  큐브나 차원에 특성 순서 지정 기능을 추가하여 특성 멤버의 순서 지정 방식을 지정할 수 있습니다. 특성의 이름이나 키 또는 특성 관계를 기반으로 하는 다른 특성의 이름이나 키를 기준으로 멤버 순서를 지정할 수 있습니다. 기본적으로 멤버는 이름을 기준으로 순서가 지정됩니다. 이 기능은 차원의 특성에 대한 **OrderBy** 및 **OrderByAttributeID** 속성 설정을 변경합니다.  
  
 특성 순서 지정 기능을 추가하려면 비즈니스 인텔리전스 마법사의 **기능 선택** 페이지에서 **특성 순서 지정** 옵션을 선택합니다. 그런 다음 마법사의 안내를 따라 특성 순서 지정을 적용할 차원을 선택하고 선택한 차원에 대한 특성의 순서를 지정하는 방식을 선택합니다.  
  
## <a name="selecting-a-dimension"></a>차원 선택  
 마법사의 첫 번째 **특성 순서 지정** 페이지에서 특성 순서 지정을 적용할 차원을 지정합니다. 선택한 차원에 특성 순서 지정 기능을 추가하면 차원이 변경됩니다. 이러한 변경 내용은 선택된 차원을 포함하는 모든 큐브에 상속됩니다.  
  
## <a name="specifying-ordering"></a>순서 지정  
 마법사의 두 번째 **특성 순서 지정** 페이지에서 차원에 있는 모든 특성의 순서를 지정하는 방식을 지정합니다.  
  
 **순서 특성** 열에서 순서 지정에 사용할 특성을 변경할 수 있습니다. 멤버 순서 지정에 사용 하려는 특성 목록에 없으면 목록 아래로 스크롤한 다음 선택  **\<새 특성... >** 열려는 **열 선택** 할 수 있는 대화 상자 차원 테이블의 열을 선택 합니다. **열 선택** 대화 상자에서 열을 선택하면 특성의 멤버 순서를 지정하는 추가 특성이 생성됩니다.  
  
 그런 다음 **조건** 열에서 **키** 또는 **이름**을 중에서 어떤 기준으로 특성 멤버의 순서를 지정할 것인지 선택합니다.  
  
  
