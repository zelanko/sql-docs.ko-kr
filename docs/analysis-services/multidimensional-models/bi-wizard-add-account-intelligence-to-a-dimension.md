---
title: "차원에 계정 인텔리전스 추가 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], Business Intelligence enhancements
- Business Intelligence enhancements [Analysis Services], account intelligence
- account intelligence [Analysis Services]
ms.assetid: 36f454ae-a9f2-4a59-b19d-40310af9f901
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: defce52a3e89858c08eff6626601392066996891
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="bi-wizard---add-account-intelligence-to-a-dimension"></a>BI 마법사-차원에 계정 인텔리전스 추가
  계정 특성의 멤버에 대해 수입 및 비용과 같은 표준 계정 분류를 할당하려면 큐브나 차원에 향상된 계정 인텔리전스 기능을 추가합니다. 이러한 향상된 기능을 사용하면 Asset, Liability 등의 계정 유형을 식별할 수 있으며 각 계정 유형에 적절한 집계를 할당할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 분류를 사용하여 시간별로 계정을 집계할 수 있습니다.  
  
> [!NOTE]  
>  계정 인텔리전스는 기존 데이터 원본 기반의 차원에만 사용할 수 있습니다. 데이터 원본을 사용하지 않고 만든 차원의 경우 계정 인텔리전스를 추가하기 전에 스키마 생성 마법사를 실행하여 데이터 원본 뷰를 만들어야 합니다.  
  
 계정 이름, 계정 번호, 계정 유형 등의 계정 정보를 지정하는 차원에 계정 인텔리전스를 적용합니다. 계정 인텔리전스를 추가하려면 비즈니스 인텔리전스 마법사의 **기능 선택** 페이지에서 **계정 인텔리전스 정의** 옵션을 선택합니다. 그런 다음 마법사의 안내를 따라 계정 인텔리전스를 적용할 차원을 선택하고 선택한 계정 차원에서 계정 특성을 식별한 후 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 인식되는 계정 유형에 차원 테이블의 계정 유형을 매핑합니다.  
  
## <a name="selecting-a-dimension"></a>차원 선택  
 마법사의 첫 번째 **계정 인텔리전스 정의** 페이지에서 계정 인텔리전스를 적용할 차원을 지정합니다. 선택한 차원에 향상된 계정 인텔리전스 기능을 추가하면 차원이 변경됩니다. 이러한 변경 내용은 선택된 차원을 포함하는 모든 큐브에 상속됩니다.  
  
## <a name="specifying-account-attributes"></a>계정 특성 지정  
 마법사의 **차원 특성 구성** 페이지에서 선택한 계정 차원의 계정 특성을 지정합니다. 먼저 **포함** 열에서 차원의 차원 특성에 매핑할 각 계정 특성 유형의 확인란을 선택합니다. 그런 다음 **차원 특성** 열에서 드롭다운 목록을 확장한 다음 선택한 특성 유형에 해당하는 차원의 특성을 선택합니다. 목록에서 특성을 선택하면 해당 계정 특성의 **Type** 속성이 설정됩니다.  
  
## <a name="mapping-account-types"></a>계정 유형 매핑  
 두 번째 **계정 인텔리전스 정의** 페이지에서는 차원 테이블의 계정 유형 값을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 인식되는 계정 유형에 매핑합니다. 이 페이지는 차원에 **계정 유형** 차원 특성을 포함한 경우에만 나타납니다. **계정 유형** 차원을 포함하려면 마법사의 **계정 인텔리전스 정의** 설정 페이지에서 **계정 유형**확인란을 선택하고 적절한 특성을 선택합니다.  
  
 두 번째 **계정 인텔리전스 정의** 페이지에는 다음과 같은 두 개의 열이 있습니다.  
  
-   **원본 테이블 계정 유형** 열 - 마법사가 차원 테이블에서 가져오는 계정 유형이 나열됩니다.  
  
-   **기본 제공 계정 유형** 열 - [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 인식되는 해당 계정 유형을 식별합니다. 다음 표에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 인식되는 계정 유형과 이러한 각 유형의 기본 집계를 나열합니다. 차원 테이블 이름과 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 사용하는 계정 유형 이름이 동일한 경우에는 자동으로 선택됩니다.  
  
    |서버 계정 유형|집계|Description|  
    |-------------------------|-----------------|-----------------|  
    |**통계**|**InclusionThresholdSetting**|항목의 계산된 비율 또는 시간에 따라 집계되지 않는 항목의 합계입니다. 이 계정 유형은 변환 규칙을 사용하여 통화 간을 변환하지 않습니다.|  
    |**Liability**|**LastNonEmpty**|특정 시간에 진 빚의 가치나 금액입니다. 이 계정 유형은 시간에 따라 누적되지 않으므로 자연히 시간에 따라 집계되지 않습니다. 예를 들어 Year 금액은 데이터가 있는 마지막 월의 값입니다. 이 계정 유형은 End of Period 비율을 사용하여 통화 간을 변환합니다.|  
    |**Asset**|**LastNonEmpty**|특정 시간에 보유하고 있는 빚의 가치나 금액입니다. 이 계정 유형은 시간에 따라 누적되지만 시간에 따라 자연히 집계되지는 않습니다. 예를 들어 Year 금액은 데이터가 있는 마지막 월의 값입니다. 이 계정 유형은 End of Period 비율을 사용하여 통화 간을 변환합니다.|  
    |**Balance**|**LastNonEmpty**|특정 시간의 항목 합계입니다. 이 계정 유형은 누적되지만 시간에 따라 자연히 집계되지 않습니다. 예를 들어 Year 금액은 데이터가 있는 마지막 월의 값입니다.|  
    |**Flow**|**합계**|항목의 증분 합계입니다. 이 계정 유형은 시간에 따라 **Sum** 으로 집계되지만 통화 변환 규칙을 사용하여 통화 간을 변환하지 않습니다.|  
    |**Expense**|**합계**|소비한 항목의 가치나 금액입니다. 이 계정 유형은 시간에 따라 **Sum** 으로 집계되며 평균 비율을 사용하여 통화 간을 변환합니다.|  
    |**Income**|**합계**|받은 항목의 가치나 금액입니다. 이 계정 유형은 시간에 따라 **Sum** 으로 집계되며 평균 비율을 사용하여 통화 간을 변환합니다.|  
  
    > [!NOTE]  
    >  필요한 경우 차원의 여러 계정 유형을 특정 서버 계정 유형에 매핑할 수 있습니다.  
  
 데이터베이스에 대한 각 계정 유형에 매핑되는 기본 집계를 변경하려면 데이터베이스 디자이너를 사용합니다.  
  
1.  솔루션 탐색기에서 Analysis Services 프로젝트를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 편집**을 클릭합니다.  
  
2.  **계정 유형 매핑** 상자의 **이름**에서 계정 유형을 선택합니다.  
  
3.  **별칭** 입력란에 이 계정 유형의 별칭을 입력합니다.  
  
4.  **집계 함수** 드롭다운 목록 상자에서 이 계정 유형의 기본 집계 함수를 변경합니다.  
  
  

