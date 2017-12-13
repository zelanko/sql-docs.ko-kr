---
title: "ASSL XML 표기 규칙 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- whitespace [Analysis Services Scripting Language]
- trailing whitespace
- XSD data types [Analysis Services Scripting Language]
- inheritance [Analysis Services Scripting Language]
- cardinality [Analysis Services Scripting Language]
- white space [Analysis Services Scripting Language]
- ASSL, XML conventions
- defaults [Analysis Services Scripting Language]
- leading whitespace
- Analysis Services Scripting Language, XML conventions
- XML [Analysis Services Scripting Language]
- hierarchies [Analysis Services Scripting Language]
- inherited defaults [Analysis Services Scripting Language]
ms.assetid: bce4edad-4420-41ce-9672-8c00c5c0dec6
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9627648fa47b750f4b9b98b45b5878cea0806961
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="assl-xml-conventions"></a>ASSL XML 표기 규칙
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Analysis Services Scripting Language (ASSL) 자식 요소를 포함할 수 정의 하는 요소 유형의 집합으로 개체의 계층 구조를 나타냅니다.  
  
 개체 계층을 나타내기 위해 ASSL에서는 다음과 같은 XML 표기 규칙을 사용합니다.  
  
-   ‘xml:lang’과 같은 표준 XML 특성을 제외한 개체와 속성은 모두 요소로 표현됩니다.  
  
-   요소 이름과 열거형 값의 파스칼식 Microsoft.NET Framework 명명 규칙을 따르는 없는 밑줄을 사용 합니다.  
  
-   모든 값의 대/소문자는 유지됩니다. 열거형의 값도 대/소문자를 구분합니다.  
  
 이 표기 규칙 목록 외에도 Analysis Services는 카디널리티, 상속, 공백, 데이터 형식 및 기본값에 관한 특정 표기 규칙을 따릅니다.  
  
