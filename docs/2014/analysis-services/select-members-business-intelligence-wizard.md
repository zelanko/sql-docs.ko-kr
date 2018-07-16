---
title: Members (Business Intelligence Wizard)를 선택 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.memberconversion.f1
ms.assetid: 1a147461-d594-41e7-a41d-09d2d003e1e0
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8b1bdcf78e3a7fd35da53e7a39bea5c24e217ae8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321243"
---
# <a name="select-members-business-intelligence-wizard"></a>멤버 선택(비즈니스 인텔리전스 마법사)
  **멤버 선택** 페이지를 사용하여 비즈니스 인텔리전스 마법사가 **통화 변환 옵션 설정** 페이지에 지정된 통화 변환 기능을 적용할 멤버를 결정할 수 있습니다.  
  
> [!NOTE]  
>  이 페이지는 차원 디자이너에서 비즈니스 인텔리전스 마법사를 시작하거나 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 솔루션 탐색기에서 차원을 마우스 오른쪽 단추로 클릭하여 비즈니스 인텔리전스 마법사를 시작할 경우 표시되지 않습니다.  
  
## <a name="options"></a>변수  
 **측정값 차원**  
 큐브에 포함된 하나 이상의 측정값에 통화 변환 기능을 적용하려면 선택합니다.  
  
 선택하면 다음 표에 나열된 옵션이 표에 표시됩니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**기본 제공 측정값 유형**|지정한 측정값에 대한 통화 변환 기능을 포함하려면 선택합니다.|  
|**측정값**|**기본 제공 측정값 유형** 에서 선택한 측정값을 변환할 때 사용할 환율이 포함된 요율 측정값 그룹에서 측정값을 선택합니다.|  
  
 **계정 계층**  
 큐브에 포함된 계정 차원의 계정 계층에서 하나 이상의 멤버에 통화 변환 기능을 적용하려면 선택합니다. 계정 계층은 계정 내에서 계층 구조 차원 `Type` 속성이 *계정*합니다.  
  
 선택하면 다음 표에 나열된 옵션이 표에 표시됩니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**계정 멤버**|지정한 계정 계층 멤버에 대한 통화 변환 기능을 포함하려면 선택합니다.|  
|**측정값**|**계정 멤버** 에서 선택한 멤버의 측정값을 변환할 때 사용할 환율이 포함된 요율 측정값 그룹에서 측정값을 선택합니다.|  
  
 **유형을 기반으로 하는 계정 계층**  
 계정 계층에서의 모든 멤버에 통화 변환 기능을 적용 하려면 선택 특성 `Type` 지정한 계정 유형으로 설정 합니다.  
  
 선택하면 다음 표에 나열된 옵션이 표에 표시됩니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**계정 유형**|지정한 계정 유형에 대한 통화 변환 기능을 포함하려면 선택합니다.|  
|**측정값**|**계정 유형** 에서 선택한 계정 유형을 사용하는 특성 멤버에 대한 측정값을 변환할 때 사용할 환율이 포함된 요율 측정값 그룹에서 측정값을 선택합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [비즈니스 인텔리전스 마법사 F1 도움말](business-intelligence-wizard-f1-help.md)   
 [큐브 디자이너 &#40;Analysis Services-다차원 데이터&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [차원 디자이너 &#40;Analysis Services-다차원 데이터&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
