---
title: XML 규칙 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 41e0a3fcf4348efcb2108a1205c1d2d8eabfb85c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62736396"
---
# <a name="assl-xml-conventions"></a>ASSL XML 표기 규칙
  ASSL(Analysis Services Scripting Language)은 개체의 계층을 요소 유형의 집합으로 나타내며, 각 요소 유형은 포함할 수 있는 자식 요소를 정의합니다.  
  
 개체 계층을 나타내기 위해 ASSL에서는 다음과 같은 XML 표기 규칙을 사용합니다.  
  
-   모든 개체 및 속성은 ' xml: lang ' 같은 표준 XML 특성을 제외 하 고 요소로 표시 됩니다.  
  
-   요소 이름과 열거형 값은 모두 밑줄을 사용하지 않는 파스칼식 Microsoft .NET Framework 명명 규칙을 따릅니다.  
  
-   모든 값의 대/소문자는 유지됩니다. 열거형의 값도 대/소문자를 구분합니다.  
  
 이 표기 규칙 목록 외에도 Analysis Services는 카디널리티, 상속, 공백, 데이터 형식 및 기본값에 관한 특정 표기 규칙을 따릅니다.  
  
## <a name="cardinality"></a>카디널리티  
 요소의 카디널리티가 1보다 큰 경우에는 XML 요소 컬렉션에서 이 요소를 캡슐화합니다. 컬렉션 이름에는 컬렉션에 포함된 복수 형태의 요소를 사용합니다. 예를 들어, 다음 XML 조각은 `Dimensions` 요소 내의 `Database` 컬렉션을 나타냅니다.  
  
 `<Database>`  
  
 `...`  
  
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
 겹치는 부분이 있으면서도 상당히 다른 속성 집합을 가지고 있는 서로 다른 개체가 있을 때 상속이 사용됩니다. 겹치면서도 서로 다른 개체의 예로는 가상 큐브, 연결된 큐브 및 일반 큐브가 있습니다. Analysis Services에서는 겹치면서도 서로 다른 개체에 대해 XML 인스턴스 네임스페이스의 표준 `type` 특성을 사용하여 상속을 나타냅니다. 예를 들어, 다음 XML 조각에서는 `type` 요소가 일반 큐브에서 상속되는지 또는 가상 큐브에서 상속되는지를 `Cube` 특성을 통해 식별하는 방법을 보여 줍니다.  
  
 `<Cubes>`  
  
 `<Cube xsi:type="RegularCube">`  
  
 `<Name>Sales</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `<Cube xsi:type="VirtualCube">`  
  
 `<Name>SalesAndInventory</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `</Cubes>`  
  
 ``  
  
 여러 형식에 같은 이름의 속성이 있는 경우에는 일반적으로 상속을 사용하지 않습니다. 예를 들어, `Name` 및 `ID` 속성은 많은 요소에 나타나지만 이러한 속성은 추상 형식으로 승격되지 않습니다.  
  
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
  
 `Int`  
 -231 ~ 231-1 범위의 정수 값입니다.  
  
 `Long`  
 -263-263-1 범위의 정수 값입니다.  
  
 `String`  
 다음과 같은 전역 규칙을 따르는 문자열 값입니다.  
  
-   제어 문자가 제거됩니다.  
  
-   선행 공백과 후행 공백이 잘립니다.  
  
-   내부 공백이 유지됩니다.  
  
 
  `Name` 및 `ID` 속성에는 문자열 요소의 유효한 문자에 대한 특별한 제한이 있습니다. 및 `ID` 규칙에 대 `Name` 한 자세한 내용은 [개체 및 개체 특성](assl-objects-and-object-characteristics.md)을 참조 하세요.  
  
 `DateTime`  
 .NET Framework `DateTime` 구조체입니다. 
  `DateTime` 값은 NULL일 수 없습니다. 
  `DataTime` 데이터 형식에서 지원되는 가장 이른 날짜는 1601년 1월 1일이며 프로그래머는 이 날짜를 `DateTime.MinValue`로 사용할 수 있습니다. 지원되는 가장 낮은 날짜는 `DateTime` 값이 누락되었음을 나타냅니다.  
  
 `Boolean`  
 {true, false} 또는 {0, 1}처럼 두 개의 값만 가지는 열거형입니다.  
  
## <a name="default-values"></a>기본값  
 Analysis Services에서는 다음 표에 나열된 기본값을 사용합니다.  
  
|XML 데이터 형식|기본값|  
|-------------------|-------------------|  
|`Boolean`|False|  
|`String`|""(빈 문자열)|  
|`Integer`디스크나`Long`|0(영)|  
|`Timestamp`|오전 12:00:00, 1/1/0001 (0 틱이 있는 .NET Framework `System.DateTime` 에 해당)|  
  
 존재하기는 하지만 비어 있는 요소는 기본값이 아닌 Null 문자열 값을 갖는 것으로 해석됩니다.  
  
### <a name="inherited-defaults"></a>상속된 기본값  
 개체에 지정된 일부 속성은 자식 또는 하위 항목 개체의 동일한 속성에 기본값을 제공합니다. 예를 들어, `Cube.StorageMode`는 `Partition.StorageMode`에 기본값을 제공합니다. Analysis Services에서 상속된 기본값에 적용하는 규칙은 다음과 같습니다.  
  
-   XML에서 자식 개체의 속성이 Null이면 속성의 기본값은 상속된 값으로 기본 설정됩니다. 그러나 서버의 값을 쿼리하는 경우 서버가 XML 요소의 null 값을 반환합니다.  
  
-   자식 개체의 속성이 자식 개체에 직접 설정되었는지 또는 상속되었는지 여부를 프로그래밍 방식으로 확인할 수는 없습니다.  
  
 일부 요소에는 요소가 누락되었을 때 적용되는 기본값이 정의되어 있습니다. 예를 들어, 다음 XML 조각에서 한 `Dimension` 요소에는 `Dimension` 요소가 있고 다른 `Visible` 요소에는 해당 요소가 없어도 두 `Dimension` 요소는 동일합니다.  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 상속 된 기본값에 대 한 자세한 내용은 [개체 및 개체 특성](assl-objects-and-object-characteristics.md)을 참조 하세요.  
  
  
