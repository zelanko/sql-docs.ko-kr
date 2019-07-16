---
title: Analysis Services 테이블 형식 모델 개체 수준 보안 | Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d354aa64e8b6a1e98941011c30550a056f4c01c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162782"
---
# <a name="object-level-security"></a>개체 수준 보안
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
데이터 모델 보안을 효율적으로 구현 시작 [역할](../../analysis-services/tabular-models/roles-ssas-tabular.md) 및 행 수준 필터를 데이터 모델 개체 및 데이터에 사용자 권한을 정의 합니다. 테이블 형식 1400 모델부터 정의할 수도 있습니다 테이블 수준 보안 및 열 수준 보안을 포함 하는 개체 수준 보안을 [역할 개체](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl)합니다.

## <a name="table-level-security"></a>테이블 수준 보안

테이블 수준 보안을 사용 하 여 테이블 데이터에 액세스만 제한 하지 수 있지만 있는 경우 테이블 검색에서 악의적인 사용자를 방지 하기 위해 노력 하는 중요 한 테이블 이름. 

 Model.bim의 JSON 기반 메타 데이터에서 테이블 수준 보안이 설정 된 [TMSL Tabular Model Scripting Language ()](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference), 또는 [개체 모델 TOM (테이블 형식)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo)합니다. 설정를 **사용 된 metadataPermission** 의 속성을 **대 한** 클래스를 [역할 개체](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl) 에 **없음**.

이 예제에서는 Product 테이블에 대 한 클래스의 사용 된 metadataPermission 속성은 none으로 설정 됩니다.

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

열 수준 보안을 사용 하 여 테이블 수준 보안을 비슷하게 있습니다 수만 액세스를 제한 하지 열 데이터 뿐만 아니라 중요 한 열 이름, 악의적인 사용자가 열을 검색 하는 것을 방지 합니다.

 Model.bim의 JSON 기반 메타 데이터에서 열 수준 보안이 설정 된 [TMSL Tabular Model Scripting Language ()](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference), 또는 [개체 모델 TOM (테이블 형식)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo)합니다. 설정를 **사용 된 metadataPermission** 의 속성을 **columnPermissions** 클래스를 [역할 개체](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl) 에 **없음**.

이 예제에서는 직원 테이블의 기본 요금 열에 대 한 columnPermissions 클래스의 사용 된 metadataPermission 속성은 none으로 설정 됩니다.

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

## <a name="restrictions"></a>Restrictions

*  관계 체인을 중단 하는 경우 모델에 대 한 테이블 수준 보안을 설정할 수 없습니다. 디자인 타임에 오류가 생성 됩니다.
 예를 들어 테이블 A 및 B 및 B와 C 간의 관계가 있는 경우 표 2. 보호할 수 없습니다. 표 A에 대 한 쿼리 테이블 A 및 B 및 B, C. 간의 관계를 전송할 수 없습니다. 테이블 B를 보호 하는 경우 이 예제의 경우 2. 테이블 A와 간에 별도 관계를 구성할 수 있습니다.

    ![테이블 수준 보안](../../analysis-services/tabular-models/media/ssas-ols.png)  


*  보안된 데이터를 의도 하지 않은 액세스가 발생 시킬 수 있습니다 것 때문에 다른 역할에서 행 수준 보안 및 개체 수준 보안을 결합할 수 없습니다. 이러한 조합 역할의 멤버인 사용자에 대 한 쿼리 시 오류가 생성 됩니다.

*  동적 계산 (측정값, Kpi, DetailRows)은 보안된 테이블 또는 열을 참조 하는 경우 자동으로 제한 됩니다. 명시적 측정값을 보호 하는 메커니즘이 없습니다 이지만, 암시적으로 보안된 테이블 또는 열 참조 식을 업데이트 하 여 측정값을 보호 하려면 가능성이 있습니다.

*  보안된 열을 참조 하는 관계 열이 테이블에 보안이 설정 되지 않은 제공 작동 합니다.




## <a name="see-also"></a>관련 항목  
[Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
[역할 개체(TMSL)](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl)  
[TMSL(Tabular Model Scripting Language)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)  
[테이블 형식 개체 모델 (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo)합니다.

  
