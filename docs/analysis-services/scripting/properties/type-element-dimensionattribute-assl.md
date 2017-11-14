---
title: "요소 (DimensionAttribute) (ASSL)를 입력 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Type Element (DimensionAttribute)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 64fce1f5-39b7-4d0a-ae60-21203a03bd0d
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cd1ed987305726ea9e08eb507e2a1451d99e525b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="type-element-dimensionattribute-assl"></a>Type 요소(DimensionAttribute)(ASSL)
  특성의 유형을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute>  
      ...  
   <Type>...</Type>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*일반*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*계정*|계정 이름을 나타내는 특성입니다.|  
|*AccountNumber*|계정 번호를 나타내는 특성입니다.|  
|*AccountType*|계정 유형을 나타내는 특성입니다.|  
|*주소*|주소를 나타내는 특성입니다.|  
|*AddressBuilding*|주소의 건물 식별자를 나타내는 특성입니다.|  
|*AddressCity*|주소의 구/군/시를 나타내는 특성입니다.|  
|*AddressCountry*|주소의 국가/지역을 나타내는 특성입니다.|  
|*AddressFax*|팩스 번호를 나타내는 특성입니다.|  
|*AddressFloor*|주소의 층 식별자를 나타내는 특성입니다.|  
|*AddressHouse*|주소의 집 호수를 나타내는 특성입니다.|  
|*AddressPhone*|전화 번호를 나타내는 특성입니다.|  
|*AddressQuarter*|주소의 구역을 나타내는 특성입니다.|  
|*AddressRoom*|주소의 방 식별자를 나타내는 특성입니다.|  
|*AddressStateOrProvince*|주소의 시/도를 나타내는 특성입니다.|  
|*AddressStreet*|주소의 번지를 나타내는 특성입니다.|  
|*AddressZip*|주소의 우편 번호를 나타내는 특성입니다.|  
|*BOMResource*|제품 구성 정보(BOM) 리소스를 나타내는 특성입니다.|  
|*캡션*|캡션을 나타내는 특성입니다.|  
|*CaptionAbbreviation*|약어를 나타내는 특성입니다.|  
|*CaptionDescription*|설명을 나타내는 특성입니다.|  
|*채널*|채널을 나타내는 특성입니다.|  
|*도시*|구/군/시를 나타내는 특성입니다.|  
|*회사*|회사를 나타내는 특성입니다.|  
|*대륙*|대륙을 나타내는 특성입니다.|  
|*국가*|국가/지역을 나타내는 특성입니다.|  
|*County*|지방을 나타내는 특성입니다.|  
|*CurrencyDestination*|통화 환율의 대상 통화를 나타내는 특성입니다.|  
|*CurrencyISOcode*|통화 ISO 코드를 나타내는 특성입니다.|  
|*CurrencName*|통화 이름을 나타내는 특성입니다.|  
|*CurrencySource*|통화 환율의 원본 통화를 나타내는 특성입니다.|  
|*CustomerGroup*|고객 그룹을 나타내는 특성입니다.|  
|*CustomerHousehold*|고객의 가족을 나타내는 특성입니다.|  
|*고객*|고객을 나타내는 특성입니다.|  
|*날짜*|날짜를 나타내는 특성입니다.|  
|*DateCanceled*|취소 날짜를 나타내는 특성입니다.|  
|*DateDuration*|기간을 나타내는 특성입니다.|  
|*DateEnded*|종료 날짜를 나타내는 특성입니다.|  
|*DateModified*|수정한 날짜를 나타내는 특성입니다.|  
|*DateStart*|시작 날짜를 나타내는 특성입니다.|  
|*DayOfHalfYears*|반기 일자 서수를 나타내는 특성입니다.|  
|*DayOfMonth*|월간 일자 서수를 나타내는 특성입니다.|  
|*DayOfQuarter*|사분기 일자 서수를 나타내는 특성입니다.|  
|*DayOfTrimester*|삼분기 일자 서수를 나타내는 특성입니다.|  
|*DayOfWeek*|요일 서수를 나타내는 특성입니다.|  
|*DayOfYear*|연간 일자 서수를 나타내는 특성입니다.|  
|*(일)*|날짜를 나타내는 특성입니다.|  
|*DaysOfTenDays*|10일 기준 일자 서수를 나타내는 특성입니다.|  
|*FiscalDay*|회계 달력의 일자를 나타내는 특성입니다.|  
|*FiscalDayOfHalfYears*|회계 달력의 반기 일자 서수를 나타내는 특성입니다.|  
|*FiscalDayOfMonth*|회계 달력의 월간 일자 서수를 나타내는 특성입니다.|  
|*FiscalDayOfQuarter*|회계 달력의 사분기 일자 서수를 나타내는 특성입니다.|  
|*FiscalDayOfTrimester*|회계 달력의 삼분기 일자 서수를 나타내는 특성입니다.|  
|*FiscalDayOfWeek*|회계 달력의 주간 일자 서수를 나타내는 특성입니다.|  
|*FiscalDayOfYear*|회계 달력의 연간 일자 서수를 나타내는 특성입니다.|  
|*FiscalHalfYears*|회계 달력의 반기를 나타내는 특성입니다.|  
|*FiscalHalfYearsOfYear*|회계 달력의 연간 반기 서수를 나타내는 특성입니다.|  
|*회계 월*|회계 달력의 월을 나타내는 특성입니다.|  
|*FiscalMonthOfHalfYears*|회계 달력의 반기 월 서수를 나타내는 특성입니다.|  
|*FiscalMonthOfQuarter*|회계 달력의 사분기 월 서수를 나타내는 특성입니다.|  
|*FiscalMonthOfTrimester*|회계 달력의 삼분기 월 서수를 나타내는 특성입니다.|  
|*FiscalMonthOfYear*|회계 달력의 연간 월 서수를 나타내는 특성입니다.|  
|*FiscalQuarter*|회계 달력의 사분기를 나타내는 특성입니다.|  
|*FiscalQuarterOfHalfYear*|회계 달력의 반기 사분기 서수를 나타내는 특성입니다.|  
|*FiscalQuarterOfYear*|회계 달력의 연간 사분기 서수를 나타내는 특성입니다.|  
|*FiscalTrimester*|회계 달력의 삼분기를 나타내는 특성입니다.|  
|*FiscalTrimesterOfYear*|회계 달력의 연간 삼분기 서수를 나타내는 특성입니다.|  
|*FiscalWeek*|회계 달력의 주를 나타내는 특성입니다.|  
|*FiscalWeekOfHalfYears*|회계 달력의 반기 주 서수를 나타내는 특성입니다.|  
|*FiscalWeekOfMonth*|회계 달력의 월간 주 서수를 나타내는 특성입니다.|  
|*FiscalWeekOfQuarter*|회계 달력의 사분기 주 서수를 나타내는 특성입니다.|  
|*FiscalWeekOfTrimester*|회계 달력의 삼분기 주 서수를 나타내는 특성입니다.|  
|*FiscalWeekOfYear*|회계 달력의 연간 주 서수를 나타내는 특성입니다.|  
|*FiscalYear*|회계 달력의 연도를 나타내는 특성입니다.|  
|*FormattingColor*|서식 지정에 사용된 색을 나타내는 특성입니다.|  
|*FormattingFont*|서식 지정에 사용된 글꼴을 나타내는 특성입니다.|  
|*FormattingFontEffects*|서식 지정에 사용된 글꼴 효과를 나타내는 특성입니다.|  
|*FormattingFontSize*|서식 지정에 사용된 글꼴 크기를 나타내는 특성입니다.|  
|*FormattingOrder*|서식 지정에 사용된 순서를 나타내는 특성입니다.|  
|*FormattingSubtotal*|부분합을 나타내는 특성입니다.|  
|*GeoBoundaryBottom*|지리적 경계의 아래쪽 값을 나타내는 특성입니다.|  
|*GeoBoundaryFront*|지리적 경계의 앞쪽 값을 나타내는 특성입니다.|  
|*GeoBoundaryLeft*|지리적 경계의 왼쪽 값을 나타내는 특성입니다.|  
|*GeoBoundaryPolygon*|지리적 경계의 다각형 정의를 나타내는 특성입니다.|  
|*GeoBoundaryRear*|지리적 경계의 뒤쪽 값을 나타내는 특성입니다.|  
|*GeoBoundaryRight*|지리적 경계의 오른쪽 값을 나타내는 특성입니다.|  
|*GeoBoundaryTop*|지리적 경계의 위쪽 값을 나타내는 특성입니다.|  
|*GeoCentroidX*|지리적인 지역의 X축 중심을 나타내는 특성입니다.|  
|*GeoCentroidY*|지리적인 지역의 Y축 중심을 나타내는 특성입니다.|  
|*GeoCentroidZ*|지리적인 지역의 Z축 중심을 나타내는 특성입니다.|  
|*HalfYears*|반기를 나타내는 특성입니다.|  
|*HalfYearsOfYear*|연간 반기 서수를 나타내는 특성입니다.|  
|*시간*|시간을 나타내는 특성입니다.|  
|*Id*|ID 또는 키를 나타내는 특성입니다.|  
|*IsHoliday*|휴일인지 여부를 나타내는 특성입니다.|  
|*ISO8601DayOfWeek*|ISO 8601 달력의 주간 일자 서수를 나타내는 특성입니다.|  
|*ISO8601DayOfYear*|ISO 8601 달력의 연간 일자 서수를 나타내는 특성입니다.|  
|*ISO8601Days*|ISO 8601 달력의 일자를 나타내는 특성입니다.|  
|*ISO8601Week*|ISO 8601 달력의 주를 나타내는 특성입니다.|  
|*ISO8601WeekOfYear*|ISO 8601 달력의 연간 주 서수를 나타내는 특성입니다.|  
|*ISO8601Year*|ISO 8601 달력의 연도를 나타내는 특성입니다.|  
|*IsWeekDay*|평일인지 여부를 나타내는 특성입니다.|  
|*IsWorkingDay*|영업일인지 여부를 나타내는 특성입니다.|  
|*ManufacturingDay*|제조 달력의 일자를 나타내는 특성입니다.|  
|*ManufacturingDayOfHalfYears*|제조 달력의 반기 일자 서수를 나타내는 특성입니다.|  
|*ManufacturingDayOfMonth*|제조 달력의 월간 일자 서수를 나타내는 특성입니다.|  
|*ManufacturingDayOfQuarter*|제조 달력의 사분기 일자 서수를 나타내는 특성입니다.|  
|*ManufacturingDayOfTrimester*|제조 달력의 삼분기 일자 서수를 나타내는 특성입니다.|  
|*ManufacturingDayOfWeek*|제조 달력의 주간 일자 서수를 나타내는 특성입니다.|  
|*ManufacturingDayOfYear*|제조 달력의 연간 일자 서수를 나타내는 특성입니다.|  
|*ManufacturingHalfYears*|제조 달력의 반기를 나타내는 특성입니다.|  
|*ManufacturingHalfYearsOfYear*|제조 달력의 연간 반기 서수를 나타내는 특성입니다.|  
|*ManufacturingMonth*|제조 달력의 월을 나타내는 특성입니다.|  
|*ManufacturingMonthOfHalfYears*|제조 달력의 반기 월 서수를 나타내는 특성입니다.|  
|*ManufacturingMonthOfQuarter*|제조 달력의 사분기 월 서수를 나타내는 특성입니다.|  
|*ManufacturingMonthOfTrimester*|제조 달력의 삼분기 월 서수를 나타내는 특성입니다.|  
|*ManufacturingMonthOfYear*|제조 달력의 연간 월 서수를 나타내는 특성입니다.|  
|*ManufacturingQuarter*|제조 달력의 사분기를 나타내는 특성입니다.|  
|*ManufacturingQuarterOfHalfYear*|제조 달력의 반기 사분기 서수를 나타내는 특성입니다.|  
|*ManufacturingQuarterOfYear*|제조 달력의 연간 사분기 서수를 나타내는 특성입니다.|  
|*ManufacturingTrimester*|제조 달력의 삼분기를 나타내는 특성입니다.|  
|*ManufacturingTrimesterOfYear*|제조 달력의 연간 삼분기 서수를 나타내는 특성입니다.|  
|*ManufacturingWeek*|제조 달력의 주를 나타내는 특성입니다.|  
|*ManufacturingWeekOfHalfYears*|제조 달력의 반기 주 서수를 나타내는 특성입니다.|  
|*ManufacturingWeekOfMonth*|제조 달력의 월간 주 서수를 나타내는 특성입니다.|  
|*ManufacturingWeekOfQuarter*|제조 달력의 사분기 주 서수를 나타내는 특성입니다.|  
|*ManufacturingWeekOfTrimester*|제조 달력의 삼분기 주 서수를 나타내는 특성입니다.|  
|*ManufacturingWeekOfYear*|제조 달력의 연간 주 서수를 나타내는 특성입니다.|  
|*ManufacturingYear*|제조 달력의 연도를 나타내는 특성입니다.|  
|*분*|분을 나타내는 특성입니다.|  
|*MonthOfHalfYears*|반기 월 서수를 나타내는 특성입니다.|  
|*MonthOfQuarter*|사분기 월 서수를 나타내는 특성입니다.|  
|*MonthOfTrimester*|삼분기 월 서수를 나타내는 특성입니다.|  
|*MonthOfYear*|연간 월 서수를 나타내는 특성입니다.|  
|*월*|월을 나타내는 특성입니다.|  
|*조직 구성 단위*|부서를 나타내는 특성입니다.|  
|*OrgTitle*|직함을 나타내는 특성입니다.|  
|*PercentOwnership*|소유권 비율을 나타내는 특성입니다.|  
|*PercentVoteRight*|의결권 비율을 나타내는 특성입니다.|  
|*사람*|사람을 나타내는 특성입니다.|  
|*PersonContact*|사람의 연락처 정보를 나타내는 특성입니다.|  
|*PersonDemographic*|사람의 인구 통계 정보를 나타내는 특성입니다.|  
|*PersonFirstName*|사람의 이름을 나타내는 특성입니다.|  
|*PersonFullName*|사람의 전체 이름을 나타내는 특성입니다.|  
|*PersonLastName*|사람의 성을 나타내는 특성입니다.|  
|*PersonMiddleName*|사람의 중간 이름을 나타내는 특성입니다.|  
|*PhysicalColor*|색을 나타내는 특성입니다.|  
|*PhysicalDensity*|밀도를 나타내는 특성입니다.|  
|*PhysicalDepth*|깊이를 나타내는 특성입니다.|  
|*PhysicalHeight*|높이를 나타내는 특성입니다.|  
|*PhysicalSize*|크기를 나타내는 특성입니다.|  
|*PhysicalVolume*|부피를 나타내는 특성입니다.|  
|*PhysicalWeight*|무게를 나타내는 특성입니다.|  
|*PhysicalWidth*|너비를 나타내는 특성입니다.|  
|*Point*|포인트를 나타내는 특성입니다.|  
|*PostalCode*|우편 번호를 나타내는 특성입니다.|  
|*Product*|제품을 나타내는 특성입니다.|  
|*ProductBrand*|제품 브랜드를 나타내는 특성입니다.|  
|*ProductCategory*|제품 범주를 나타내는 특성입니다.|  
|*ProductGroup*|제품 그룹을 나타내는 특성입니다.|  
|*ProductSKU*|제품 SKU(Stock Keeping Unit)를 나타내는 특성입니다.|  
|*ProjectCode*|프로젝트 코드를 나타내는 특성입니다.|  
|*Projectcompletion*|프로젝트의 완료 상태를 나타내는 특성입니다.|  
|*ProjectEnddate*|프로젝트 종료일을 나타내는 특성입니다.|  
|*프로젝트 이름*|프로젝트 이름을 나타내는 특성입니다.|  
|*ProjectStartDate*|프로젝트 시작일을 나타내는 특성입니다.|  
|*프로 모션*|홍보 행사를 나타내는 특성입니다.|  
|*QtyRangeHigh*|수량 범위 상한을 나타내는 특성입니다.|  
|*QtyRangeLow*|수량 범위 하한을 나타내는 특성입니다.|  
|*정량*|정량 특성을 나타내는 특성입니다.|  
|*QuarterOfHalfYear*|반기 사분기 서수를 나타내는 특성입니다.|  
|*QuarterOfYear*|연간 사분기 서수를 나타내는 특성입니다.|  
|*분기*|사분기를 나타내는 특성입니다.|  
|*속도*|요율을 나타내는 특성입니다.|  
|*RateType*|요율 유형을 나타내는 특성입니다.|  
|*Region*|사용자 정의 지역을 나타내는 특성입니다.|  
|*일반*|일반 특성을 나타내는 특성입니다.|  
|*RelationToParent*|부모와의 관계를 나타내는 특성입니다.|  
|*ReportingDay*|보고 달력의 일자를 나타내는 특성입니다.|  
|*ReportingDayOfHalfYears*|보고 달력의 반기 일자 서수를 나타내는 특성입니다.|  
|*ReportingDayOfMonth*|보고 달력의 월간 일자 서수를 나타내는 특성입니다.|  
|*ReportingDayOfQuarter*|보고 달력의 사분기 일자 서수를 나타내는 특성입니다.|  
|*ReportingDayOfTrimester*|보고 달력의 삼분기 일자 서수를 나타내는 특성입니다.|  
|*ReportingDayOfWeek*|보고 달력의 주간 일자 서수를 나타내는 특성입니다.|  
|*ReportingDayOfYear*|보고 달력의 연간 일자 서수를 나타내는 특성입니다.|  
|*ReportingHalfYears*|보고 달력의 반기를 나타내는 특성입니다.|  
|*ReportingHalfYearsOfYear*|보고 달력의 연간 반기 서수를 나타내는 특성입니다.|  
|*ReportingMonth*|보고 달력의 월을 나타내는 특성입니다.|  
|*ReportingMonthOfHalfYears*|보고 달력의 반기 월 서수를 나타내는 특성입니다.|  
|*ReportingMonthOfQuarter*|보고 달력의 사분기 월 서수를 나타내는 특성입니다.|  
|*ReportingMonthOfTrimester*|보고 달력의 삼분기 월 서수를 나타내는 특성입니다.|  
|*ReportingMonthOfYear*|보고 달력의 연간 월 서수를 나타내는 특성입니다.|  
|*ReportingQuarter*|보고 달력의 사분기를 나타내는 특성입니다.|  
|*ReportingQuarterOfHalfYear*|보고 달력의 반기 사분기 서수를 나타내는 특성입니다.|  
|*ReportingQuarterOfYear*|보고 달력의 연간 사분기 서수를 나타내는 특성입니다.|  
|*ReportingTrimester*|보고 달력의 삼분기를 나타내는 특성입니다.|  
|*ReportingTrimesterOfYear*|보고 달력의 연간 삼분기 서수를 나타내는 특성입니다.|  
|*ReportingWeek*|보고 달력의 주를 나타내는 특성입니다.|  
|*ReportingWeekOfHalfYears*|보고 달력의 반기 주 서수를 나타내는 특성입니다.|  
|*ReportingWeekOfMonth*|보고 달력의 월간 주 서수를 나타내는 특성입니다.|  
|*ReportingWeekOfQuarter*|보고 달력의 사분기 주 서수를 나타내는 특성입니다.|  
|*ReportingWeekOfTrimester*|보고 달력의 삼분기 주 서수를 나타내는 특성입니다.|  
|*ReportingWeekOfYear*|보고 달력의 연간 주 서수를 나타내는 특성입니다.|  
|*ReportingYear*|보고 달력의 연도를 나타내는 특성입니다.|  
|*담당자*|담당자를 나타내는 특성입니다.|  
|*시나리오*|시나리오를 나타내는 특성입니다.|  
|*초*|초를 나타내는 특성입니다.|  
|*시퀀스*|시퀀스 특성을 나타내는 특성입니다.|  
|*ShortCaption*|간단한 캡션을 나타내는 특성입니다.|  
|*StateOrProvince*|시/도를 나타내는 특성입니다.|  
|*TenDayOfHalfYears*|반기 10일 서수를 나타내는 특성입니다.|  
|*TenDayOfQuarter*|사분기 10일 서수를 나타내는 특성입니다.|  
|*TenDayOfTrimester*|삼분기 10일 서수를 나타내는 특성입니다.|  
|*TenDayOfYear*|연간 10일 서수를 나타내는 특성입니다.|  
|*TenDays*|10일을 나타내는 특성입니다.|  
|*TenDaysOfMonth*|월간 10일 서수를 나타내는 특성입니다.|  
|*삼분기*|삼분기를 나타내는 특성입니다.|  
|*TrimesterOfYear*|연간 삼분기 서수를 나타내는 특성입니다.|  
|*UndefinedTime*|정의되지 않은 시간을 나타내는 특성입니다.|  
|*유틸리티*|유틸리티를 나타내는 특성입니다.|  
|*버전*|버전을 나타내는 특성입니다.|  
|*WebHtml*|HTML 콘텐츠를 나타내는 특성입니다.|  
|*WebMailAlias*|전자 메일 별칭을 나타내는 특성입니다.|  
|*WebUrl*|URL 주소를 나타내는 특성입니다.|  
|*WebXmlOrXsl*|XML 또는 XSL 콘텐츠를 나타내는 특성입니다.|  
|*WeekOfHalfYears*|반기 주 서수를 나타내는 특성입니다.|  
|*WeekOfMonth*|월간 주 서수를 나타내는 특성입니다.|  
|*WeekOfQuarter*|사분기 주 서수를 나타내는 특성입니다.|  
|*WeekOfTrimester*|삼분기 주 서수를 나타내는 특성입니다.|  
|*WeekOfYear*|연간 주 서수를 나타내는 특성입니다.|  
|*주*|주를 나타내는 특성입니다.|  
|*년*|연도를 나타내는 특성입니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AttributeType>합니다.  
  
 부모에 해당 하는 요소 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DimensionAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Attributes 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)   
 [Dimension 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

