---
title: 향상 된 기능 (비즈니스 인텔리전스 마법사)를 선택 합니다. | Microsoft Docs
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
- sql12.asvs.biwizard.bienhancement.f1
ms.assetid: 39e2f36c-2c02-4a71-af8f-5dbd373190dc
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 35634d3094647cd7698ec1961b94cb2b6b5744e6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243983"
---
# <a name="choose-enhancement-business-intelligence-wizard"></a>기능 선택(비즈니스 인텔리전스 마법사)
  **기능 선택** 페이지를 사용하여 큐브 또는 차원에 추가할 비즈니스 인텔리전스 기능을 선택할 수 있습니다.  
  
## <a name="options"></a>변수  
 **사용 가능한 기능**  
 추가할 비즈니스 인텔리전스 기능을 선택합니다. 다음 표에서는 사용 가능한 기능을 나열합니다.  
  
|기능|Description|  
|-----------------|-----------------|  
|**시간 인텔리전스 정의**|선택한 계층에 대한 시간 보기를 추가합니다. 여기에는 월간 누계 보기, 이동 평균 보기 및 기간별 누계 보기가 포함됩니다.<br /><br /> 참고: 이 옵션은 큐브에 대해서만 사용할 수 있습니다.|  
|**계정 인텔리전스 정의**|계정 특성의 멤버에 대해 수입 및 지출과 같은 표준 계정 분류를 할당합니다.<br /><br /> 측정값에 대한 집계 함수를 *ByAccount*로 설정하면 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스는 계정 분류를 사용하여 시간별 계정 특성 멤버의 측정값을 집계합니다.|  
|**차원 인텔리전스 정의**|차원 인텔리전스를 사용하여 차원의 표준 비즈니스 유형 및 차원 특성에 유효한 유형을 지정할 수 있습니다. 클라이언트 응용 프로그램은 데이터를 분석할 때 이러한 유형 지정을 사용할 수 있습니다.|  
|**단항 연산자 지정**|큐브에 포함된 부모-자식 계층의 멤버와 연결된 기본 집계를 대체할 단항 연산자를 지정합니다.<br /><br /> 참고: 이 옵션은 큐브에 대해서만 사용할 수 있습니다.|  
|**사용자 지정 멤버 수식 만들기**|다른 연산자를 사용하여 차원 멤버와 연결된 기본 집계를 대체할 사용자 지정 멤버 수식을 만듭니다.|  
|**특성 순서 지정**|선택한 특성 멤버의 정렬 방법을 지정합니다. 선택한 특성의 이름이나 키 또는 선택한 특성과 관련된 특성의 이름이나 키를 기준으로 멤버를 정렬할 수 있습니다. 기본적으로 멤버는 선택한 특성의 이름을 기준으로 정렬됩니다.|  
|**차원 쓰기 저장을 사용 하도록 설정**|차원 구조를 수동으로 수정할 수 있게 해줍니다. 쓰기 가능 차원에 대한 업데이트는 차원 테이블에 직접 기록됩니다.|  
|**반 가산적 동작 정의**|계정 유형 특성의 개별 측정값 또는 멤버에 대해 집계 메서드를 수동으로 정의합니다. 큐브에 계정 차원이 있으면 **계정 인텔리전스 정의** 옵션을 사용하여 계정 유형을 기준으로 반가산적 동작을 자동으로 설정할 수 있습니다.<br /><br /> 참고: 이 옵션은 큐브에 대해서만 사용할 수 있습니다.|  
|**통화 변환 정의**|큐브의 다국적 데이터 변환 및 분석 규칙을 정의합니다. 변환 규칙은 비즈니스 인텔리전스 마법사에서 생성된 MDX(Multidimensional Expressions) 스크립트를 사용하여 큐브에 적용됩니다.<br /><br /> 참고: 이 옵션은 큐브에 대해서만 사용할 수 있습니다.|  
  
 **설명**  
 선택한 비즈니스 인텔리전스 기능에 대한 간단한 설명을 입력합니다.  
  
## <a name="see-also"></a>관련 항목  
 [비즈니스 인텔리전스 마법사 F1 도움말](business-intelligence-wizard-f1-help.md)   
 [큐브 디자이너 &#40;Analysis Services-다차원 데이터&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [차원 디자이너 &#40;Analysis Services-다차원 데이터&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
