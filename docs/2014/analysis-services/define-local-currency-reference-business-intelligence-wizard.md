---
title: 현지 통화 참조 정의 (비즈니스 인텔리전스 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.localcurrency.f1
ms.assetid: 74993b0d-dfca-476b-acba-d66c593680a5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 558e2c7d62edcb9fb314b49d41fd7bd15413218d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082174"
---
# <a name="define-local-currency-reference-business-intelligence-wizard"></a>현지 통화 참조 정의(비즈니스 인텔리전스 마법사)
  
  **현지 통화 참조 정의** 페이지를 사용하여 **변환 유형 선택** 페이지에서 지정한 다 대 다 또는 다 대 일 변환 유형을 다루는 통화 변환 기능에 대한 현지 통화를 정의할 수 있습니다. 현지 통화는 **측정값 선택** 페이지에서 선택한 측정값에 대한 트랜잭션이 저장되는 통화입니다.  
  
> [!NOTE]  
>  이 페이지는 차원 디자이너에서 비즈니스 인텔리전스 마법사를 시작하거나 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 솔루션 탐색기에서 차원을 마우스 오른쪽 단추로 클릭하여 비즈니스 인텔리전스 마법사를 시작할 경우 표시되지 않습니다. 
  **변환 유형 선택** 페이지에서 **일 대 다** 를 선택한 경우에도 이 페이지가 나타나지 않습니다.  
  
## <a name="options"></a>옵션  
 **팩트 테이블의 식별자**  
 
  **측정값 선택** 페이지에서 선택한 측정값을 포함하는 팩트 테이블이 참조하는 통화 차원의 현지 통화에 대한 통화 식별자를 제공하는 특성을 지정하려면 선택합니다. (해당 `Type` 속성이 *통화로*설정 된 통화 차원  
  
 트랜잭션 자체에서 해당 트랜잭션에 대한 현지 통화를 결정하는 경우 이 옵션을 사용합니다. 예를 들어 예제 데이터베이스 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]에서 Internet Sales 측정값 그룹은 Currency 차원에 대 한 일반 차원 관계를 포함 합니다. 이 측정값 그룹의 팩트 테이블에는 해당 차원의 차원 테이블에 있는 통화 식별자를 참조하는 외래 키 열이 있습니다.  
  
 **팩트 데이터에서 참조하는 통화 차원 및 특성**  
 해당 멤버가 현지 통화에 대한 통화 식별자를 나타내는 통화 차원 내에서 통화 특성을 선택합니다. 통화 특성은 해당 `Type` 속성이 *통화로*설정 된 항목입니다.  
  
> [!NOTE]  
>  이 옵션은 **팩트 테이블의 식별자** 옵션을 선택하지 않으면 사용할 수 없습니다.  
  
 **차원 테이블의 특성**  
 현지 통화에 대한 통화 식별자를 포함하는 측정값 그룹과 관련된 차원에서 특성을 지정하려면 선택합니다.  
  
 트랜잭션과 다른 비즈니스 엔터티 간의 관계(위치 등)가 해당 트랜잭션에 대한 현지 통화를 결정하는 경우 이 옵션을 사용합니다. 예를 들어 예제 데이터베이스 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]에서 Financial Reporting 측정값 그룹은 조직 차원을 통해 Currency 차원에 대 한 참조 된 차원 관계를 포함 합니다. 즉, Financial Reporting 측정값 그룹의 팩트 테이블에는 Organization 차원의 차원 테이블에 있는 멤버를 참조하는 외래 키 열이 있습니다. Organization 차원의 차원 테이블에는 Currency 차원의 차원 테이블에 있는 통화 식별자를 참조하는 외래 키 열이 있습니다.  
  
 **통화를 참조하는 차원 특성**  
 해당 멤버가 현지 통화에 대한 통화 식별자를 참조하는 차원 내에서 특성을 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 **차원 테이블의 특성** 옵션을 선택하지 않으면 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [비즈니스 인텔리전스 마법사 F1 도움말](business-intelligence-wizard-f1-help.md)   
 [큐브 디자이너 &#40;Analysis Services 다차원 데이터&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [차원 디자이너 &#40;Analysis Services 다차원 데이터&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
