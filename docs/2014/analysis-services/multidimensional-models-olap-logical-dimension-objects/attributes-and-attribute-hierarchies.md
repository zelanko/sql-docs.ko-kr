---
title: 특성 및 특성 계층 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- regular attributes [Analysis Services]
- parent attributes [Analysis Services]
- hierarchies [Analysis Services], attribute
- attributes [Analysis Services], about attributes
- account attributes [Analysis Services]
- dimensions [Analysis Services], attributes
- key attributes [Analysis Services]
- OLAP objects [Analysis Services], attributes
- attributes [Analysis Services], relationships
- attributes [Analysis Services]
- relationships [Analysis Services], attributes
ms.assetid: 59de1ea2-e7a9-4a53-9ee0-14be52e95643
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c1f1c6644e14beaee7bdcab9e3f50129f73b7bc
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60157269"
---
# <a name="attributes-and-attribute-hierarchies"></a>특성 및 특성 계층
  차원은 데이터 원본 뷰의 테이블이나 뷰에 있는 하나 이상의 열에 바인딩되는 특성의 모음입니다.  
  
## <a name="key-attribute"></a>키 특성  
 각 차원에는 키 특성이 포함되어 있습니다. 각 특성은 차원 테이블의 하나 이상의 열에 바인딩됩니다. 키 특성은 차원에서 팩트 테이블과의 외래 키 관계에 사용되는 차원 주 테이블의 열을 나타내는 특성입니다. 일반적으로 키 특성은 차원 테이블의 기본 키 열을 나타냅니다. 기본 데이터 원본에 물리적 기본 키가 없는 데이터 원본 뷰의 테이블에 논리적 기본 키를 정의할 수 있습니다. **자세한 내용은**를 참조 하세요 [데이터 원본 뷰에서 논리적 기본 키 정의 &#40;Analysis Services&#41;](../multidimensional-models/define-logical-primary-keys-in-a-data-source-view-analysis-services.md)합니다. 키 특성을 정의할 때 큐브 마법사와 차원 마법사는 데이터 원본 뷰에 있는 차원 테이블의 기본 키 열을 사용하려고 합니다. 차원 테이블에 논리적 또는 물리적 기본 키가 정의되어 있지 않으면 마법사는 차원에 대한 키 특성을 제대로 정의할 수 없습니다.  
  
## <a name="binding-an-attribute-to-columns-in-data-source-view-tables-or-views"></a>데이터 원본 뷰 테이블 또는 뷰의 열에 특성 바인딩  
 특성은 하나 이상의 데이터 원본 뷰 테이블이나 뷰의 열에 바인딩됩니다. 특성은 항상 특성에 포함된 멤버를 결정하는 하나 이상의 키 열에 바인딩됩니다. 기본적으로 특성은 키 열에만 바인딩됩니다. 특성이 특정 목적으로 하나 이상의 추가 열에 바인딩될 수도 있습니다. 예를 들어 특성의 `NameColumn` 속성은 각 특성 멤버에 대해 사용자에게 표시되는 이름을 결정합니다. 특성의 이 속성은 데이터 원본 뷰를 통해 특정 차원 열에 바인딩되거나 데이터 원본 뷰의 계산 열에 바인딩될 수도 있습니다. 자세한 내용은 [차원 특성 속성 참조](../multidimensional-models/dimension-attribute-properties-reference.md)합니다.  
  
## <a name="attribute-hierarchies"></a>특성 계층  
 기본적으로 특성 멤버는 리프 수준과 All 수준으로 구성되는 두 수준의 계층으로 구성됩니다. All 수준에는 특성과 관련된 차원이 멤버로 속해 있는 각 측정값 그룹의 여러 측정값과 관련하여 해당 특성의 멤버에 대한 집계 값이 포함됩니다. 그러나 `IsAggregatable` 속성을 False로 설정하면 All 수준은 생성되지 않습니다. 자세한 내용은 [차원 특성 속성 참조](../multidimensional-models/dimension-attribute-properties-reference.md)합니다.  
  
 특성은 해당 특성과 관련된 측정값 그룹의 데이터를 사용자가 검색할 수 있는 드릴다운 경로를 제공하는 사용자 정의 계층으로 정렬할 수 있으며 이렇게 정렬하는 것이 일반적입니다. 클라이언트 응용 프로그램에서 특성은 그룹화 및 제약 조건 정보를 제공하는 데 사용할 수 있습니다. 수준 다-대-일 관련이 있을 경우 계층 수준 간의 관계를 정의 하는 경우 사용자 정의 계층에 특성을 정렬할 한 한 일 관계 (호출을 *자연 스러운* 관계). 예를 들어 Calendar Time 계층에서 Day 수준은 Month 수준과 관련이 있고 Month 수준은 Quarter 수준과 관련이 있어야 합니다. 사용자 정의 계층에 수준 간의 관계를 정의하면 Analysis Services에서 보다 유용한 집계를 정의하여 쿼리 성능을 높일 수 있으며 처리 성능 중에 메모리를 절약할 수도 있습니다. 이 기능은 크거나 복잡한 큐브에서 중요할 수 있습니다. 자세한 내용은 [사용자 계층](user-hierarchies.md)를 [사용자 정의 계층](../multidimensional-models/user-defined-hierarchies-create.md), 및 [특성 관계 정의](../multidimensional-models/attribute-relationships-define.md)합니다.  
  
## <a name="attribute-relationships-star-schemas-and-snowflake-schemas"></a>특성 관계, 별모양 스키마 및 눈송이 스키마  
 기본적으로 별모양 스키마에서 모든 특성은 키 특성에 직접 관련되므로 사용자들은 차원의 특성 계층을 기반으로 큐브의 팩트를 검색할 수 있습니다. 눈송이 스키마에서 특성은 해당 기본 테이블이 팩트 테이블에 직접 연결되어 있는 경우 키 특성에 직접 연결되거나 눈송이 테이블을 직접 연결된 테이블에 연결하는 기본 테이블의 키에 바인딩된 특성을 통해 간접적으로 연결됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [사용자 정의 계층 만들기](../multidimensional-models/user-defined-hierarchies-create.md)   
 [특성 관계를 정의 합니다.](../multidimensional-models/attribute-relationships-define.md)   
 [차원 특성 속성 참조](../multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
