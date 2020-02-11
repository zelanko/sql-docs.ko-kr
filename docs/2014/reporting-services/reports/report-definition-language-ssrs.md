---
title: SSRS(보고서 정의 언어) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Reporting Services, RDL
- Reporting Services, RDL
- RDL [Reporting Services], about Report Definition Language
- SSRS, RDL
- Report Definition Language, about Report Definition Language
- Report Definition Language
- RDL [Reporting Services]
- reports [Reporting Services], definitions
ms.assetid: b18b025e-f4bd-4744-8f86-0ac9fb967548
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6480a8cefee9b71149c61bf952896a739526cf55
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102502"
---
# <a name="report-definition-language-ssrs"></a>SSRS(Report Definition Language)
  RDL (report definition Language)은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 정의의 XML 표현입니다. 보고서 정의에는 보고서에 대한 데이터 검색 및 레이아웃 정보가 포함됩니다. RDL은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]용으로 만들어진 XML 문법과 일치하는 XML 요소로 구성됩니다. 보고서 정의 파일 내에서 코드 어셈블리에 액세스하여 보고서 항목 값, 스타일, 서식 등을 제어하는 사용자 지정 함수를 추가할 수 있습니다.  
  
 RDL은 보고 정의 교환을 가능하게 하는 공용 스키마를 정의하여 상업 보고용 제품의 상호 운용성을 높입니다. XML로 작업하는 프로토콜 또는 프로그래밍 인터페이스를 RDL과 함께 사용할 수 있습니다. RDL은 다음과 같습니다.  
  
-   보고서 정의를 위한 XML 스키마  
  
-   기업과 타사 간의 교환 형식  
  
-   추가 네임스페이스 및 사용자 지정 요소를 지원하는 개방형의 확장 가능한 스키마  
  
