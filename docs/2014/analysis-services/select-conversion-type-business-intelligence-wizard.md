---
title: 변환 유형 선택 (비즈니스 인텔리전스 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.conversiontype.f1
ms.assetid: 2c664138-e8a1-4c47-8e7d-ee01c57e4692
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ba4018a6ce30e4e7de4e0ca3e79ae07007015650
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186171"
---
# <a name="select-conversion-type-business-intelligence-wizard"></a>변환 유형 선택(비즈니스 인텔리전스 마법사)
  **변환 유형 선택** 페이지를 사용하여 여러 통화로 저장된 트랜잭션에 대해 현지 통화와 보고 통화 간의 관계를 정의할 수 있습니다. 현지 통화는 **측정값 선택** 페이지에서 선택한 측정값에 대한 트랜잭션이 저장되는 통화입니다. 보고 통화는 **측정값 선택** 페이지에서 선택한 트랜잭션이 번역되는 통화입니다.  
  
> [!NOTE]  
>  이 페이지는 차원 디자이너에서 비즈니스 인텔리전스 마법사를 시작하거나 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 솔루션 탐색기에서 차원을 마우스 오른쪽 단추로 클릭하여 비즈니스 인텔리전스 마법사를 시작할 경우 표시되지 않습니다.  
  
## <a name="options"></a>변수  
 **다 대 다**  
 현지 통화를 사용하여 트랜잭션을 저장합니다. 통화 변환 기능은 트랜잭션을 **통화 변환 옵션 설정** 페이지에서 지정한 피벗 통화로 변환한 다음 하나 이상의 다른 보고 통화로 변환합니다.  
  
 예를 들어 피벗 통화를 미국 달러(USD)로 설정하면 팩트 테이블에서는 트랜잭션을 유로(EUR), 오스트레일리아 달러(AUD) 및 멕시코 페소(MXN)로 저장합니다. 이 옵션을 선택하면 이러한 트랜잭션이 지정한 현지 통화에서 피벗 통화로 변환된 다음 변환된 트랜잭션이 다시 피벗 통화에서 지정한 보고 통화로 변환됩니다. 그 결과 트랜잭션을 지정한 현지 통화로 저장하고 지정한 피벗 통화 또는 **보고 통화 지정** 페이지에서 지정한 보고 통화 중 하나로 표시할 수 있습니다.  
  
 **다 대 일**  
 현지 통화를 사용하여 트랜잭션을 저장합니다. 통화 변환 기능은 트랜잭션을 **통화 변환 옵션 설정** 페이지에서 지정한 피벗 통화로 변환합니다. 피벗 통화는 지정된 유일한 보고 통화로 사용됩니다.  
  
> [!NOTE]  
>  이 옵션을 선택하면 **보고 통화 지정** 페이지가 표시되지 않습니다.  
  
 예를 들어 피벗 통화를 미국 달러(USD)로 설정하면 팩트 테이블에서는 트랜잭션을 유로(EUR), 오스트레일리아 달러(AUD) 및 멕시코 페소(MXN)로 저장합니다. 이 옵션을 선택하면 이러한 트랜잭션이 지정한 현지 통화에서 피벗 통화로 변환됩니다. 그 결과 트랜잭션을 지정한 현지 통화로 저장하고 지정한 피벗 통화로 표시할 수 있습니다.  
  
 **일 대 다**  
 **통화 변환 옵션 설정** 페이지에서 지정한 피벗 통화를 사용하여 트랜잭션을 저장한 다음 하나 이상의 다른 보고 통화로 변환합니다.  
  
> [!NOTE]  
>  이 옵션을 선택하면 **현지 통화 참조 정의** 페이지가 표시되지 않습니다.  
  
 예를 들어 피벗 통화를 미국 달러(USD)로 설정하면 팩트 테이블에서는 트랜잭션을 USD로 저장합니다. 이 옵션을 선택하면 이러한 트랜잭션이 피벗 통화에서 지정한 보고 통화로 변환됩니다. 그 결과 트랜잭션을 지정한 피벗 통화로 저장하고 지정한 피벗 통화 또는 **보고 통화 지정** 페이지에서 지정한 보고 통화 중 하나로 표시할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [비즈니스 인텔리전스 마법사 F1 도움말](business-intelligence-wizard-f1-help.md)   
 [큐브 디자이너 &#40;Analysis Services-다차원 데이터&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [차원 디자이너 &#40;Analysis Services-다차원 데이터&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  