---
title: 잠금 및 데이터베이스 (XMLA)를 잠금 해제 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d9868b251ff95fae1822abb5844ff7e909940dae
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="locking-and-unlocking-databases-xmla"></a>데이터베이스 잠금 및 잠금 해제(XMLA)
  잠금 및 각각 사용 하는 데이터베이스 잠금 해제, [잠금](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) 및 [잠금 해제](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md) xml for Analysis (XMLA) 명령입니다. 일반적으로 다른 XMLA 명령은 실행 중 해당 명령을 수행하는 데 필요할 경우 자동으로 개체를 잠그거나 잠금 해제합니다. 있습니다 수 명시적으로 잠그거나 잠금 해제와 같이 단일 트랜잭션 내에서 여러 명령을 수행 하려면 데이터베이스는 [일괄 처리](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) 동안 다른 응용 프로그램에서 데이터베이스에 쓰기 트랜잭션을 커밋하지 명령입니다.  
  
## <a name="locking-databases"></a>데이터베이스 잠금  
 **Lock** 명령은 현재 활성 트랜잭션 컨텍스트 내에서 공유되거나 배타적으로 사용되는 개체를 잠급니다. 개체가 잠겨 있으면 잠금을 해제할 때까지 트랜잭션을 커밋할 수 없습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 두 가지 유형의 잠금, 공유 잠금과 배타적 잠금을 지원합니다. 지 원하는 잠금 유형에 대 한 자세한 내용은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], 참조 [Mode 요소 & #40; XMLA & #41; ](../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md).  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 데이터베이스 잠금만 허용합니다. [개체](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) 요소에 대 한 개체 참조를 포함 해야 합니다는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스입니다. **Object** 요소를 지정하지 않거나 **Object** 요소가 데이터베이스 이외의 개체를 참조하면 오류가 발생합니다.  
  
> [!IMPORTANT]  
>  데이터베이스 관리자 또는 서버 관리자만 명시적으로 **Lock** 명령을 실행할 수 있습니다.  
  
 다른 명령을 암시적으로 문제는 **잠금** 명령을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스입니다. 예: 데이터베이스에서 데이터 또는 메타 데이터를 읽을 수 있는 모든 작업 [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드 또는 [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) 를 실행 하는 메서드는 [문을](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) 명령에서 암시적으로 공유 데이터베이스에 대 한 잠금. 개체의 데이터 또는 메타 데이터 변경을 커밋하는 모든 트랜잭션은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스와 같은 프로그램 **Execute** 를 실행 하는 메서드는 [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) 명령에서 암시적으로 배타적 잠금에 대 한 문제는 데이터베이스입니다.  
  
## <a name="unlocking-objects"></a>개체 잠금 해제  
 **Unlock** 명령은 현재 활성 트랜잭션 컨텍스트 내에서 설정된 잠금을 해제합니다.  
  
> [!IMPORTANT]  
>  데이터베이스 관리자 또는 서버 관리자만 명시적으로 **Unlock** 명령을 실행할 수 있습니다.  
  
 모든 잠금은 현재 트랜잭션의 컨텍스트에 유지됩니다. 현재 트랜잭션이 커밋 또는 롤백되면 해당 트랜잭션 내에 정의된 모든 잠금이 자동으로 해제됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [요소를 잠급니다 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)   
 [요소 & #40; 잠금 해제 XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)   
 [Analysis Services에서 XMLA를 사용 하 여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
