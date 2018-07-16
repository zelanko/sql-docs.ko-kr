---
title: 비즈니스 인텔리전스 마법사를 사용 하 여 시간 인텔리전스 계산 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- period over period growth [Analysis Services]
- parallel period comparisons [Analysis Services]
- Business Intelligence enhancements [Analysis Services], time intelligence
- time views [Analysis Services]
- hierarchies [Analysis Services], time
- time periods [Analysis Services]
- moving averages
- time [Analysis Services]
- period to date [Analysis Services]
- calculations [Analysis Services], time
- time hierarchies [Analysis Services]
- time intelligence [Analysis Services]
ms.assetid: be36e8fc-f46e-4553-8623-b27d695c330b
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 319408b079ce5be4a381e02f47f5189edbde3ed0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295983"
---
# <a name="define-time-intelligence-calculations-using-the-business-intelligence-wizard"></a>비즈니스 인텔리전스 마법사를 사용하여 시간 인텔리전스 계산 정의
  시간 인텔리전스 기능은 선택한 계층에 시간 계산(또는 시간 보기)을 추가하는 큐브 기능입니다. 이 기능은 다음과 같은 계산 범주를 지원합니다.  
  
-   월간 누계  
  
-   기간별 증가  
  
-   이동 평균  
  
-   동일 기간 비교  
  
 시간 차원이 있는 큐브에 시간 인텔리전스를 적용합니다. 시간 차원은 차원의 `Type` 속성이 `Time`으로 설정되어 있는 차원입니다. 또한 해당 차원의 시간 특성에는 관련 `Type` 속성에 대한 적절한 설정(예: Years 또는 Months)이 있어야 합니다. `Type` 차원 마법사를 사용 하 여 시간 차원을 만들면 차원과 차원의 특성 모두의 속성이 올바르게 설정 수 됩니다.  
  
 큐브에 시간 인텔리전스를 추가하려면 비즈니스 인텔리전스 마법사의 **기능 선택** 페이지에서 **시간 인텔리전스 정의** 옵션을 선택합니다. 그런 다음 마법사의 안내를 따라 시간 인텔리전스를 추가할 계층을 선택하고 계층에서 시간 인텔리전스를 적용할 멤버를 지정합니다. 마법사의 마지막 페이지에서 선택한 시간 인텔리전스를 추가하기 위한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 변경 사항을 확인할 수 있습니다.  
  
## <a name="selecting-a-time-hierarchy"></a>시간 계층 선택  
 **대상 계층 및 계산 선택** 페이지에서 시간 기능을 적용할 시간 계층을 선택합니다. 비즈니스 인텔리전스 마법사를 실행할 때마다 시간 계층 하나에만 시간 기능을 적용할 수 있습니다. 여러 시간 계층에 기능을 적용하려면 마법사를 다시 실행해야 합니다.  
  
 시간 계층을 선택한 후 **사용 가능한 시간 계산** 목록에서 계층에 적용할 계산을 선택합니다. 나열 되는 계산은 계층의 수준과에 종속 된 `Type` 각 수준에 대 한 특성에 대 한 속성 설정 합니다. 예를 들어 년 계층은 연간 누계 및 전년동기대비 성장을 지원하지만 분기 계층은 이러한 계산을 지원하지 않습니다.  
  
> [!NOTE]  
>  Timeintelligence.xml 템플릿 파일은 **사용 가능한 시간 계산**에 나열되는 시간 계산을 정의합니다. 나열된 계산이 요구에 맞지 않으면 기존 계산을 변경하거나 Timeintelligence.xml 파일에 새 계산을 추가할 수 있습니다.  
  
> [!TIP]  
>  계산에 대한 설명을 보려면 위와 아래 화살표를 사용하여 원하는 계산을 선택합니다.  
  
## <a name="apply-time-views-to-members"></a>멤버에 시간 보기 적용  
 **계산 범위 정의** 페이지에서 새 시간 보기를 적용할 멤버를 지정합니다. 다음 개체 중 하나에 새 시간 보기를 적용할 수 있습니다.  
  
-   **계정 차원의 멤버**   **계산 범위 정의** 페이지의 **사용 가능한 측정값** 목록에는 계정 차원이 포함됩니다. 계정 차원의 `Type` 속성은 `Accounts`로 설정되어 있습니다. 계정 차원이 있지만 해당 차원이 **사용 가능한 측정값** 목록에 나타나지 않으면 비즈니스 인텔리전스 마법사를 사용하여 해당 차원에 계정 인텔리전스를 적용할 수 있습니다. 자세한 내용은 [차원에 계정 인텔리전스 추가](bi-wizard-add-account-intelligence-to-a-dimension.md)를 참조하세요.  
  
-   **측정값** 계정 차원을 지정하는 대신 시간 보기가 적용될 측정값을 지정할 수 있습니다. 이 경우 선택한 시간 계산을 적용할 보기를 선택합니다. 예를 들어 자산과 부채는 연간 누계 데이터이므로 자산이나 부채 측정값에는 연간 누계 계산을 적용할 필요가 없습니다.  
  
## <a name="viewing-the-time-intelligence-enhancement"></a>시간 인텔리전스 기능 보기  
 비즈니스 인텔리전스 마법사의 마지막 페이지에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 변경 사항을 확인할 수 있습니다. 시간 인텔리전스 기능의 경우 다음 표에서 설명하는 것처럼 마법사에서 선택한 시간 차원, 연결된 데이터 원본 뷰 및 연결된 큐브를 변경합니다.  
  
|Object|변경|  
|------------|------------|  
|시간 차원|각 계산(또는 보기)에 특성을 추가합니다.|  
|데이터 원본 뷰|시간 차원의 각 새 특성에 대한 시간 테이블에 계산 열을 추가합니다.|  
|Cube|계산을 수행하는 MDX(Multidimensional Expressions) 코드를 정의하는 계산 멤버를 추가합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [계산 멤버 만들기](create-calculated-members.md)  
  
  
