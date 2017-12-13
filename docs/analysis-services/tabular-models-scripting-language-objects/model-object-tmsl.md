---
title: "모델 개체 (TMSL) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 9382d0d6-2d4b-49ad-a0eb-35970f0f3afb
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e2ba45e7f346fc597e579ce7dd7d7d0369fd94de
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="model-object-tmsl"></a>모델 개체 TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]테이블 형식 모델을 정의합니다. 데이터베이스 및 지정한 명령에 지정할 수 하나의 데이터베이스에 하나의 모델만이 있습니다. 데이터베이스 개체에는 부모 개체가입니다.  
  
 모델 정의 너무 커서 한 항목의 전체 구문을 재현 합니다. 이러한 이유로 자식 개체에 대 한 링크가 있는 주요 부분을 강조 표시 하는 부분 구문 아래 찾을 수 있습니다.  
  
 아마도 모델 정의 이해 하는 가장 좋은 방법은 먼저 사용자가 잘 알고 테이블 형식 모델이 들어 있는입니다. 사용 하 여는 **코드 보기** 해당 정의를 보려면 SQL Server Data Tools의 옵션입니다. 코드를 볼 수 있도록 JSON 편집기를 설치 해야 합니다. Visual studio에서 JSON 편집기를 가져올 수 있습니다 [Community edition 다운로드](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) 또는 다른 버전의 Visual Studio입니다.  
  
> [!NOTE]  
>  모든 스크립트에서 시간에 데이터베이스를 하나만 참조할 수 있습니다. 자체 데이터베이스 이외의 개체, 데이터베이스 속성은 모델을 지정 하는 경우 선택 사항입니다. 모델 및 데이터베이스 이름을 명시적으로 제공 되는 경우 추론 하도록 사용할 수 있는 데이터베이스 간에 일대일 매핑이 있습니다.   
> 마찬가지로, 생략할 수 있습니다 모델을 데이터베이스에서 해당 속성을 설정 합니다.  
  
## <a name="object-definition"></a>개체 정의  
 모든 개체 이름, 유형, 설명, properties 컬렉션 및 주석을 포함 하 여 속성의 공통 집합을 가집니다. **모델** 개체에는 다음과 같은 속성이 있습니다.  
  
 storageLocation  
 모델을 배치할 디스크의 위치입니다.  
  
 defaultMode  
 데이터를 파티션에 사용할 수 있도록 하는 기본 메서드입니다.  
  
 defaultDataView  
 DirectQuery 모드에서 모델의 경우이 속성은 모델에 대 한 쿼리를 실행 하는 파티션을 사용 하는 결정 합니다.  유효한 값 전체 및 샘플에 포함 됩니다.  
  
 Culture  
 서식 지정에 사용할 문화권입니다.  
  
 collation  
 데이터 정렬 시퀀스입니다. 참조 [Analysis Services의 세계화 시나리오](../../analysis-services/globalization-scenarios-for-analysis-services.md) 자세한 정보에 대 한 합니다.  
  
 테이블  
 파티션, 열, 측정값, Kpi 및 주석을 포함 하 여 모델 테이블의 전체 컬렉션입니다. 참조 [개체 &#40; 테이블 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md) 대 한 자세한 내용은 합니다.  
  
 관계  
 필터 방향 및 보안을 설정 하는 속성을 비롯 하 여 테이블의 각 쌍 간의 관계를 지정 합니다. 참조 [관계 개체 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md) 대 한 자세한 내용은 합니다.  
  
 데이터 원본  
 하나 이상의 연결 모델에 데이터를 제공 하거나에 사용 되는 외부 데이터베이스에 쿼리를 통해 전달 합니다. 참조 [DataSources 개체 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md) 대 한 자세한 내용은 합니다.  
  
 역할  
 데이터베이스 사용 권한, 멤버 계정 및 필요에 따라 사용자 지정 액세스 제어에 대 한 DAX의 보안 필터를 연결 하는 개체입니다.  
  
## <a name="usage"></a>사용법  
 **모델** 개체 전체 모델에 포함 합니다. 대부분의 명령은에서 모델을 하나 및/또는 해당 부모 데이터베이스 개체를 지정 해야 합니다.  
  
 를 만들 때 바꾸거나, 모델 개체는 개체 정의의 모든 읽기 / 쓰기 속성을 지정 합니다. 읽기 / 쓰기 속성을 생략 삭제 것으로 간주 됩니다.  
  
## <a name="partial-syntax"></a>부분 구문  
 이 개체 정의 너무 크기 때문에 첫 번째 수준 속성에 대해서만 나열 됩니다. 참조 [개체 정의에서 테이블 형식 모델 스크립팅 언어 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/tmsl-reference-tabular-objects.md) 자식 개체의 목록에 대 한 합니다.  
  
```  
    "model": {  
      "description": "Model object of a Tabular database",  
      "type": "object",  
      "properties": {  
          "name": {  },  
          "description": {  },  
         "storageLocation": {  },  
         "defaultMode":  {  },  
         "defaultDataView": {  },  
         "culture": {  },  
         "collation": {  },  
         "annotations": {  },  
         "tables": {  },  
         "relationships": {  },  
         "dataSources": {  },  
         "perspectives": {  },  
            "cultures": {  },  
         "roles": {  }  
    }  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Analysis services에서 테이블 형식 모델에 대한 호환성 수준](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