##  <a name="bkmk_RDL_Specifications"></a>RDL 사양  
 특정 스키마 버전에 대한 사양을 다운로드하려면 [Report Definition Language 사양(Report Definition Language Specification)](https://go.microsoft.com/fwlink/?linkid=116865)을 참조하십시오.  
  
##  <a name="bkmk_RDL_XML_Schema_Definition"></a>RDL XML 스키마 정의  
 RDL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (Report definition Language) 파일은 XSD (XML 스키마 정의) 파일을 사용 하 여 유효성을 검사 합니다. 스키마는 .rdl 파일에 RDL 요소의 발생 규칙을 정의합니다. 요소는 데이터 형식과 카디널리티, 즉 허용되는 발생 횟수를 포함합니다. 요소에는 단순 요소와 복합 요소가 있습니다. 단순 요소에는 자식 요소 또는 특성이 없습니다. 복합 요소에는 자식이 있고 선택적으로 특성도 보유합니다.  
  
 예를 들어 스키마가 복합 유형 `ReportParameters`인 RDL 요소 `ReportParametersType`를 포함합니다. 규칙에 따라 요소의 복합 유형 이름은 요소 이름 뒤에 `Type`이라는 단어를 붙여 만듭니다. 
  `ReportParameters` 요소는 `Report` 요소(복합 유형)에 포함될 수 있고, `ReportParameter` 요소를 포함할 수 있습니다. 
  `ReportParameterType`은 단순 유형으로 값은 `Boolean`, `DateTime`, `Integer`, `Float` 또는 `String` 중 하나와 같을 수 있습니다. XML 스키마 데이터 형식에 대한 자세한 내용은 [XML 스키마 2부: Datatypes Second Edition](https://go.microsoft.com/fwlink/?linkid=4871)을 참조하세요.  
  
 RDL XSD는 제품 CD-ROM의 Extras 폴더에 있는 ReportDefinition.xsd 파일에서 사용할 수 있습니다. 다음 URL을 통해 보고서 서버에서도 사용할 수 있습니다.http://servername/reportserver/reportdefinition.xsd  
  
##  <a name="bkmk_Creating_RDL"></a>RDL 만들기  
 개방형이고 확장 가능한 RDL의 특성 덕분에 XML 스키마를 기반으로 RDL을 생성하는 다양한 도구와 애플리케이션을 작성할 수 있습니다.  
  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 RDL 파일을 빌드하는 여러 도구를 제공합니다. 자세한 내용은 [Reporting Services 도구](../tools/reporting-services-tools.md)를 참조하세요.  
  
 응용 프로그램에서 RDL을 생성 하는 가장 쉬운 방법 중 하나는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] <xref:System.Xml> 네임 스페이스 및 <xref:System.Linq> 네임 스페이스의 클래스를 사용 하는 것입니다. 특히 **XmlTextWriter** 클래스는 RDL을 쓰는 데 사용할 수 있습니다. 
  **XmlTextWriter**를 사용하여 전체 보고서 정의를 처음부터 생성하여 임의의 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 애플리케이션에서 완료할 수 있습니다. 개발자는 또한 사용자 지정 속성이 포함된 사용자 지정 보고서 항목을 추가하여 RDL을 확장할 수도 있습니다. 
  **XmlTextWriter** 클래스 및 <xref:System.Xml> 네임스페이스에 대한 자세한 내용은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 개발자 가이드를 참조하세요. LINQ(Language-Integrated Query)에 대한 자세한 내용은 MSDN에서 "LINQ to XML"을 참조하십시오.  
  
 보고서 정의 파일의 표준 파일 확장명은 .rdl입니다. 확장명이 .rdlc인 클라이언트 보고서 정의 파일을 개발할 수도 있습니다. 두 확장명 모두 MIME 형식은 텍스트/xml입니다. 보고서에 대한 자세한 내용은 [Reporting Services 보고서&#40;SSRS&#41;](reporting-services-reports-ssrs.md)를 참조하세요.  
  
##  <a name="bkmk_RDL_Types"></a>RDL 형식  
 다음 표에서는 RDL 요소 및 특성에 사용되는 유형을 보여 줍니다.  
  
|Type|Description|  
|----------|-----------------|  
|`Binary`|Base-64로 인코딩된 이진 값을 갖는 속성입니다.|  
|`Boolean`|개체 값으로 `true` 또는 `false`를 갖는 속성입니다. 다르게 지정되지 않는 이상 생략된 선택적 Boolean 개체의 값은 `False`입니다.|  
|`Date`|완전히 지정된 날짜 또는 ISO8601 날짜 형식(YYYY-MM-DD[THH:MM[:SS[.S]]])으로 지정된 날짜/시간 값을 갖는 속성입니다.|  
|`Enum`|지정된 값 목록의 하나인 문자열 텍스트 값을 갖는 속성입니다.|  
|`Float`|float 값을 갖는 속성입니다. 마침표(.)를 선택적 소수 구분 기호로 사용합니다.|  
|`Integer`|정수(int32) 값을 갖는 속성입니다.|  
|`Language`|미국 영어의 경우 "en-us"와 같이 언어 및 culture 코드가 포함된 텍스트 값을 갖는 속성입니다. 값은 기본 언어가에 정의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]된 중립 언어 또는 특정 언어 여야 합니다.|  
|`Name`|문자열 텍스트 값을 갖는 속성입니다. 이름은 항목의 네임스페이스 내에서 고유해야 합니다. 지정하지 않을 경우 항목의 네임스페이스는 가장 안쪽에 위치하고 있으며 이름이 있는 포함하는 개체입니다.|  
|`NormalizedString`|일반화된 문자열 텍스트 값을 갖는 속성입니다.|  
|`Size`|크기 요소는 숫자를 포함해야 합니다(마침표 문자가 선택적 소수 구분 기호로 사용됨). 숫자 다음에는 cm, mm, in, pt, pc와 같은 CSS 길이 단위 지정자가 와야 합니다. 숫자와 지정자 사이의 공백은 선택적입니다. 크기 지정자에 대한 자세한 내용은 [CSS 길이 단위 참조(CSS Length Units Reference)](https://www.w3schools.com/CSSref/css_units.asp)를 참조하십시오.<br /><br /> RDL에서 `Size`의 최대값은 160인치이고 최소 크기는 0인치입니다.|  
|`String`|문자열 텍스트 값을 갖는 속성입니다.|  
|`UnsignedInt`|서명되지 않은 정수(int32) 값을 갖는 속성입니다.|  
|`Variant`|단순 XML 유형을 갖는 속성입니다.|  
  
##  <a name="bkmk_RDL_Data_Types"></a>RDL 데이터 형식  
 DataType 열거형은 특성, 식 또는 매개 변수의 데이터 형식을 RDL로 정의합니다. 다음 표에서는 CLR(공용 언어 런타임) 데이터 형식과 RDL 데이터 형식의 관련을 보여 줍니다.  
  
|**CLR 형식**|**해당 데이터 형식**|  
|-----------------------|---------------------------------|  
|부울|부울|  
|DateTime, DateTimeOffset|DateTime|  
|Int16, Int32, UInt16, Byte, SByte|정수|  
|Single, Double|Float|  
|String, Char, GUID, Timespan|String|  
  
## <a name="see-also"></a>참고 항목  
 [SSRS&#41;&#40;보고서 정의 스키마 버전을 찾습니다.](find-the-report-definition-schema-version-ssrs.md)   
 [보고서에서 사용자 지정 어셈블리 사용](../custom-assemblies/using-custom-assemblies-with-reports.md)   
 [사용자 지정 보고서 항목](../custom-report-items/custom-report-items.md)  
  
  
