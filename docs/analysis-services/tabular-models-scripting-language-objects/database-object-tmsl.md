---
title: "데이터베이스 개체 (TMSL) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: ae5c046b-8242-4046-ae76-2c070503fd93
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 239c6e21a7c0e05f52fa00c17d11c5ff81d8a216
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="database-object-tmsl"></a>데이터베이스 개체 TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  동일한 수준 모델을 기반으로 한 호환성 수준 1200 이상에서 테이블 형식 데이터베이스를 정의 합니다. 이 항목의 생성, 변경, 삭제 및 데이터베이스 관리 작업을 수행 하는 요청에 대 한 페이로드를 제공 하는 데이터베이스 개체 정의 설명 합니다.  
  
> [!NOTE]  
>  모든 스크립트에서 시간에 데이터베이스를 하나만 참조할 수 있습니다. 자체 데이터베이스 이외의 개체, 데이터베이스 속성은 모델을 지정 하는 경우 선택 사항입니다. 모델 및 데이터베이스 이름을 명시적으로 제공 되는 경우 추론 하도록 사용할 수 있는 데이터베이스 간에 일대일 매핑이 있습니다.   
> 마찬가지로, 생략할 수 있습니다 모델을 데이터베이스에서 해당 속성을 설정 합니다.  
  
## <a name="object-definition"></a>개체 정의  
 모든 개체 이름, 유형, 설명, properties 컬렉션 및 주석을 포함 하 여 속성의 공통 집합을 가집니다. **데이터베이스** 개체에는 다음과 같은 속성이 있습니다.  
  
 compatibilitylevel  
 현재 유효한 값은 1200으로 1400 합니다. 더 낮은 호환성 수준 다른 메타 데이터 엔진을 사용 합니다.  
  
 readwritemode  
 데이터베이스의 모드를 열거합니다. 높은 가용성 또는 확장성 구성에서 읽기 전용 데이터베이스를 만들기에 공통 되기 합니다. 유효한 값은 readWrite,  
                읽기 전용  
                또는 readOnlyExclusive 합니다. 참조 [고가용성 및 Analysis Services의 확장성](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md) 및 [ReadOnly 및 ReadWrite 모드 간 Analysis Services 데이터베이스 전환](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md) 이 속성을 사용 하는 방법에 대 한 자세한 내용은 합니다.  
  
## <a name="usage"></a>사용법  
 **데이터베이스** 거의 모든 명령에서 개체를 사용 합니다. 참조 [명령에서 테이블 형식 모델 스크립팅 언어 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) 목록에 대 한 합니다. A **데이터베이스** 개체의 서버 개체의 자식입니다.  
  
 를 만들 때 바꾸거나, 데이터베이스 개체는 개체 정의의 모든 읽기 / 쓰기 속성을 지정 합니다. 읽기 / 쓰기 속성을 생략 삭제 것으로 간주 됩니다.  
  
## <a name="partial-syntax"></a>부분 구문  
 이 개체 정의 너무 크기 때문에 직접 속성만 나열 됩니다. **모델** 개체 데이터베이스 정의 제공 합니다. 참조 [개체 &#40; 모델 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md) 하는 개체를 정의 하는 방법입니다.  
  
```  
    "database": {  
      "type": "object",  
      "properties": {  
        "name": {  
          "type": "string"  
        },  
        "id": {  
          "type": "string"  
        },  
        "description": {  
          "type": "string"  
        },  
        "compatibilityLevel": {  
          "type": "integer"  
        },  
        "readWriteMode": {  
          "enum": [  
            "readWrite",  
            "readOnly",  
            "readOnlyExclusive"  
          ]  
        },  
        "model": {  
          "type": "object",  
          ...  
        }  
    }  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [고가용성 및 Analysis Services의 확장성](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)  
  
  