## <a name="cardinality"></a>카디널리티  
 요소의 카디널리티가 1보다 큰 경우에는 XML 요소 컬렉션에서 이 요소를 캡슐화합니다. 컬렉션 이름에는 컬렉션에 포함된 복수 형태의 요소를 사용합니다. 예를 들어 다음 XML 조각은 나타냅니다는 **차원** 컬렉션 내에서 한 **데이터베이스** 요소:  
  
 `<Database>`  
  
 `…`  
  
 `<Dimensions>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `</Dimensions>`  
  
 `</Database>`  
  
 ``  
  
 요소가 표시되는 순서는 중요하지 않습니다.  
  
## <a name="inheritance"></a>상속  
 겹치는 부분이 있으면서도 상당히 다른 속성 집합을 가지고 있는 서로 다른 개체가 있을 때 상속이 사용됩니다. 겹치면서도 서로 다른 개체의 예로는 가상 큐브, 연결된 큐브 및 일반 큐브가 있습니다. 겹치면서 고유 개체에 대 한 Analysis Services 사용 하 여 표준 **형식** 특성에서 XML 인스턴스 Namespace 상속을 나타냅니다. 예를 들어 다음 XML 조각에서는 방법을 **형식** 특성은 특정 여부는 **큐브** 요소가 일반 큐브에서 또는 가상 큐브에서 상속:  
  
 `<Cubes>`  
  
 `<Cube xsi:type=”RegularCube”>`  
  
 `<Name>Sales</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `<Cube xsi:type=”VirtualCube”>`  
  
 `<Name>SalesAndInventory</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `</Cubes>`  
  
 ``  
  
 여러 형식에 같은 이름의 속성이 있는 경우에는 일반적으로 상속을 사용하지 않습니다. 예를 들어는 **이름** 및 **ID** 추상 형식으로 이러한 속성을 승격 하지 않은 있지만 많은 요소에는 속성이 나타납니다.  
  
## <a name="whitespace"></a>공백  
 요소 값 안의 공백은 유지됩니다. 그러나 선행 공백과 후행 공백은 항상 잘립니다. 예를 들어, 다음 요소는 동일한 텍스트를 가지고 있지만 텍스트의 공백 수가 다르므로 서로 다른 값을 가진 것으로 처리됩니다.  
  
 `<Description>My text<Description>`  
  
 `<Description>My  text<Description>`  
  
 ``  
  
 그러나 다음 요소는 선행 및 후행 공백만 다르므로 같은 값을 가진 것으로 처리됩니다.  
  
 `<Description>My text<Description>`  
  
 `<Description>  My text  <Description>`  
  
 ``  
  
## <a name="data-types"></a>데이터 형식  
 Analysis Services는 다음과 같은 표준 XSD(XML 스키마 정의 언어) 데이터 형식을 사용합니다.  
  
 **Int**  
 -231에서 231-1 사이의 정수 값입니다.  
  
 **Long**  
 -263에서 263-1 사이의 정수 값입니다.  
  
 **문자열**  
 다음과 같은 전역 규칙을 따르는 문자열 값입니다.  
  
-   제어 문자가 제거됩니다.  
  
-   선행 공백과 후행 공백이 잘립니다.  
  
-   내부 공백이 유지됩니다.  
  
 **이름** 및 **ID** 속성 문자열 요소의 유효한 문자에 대 한 특별 한 제한이 있습니다. 에 대 한 자세한 내용은 **이름** 및 **ID** 규칙, 참조 [ASSL 개체 및 개체 특징](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)합니다.  
  
 **DateTime**  
 A **DateTime** .NET Framework에서 구조입니다. A **DateTime** 값은 NULL 일 수 없습니다. 지 원하는 가장 낮은 날짜는 **날짜/시간** 데이터 형식이 1601 년 1 월 1 일으로 프로그래머에 게 사용 하지 않는 **DateTime.MinValue**합니다. 지원 되는 가장 낮은 날짜 나타냅니다는 **DateTime** 값이 없습니다.  
  
 **Boolean**  
 {true, false} 또는 {0, 1}처럼 두 개의 값만 가지는 열거형입니다.  
  
## <a name="default-values"></a>기본값  
 Analysis Services에서는 다음 표에 나열된 기본값을 사용합니다.  
  
|XML 데이터 형식|기본값|  
|-------------------|-------------------|  
|**Boolean**|False|  
|**문자열**|""(빈 문자열)|  
|**정수** 또는 **긴**|0(영)|  
|**타임 스탬프**|12시: 00 AM, 1/1/0001 (해당 하는.NET Frameworks **System.DateTime** 틱 수가 0 인)|  
  
 존재하기는 하지만 비어 있는 요소는 기본값이 아닌 Null 문자열 값을 갖는 것으로 해석됩니다.  
  
### <a name="inherited-defaults"></a>상속된 기본값  
 개체에 지정된 일부 속성은 자식 또는 하위 항목 개체의 동일한 속성에 기본값을 제공합니다. 예를 들어 **Cube.StorageMode** 에 대 한 기본값을 제공 **Partition.StorageMode**합니다. Analysis Services에서 상속된 기본값에 적용하는 규칙은 다음과 같습니다.  
  
-   XML에서 자식 개체의 속성이 Null이면 속성의 기본값은 상속된 값으로 기본 설정됩니다. 그러나 서버의 값을 쿼리하는 경우 서버가 XML 요소의 null 값을 반환합니다.  
  
-   자식 개체의 속성이 자식 개체에 직접 설정되었는지 또는 상속되었는지 여부를 프로그래밍 방식으로 확인할 수는 없습니다.  
  
 일부 요소에는 요소가 누락되었을 때 적용되는 기본값이 정의되어 있습니다. 예를 들어는 **차원** 다음 XML 조각에서 요소는 경우에 동일 **차원** 요소를 포함 한 **Visible** 요소인 하지만 다른  **차원** 요소는 그렇지 않습니다.  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 상속 된 기본값에 대 한 자세한 내용은 참조 하십시오. [ASSL 개체 및 개체 특징](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)합니다.  
  
  
