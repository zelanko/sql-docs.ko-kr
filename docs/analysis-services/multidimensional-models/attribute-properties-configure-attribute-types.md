---
title: 특성 유형 구성 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e7be9da1b7405aa522dc29057764e7351924b41
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34025571"
---
# <a name="attribute-properties---configure-attribute-types"></a>속성을 특성-특성 유형 구성
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 특성 유형은 업무 기능에 따라 특성을 분류하는 데 유용합니다. 다양한 특성 유형이 있으며 이들 대부분은 클라이언트 애플리케이션에서 특성을 표시하거나 지원하는 용도로 사용됩니다. 하지만 일부 특성 유형이 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대해 특정한 의미를 지니기도 합니다. 예를 들어 일부 특성 유형은 시간 차원에 대한 다양한 달력의 기간을 나타내는 특성을 식별합니다.  
  
##  <a name="setting_attibute_types"></a> 특성 유형 설정  
 특성에 대한 **Type** 속성의 값이 해당 특성에 대한 특성 유형을 결정합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 여러 마법사는 차원이나 특성을 정의할 때 특성 유형을 설정합니다. 이러한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 마법사는 차원에 기능을 추가할 때도 특성 유형을 설정합니다. 예를 들어 비즈니스 인텔리전스 마법사는 차원에 있는 계정의 이름, 코드, 번호 및 구조가 포함된 특성을 식별하기 위해 계정 인텔리전스를 추가할 때 차원의 특성에 여러 특성 유형을 적용합니다. 비즈니스 인텔리전스 마법사에서도 통화 변환 등에 특성 유형을 사용합니다. 자세한 내용은 [통화 유형 차원 만들기](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)를 참조하세요.  
  
 다음 표에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 지원되는 특성 유형을 나열합니다. 이러한 표는 특성 유형을 다음 범주로 구분합니다.  
  
