---
title: 차원 특성 속성 참조 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- properties [Analysis Services], attributes
- attributes [Analysis Services], properties
ms.assetid: 7f83d1cb-4732-424f-adc5-2449c1dd1008
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: db132a4a4cf6e8c2b73067220a5ed91a5316afef
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075193"
---
# <a name="dimension-attribute-properties-reference"></a>차원 특성 속성 참조
   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에는 차원 및 차원 특성의 작동 방식을 결정하는 많은 속성이 있습니다. 다음 표에서는 이러한 각 특성 속성을 나열하고 설명합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|`AttributeHierarchyDisplayFolder`|연관된 특성 계층을 최종 사용자에게 표시할 폴더를 식별합니다.|  
|`AttributeHierarchyEnabled`|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 특성에 대한 특성 계층을 생성할지 여부를 결정합니다. 특성 계층이 설정되지 않으면 사용자 정의 계층에서 해당 특성을 사용할 수 없고 MDX(Multidimensional Expressions) 문에서 특성 계층을 참조할 수 없습니다.|  
|`AttributeHierarchyOptimizedState`|특성 계층에 적용되는 최적화 수준을 결정합니다. 기본적으로 특성 계층은 `FullyOptimized`입니다. 즉, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 특성 계층에 대한 인덱스를 작성하여 쿼리 성능을 향상시킵니다.  다른 옵션인 `NotOptimized`는 특성 계층에 대해 작성된 인덱스가 없다는 의미입니다. 특성에 대해 추가 인덱스가 작성되지 않으므로 `NotOptimized` 사용은 특성 계층이 쿼리 이외의 용도로 사용될 경우에 유용합니다. 특성 계층은 다른 특성을 정렬하는 데 사용할 수도 있습니다.|  
|`AttributeHierarchyOrdered`|연관된 특성 계층의 정렬 여부를 결정합니다. 기본값은 `True`입니다. 그러나 특성 계층이 쿼리에 사용되지 않을 경우 이 속성 값을 `False`로 변경하여 처리 시간을 단축할 수 있습니다.|  
|`AttributeHierarchyVisible`|클라이언트 애플리케이션에서 특성 계층을 볼 수 있는지 여부를 결정합니다. 기본값은 `True`입니다. 그러나 특성 계층이 쿼리에 사용되지 않을 경우 이 속성 값을 `False`로 변경하여 처리 시간을 단축할 수 있습니다.|  
|`CustomRollupColumn`|사용자 지정 롤업 수식을 정의하는 열을 지정합니다.|  
|`CustomRollupPropertiesColumn`|사용자 지정 롤업 수식의 속성을 포함하는 열을 지정합니다.|  
|`DefaultMember`|특성의 기본 측정값을 정의하는 MDX(Multidimensional Expressions) 식을 지정합니다.|  
|`Description`|특성에 대한 설명을 포함합니다.|  
|`DiscretizationBucketCount`|불연속화할 버킷의 수를 포함합니다.|  
|`DiscretizationMethod`|불연속화에 사용할 방법을 정의합니다.|  
|`EstimatedCount`|특성의 예상 멤버 수를 지정합니다. 집계 디자인 마법사를 실행할 때까지 기본값은 0입니다. 마법사에서 레코드 수를 계산하도록 하거나 예상 값을 직접 입력할 수 있습니다. 멤버 수를 알고 있으며 데이터베이스에 멤버 수를 쿼리하는 시간을 단축하고 싶은 경우 값을 직접 입력합니다. 프로덕션 데이터의 테스트 하위 집합으로 작업하는 경우에는 집계 디자인이 테스트 데이터 대신 프로덕션 데이터에 맞게 최적화될 수 있도록 프로덕션 데이터의 멤버 수를 사용합니다.|  
|`GroupingBehavior`|특성을 그룹화하는 방법에 대한 힌트를 클라이언트 애플리케이션에 제공하는 사용자 정의 값입니다.|  
|`ID`|차원의 고유 ID를 포함합니다.|  
|`InstanceSelection`|목록의 예상 항목 수를 기반으로 항목 목록의 표시 방법에 대한 힌트를 클라이언트 애플리케이션에 제공합니다. 다음과 같은 옵션을 사용할 수 있습니다.<br /><br /> **None** 클라이언트 응용 프로그램에 힌트를 제공하지 않습니다. 이것은 기본값입니다.<br /><br /> **DropDown** 항목 수가 드롭다운 목록에 표시할 수 있을 만큼 적습니다.<br /><br /> **List** 항목 수가 드롭다운 **목록**에 표시하기에는 너무 많지만 필터링이 필요한 정도는 아닙니다.<br /><br /> **FilteredList** 항목 수가 많아 표시할 항목을 사용자가 필터링해야 합니다.<br /><br /> **MandatoryFilter** 항목 수가 너무 많아 표시 항목을 항상 필터링해야 합니다.|  
|`IsAggregatable`|특성 멤버 값을 집계할 수 있는지 여부를 지정합니다. 기본값은 `True`이며 특성 계층에 (All) 수준이 포함됨을 의미합니다. 이 속성 값이 `False`이면 특성 계층에 (All) 수준이 포함되지 않습니다.|  
|`KeyColumns`|특성의 키를 나타내는 열을 포함합니다. 이러한 열은 특성이 바인딩된 데이터 원본 뷰의 기본 관계형 테이블에 있는 열을 나타냅니다.  `NameColumn` 속성 값을 지정하지 않는 한 각 멤버의 이 열 값이 사용자에게 표시됩니다.|  
|`MemberNamesUnique`|특성 계층의 멤버 이름이 고유해야 하는지 여부를 결정합니다.|  
|`MembersWithData`|부모 특성이 리프가 아닌 멤버에 대한 데이터 멤버를 표시할지 여부를 결정하는 데 사용합니다. 이 속성 값은 `Usage` 속성 값을 Parent로 설정한 경우에만 사용됩니다. 즉, 부모-자식 계층이 정의된 경우입니다. 다음과 같은 옵션을 사용할 수 있습니다.<br /><br /> **NonLeafDataHidden** 리프가 아닌 데이터가 숨겨집니다.<br /><br /> **NonLeafDataVisible** 리프가 아닌 데이터가 표시됩니다.|  
|`MembersWithDataCaption`|부모 특성이 시스템 생성 데이터 멤버에 대한 캡션을 만들기 위해 사용하는 템플릿 문자열을 제공합니다. 이 속성 값은 `Usage` 속성 값을 Parent로 설정한 경우에만 사용됩니다. 즉, 부모-자식 계층이 정의된 경우입니다. |  
|`Name`|특성의 이름을 포함합니다.|  
|`NameColumn`|특성의 키 열에 있는 값 대신 사용자에게 표시되는 특성의 이름을 제공하는 열을 식별합니다. 이 열은 특성 멤버의 키 열 값이 암호화되어 있거나 사용자에게 유용하지 않을 때 또는 키 열이 복합 키를 기반으로 할 경우 사용됩니다. `NameColumn` 속성은 부모-자식 계층에서 사용되지 않습니다. 대신 자식 멤버의 `NameColumn` 속성이 부모-자식 계층의 멤버 이름으로 사용됩니다.|  
|`NamingTemplate`|부모 특성에서 생성된 부모-자식 계층에서 수준의 이름이 지정되는 방식을 정의합니다. 이 속성 값은 `Usage` 속성 값을 Parent로 설정한 경우에만 사용됩니다. 즉, 부모-자식 계층이 정의된 경우입니다.|  
|`OrderBy`|특성 계층에 포함된 멤버의 정렬 방식을 설명합니다. 기본값은 Name입니다. 이 값은 `NameColumn` 속성의 값에 따라 특성 멤버의 정렬을 지정합니다(있는 경우). 기본값이 아니면 멤버는 키 열의 값으로 정렬됩니다. 다음과 같은 옵션을 사용할 수 있습니다.<br /><br /> `NameColumn` 값을 기준으로 정렬 된 `NameColumn` 속성입니다.<br /><br /> **Key** 특성 멤버의 키 열 값을 기준으로 정렬됩니다.<br /><br /> **AttributeKey** 지정된 특성의 멤버 키 값을 기준으로 정렬됩니다. 단, 멤버 키는 해당 특성과 특성 관계에 있어야 합니다.<br /><br /> **AttributeName** 지정된 특성의 멤버 이름 값을 기준으로 정렬됩니다. 단, 멤버 이름은 해당 특성과 특성 관계에 있어야 합니다.|  
|`OrderByAttribute`|특성 계층의 멤버를 정렬하는 기준 특성을 식별합니다.|  
|`RootMemberIf`|부모-자식 계층의 루트 또는 최상위 멤버를 식별하는 방법을 결정합니다. 이 속성 값은 `Usage` 속성 값을 Parent로 설정한 경우에만 사용됩니다. 즉, 부모-자식 계층이 정의된 경우입니다. 기본값은 `ParentIsBlankSelfOrMissing`이며 `ParentIsBlank`, `ParentIsSelf` 또는 `ParentIsMissing`에 대해 설명된 조건 중 하나 이상을 만족하는 멤버만 루트 멤버로 처리됨을 의미합니다. 사용할 수 있는 값은 다음과 같습니다.<br /><br /> `ParentIsBlank` Null, 0 또는 빈 문자열을 키 열에 있는 멤버만 루트 멤버로 처리 됩니다.<br /><br /> `ParentIsSelf` 부모로 자신 있는 멤버만 루트 멤버로 처리 됩니다.<br /><br /> `ParentIsMissing` 부모를 찾을 수 없는 멤버만 루트 멤버로 처리 됩니다.|  
|`Type`|특성의 유형을 포함합니다. 자세한 내용은 [특성 유형 구성](attribute-properties-configure-attribute-types.md)을 참조하세요.|  
|`UnaryOperatorColumn`|단항 연산자를 제공하는 열을 지정합니다. 단항 연산자를 제공하는 열의 세부 정보를 정의하는 DataItem 유형의 바인딩입니다.|  
|`Usage`|특성의 사용 방식을 설명합니다.<br /><br /> 다음과 같은 옵션을 사용할 수 있습니다.<br /><br /> `Regular` 특성이 일반 특성이입니다. 이것은 기본값입니다.<br /><br /> **Key** 특성이 키 특성입니다.<br /><br /> **Parent** 특성이 부모 특성입니다.|  
|`ValueColumn`|특성 값을 제공하는 열을 식별합니다. 특성의 `NameColumn` 요소를 지정한 경우 동일한 `DataItem` 값이 `ValueColumn` 요소의 기본값으로 사용됩니다. 특성의 `NameColumn` 요소를 지정하지 않았으며 특성의 `KeyColumns` 컬렉션에 문자열 데이터 형식의 키 열을 나타내는 단일 `KeyColumn` 요소가 포함되어 있는 경우 동일한 `DataItem` 값이 `ValueColumn` 요소의 기본값으로 사용됩니다.|  
  
> [!NOTE]  
>  에 대 한 값을 설정 하는 방법에 대 한 자세한 내용은 합니다 `KeyColumn` null 값 및 다른 데이터 무결성 문제를 사용 하 여 작업할 때 속성 참조 [Analysis Services 2005에서 데이터 무결성 문제 처리](https://go.microsoft.com/fwlink/?LinkId=81891)합니다.  
  
> [!NOTE]  
>  특성의 기본 멤버는 쿼리에 계층 멤버가 명시적으로 포함되어 있지 않을 때 식을 평가하는 데 사용됩니다. 특성의 기본 멤버는 해당 특성의 `DefaultMember` 속성으로 지정됩니다. 차원의 계층이 쿼리에 포함될 때는 항상 계층의 수준에 해당되는 특성의 모든 기본 멤버가 무시됩니다. 쿼리에 포함된 차원의 계층이 없으면 기본 멤버가 차원의 모든 특성에 사용됩니다. 기본 멤버에 대한 자세한 내용은 [기본 멤버 정의](attribute-properties-define-a-default-member.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [특성 및 특성 계층](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  
