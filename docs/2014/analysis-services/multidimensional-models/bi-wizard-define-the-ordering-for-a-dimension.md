---
title: 차원에 대 한 순서 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- OrderBy property
- dimensions [Analysis Services], ordering
- Business Intelligence enhancements [Analysis Services], ordering
- dimensions [Analysis Services], Business Intelligence enhancements
- ordering dimensions [Analysis Services]
- OrderByAttributeID property
ms.assetid: c42fbd58-244d-4e0a-b715-6f919cbc3ad9
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8cd5ea148e374c18c530ba0a15c80dbb23983020
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544585"
---
# <a name="define-the-ordering-for-a-dimension"></a>차원 순서 정의
  큐브나 차원에 특성 순서 지정 기능을 추가하여 특성 멤버의 순서 지정 방식을 지정할 수 있습니다. 특성의 이름이나 키 또는 특성 관계를 기반으로 하는 다른 특성의 이름이나 키를 기준으로 멤버 순서를 지정할 수 있습니다. 기본적으로 멤버는 이름을 기준으로 순서가 지정됩니다. 이 기능은 차원의 특성에 대한 `OrderBy` 및 `OrderByAttributeID` 속성 설정을 변경합니다.  
  
 특성 순서 지정 기능을 추가하려면 비즈니스 인텔리전스 마법사의 **기능 선택** 페이지에서 **특성 순서 지정** 옵션을 선택합니다. 그런 다음 마법사의 안내를 따라 특성 순서 지정을 적용할 차원을 선택하고 선택한 차원에 대한 특성의 순서를 지정하는 방식을 선택합니다.  
  
## <a name="selecting-a-dimension"></a>차원 선택  
 마법사의 첫 번째 **특성 순서 지정** 페이지에서 특성 순서 지정을 적용할 차원을 지정합니다. 선택한 차원에 특성 순서 지정 기능을 추가하면 차원이 변경됩니다. 이러한 변경 내용은 선택된 차원을 포함하는 모든 큐브에 상속됩니다.  
  
## <a name="specifying-ordering"></a>순서 지정  
 마법사의 두 번째 **특성 순서 지정** 페이지에서 차원에 있는 모든 특성의 순서를 지정하는 방식을 지정합니다.  
  
 **순서 특성** 열에서 순서 지정에 사용할 특성을 변경할 수 있습니다. 멤버를 정렬 하는 데 사용 하려는 특성이 목록에 없는 경우 목록을 아래로 스크롤하여 선택한 다음 **\<New attribute...>** **열** 선택 대화 상자를 열어 차원 테이블의 열을 선택할 수 있습니다. **열 선택** 대화 상자에서 열을 선택하면 특성의 멤버 순서를 지정하는 추가 특성이 생성됩니다.  
  
 그런 다음 **조건** 열에서 **키** 또는 **이름**을 중에서 어떤 기준으로 특성 멤버의 순서를 지정할 것인지 선택합니다.  
  
  
