---
title: "Analysis Services 데이터베이스에 대한 확장 필드 속성(SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1d7d87e2-bf0d-4ebb-a287-80b5a967a3f2
caps.latest.revision: "7"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d3cd894cfb7466ae39ac921b8b3405da6c2e77a3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="extended-field-properties-for-an-analysis-services-database-ssrs"></a>Analysis Services 데이터베이스에 대한 확장 필드 속성(SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 처리 확장 프로그램은 확장 필드 속성을 지원합니다. 확장 필드 속성은 **Value** 및 **IsMissing** 외에 데이터 원본에서 사용할 수 있고 데이터 처리 확장 프로그램에서 지원되는 속성입니다. 확장 속성은 보고서 데이터 집합에 대한 필드 컬렉션의 일부로 보고서 데이터 창에 나타나지 않습니다. 기본 제공 **Fields** 컬렉션을 사용하여 이름으로 확장 필드 속성 값을 지정하는 식을 작성하면 보고서에 확장 필드 속성 값을 포함할 수 있습니다.  
  
 확장 속성에는 미리 정의된 속성과 사용자 지정 속성이 포함됩니다. 미리 정의된 속성은 여러 데이터 원본에 공통되는 속성으로, 특정 필드 속성 이름에 매핑되고 기본 제공 **Fields** 컬렉션을 통해 이름으로 액세스될 수 있습니다. 사용자 지정 속성은 각 데이터 공급자별로 정의되며 확장 속성 이름을 문자열로 사용하는 구문에 의해서만 기본 제공 **Fields** 컬렉션을 통해 액세스될 수 있습니다.  
  
 그래픽 모드에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] MDX 쿼리 디자이너를 사용하여 쿼리를 정의하면 미리 정의된 셀 속성 및 차원 속성 집합이 자동으로 MDX 쿼리에 추가됩니다. 보고서의 MDX 쿼리에 구체적으로 나열된 확장 속성만 사용할 수 있습니다. 보고서에 따라 기본 MDX 명령 텍스트를 수정하여 큐브에 정의된 다른 차원 속성이나 사용자 지정 속성을 포함할 수도 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본에서 사용할 수 있는 확장 필드에 대한 자세한 내용은 [속성 값 만들기 및 사용&#40;MDX&#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)을 참조하세요.  
  
## <a name="working-with-field-properties-in-a-report"></a>보고서에서 필드 속성 사용  
 확장 필드 속성에는 미리 정의된 속성과 데이터 공급자 관련 속성이 포함됩니다. 필드 속성은 데이터 집합에 대해 작성된 쿼리에 포함되어 있어도 **보고서 데이터** 창의 필드 목록에 나타나지 않습니다. 따라서 필드 속성을 보고서 디자인 화면으로 끌 수 없습니다. 대신 필드를 보고서로 끈 다음 필드의 **Value** 속성을 사용하려는 속성으로 변경해야 합니다. 예를 들어 큐브의 셀 데이터 형식이 이미 지정되어 있는 경우 `=Fields!FieldName.FormattedValue`식을 통해 FormattedValue 필드 속성을 사용할 수 있습니다.  
  
 미리 정의되지 않은 확장 속성을 참조하려면 식에 다음 구문을 사용하십시오.  
  
-   *Fields!FieldName("PropertyName")*  
  
## <a name="predefined-field-properties"></a>미리 정의된 필드 속성  
 대부분의 경우 미리 정의된 필드 속성은 측정값, 수준 또는 차원에 적용됩니다. 미리 정의된 필드 속성의 해당 값은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본에 저장되어 있어야 합니다. 예를 들어 값이 없거나 수준에서 측정값 전용 필드 속성을 지정한 경우에는 Null 값이 반환됩니다.  
  
 다음 구문 중 하나를 사용하여 식에서 미리 정의된 속성을 참조할 수 있습니다.  
  
-   *Fields!FieldName.PropertyName*  
  
-   *Fields!FieldName("PropertyName")*  
  
 다음 표에서는 사용할 수 있는 미리 정의된 필드 속성 목록을 보여 줍니다.  
  
|**속성**|**형식**|**설명 또는 필요한 값**|  
|------------------|--------------|---------------------------------------|  
|**Value**|**개체**|필드의 데이터 값을 지정합니다.|  
|**IsMissing**|**Boolean**|필드가 결과 데이터 집합에 있는지 여부를 나타냅니다.|  
|**UniqueName**|**문자열**|수준의 정규화된 이름을 반환합니다. 예를 들어 직원의 **UniqueName** 값은 *[Employee].[Employee Department].[Department].&[Sales].&[North American Sales Manager].&[272]*일 수 있습니다.|  
|**BackgroundColor**|**문자열**|필드에 대해 데이터베이스에 정의된 배경색을 반환합니다.|  
|**색**|**문자열**|항목에 대해 데이터베이스에 정의된 전경색을 반환합니다.|  
|**FontFamily**|**문자열**|항목에 대해 데이터베이스에 정의된 글꼴 이름을 반환합니다.|  
|**FontSize**|**문자열**|항목에 대해 데이터베이스에 정의된 글꼴 크기를 반환합니다.|  
|**FontWeight**|**문자열**|항목에 대해 데이터베이스에 정의된 글꼴 두께를 반환합니다.|  
|**FontStyle**|**문자열**|항목에 대해 데이터베이스에 정의된 글꼴 스타일을 반환합니다.|  
|**TextDecoration**|**문자열**|항목에 대해 데이터베이스에 정의된 특수 텍스트 서식을 반환합니다.|  
|**FormattedValue**|**문자열**|측정값 또는 주요 숫자 값의 형식화된 값을 반환합니다. 예를 들어 **Sales Amount Quota** 에 대한 **FormattedValue** 속성은 $1,124,400.00과 같은 통화 형식을 반환합니다.|  
|**Key**|**개체**|수준의 키를 반환합니다.|  
|**LevelNumber**|**정수**|부모-자식 계층에 대해 수준 또는 차원 번호를 반환합니다.|  
|**ParentUniqueName**|**문자열**|부모-자식 계층에 대해 부모 수준의 정규화된 이름을 반환합니다.|  
  
> [!NOTE]  
>  이러한 확장 필드 속성의 값은 보고서가 실행되어 해당 데이터 집합에 대한 데이터가 검색될 때 데이터 원본(예: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브)이 이러한 값을 제공하는 경우에만 존재합니다. 이러한 값이 존재하는 경우 다음 섹션에 설명된 구문을 사용하여 모든 식에서 해당 필드 속성 값을 참조할 수 있습니다. 그러나 이러한 필드는 이 데이터 공급자에만 해당되므로 이러한 값을 변경해도 보고서 정의와 함께 저장되지 않습니다.  
  
### <a name="example-extended-properties"></a>확장 속성 예  
 확장 속성을 설명하기 위해 다음 MDX 쿼리와 결과 집합에는 큐브에 대해 정의된 차원 특성에서 사용할 수 있는 몇 개의 멤버 속성이 포함되어 있습니다. 포함된 멤버 속성은 MEMBER_CAPTION, UNIQUENAME, Properties("Day Name"), MEMBER_VALUE, PARENT_UNIQUE_NAME 및 MEMBER_KEY입니다.  
  
 이 MDX 쿼리는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 예제 데이터베이스에 포함된 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW 데이터베이스의 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 큐브에 대해 실행됩니다.  
  
```  
WITH MEMBER [Measures].[DateCaption]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_CAPTION'   
   MEMBER [Measures].[DateUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.UNIQUENAME'   
   MEMBER [Measures].[DateDayName]   
      AS '[Date].[Date].Properties("Day Name")'   
   MEMBER [Measures].[DateValueinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_VALUE'   
   MEMBER [Measures].[DateParentUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.PARENT_UNIQUE_NAME'   
   MEMBER [Measures].[DateMemberKeyinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_KEY'   
SELECT {  
   [Measures].[DateCaption],   
   [Measures].[DateUniqueName],   
   [Measures].[DateDayName],   
   [Measures].[DateValueinOriginalDatatype],  
   [Measures].[DateParentUniqueName],  
   [Measures].[DateMemberKeyinOriginalDatatype]  
   } ON COLUMNS , [Date].[Date].ALLMEMBERS ON ROWS   
FROM [Adventure Works]  
  
```  
  
 MDX 쿼리 창에서 이 쿼리를 실행하면 1158개 행이 포함된 결과 집합이 나타납니다. 다음 표에서는 처음 4개 행을 보여 줍니다.  
  
|DateCaption|DateUniqueName|DateDayName|DateValueinOriginalDatatype|DateParentUniqueName|DateMemberKeyinOriginalDatatype|  
|-----------------|--------------------|-----------------|---------------------------------|--------------------------|-------------------------------------|  
|All Periods|[Date].[Date].[All Periods]|(null)|(null)|(null)|0|  
|1-Jul-01|[Date].[Date].&[1]|일요일|7/1/2001|[Date].[Date].[All Periods]|1.|  
|2-Jul-01|[Date].[Date].&[2]|월요일|7/2/2001|[Date].[Date].[All Periods]|2|  
|3-Jul-01|[Date].[Date].&[3]|화요일|7/3/2001|[Date].[Date].[All Periods]|3|  
  
 그래픽 모드로 MDX 쿼리 디자이너를 사용하여 작성한 기본 MDX 쿼리는 차원 속성으로 MEMBER_CAPTION과 UNIQUENAME만 포함합니다. 기본적으로 이러한 값은 항상 **String**데이터 형식입니다.  
  
 원래 데이터 형식에 멤버 속성이 필요한 경우 텍스트 기반 쿼리 디자이너에서 기본 MDX 문을 수정하여 추가 속성 MEMBER_VALUE를 포함할 수 있습니다. 간단한 다음 MDX 문에서 MEMBER_VALUE는 검색할 차원 속성 목록에 추가되었습니다.  
  
```  
SELECT NON EMPTY {[Measures].[Order Count]} ON COLUMNS,   
NON EMPTY { ([Date].[Month of Year].[Month of Year] ) }   
DIMENSION PROPERTIES   
   MEMBER_CAPTION, MEMBER_UNIQUE_NAME, MEMBER_VALUE ON ROWS   
FROM [Adventure Works]  
CELL PROPERTIES   
   VALUE, BACK_COLOR, FORE_COLOR,   
   FORMATTED_VALUE, FORMAT_STRING,   
   FONT_NAME, FONT_SIZE, FONT_FLAGS  
```  
  
 다음 표에서는 MDX 결과 창에 나타나는 결과의 처음 4개 행을 보여 줍니다.  
  
|Month of Year|Order Count|  
|-------------------|-----------------|  
|January|2,481|  
|February|2,684|  
|March|2,749|  
|April|2,739|  
  
 속성은 MDX SELECT 문의 일부이지만 결과 집합 열에 나타나지 않습니다. 그러나 확장 속성 기능을 사용하여 이 데이터를 보고서에 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 MDX 쿼리 결과 창에서 셀을 두 번 클릭하면 큐브에 설정된 경우 셀 속성 값을 볼 수 있습니다. 1,379가 포함된 첫 번째 Order Count 셀을 두 번 클릭하면 다음 셀 속성이 있는 팝업 창이 표시됩니다.  
  
|속성|Value|  
|--------------|-----------|  
|CellOrdinal|0|  
|Value|2481|  
|BACK_COLOR|(null)|  
|FORE_COLOR|(null)|  
|FORMATTED_VALUE|2,481|  
|FORMAT_STRING|#,#|  
|FONT_NAME|(null)|  
|FONT_SIZE|(null)|  
|FONT_FLAGS|(null)|  
  
 이 쿼리를 사용하여 보고서 데이터 집합을 만들고 테이블에 바인딩하면 필드의 기본 VALUE 속성(예: `=Fields!Month_of_Year!Value`)을 볼 수 있습니다. 이 식을 테이블에 대한 정렬 식으로 설정하면 Value 필드가 **String** 데이터 형식을 사용하므로 테이블이 월을 기준으로 사전순으로 정렬됩니다. 월이 연도에서 발생하는 순서대로, 즉 1월이 처음이고 12월이 마지막이 되도록 테이블을 정렬하려면 다음 식을 사용합니다.  
  
```  
=Fields!Month_of_Year("MEMBER_VALUE")  
```  
  
 이렇게 하면 데이터 원본의 원래 정수 데이터 형식으로 필드 값이 정렬됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [식의 기본 제공 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