|용어|정의|  
|----------|----------------|  
|[일반 특성 유형](#general_attribute_types)|이러한 값은 모든 특성에 사용할 수 있으며 클라이언트 애플리케이션의 특성 분류를 허용하는 용도로만 존재합니다.|  
|[계정 차원 특성 유형](#account_dimension_attribute_types)|이러한 값은 계정 차원에 속한 특성을 식별합니다. 계정 차원에 대한 자세한 내용은 [부모-자식 유형 차원의 재무 계정 만들기](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)를 참조하세요.|  
|[통화 차원 특성 유형](#currency_dimension_attribute_types)|이러한 값은 통화 차원에 속한 특성을 식별합니다. 통화 차원에 대한 자세한 내용은 [통화 유형 차원 만들기](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)를 참조하세요.|  
|[느린 변경 차원 특성](#slowly_changing_dimension_attribute_types)|이러한 값은 느린 변경 차원에 속한 특성을 식별합니다.|  
|[시간 차원 특성](#time_dimension_attribute_types)|이러한 값은 시간 차원에 속한 특성을 식별합니다. 시간 차원에 대한 자세한 내용은 [날짜 유형 차원 만들기](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md)를 참조하세요.|  
  
###  <a name="general_attribute_types"></a> General Attribute Types  
  
|특성 유형 값|Description|  
|--------------------------|-----------------|  
|**주소**|주소를 나타냅니다.|  
|**AddressBuilding**|주소의 건물 식별자를 나타냅니다.|  
|**AddressCity**|주소의 구/군/시를 나타냅니다.|  
|**AddressCountry**|주소의 국가/지역을 나타냅니다.|  
|**AddressFax**|팩스 번호를 나타냅니다.|  
|**AddressFloor**|주소의 층 식별자를 나타냅니다.|  
|**AddressHouse**|주소의 집 호수를 나타냅니다.|  
|**AddressPhone**|전화 번호를 나타냅니다.|  
|**AddressQuarter**|주소의 구역을 나타냅니다.|  
|**AddressRoom**|주소의 방 식별자를 나타냅니다.|  
|**AddressStateOrProvince**|주소의 시/도를 나타냅니다.|  
|**AddressStreet**|주소의 번지를 나타냅니다.|  
|**AddressZip**|주소의 우편 번호를 나타냅니다.|  
|**BomResource**|제품 구성 정보(BOM) 리소스를 나타냅니다.|  
|**캡션**|캡션을 나타냅니다.|  
|**CaptionAbbreviation**|약어를 나타냅니다.|  
|**CaptionDescription**|설명을 나타냅니다.|  
|**채널**|채널을 나타냅니다.|  
|**City**|구/군/시를 나타냅니다.|  
|**회사**|회사를 나타냅니다.|  
|**Continent**|대륙을 나타냅니다.|  
|**Country**|국가/지역을 나타냅니다.|  
|**국가**|지방을 나타냅니다.|  
|**CustomerGroup**|고객 그룹을 나타냅니다.|  
|**CustomerHousehold**|고객 가계를 나타냅니다.|  
|**고객**|고객을 나타냅니다.|  
|**DateCanceled**|취소 날짜를 나타냅니다.|  
|**DateDuration**|기간을 나타냅니다.|  
|**DateEnded**|종료 날짜를 나타냅니다.|  
|**DateModified**|수정한 날짜를 나타냅니다.|  
|**DateStart**|시작 날짜를 나타냅니다.|  
|**DeletedFlag**|(업무 기능에 따라) 멤버가 삭제되었는지 또는 삭제되어야 할지 여부를 나타냅니다.<br /><br /> 참고: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 이 특성 유형을 사용하여 멤버가 삭제되어야 할지 여부를 결정하지 않습니다. 대신에 이 특성 유형은 클라이언트 애플리케이션에서 표시하는 용도로만 사용됩니다.|  
|**FormattingColor**|서식 지정에 사용된 색을 나타냅니다.|  
|**FormattingFont**|서식 지정에 사용된 글꼴을 나타냅니다.|  
|**FormattingFontEffects**|서식 지정에 사용된 글꼴 효과를 나타냅니다.|  
|**FormattingFontSize**|서식 지정에 사용된 글꼴 크기를 나타냅니다.|  
|**FormattingOrder**|서식 지정에 사용된 순서를 나타냅니다.|  
|**FormattingSubtotal**|부분합을 나타냅니다.|  
|**GeoBoundaryBottom**|지리적 경계의 아래쪽 값을 나타냅니다.|  
|**GeoBoundaryFront**|지리적 경계의 앞쪽 값을 나타냅니다.|  
|**GeoBoundaryLeft**|지리적 경계의 왼쪽 값을 나타냅니다.|  
|**GeoBoundaryPolygon**|지리적 경계의 다각형 정의를 나타냅니다.|  
|**GeoBoundaryRear**|지리적 경계의 뒤쪽 값을 나타냅니다.|  
|**GeoBoundaryRight**|지리적 경계의 오른쪽 값을 나타냅니다.|  
|**GeoBoundaryTop**|지리적 경계의 위쪽 값을 나타냅니다.|  
|**GeoCentroidX**|지리적인 지역의 X축 중심을 나타냅니다.|  
|**GeoCentroidY**|지리적인 지역의 Y축 중심을 나타냅니다.|  
|**GeoCentroidZ**|지리적인 지역의 Z축 중심을 나타냅니다.|  
|**ID**|ID(식별자) 또는 키를 나타냅니다.|  
|**이미지**|정의되지 않은 그래픽 형식의 이미지를 나타냅니다.|  
|**ImageBmp**|비트맵 그래픽 형식의 이미지를 나타냅니다.|  
|**ImageGif**|GIF(Graphics Interchange Format) 그래픽 형식의 이미지를 나타냅니다.|  
|**ImageJpg**|JPEG(Joint Photographic Experts Group) 그래픽 형식의 이미지를 나타냅니다.|  
|**ImagePng**|PNG(Portable Network Graphics) 그래픽 형식의 이미지를 나타냅니다.|  
|**ImageTiff**|TIFF(Tagged Image File Format) 그래픽 형식의 이미지를 나타냅니다.|  
|**OrganizationalUnit**|부서를 나타냅니다.|  
|**OrgTitle**|직함을 나타냅니다.|  
|**PercentOwnership**|소유권 비율을 나타냅니다.|  
|**PercentVoteRight**|의결권 비율을 나타냅니다.|  
|**Person**|사람을 나타냅니다.|  
|**PersonContact**|사람의 연락처 정보를 나타냅니다.|  
|**PersonDemographic**|사람의 인구 통계 정보를 나타냅니다.|  
|**PersonFirstName**|사람의 이름을 나타냅니다.|  
|**PersonFullName**|사람의 전체 이름을 나타냅니다.|  
|**PersonLastName**|사람의 성을 나타냅니다.|  
|**PersonMiddleName**|사람의 중간 이름을 나타냅니다.|  
|**PhysicalColor**|색을 나타냅니다.|  
|**PhysicalDensity**|밀도를 나타냅니다.|  
|**PhysicalDepth**|깊이를 나타냅니다.|  
|**PhysicalHeight**|높이를 나타냅니다.|  
|**PhysicalSize**|크기를 나타냅니다.|  
|**PhysicalVolume**|부피를 나타냅니다.|  
|**PhysicalWeight**|무게를 나타냅니다.|  
|**PhysicalWidth**|너비를 나타냅니다.|  
|**점**|포인트를 나타냅니다.|  
|**PostalCode**|우편 번호를 나타냅니다.|  
|**Product**|제품을 나타냅니다.|  
|**ProductBrand**|제품 브랜드를 나타냅니다.|  
|**ProductCategory**|제품 범주를 나타냅니다.|  
|**ProductGroup**|제품 그룹을 나타냅니다.|  
|**ProductSKU**|제품 SKU(Stock Keeping Unit)를 나타냅니다.|  
|**프로젝트**|프로젝트를 나타냅니다.|  
|**ProjectCode**|프로젝트 코드를 나타냅니다.|  
|**ProjectCompletion**|프로젝트의 완료 상태를 나타냅니다.|  
|**ProjectEndDate**|프로젝트 종료일을 나타냅니다.|  
|**ProjectName**|프로젝트 이름을 나타냅니다.|  
|**ProjectStartDate**|프로젝트 시작일을 나타냅니다.|  
|**홍보 행사**|홍보 행사를 나타냅니다.|  
|**QtyRangeHigh**|수량 범위 상한을 나타냅니다.|  
|**QtyRangeLow**|수량 범위 하한을 나타냅니다.|  
|**정량**|정량 특성을 나타냅니다.|  
|**Rate**|요율을 나타냅니다.|  
|**RateType**|요율 유형을 나타냅니다.|  
|**Region**|사용자 정의 지역을 나타냅니다.|  
|**Regular**|일반 특성을 나타냅니다.|  
|**RelationToParent**|부모와의 관계를 나타냅니다.|  
|**Representative**|담당자를 나타냅니다.|  
|**시나리오**|시나리오를 나타냅니다.|  
|**시퀀스**|시퀀스 특성을 나타냅니다.|  
|**ShortCaption**|간단한 캡션을 나타냅니다.|  
|**StateOrProvince**|시/도를 나타냅니다.|  
|**유틸리티**|유틸리티를 나타냅니다.|  
|**버전**|버전을 나타냅니다.|  
|**WebHtml**|HTML 콘텐츠를 나타냅니다.|  
|**WebMailAlias**|전자 메일 별칭을 나타냅니다.|  
|**WebUrl**|URL 주소를 나타냅니다.|  
|**WebXmlOrXsl**|XML 또는 XSL 콘텐츠를 나타냅니다.|  
  
###  <a name="account_dimension_attribute_types"></a> Account Dimension Attribute Types  
  
|특성 유형 값|Description|  
|--------------------------|-----------------|  
|**계정**|계정 부모를 나타냅니다. 이 특성 유형은 대개 계정 차원의 부모 특성에 적용됩니다.|  
|**AccountName**|계정 이름을 나타냅니다. 이 특성 유형은 대개 계정 차원의 키 특성에 적용됩니다.|  
|**AccountNumber**|계정 번호를 나타냅니다.|  
|**AccountType**|계정 유형을 나타냅니다. 이 특성 유형은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 계정 유형 차원에 있는 계정 멤버의 집계 함수를 식별합니다.|  
  
###  <a name="currency_dimension_attribute_types"></a> 통화 차원 특성 유형  
  
|특성 유형 값|Description|  
|--------------------------|-----------------|  
|**CurrencyDestination**|통화 환율의 대상 통화를 나타냅니다. 이 특성 유형은 대개 통화 변환에서 사용하기 위해 보고 차원의 키 특성에 적용됩니다. 통화 변환에 대한 자세한 내용은 [통화 변환&#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md)을 참조하세요.|  
|**CurrencyIsoCode**|통화 ISO(International Standards Organization) 코드를 나타냅니다. 통화 변환에 대한 자세한 내용은 [통화 변환&#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md)을 참조하세요.|  
|**CurrencyName**|통화 이름을 나타냅니다. 통화 변환에 대한 자세한 내용은 [통화 변환&#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md)을 참조하세요.|  
|**CurrencySource**|통화 환율의 원본 통화를 나타냅니다. 이 특성 유형은 대개 통화 변환에서 사용하기 위해 통화 차원의 키 특성에 적용됩니다. 통화 변환에 대한 자세한 내용은 [통화 변환&#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md)을 참조하세요.|  
  
###  <a name="slowly_changing_dimension_attribute_types"></a> 느린 변경 차원 특성 유형  
  
|특성 유형 값|Description|  
|--------------------------|-----------------|  
|**ScdEndDate**|느린 변경 차원에 속한 멤버의 유효한 종료 날짜를 나타냅니다.|  
|**ScdOriginalID**|느린 변경 차원에 속한 멤버의 원래 식별자를 나타냅니다.|  
|**ScdStartDate**|느린 변경 차원에 속한 멤버의 유효한 시작 날짜를 나타냅니다.|  
|**ScdStatus**|느린 변경 차원에 속한 멤버의 유효한 상태를 나타냅니다.|  
  
###  <a name="time_dimension_attribute_types"></a> 시간 차원 특성 유형  
  
|특성 유형 값|Description|  
|--------------------------|-----------------|  
|**날짜**|날짜를 나타냅니다. 이 특성 유형은 대개 시간 차원이나 서버 시간 차원의 키 특성에 적용됩니다.|  
|**DayOfHalfYear**|반기 일자 서수를 나타냅니다.|  
|**DayOfMonth**|월간 일자 서수를 나타냅니다.|  
|**DayOfQuarter**|사분기 일자 서수를 나타냅니다.|  
|**DayOfTenDays**|10일 기준 일자 서수를 나타냅니다.|  
|**DayOfTrimester**|삼분기 일자 서수를 나타냅니다.|  
|**DayOfWeek**|요일 서수를 나타냅니다.|  
|**DayOfYear**|연간 일자 서수를 나타냅니다.|  
|**일**|날짜를 나타냅니다.|  
|**FiscalDate**|회계 달력의 일자를 나타냅니다.|  
|**FiscalDayOfHalfYear**|회계 달력의 반기 일자 서수를 나타냅니다.|  
|**FiscalDayOfMonth**|회계 달력의 월간 일자 서수를 나타냅니다.|  
|**FiscalDayOfQuarter**|회계 달력의 사분기 일자 서수를 나타냅니다.|  
|**FiscalDayOfTrimester**|회계 달력의 삼분기 일자 서수를 나타냅니다.|  
|**FiscalDayOfWeek**|회계 달력의 주간 일자 서수를 나타냅니다.|  
|**FiscalDayOfYear**|회계 달력의 연간 일자 서수를 나타냅니다.|  
|**FiscalHalfYears**|회계 달력의 반기를 나타냅니다.|  
|**FiscalHalfYearOfYear**|회계 달력의 연간 반기 서수를 나타냅니다.|  
|**FiscalMonths**|회계 달력의 월을 나타냅니다.|  
|**FiscalMonthOfHalfYear**|회계 달력의 반기 월 서수를 나타냅니다.|  
|**FiscalMonthOfQuarter**|회계 달력의 사분기 월 서수를 나타냅니다.|  
|**FiscalMonthOfTrimester**|회계 달력의 삼분기 월 서수를 나타냅니다.|  
|**FiscalMonthOfYear**|회계 달력의 연간 월 서수를 나타냅니다.|  
|**FiscalQuarters**|회계 달력의 사분기를 나타냅니다.|  
|**FiscalQuarterOfHalfYear**|회계 달력의 반기 사분기 서수를 나타냅니다.|  
|**FiscalQuarterOfYear**|회계 달력의 연간 사분기 서수를 나타냅니다.|  
|**FiscalTrimesters**|회계 달력의 삼분기를 나타냅니다.|  
|**FiscalTrimesterOfYear**|회계 달력의 연간 삼분기 서수를 나타냅니다.|  
|**FiscalWeeks**|회계 달력의 주를 나타냅니다.|  
|**FiscalWeekOfHalfYear**|회계 달력의 반기 주 서수를 나타냅니다.|  
|**FiscalWeekOfMonth**|회계 달력의 월간 주 서수를 나타냅니다.|  
|**FiscalWeekOfQuarter**|회계 달력의 사분기 주 서수를 나타냅니다.|  
|**FiscalWeekOfTrimester**|회계 달력의 삼분기 주 서수를 나타냅니다.|  
|**FiscalWeekOfYear**|회계 달력의 연간 주 서수를 나타냅니다.|  
|**FiscalYears**|회계 달력의 연도를 나타냅니다.|  
|**HalfYears**|반기를 나타냅니다.|  
|**HalfYearOfYear**|연간 반기 서수를 나타냅니다.|  
|**시간**|시간을 나타냅니다.|  
|**IsHoliday**|휴일인지 여부를 나타냅니다.|  
|**ISO8601Date**|ISO 8601 달력의 날짜를 나타냅니다.|  
|**ISO8601DayOfWeek**|ISO 8601 달력의 주간 일자 서수를 나타냅니다.|  
|**ISO8601DayOfYear**|ISO 8601 달력의 연간 일자 서수를 나타냅니다.|  
|**ISO8601Weeks**|ISO 8601 달력의 주를 나타냅니다.|  
|**ISO8601WeekOfYear**|ISO 8601 달력의 연간 주 서수를 나타냅니다.|  
|**ISO8601Years**|ISO 8601 달력의 연도를 나타냅니다.|  
|**IsPeakDay**|최고 기록일인지 여부를 나타냅니다.|  
|**IsWeekDay**|평일인지 여부를 나타냅니다.|  
|**IsWorkingDay**|영업일인지 여부를 나타냅니다.|  
|**ManufacturingDate**|제조 달력의 일자를 나타냅니다.|  
|**ManufacturingDayOfHalfYear**|제조 달력의 반기 일자 서수를 나타냅니다.|  
|**ManufacturingDayOfMonth**|제조 달력의 월간 일자 서수를 나타냅니다.|  
|**ManufacturingDayOfQuarter**|제조 달력의 사분기 일자 서수를 나타냅니다.|  
|**ManufacturingDayOfTrimester**|제조 달력의 삼분기 일자 서수를 나타냅니다.|  
|**ManufacturingDayOfWeek**|제조 달력의 주간 일자 서수를 나타냅니다.|  
|**ManufacturingDayOfYear**|제조 달력의 연간 일자 서수를 나타냅니다.|  
|**ManufacturingHalfYears**|제조 달력의 반기를 나타냅니다.|  
|**ManufacturingHalfYearOfYear**|제조 달력의 연간 반기 서수를 나타냅니다.|  
|**ManufacturingMonths**|제조 달력의 월을 나타냅니다.|  
|**ManufacturingMonthOfHalfYear**|제조 달력의 반기 월 서수를 나타냅니다.|  
|**ManufacturingMonthOfQuarter**|제조 달력의 사분기 월 서수를 나타냅니다.|  
|**ManufacturingMonthOfTrimester**|제조 달력의 삼분기 월 서수를 나타냅니다.|  
|**ManufacturingMonthOfYear**|제조 달력의 연간 월 서수를 나타냅니다.|  
|**ManufacturingQuarters**|제조 달력의 사분기를 나타냅니다.|  
|**ManufacturingQuarterOfHalfYear**|제조 달력의 반기 사분기 서수를 나타냅니다.|  
|**ManufacturingQuarterOfYear**|제조 달력의 연간 사분기 서수를 나타냅니다.|  
|**ManufacturingWeeks**|제조 달력의 주를 나타냅니다.|  
|**ManufacturingWeekOfHalfYear**|제조 달력의 반기 주 서수를 나타냅니다.|  
|**ManufacturingWeekOfMonth**|제조 달력의 월간 주 서수를 나타냅니다.|  
|**ManufacturingWeekOfQuarter**|제조 달력의 사분기 주 서수를 나타냅니다.|  
|**ManufacturingWeekOfTrimester**|제조 달력의 삼분기 주 서수를 나타냅니다.|  
|**ManufacturingWeekOfYear**|제조 달력의 연간 주 서수를 나타냅니다.|  
|**ManufacturingYears**|제조 달력의 연도를 나타냅니다.|  
|**분**|분을 나타냅니다.|  
|**Months**|월을 나타냅니다.|  
|**MonthOfHalfYear**|반기 월 서수를 나타냅니다.|  
|**MonthOfQuarter**|사분기 월 서수를 나타냅니다.|  
|**MonthOfTrimester**|삼분기 월 서수를 나타냅니다.|  
|**MonthOfYear**|연간 월 서수를 나타냅니다.|  
|**Quarters**|사분기를 나타냅니다.|  
|**QuarterOfHalfYear**|반기 사분기 서수를 나타냅니다.|  
|**QuarterOfYear**|연간 사분기 서수를 나타냅니다.|  
|**ReportingDate**|보고 달력의 일자를 나타냅니다.|  
|**ReportingDayOfHalfYear**|보고 달력의 반기 일자 서수를 나타냅니다.|  
|**ReportingDayOfMonth**|보고 달력의 월간 일자 서수를 나타냅니다.|  
|**ReportingDayOfQuarter**|보고 달력의 사분기 일자 서수를 나타냅니다.|  
|**ReportingDayOfTrimester**|보고 달력의 삼분기 일자 서수를 나타냅니다.|  
|**ReportingDayOfWeek**|보고 달력의 주간 일자 서수를 나타냅니다.|  
|**ReportingDayOfYear**|보고 달력의 연간 일자 서수를 나타냅니다.|  
|**ReportingHalfYears**|보고 달력의 반기를 나타냅니다.|  
|**ReportingHalfYearOfYear**|보고 달력의 연간 반기 서수를 나타냅니다.|  
|**ReportingMonths**|보고 달력의 월을 나타냅니다.|  
|**ReportingMonthOfHalfYear**|보고 달력의 반기 월 서수를 나타냅니다.|  
|**ReportingMonthOfQuarter**|보고 달력의 사분기 월 서수를 나타냅니다.|  
|**ReportingMonthOfTrimester**|보고 달력의 삼분기 월 서수를 나타냅니다.|  
|**ReportingMonthOfYear**|보고 달력의 연간 월 서수를 나타냅니다.|  
|**ReportingQuarters**|보고 달력의 사분기를 나타냅니다.|  
|**ReportingQuarterOfHalfYear**|보고 달력의 반기 사분기 서수를 나타냅니다.|  
|**ReportingQuarterOfYear**|보고 달력의 연간 사분기 서수를 나타냅니다.|  
|**ReportingTrimesters**|보고 달력의 삼분기를 나타냅니다.|  
|**ReportingTrimesterOfYear**|보고 달력의 연간 삼분기 서수를 나타냅니다.|  
|**ReportingWeeks**|보고 달력의 주를 나타냅니다.|  
|**ReportingWeekOfHalfYear**|보고 달력의 반기 주 서수를 나타냅니다.|  
|**ReportingWeekOfMonth**|보고 달력의 월간 주 서수를 나타냅니다.|  
|**ReportingWeekOfQuarter**|보고 달력의 사분기 주 서수를 나타냅니다.|  
|**ReportingWeekOfTrimester**|보고 달력의 삼분기 주 서수를 나타냅니다.|  
|**ReportingWeekOfYear**|보고 달력의 연간 주 서수를 나타냅니다.|  
|**ReportingYears**|보고 달력의 연도를 나타냅니다.|  
|**초**|초를 나타냅니다.|  
|**TenDayOfHalfYear**|반기 10일 서수를 나타냅니다.|  
|**TenDayOfMonth**|월간 10일 서수를 나타냅니다.|  
|**TenDayOfQuarter**|사분기 10일 서수를 나타냅니다.|  
|**TenDayOfTrimester**|삼분기 10일 서수를 나타냅니다.|  
|**TenDayOfYear**|연간 10일 서수를 나타냅니다.|  
|**TenDays**|10일을 나타냅니다.|  
|**Trimesters**|삼분기를 나타냅니다.|  
|**TrimesterOfYear**|연간 삼분기 서수를 나타냅니다.|  
|**UndefinedTime**|정의되지 않은 시간을 나타냅니다.|  
|**WeekOfYear**|연간 주 서수를 나타냅니다.|  
|**Weeks**|주를 나타냅니다.|  
|**WinterSummerSeason**|겨울철/여름철에 속한 날인지 여부를 나타냅니다.|  
|**Years**|연도를 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [특성 및 특성 계층](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [차원 특성 속성 참조](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
