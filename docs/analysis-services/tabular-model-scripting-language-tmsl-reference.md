---
title: "테이블 형식 모델 스크립팅 언어 (TMSL) 참조 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c700d7f8-7e01-4052-a9ad-8200dd4009f2
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 3e1a38f2d4466c70259d9f58787b88c939459f59
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="tabular-model-scripting-language-tmsl-reference"></a>테이블 형식 모델 스크립팅 언어 (TMSL) 참조
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]스크립팅 언어 TMSL (tabular Model)은 호환성 수준 1200 이상에서 Analysis Services 테이블 형식 모델 데이터베이스에 대 한 명령 및 개체 모델 정의 구문입니다. TMSL, XMLA 프로토콜을 통해 Analysis Services에 통신 합니다. 여기서는 [XMLA 합니다. 실행](../analysis-services/xmla/xml-elements-methods-execute.md) 메서드 둘 다 받습니다 JSON 기반 **문을** 에서 기존 XML 기반 스크립트 뿐만 아니라 TMSL 스크립트 [Analysis Services Scripting Language &#40; ASSL XMLA &#41; ](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).  
  
 TMSL의 주요 요소는 다음과 같습니다.  
  
-   테이블 형식 모델 의미 체계에 따라 테이블 형식 메타 데이터입니다. 테이블 형식 모델 테이블, 열 및 관계가 구성 됩니다. 테이블, 열, 관계 등 TMSL에 해당 하는 개체 정의 이제, 레지스터입니다.  
  
     새 메타 데이터 엔진 이러한 정의 지원합니다.  
  
-   개체 정의 XML 대신 JSON으로 구성 됩니다.  
  
 어떻게 페이로드 서식이 지정 된 (JSON 또는 XML)를 제외 하 고 TMSL와 ASSL을 모두는 명령 및 서버 통신 및 데이터 전송에 사용 되는 XMLA 메서드에 대 한 메타 데이터를 제공 하는 방법에 기능적으로 동일 합니다.  
  
## <a name="how-to-use-tmsl"></a>TMSL을 사용 하는 방법  
 TMSL 스크립트를 탐색 하는 가장 쉬운 방법은 명령을 사용 하는 CREATE, ALTER, DELETE 또는 프로세스 SQL Server Management Studio (SSMS) 이미 알고 있는 모델에 합니다. 기존 모델을 사용 하는 assuming, 호환성 수준이 1200 이상일로 먼저 업그레이드 해야 합니다.  
  
1.  사용 하려는 명령의 찾을: [테이블 형식 모델 스크립팅 언어 &#40; 명령 TMSL &#41;](../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md)  
  
2.  명령에 사용 되는 개체에 대 한 개체 정의 참조를 확인: [테이블 형식 모델 스크립팅 언어 &#40;의 개체 정의 TMSL &#41;](../analysis-services/tabular-models-scripting-language-objects/tmsl-reference-tabular-objects.md)  
  
3.  TMSL 스크립트를 전송 하기 위한 방법을 선택 합니다.  
  
    -   Management Studio의 XMLA 창  
  
    -   **호출 ascmd** AMO PowerShell을 통해 ([Invoke-ascmd cmdlet](../analysis-services/powershell/invoke-ascmd-cmdlet.md))  
  
    -   [Analysis Services DDL 실행 태스크](../integration-services/control-flow/analysis-services-execute-ddl-task.md) SSIS에서 합니다.  
  
## <a name="model-definition-schema"></a>모델 정의 스키마  
 다음 스크린 샷에서 축소는 주요 개체를 표시 하는 스키마의 축약된 버전을 보여 줍니다.  
  
 ![SSAS_TabularMetadata](../analysis-services/media/ssas-tabularmetadata.JPG "SSAS_TabularMetadata")  
  
## <a name="scripting-languages-in-analysis-services"></a>Analysis Services의 두 가지 스크립팅 언어  
 Analysis Services ASSL 및 TMSL 스크립트 언어를 지원 합니다. 호환성 수준 1200 이상 만든 표 형식 모델만 TMS JSON 형식으로 설명 합니다.  
  
 [스크립팅 언어 &#40; analysis Services ASSL XMLA &#41; ](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md) 첫 번째 스크립트 언어 였으며 여전히 다차원 모델과 테이블 형식 모델에 더 낮은 호환성 수준 (1100 또는 1103)에 대 한 유일한 스크립트 언어입니다. Assl에서는 110x에서 테이블 형식 모델에에서 설명 된 다차원 용어와 같은 **큐브** (모델)에 대 한 및 **measuregroup** (테이블)에 대 한 합니다.  
  
> [!NOTE]  
>  [SQL Server 데이터 도구 (SSDT), TMSL를 전환 하 여 사용 하도록 이전 버전 테이블 형식 모델을 업그레이드할 수 있습니다는 **CompatibilityLevel** 1200 이상. 업그레이드는 되돌릴 수 기억 합니다. 를 업그레이드 하기 전에 원래 버전을 나중에 필요할 경우 모델을 백업 합니다.  
  
 다음 테이블은 특정 호환성 수준에서 다양 한 버전에서 Analysis Services 데이터 모델에 대 한 스크립팅 언어 매트릭스입니다.  

||||||  
|-|-|-|-|-|  
|**버전(Version)**|**다차원**|**테이블 형식 110x**|**테이블 형식 1200**| **테이블 형식 1400** |
|Azure Analysis Services|NA|NA|TMSL|TMSL| 
|SQL Server 2017|ASSL|ASSL|TMSL|TMSL| 
|SQL Server 2016|ASSL|ASSL|TMSL|TMSL| 
|SQL Server 2014|ASSL|ASSL|NA|NA|   
|SQL Server 2012|ASSL|ASSL|NA|NA|  

  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services에서 테이블 형식 모델에 대 한 호환성 수준](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [스크립팅 언어 &#40; analysis Services ASSL XMLA &#41;](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [Analysis Services 인스턴스의 서버 모드 확인](../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
