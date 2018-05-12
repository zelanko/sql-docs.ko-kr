---
title: 셀 속성 사용 (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 481d89abac98dee1095e55a9890cea100f6c4db6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-cell-properties---using-cell-properties"></a>셀 속성을 사용 하 여 MDX 셀 속성-
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  MDX의 셀 속성은 큐브와 같은 다차원 데이터 원본의 셀 내용 및 형식에 대한 정보를 포함합니다.  
  
 MDX SELECT 문에서 CELL PROPERTIES 키워드를 사용하여 기본 셀 속성을 검색할 수 있습니다. 기본 셀 속성은 일반적으로 셀 데이터의 시각적 표현을 돕는 데 자주 사용됩니다.  
  
## <a name="cell-properties-keyword-syntax"></a>CELL PROPERTIES 키워드 구문  
 MDX **CELL PROPERTIES** 문의 **SELECT** 키워드에 다음 구문을 사용하십시오.  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
[<cell_props>]  
```  
  
 다음 구문은 `<cell_props>` 값의 형식 및 이 값에서 한 개 이상의 기본 셀 속성과 함께 **CELL PROPERTIES** 키워드가 사용되는 방식을 보여 줍니다.  
  
```  
<cell_props> ::= CELL PROPERTIES <property> [, <property>...]  
```  
  
## <a name="supported-intrinsic-cell-properties"></a>지원되는 기본 셀 속성  
 다음 표에서는 `<property>` 값에서 사용되는 기본 셀 속성을 나열합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**ACTION_TYPE**|셀에 존재하는 동작 유형을 나타내는 비트 마스크입니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **MDACTION_TYPE_URL**<br /><br /> **MDACTION_TYPE_HTML**<br /><br /> **MDACTION_TYPE_STATEMENT**<br /><br /> **MDACTION_TYPE_DATASET**<br /><br /> **MDACTION_TYPE_ROWSET**<br /><br /> **MDACTION_TYPE_COMMANDLINE**<br /><br /> **MDACTION_TYPE_PROPRIETARY**<br /><br /> **MDACTION_TYPE_REPORT**<br /><br /> **MDACTION_TYPE_DRILLTHROUGH**<br /><br /> <br /><br /> 참고: where 절 내에 집합을 포함하는 쿼리는 드릴스루 동작을 포함하지 않습니다.|  
|**BACK_COLOR**|**VALUE** 또는 **FORMATTED_VALUE** 속성을 표시하는 배경색입니다. 자세한 내용은 [FORE_COLOR 및 BACK_COLOR 내용&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)을 참조하세요.|  
|**CELL_ORDINAL**|데이터 집합 내의 셀 서수 번호입니다.|  
|**FONT_FLAGS**|글꼴 효과를 자세하게 지정하는 비트 마스크입니다. 값은 다음과 같은 하나 이상의 상수에 대한 비트 OR 연산의 결과입니다.<br /><br /> **MDFF_BOLD** = 1<br /><br /> **MDFF_ITALIC** = 2<br /><br /> **MDFF_UNDERLINE** = 4<br /><br /> **MDFF_STRIKEOUT** = 8<br /><br /> <br /><br /> 예를 들어 값 5는 굵게(**MDFF_BOLD**) 및 밑줄(**MDFF_UNDERLINE**) 글꼴 효과의 조합을 나타냅니다.|  
|**FONT_NAME**|**VALUE** 또는 **FORMATTED_VALUE** 속성을 표시하는 데 사용할 글꼴입니다.|  
|**FONT_SIZE**|**VALUE** 또는 **FORMATTED_VALUE** 속성을 표시하는 데 사용할 글꼴 크기입니다.|  
|**FORE_COLOR**|**VALUE** 또는 **FORMATTED_VALUE** 속성을 표시하는 전경색입니다. 자세한 내용은 [FORE_COLOR 및 BACK_COLOR 내용&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)을 참조하세요.|  
|**FORMAT**|**FORMAT_STRING**과 동일합니다.|  
|**FORMAT_STRING**|**FORMATTED_VALUE** 속성 값을 만드는 데 사용된 형식 문자열입니다. 자세한 내용은 [FORMAT_STRING 내용&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)을 참조하세요.|  
|**FORMATTED_VALUE**|**VALUE** 속성의 형식이 지정된 표시를 나타내는 문자열입니다.|  
|**LANGUAGE**|**FORMAT_STRING** 이 적용될 로캘입니다. **LANGUAGE** 는 대개 통화 변환을 위해 사용됩니다.|  
|**UPDATEABLE**|셀을 업데이트할 수 있는지 여부를 나타내는 값입니다. 이 속성 값은 다음 중 하나일 수 있습니다.|  
||**MD_MASK_ENABLED** (0x00000000)   셀을 업데이트할 수 있습니다.|  
||**MD_MASK_NOT_ENABLED** (0x10000000)   셀을 업데이트할 수 없습니다.|  
||**CELL_UPDATE_ENABLED** (0x00000001)   셀 집합에서 셀을 업데이트할 수 있습니다.|  
||**CELL_UPDATE_ENABLED_WITH_UPDATE** (0x00000002)   update 문을 사용하여 셀을 업데이트할 수 있습니다. 쓰기가 허용되지 않은 리프 셀을 업데이트하면 업데이트에 실패할 수 있습니다.|  
||**CELL_UPDATE_NOT_ENABLED_FORMULA** (0x10000001)   셀이 셀 좌표를 따라 계산 멤버를 가지므로 업데이트할 수 없습니다. 셀이 where 절 내의 집합으로 검색되었습니다. 수식이 셀 값에 영향을 주거나 계산 셀이 셀 값(집계 경로상의 한 곳)에 있더라도 셀을 업데이트할 수 있습니다. 이 시나리오에서는 계산이 결과에 영향을 주므로 최종 셀 값은 업데이트된 값이 아닐 수 있습니다.|  
||**CELL_UPDATE_NOT_ENABLED_NONSUM_MEASURE** (0x10000002)   합계 유형이 아닌 측정값(카운트, 최소, 최대, 고유 카운트, 반가산적 측정값)은 업데이트할 수 없으므로 셀을 업데이트할 수 없습니다.|  
||**CELL_UPDATE_NOT_ENABLED_NACELL_VIRTUALCUBE** (0x10000003)   셀이 측정값 및 측정값의 측정값 그룹과 관련이 없는 차원 멤버 간의 교집합에 위치하여 존재하지 않으므로 업데이트할 수 없습니다.|  
||**CELL_UPDATE_NOT_ENABLED_SECURE** (0x10000005)   셀에 보안이 설정되어 있으므로 셀을 업데이트할 수 없습니다.|  
||**CELL_UPDATE_NOT_ENABLED_CALCLEVEL** (0x10000006)   나중에 사용하도록 예약되어 있습니다.|  
||**CELL_UPDATE_NOT_ENABLED_CANNOTUPDATE** (0x10000007)   내부적인 이유로 인해 셀을 업데이트할 수 없습니다.|  
||**CELL_UPDATE_NOT_ENABLED_INVALIDDIMENSIONTYPE** (0x10000009)   마이닝 모델, 간접 또는 데이터 마이닝 차원에서는 업데이트가 지원되지 않으므로 셀을 업데이트할 수 없습니다.|  
|**VALUE**|형식이 지정되지 않은 셀 값입니다.|  
  
 **CELL_ORDINAL**, **FORMATTED_VALUE**및 **VALUE** 셀 속성만 필수입니다. 모든 셀 속성(기본 또는 공급자별)은 해당 데이터 형식 및 공급자 지원을 포함해 **PROPERTIES** 스키마 행 집합에 정의되어 있습니다. **PROPERTIES** 스키마 행 집합에 대한 자세한 내용은 [MDSCHEMA_PROPERTIES 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-properties-rowset.md)을 참조하세요.  
  
 기본적으로 **CELL PROPERTIES** 키워드가 사용되지 않는 경우 **VALUE**, **FORMATTED_VALUE**및 **CELL_ORDINAL** 셀 속성이 순서대로 반환됩니다. **CELL PROPERTIES** 키워드를 사용하면 키워드로 명시적으로 지정한 셀 속성만 반환됩니다.  
  
 다음 예에서는 MDX 쿼리에서 **CELL PROPERTIES** 키워드를 사용하는 방법을 설명합니다.  
  
```  
SELECT  
   {[Measures].[Reseller Gross Profit]} ON COLUMNS,  
   {[Reseller].[Reseller Type].[Reseller Name].Members} ON ROWS  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORMAT_STRING, FORE_COLOR, BACK_COLOR  
```  
  
 셀 속성은 일반 행 집합을 반환하는 MDX 쿼리에 대해 반환되지 않습니다. 이 경우 각 셀은 **FORMATTED_VALUE** 셀 속성만 반환된 것처럼 표시됩니다.  
  
## <a name="setting-cell-properties"></a>셀 속성 설정  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 의 다양한 위치에서 셀 속성을 설정할 수 있습니다. 예를 들어 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에 있는 큐브 편집기의 큐브 구조 탭에서 일반 측정값에 대해 Format String 속성을 설정할 수 있습니다. 또한 큐브 편집기의 계산 탭에서 큐브에 정의된 계산 측정값에 대해서도 동일한 속성을 설정할 수 있습니다. 쿼리의 WITH 절에 정의된 계산 측정값에도 형식 문자열이 정의됩니다. 다음 쿼리에서는 계산 측정값에 대해 셀 속성을 설정하는 방법을 보여 줍니다.  
  
```  
WITH MEMBER MEASURES.CELLPROPERTYDEMO AS [Measures].[Internet Sales Amount]  
, FORE_COLOR=RGB(0,0,255)  
, BACK_COLOR=IIF([Measures].[Internet Sales Amount]>7000000, RGB(255,0,0), RGB(0,255,0))  
, FONT_SIZE=10  
, FORMAT_STRING='#,#.000'  
SELECT MEASURES.CELLPROPERTYDEMO ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS ON 1  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORE_COLOR, BACK_COLOR, FONT_SIZE  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 쿼리 기본 사항 & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
