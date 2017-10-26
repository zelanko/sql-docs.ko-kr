---
title: "테이블 형식 모델 개체 수준 보안 | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: 
ms.assetid: 
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ed695cd15d9e0622ff28ed449395f0684b2cf9f1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="object-level-security"></a>개체 수준 보안

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

데이터 모델 보안을 효과적으로 구현 하 여 시작 [역할](../../analysis-services/tabular-models/roles-ssas-tabular.md) 및 행 수준 필터를 데이터 모델 개체 및 데이터에 사용자 권한을 정의 합니다. 테이블 형식 1400 모델 부터는 정의할 수도 있습니다 테이블 수준 보안 및 열 수준 보안을 포함 하는 개체 수준 보안은 [역할 개체](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)합니다.

## <a name="table-level-security"></a>테이블 수준 보안

테이블 수준 보안과 함께 있습니다 수만 액세스를 제한 하지 테이블 데이터를 하지만 있는 중요 한 테이블 이름을 검색 하는 경우 테이블에서 악의적인 사용자가 하지 않도록 합니다. 

 Model.bim에서 JSON 기반 메타 데이터에 테이블 수준 보안이 설정 된 [스크립팅 언어 TMSL (Tabular Model)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md), 또는 [테이블 형식 개체 모델 (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)합니다. 설정의 **metadataPermission** 속성의는 **대** 클래스에 [역할 개체](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md) 를 **none**합니다.

이 예제에서는 Product 테이블에 대 한 대 클래스의 metadataPermission 속성을 none으로 설정 됩니다.

```
"roles": [
  {
    "name": "Users",
    "description": "All allowed users to query the model",
    "modelPermission": "read",
    "tablePermissions": [
      {
        "name": "Product",
        "metadataPermission": "none"
      }
    ]
  }
```

## <a name="column-level-security"></a>열 수준 보안

열 수준 보안이 포함 된 테이블 수준 보안과 비슷합니다 있습니다 수만 액세스를 제한 하지 열 데이터 뿐만 아니라 중요 한 열 이름, 악의적인 사용자가 열을 검색 하는 것을 방지 합니다.

 Model.bim에서 JSON 기반 메타 데이터에서 열 수준 보안이 설정 된 [스크립팅 언어 TMSL (Tabular Model)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md), 또는 [테이블 형식 개체 모델 (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)합니다. 설정의 **metadataPermission** 속성의는 **columnPermissions** 클래스에 [역할 개체](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md) 를 **none**합니다.

이 예제에서는 Employees 테이블에 기본 비율 열에 대 한 columnPermissions 클래스의 metadataPermission 속성을 none으로 설정 됩니다.

```
"roles": [
  {
    "name": "Users",
    "description": "All allowed users to query the model",
    "modelPermission": "read",
    "tablePermissions": [
      {
        "name": "Employee",
        "columnPermissions": [
          {
            "name": "Base Rate",
            "metadataPermission": "none"
          }
        ]
      }
    ]
  }
```

## <a name="restrictions"></a>제한 사항

*  관계 체인을 중단 하는 경우 모델에 대 한 테이블 수준 보안을 설정할 수 없습니다. 디자인 타임에 오류가 발생 합니다.
 예를 들어 테이블 A 및 B, 및 B와 C 간의 관계가 있는 경우 표 2. 보호할 수 없습니다. 표 A에 대 한 쿼리 테이블 A와 B 및 B, C. 간의 관계를 통과 없습니다 테이블 B를 보호 하는 경우 이 경우 테이블 A와 B. 간에 별도 관계는 구성할 수 없습니다.

    ![테이블 수준 보안](../../analysis-services/tabular-models/media/ssas-ols.png)  


*  보안된 데이터를 의도 하지 않은 액세스 발생 하기 때문에 다른 역할에서 행 수준 보안 및 개체 수준 보안을 결합할 수 없습니다. 이러한 조합 역할의 구성원 인 사용자에 대 한 쿼리 시 오류가 발생 합니다.

*  보안 된 테이블 또는 열을 참조 하는 경우 동적 계산 (측정값, Kpi, DetailRows) 자동으로 제한 됩니다. 측정값을 명시적으로 보호 하는 메커니즘이 이지만, 암시적으로 보안된 테이블 또는 열 참조 식을 업데이트 하 여 측정값을 보호 하는 것이 같습니다.

*  보안된 열을 참조 하는 관계 열이 테이블에 보안이 설정 되지 않은 제공 된 작업입니다.




## <a name="see-also"></a>관련 항목:  
[Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
[역할 개체 TMSL)](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)  
[TMSL(Tabular Model Scripting Language)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
[테이블 형식 개체 모델 (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)합니다.

  

