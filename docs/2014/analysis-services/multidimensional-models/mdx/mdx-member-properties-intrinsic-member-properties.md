---
title: 내장 멤버 속성 (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- intrinsic member properties [MDX]
ms.assetid: 84e6fe64-9b37-4e79-bedf-ae02e80bfce8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 268203d044734bb4e6a1d2acf6311ee7ef828a53
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546365"
---
# <a name="intrinsic-member-properties-mdx"></a>기본 멤버 속성(MDX)
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에서는 차원 멤버의 기본 속성을 표시합니다. 이러한 기본 속성을 쿼리에 포함하면 사용자 지정 애플리케이션에 사용할 추가 데이터 또는 메타데이터를 반환하거나 모델을 간편하게 검토 또는 생성할 수 있습니다. SQL Server 클라이언트 도구를 사용하는 경우 SSMS(SQL Server Management Studio)에서 기본 속성을 볼 수 있습니다.  
  
 기본 속성으로는 모든 멤버가 모든 수준에서 표시하는 `ID`, `KEY`, `KEYx` 및 `NAME`이 있습니다. 특히 `LEVEL_NUMBER` 또는 `PARENT_UNIQUE_NAME`과 같은 위치 정보를 반환할 수도 있습니다.  
  
 쿼리 작성 방법 및 쿼리 실행에 사용하는 클라이언트 애플리케이션에 따라 결과 집합에 멤버 속성이 표시될 수도 있고 그렇지 않을 수도 있습니다. 쿼리 테스트 또는 실행에 SQL Server Management Studio를 사용하는 경우 결과 집합에서 멤버를 두 번 클릭하여 각 멤버의 기본 속성 값이 표시된 멤버 속성 대화 상자를 열 수 있습니다.  
  
 차원 멤버 속성을 사용하고 보는 방법에 대한 개요를 보려면 [SSMS에서 MDX 쿼리 창에서 SSAS 멤버 속성 보기](https://go.microsoft.com/fwlink/?LinkId=317362)를 참조하십시오.  
  
> [!NOTE]  
>  1999 년 3 월 (2.6)에 설명 된 OLE DB 사양의 OLAP 섹션을 준수 하는 공급자는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 이 항목에 나열 된 기본 멤버 속성을 지원 합니다.  
>   
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 이외의 공급자가 기본 멤버 속성을 추가로 지원할 수도 있습니다. 다른 공급자가 지원하는 기본 멤버 속성에 대한 자세한 내용은 해당 공급자가 제공하는 설명서를 참조하십시오.  
  
## <a name="types-of-member-properties"></a>멤버 속성의 유형  
 에서 지 원하는 기본 멤버 속성은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 다음 두 가지 유형입니다.  
  
 상황에 맞는 멤버 속성  
 이 유형의 멤버 속성은 특정 계층 또는 수준의 컨텍스트에서 사용해야 하고 지정한 차원 또는 수준의 각 멤버에 대한 값을 제공합니다.  
  
 다음 예를 보면 `KEY` 속성의 경로가 포함되어 있습니다. `MEMBER [Measures].[Parent Member Key] AS [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("KEY")`  
  
 상황에 맞지 않는 멤버 속성  
 이 유형의 멤버 속성은 특정 차원 또는 수준의 컨텍스트에서 사용할 수 없고 한 축의 모든 멤버에 대한 값을 반환합니다.  
  
 상황에 맞지 않는 속성은 독립적이며 경로 정보를 포함하지 않습니다. 다음 예에서는 `PARENT_UNIQUE_NAME`에 대해 차원이나 수준이 지정되어 있지 않습니다. `DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS`  
  
 기본 멤버 속성이 상황에 맞든 맞지 않든 상관없이 다음의 사용 규칙이 적용됩니다.  
  
-   축에 표시되는 차원 멤버와 관련된 기본 멤버 속성만 지정할 수 있습니다.  
  
-   상황에 맞지 않는 기본 멤버 속성을 가진 같은 쿼리에서 상황에 맞는 멤버 속성에 대한 요청을 혼합할 수 있습니다.  
  
-   `PROPERTIES` 키워드를 사용하여 속성에 대해 쿼리합니다.  
  
 다음 섹션에서는에서 사용할 수 있는 다양 한 상황에 맞는 기본 멤버 속성과 상황에 맞지 않는 기본 멤버 속성을 모두 설명 하 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 고 `PROPERTIES` 각 속성 형식에 키워드를 사용 하는 방법에 대해 설명 합니다.  
  
## <a name="context-sensitive-member-properties"></a>상황에 맞는 멤버 속성  
 모든 차원 멤버와 수준 멤버는 상황에 맞는 기본 멤버 속성 목록을 지원합니다. 다음 표에서는 이러한 상황에 맞는 속성을 나열합니다.  
  
|속성|설명|  
|--------------|-----------------|  
|`ID`|내부적으로 유지 관리되는 멤버 ID입니다.|  
|`Key`|원본 데이터 형식에서 멤버 키의 값입니다. MEMBER_KEY는 이전 버전과의 호환성을 위해 제공됩니다.  비복합 키의 경우 MEMBER_KEY 값이 KEY0과 동일하고 복합 키의 경우 MEMBER_KEY 속성이 Null입니다.|  
|`KEYx`|멤버에 대한 키이며 x는 키의 서수 값(0부터 시작)입니다. KEY0은 복합 키와 비복합 키에 모두 사용할 수 있지만 주로 복합 키에 사용합니다.<br /><br /> KEY0, KEY1, KEY2 등이 모여 복합 키가 형성됩니다. 쿼리에서 각 키를 사용하여 복합 키의 해당 부분을 반환할 수 있습니다. 예를 들어 KEY0을 지정하면 복합 키의 첫 번째 부분이 반환되고 KEY1을 지정하면 복합 키의 다음 부분이 반환됩니다.<br /><br /> 복합 키가 아닌 경우 KEY0은 `Key`와 같습니다.<br /><br /> `KEYx`는 컨텍스트 내에서는 물론 컨텍스트 없이도 사용할 수 있습니다. 이러한 이유로 이 키는 두 목록에 모두 나와 있습니다.<br /><br /> 이 멤버 속성을 사용하는 방법에 대한 예는 [간단한 MDX Tidbit: Key0, Key1, Key2](https://go.microsoft.com/fwlink/?LinkId=317364)를 참조하세요.|  
|`Name`|멤버의 이름입니다.|  
  
### <a name="properties-syntax-for-context-sensitive-properties"></a>상황에 맞는 속성에 대한 PROPERTIES 구문  
 특정 차원 또는 수준의 컨텍스트에서 이 멤버 속성을 사용하고 지정한 차원 또는 수준의 각 멤버에 대한 값을 제공합니다.  
  
 차원 멤버 속성의 경우 속성 이름 앞에 해당 속성이 적용되는 차원 이름을 둡니다. 다음 예에서는 적합한 구문을 보여 줍니다.  
  
 `DIMENSION PROPERTIES Dimension.Property_name`  
  
 수준 멤버 속성의 경우 속성 이름 앞에 단순히 수준 이름만 두거나 추가 지정을 위해 차원 이름과 수준 이름을 앞에 둘 수 있습니다. 다음 예에서는 적합한 구문을 보여 줍니다.  
  
 `DIMENSION PROPERTIES [Dimension.]Level.Property_name`  
  
 이를 보여 주기 위해 `[Sales]` 차원에서 참조된 각 멤버의 이름을 모두 반환할 수도 있을 것입니다. 이러한 이름을 반환하려면 MDX 쿼리에 다음과 같은 문을 사용하면 됩니다.  
  
 `DIMENSION PROPERTIES [Sales].Name`  
  
## <a name="non-context-sensitive-member-properties"></a>상황에 맞지 않는 멤버 속성  
 모든 멤버가 컨텍스트에 상관없이 동일한 기본 멤버 속성 목록을 지원합니다. 이러한 속성들은 사용자에게 보다 나은 경험을 주기 위해 애플리케이션에서 사용할 수 있는 정보를 추가로 제공합니다.  
  
 다음 표에서는에서 지 원하는 상황에 맞지 않는 기본 속성을 보여 줍니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
> [!NOTE]  
>  MEMBERS 스키마 행 집합의 열은 다음 표에 나열된 기본 멤버 속성을 지원합니다. 스키마 행 집합에 대 한 자세한 내용은 `MEMBERS` [MDSCHEMA_MEMBERS 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-members-rowset)을 참조 하세요.  
  
|속성|설명|  
|--------------|-----------------|  
|`CATALOG_NAME`|이 멤버가 속한 큐브 이름입니다.|  
|`CHILDREN_CARDINALITY`|멤버의 자식 수입니다. 예상치일 수 있으므로 이 값을 정확한 수로 간주하면 안 됩니다. 공급자는 가능한 한 최적의 예상치를 반환해야 합니다.|  
|`CUSTOM_ROLLUP`|사용자 지정 멤버 식입니다.|  
|`CUSTOM_ROLLUP_PROPERTIES`|사용자 지정 멤버 속성입니다.|  
|`DESCRIPTION`|사람이 읽을 수 있는 멤버 설명입니다.|  
|`DIMENSION_UNIQUE_NAME`|이 멤버가 속한 차원의 고유한 이름입니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|`HIERARCHY_UNIQUE_NAME`|계층의 고유한 이름입니다. 멤버가 둘 이상의 계층에 속한 경우 멤버가 속한 각 계층마다 하나의 행이 있습니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|`IS_DATAMEMBER`|멤버가 데이터 멤버인지 여부를 나타내는 부울입니다.|  
|`IS_PLACEHOLDERMEMBER`|멤버가 자리 표시자인지 여부를 나타내는 부울입니다.|  
|`KEYx`|멤버에 대한 키이며 x는 키의 서수 값(0부터 시작)입니다. KEY0은 복합 키와 비복합 키에 모두 사용할 수 있습니다.<br /><br /> 복합 키가 아닌 경우 KEY0은 `Key`와 같습니다.<br /><br /> KEY0, KEY1, KEY2 등이 모여 복합 키가 형성됩니다. 쿼리에서 각 키를 참조하여 복합 키의 해당 부분을 반환할 수 있습니다. 예를 들어 KEY0을 지정하면 복합 키의 첫 번째 부분이 반환되고 KEY1을 지정하면 복합 키의 다음 부분이 반환됩니다.<br /><br /> `KEYx`는 컨텍스트 내에서는 물론 컨텍스트 없이도 사용할 수 있습니다. 이러한 이유로 이 키는 두 목록에 모두 나와 있습니다.<br /><br /> 이 멤버 속성을 사용하는 방법에 대한 예는 [간단한 MDX Tidbit: Key0, Key1, Key2](https://go.microsoft.com/fwlink/?LinkId=317364)를 참조하세요.|  
|`LCID` *x*|로캘 ID 16진수 값으로 멤버 캡션을 변환한 값이며 *x* 는 로캘 ID 10진수 값(예: 영어-캐나다의 경우 LCID1009)입니다. 데이터 원본에 바인딩된 캡션 열이 변환에 있는 경우에만 이 값을 사용할 수 있습니다.|  
|`LEVEL_NUMBER`|계층 루트에서 멤버까지의 거리입니다. 루트 수준은 0입니다.|  
|`LEVEL_UNIQUE_NAME`|이 멤버가 속한 수준의 고유한 이름입니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|`MEMBER_CAPTION`|멤버에 연결된 레이블 또는 캡션입니다. 캡션은 주로 표시용으로 사용합니다. 캡션이 없는 경우 쿼리는 `MEMBER_NAME`을 반환합니다.|  
|`MEMBER_KEY`|원본 데이터 형식에서 멤버 키의 값입니다. MEMBER_KEY는 이전 버전과의 호환성을 위해 제공됩니다.  비복합 키의 경우 MEMBER_KEY 값이 KEY0과 동일하고 복합 키의 경우 MEMBER_KEY 속성이 Null입니다.|  
|`MEMBER_NAME`|멤버의 이름입니다.|  
|`MEMBER_TYPE`|멤버의 유형입니다. 이 속성 값은 다음 중 하나일 수 있습니다. <br />**MDMEMBER_TYPE_REGULAR**<br />**MDMEMBER_TYPE_ALL**<br />**MDMEMBER_TYPE_FORMULA**<br />**MDMEMBER_TYPE_MEASURE**<br />**MDMEMBER_TYPE_UNKNOWN**<br /><br /> <br /><br /> MDMEMBER_TYPE_FORMULA가 MDMEMBER_TYPE_MEASURE보다 우선합니다. 따라서 Measures 차원에 수식(계산) 멤버가 있는 경우 계산 멤버에 대한 `MEMBER_TYPE` 속성은 MDMEMBER_TYPE_FORMULA입니다.|  
|`MEMBER_UNIQUE_NAME`|멤버의 고유한 이름입니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|`MEMBER_VALUE`|원본 형식으로 된 멤버의 값입니다.|  
|`PARENT_COUNT`|이 멤버에 있는 부모 수입니다.|  
|`PARENT_LEVEL`|계층 루트 수준에서 멤버 부모까지의 거리입니다. 루트 수준은 0입니다.|  
|`PARENT_UNIQUE_NAME`|멤버 부모의 고유한 이름입니다. 루트 수준의 모든 멤버에 대해서 `NULL`이 반환됩니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|`SKIPPED_LEVELS`|멤버의 건너뛴 수준 수입니다.|  
|`UNARY_OPERATOR`|멤버에 대한 단항 연산자입니다.|  
|`UNIQUE_NAME`|멤버의 정규화된 이름으로, [dimension].[level].[key6.] 형식입니다.|  
  
### <a name="properties-syntax-for-non-context-sensitive-properties"></a>상황에 맞지 않는 속성에 대한 PROPERTIES 구문  
 다음 구문을 사용하여 `PROPERTIES` 키워드를 사용하는 상황에 맞지 않는 기본 멤버 속성을 지정할 수 있습니다.  
  
 `DIMENSION PROPERTIES Property`  
  
 이 구문에서는 차원이나 수준별로 속성을 정규화할 수 없습니다. 상황에 맞지 않는 기본 멤버 속성이 축의 모든 멤버에 적용되므로 속성을 정규화할 수 없습니다.  
  
 예를 들어 `DESCRIPTION` 기본 멤버 속성을 지정하는 MDX 문의 구문은 다음과 같습니다.  
  
 `DIMENSION PROPERTIES DESCRIPTION`  
  
 이 문은 축 차원의 각 멤버에 대한 설명을 반환합니다. 차원 또는 수준 *에서와* 같이 차원이 나 수준으로 속성을 정규화 하 려 한 경우이 `.DESCRIPTION` *Level* `.DESCRIPTION` 문은 유효성을 검사 하지 않습니다.  
  
### <a name="example"></a>예제  
 다음 예에서는 기본 속성을 반환하는 MDX 쿼리를 보여 줍니다.  
  
 **예제 1: 쿼리에서 상황에 맞는 기본 속성 사용**  
  
 다음 예에서는 각 제품 범주의 부모 ID, 키 및 이름을 반환합니다. 속성이 측정값으로 표시되어 있습니다. 따라서 SSMS의 멤버 속성 대화 상자 대신 쿼리를 실행할 때 셀 집합에서 속성을 볼 수 있습니다. 다음과 같은 쿼리를 실행하여 이미 배포된 큐브에서 멤버 메타데이터를 검색할 수 있습니다.  
  
```  
WITH  
MEMBER [Measures].[Parent Member ID] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("ID")  
MEMBER [Measures].[Parent Member Key] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("KEY")  
MEMBER [Measures].[Parent Member Name] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("Name")  
SELECT  
 {[Measures].[Parent Member ID], [Measures].[Parent Member Key], [Measures].[Parent Member Name] } on COLUMNS,   
 [Product].[Product Categories].AllMembers on ROWS  
FROM [Adventure Works]  
```  
  
 **예제 2: 상황에 맞지 않는 기본 속성**  
  
 다음 예는 상황에 맞지 않는 기본 속성의 전체 목록입니다. SSMS에서 쿼리를 실행한 후 개별 멤버를 클릭하여 멤버 속성 대화 상자에서 속성을 볼 수 있습니다.  
  
```  
SELECT [Measures].[Sales Amount Quota] on COLUMNS,  
[Employee].[Employees].members  
DIMENSION PROPERTIES  
 CATALOG_NAME ,   
 CHILDREN_CARDINALITY ,  
 CUSTOM_ROLLUP ,   
 CUSTOM_ROLLUP_PROPERTIES ,   
 DESCRIPTION ,   
 DIMENSION_UNIQUE_NAME ,   
 HIERARCHY_UNIQUE_NAME ,  
 IS_DATAMEMBER ,   
 IS_PLACEHOLDERMEMBER ,   
 KEY0 ,  
 LCID ,  
 LEVEL_NUMBER ,  
 LEVEL_UNIQUE_NAME ,  
 MEMBER_CAPTION ,   
 MEMBER_KEY ,   
 MEMBER_NAME ,   
 MEMBER_TYPE ,  
 MEMBER_UNIQUE_NAME ,   
 MEMBER_VALUE ,   
 PARENT_COUNT ,   
 PARENT_LEVEL ,   
 PARENT_UNIQUE_NAME ,  
 SKIPPED_LEVELS ,   
 UNARY_OPERATOR ,   
 UNIQUE_NAME    
 ON ROWS  
FROM [Adventure Works]  
WHERE [Employee].[Employee Department].[Department].&[Sales]  
```  
  
 **예제 3: 멤버 속성을 결과 집합에 데이터로 반환**  
  
 다음 예에서는 지정된 로캘에 대한 Adventure Works 큐브의 Product 차원에 있는 제품 카테고리 멤버의 번역된 캡션을 반환합니다.  
  
```  
WITH   
MEMBER Measures.CategoryCaption AS Product.Category.CurrentMember.MEMBER_CAPTION  
MEMBER Measures.SpanishCategoryCaption AS Product.Category.CurrentMember.Properties("LCID3082")  
MEMBER Measures.FrenchCategoryCaption AS Product.Category.CurrentMember.Properties("LCID1036")  
SELECT   
{ Measures.CategoryCaption, Measures.SpanishCategoryCaption, Measures.FrenchCategoryCaption } ON 0  
,[Product].[Category].MEMBERS ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [PeriodsToDate &#40;MDX&#41;](/sql/mdx/periodstodate-mdx)   
 [MDX &#40;자식&#41;](/sql/mdx/children-mdx)   
 [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx)   
 [MDX&#41; &#40;&#40;집합 수&#41;](/sql/mdx/count-set-mdx)   
 [MDX &#40;필터&#41;](/sql/mdx/filter-mdx)   
 [AddCalculatedMembers &#40;MDX&#41;](/sql/mdx/addcalculatedmembers-mdx)   
 [DrilldownLevel &#40;MDX&#41;](/sql/mdx/drilldownlevel-mdx)   
 [MDX &#40;속성&#41;](/sql/mdx/properties-mdx)   
 [PrevMember &#40;MDX&#41;](/sql/mdx/prevmember-mdx)   
 [MDX&#41;&#40;멤버 속성 사용](mdx-member-properties.md)   
 [MDX 함수 참조&#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)  
  
  
