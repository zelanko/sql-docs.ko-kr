---
title: XML로 내보내기(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 11d72068-2d97-495e-948f-12d1e8c1957d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1e8966ddbecc88b5bcf6d2a5024f0dd2228b4fc2
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56286791"
---
# <a name="exporting-to-xml-report-builder-and-ssrs"></a>XML로 내보내기(보고서 작성기 및 SSRS)
  XML 렌더링 확장 프로그램은 페이지가 매겨진 보고서를 XML 형식으로 반환합니다. 보고서의 XML 스키마는 보고서마다 고유하며 데이터만 포함합니다. 레이아웃 정보는 렌더링되지 않으며 페이지 번호는 XML 렌더링 확장 프로그램을 통해 유지되지 않습니다. 이 확장 프로그램에서 생성된 XML은 데이터베이스로 가져오거나 XML 데이터 메시지로 사용하거나 사용자 지정 애플리케이션으로 전송할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ReportItems"></a> 보고서 항목  
 다음 표는 보고서 항목을 렌더링하는 방법을 설명합니다.  
  
|항목|렌더링 동작|  
|----------|------------------------|  
|보고서|XML 문서의 최상위 요소로 렌더링합니다.|  
|데이터 영역|해당 컨테이너 요소 내의 요소로 렌더링합니다. 데이터 영역에는 데이터를 텍스트와 차트, 데이터 막대, 스파크라인, 계기 및 데이터를 시각화하는 표시기로 표시하는 목록, 테이블 및 행렬이 있습니다.|  
|그룹 및 세부 정보 섹션|각 인스턴스를 해당 컨테이너 요소 내의 요소로 렌더링합니다.|  
|입력란|해당 컨테이너 내의 특성 또는 요소로 렌더링합니다.|  
|직사각형|해당 컨테이너 내의 요소로 렌더링합니다.|  
|행렬 열 그룹|행 그룹 내의 요소로 렌더링합니다.|  
|지도|해당 컨테이너 요소 내의 요소로 렌더링합니다. 지도 계층은 지도의 자식 요소이며 각 지도 계층에는 지도 멤버 및 지도 멤버 특성의 요소가 포함되어 있습니다.|  
|차트|해당 컨테이너 요소 내의 요소로 렌더링합니다. 계열은 차트의 자식 요소이며 범주는 계열의 자식 요소입니다. 각 차트 값에 대한 모든 차트 레이블을 렌더링합니다. 레이블과 값은 특성으로 포함됩니다.|  
|데이터 막대|차트와 마찬가지로 해당 컨테이너 요소 내의 요소로 렌더링합니다. 일반적으로 데이터 막대에는 계층이나 레이블이 포함되지 않고 값만 포함됩니다.|  
|스파크라인|차트와 마찬가지로 해당 컨테이너 요소 내의 요소로 렌더링합니다. 일반적으로 스파크라인에는 계층이나 레이블이 포함되지 않고 값만 포함됩니다.|  
|계기|해당 컨테이너 요소 내의 요소로 렌더링합니다. 눈금의 최소값과 최대값, 범위의 시작 값과 끝 값, 포인터의 값을 특성으로 사용하여 단일 요소로 렌더링합니다.|  
|표시기|계기와 마찬가지로 해당 컨테이너 요소 내의 요소로 렌더링합니다. 활성 상태 이름, 사용 가능한 상태 및 데이터 값을 특성으로 사용하여 단일 요소로 렌더링합니다.|  
  
 XML 렌더링 확장 프로그램을 사용하여 렌더링한 보고서는 다음과 같은 규칙을 따릅니다.  
  
-   XML 요소 및 특성은 보고서 정의에 나타나는 순서대로 렌더링됩니다.  
  
-   페이지 매기기는 무시됩니다.  
  
-   페이지 머리글과 바닥글은 렌더링되지 않습니다.  
  
-   토글을 통해 표시할 수 없는 숨겨진 항목은 렌더링되지 않습니다. 처음에 표시되는 항목과 토글을 통해 표시할 수 있는 숨겨진 항목은 렌더링됩니다.  
  
-   이미지, 줄 및 사용자 지정 보고서 항목**Images, lines, and custom report items** 은 무시됩니다.  
  
  
##  <a name="DataTypes"></a> 데이터 형식  
 입력란 요소 또는 특성은 입력란에 표시되는 값에 따라 XSD 데이터 형식이 지정됩니다.  
  
|입력란 값|지정되는 데이터 형식|  
|--------------------------------|---------------------------|  
|**Int16**, **Int32**, **Int64**, **UInt16**, **UInt32**, **UInt64**, **Byte**, **SByte**|**xsd:integer**|  
|**Decimal** (또는 **Decimal** 및 정수 또는 바이트 데이터 형식)|**xsd:decimal**|  
|**Float** (또는 **Decimal** 및 정수 또는 바이트 데이터 형식)|**xsd:float**|  
|**Double** (또는 **Decimal** 및 정수 또는 바이트 데이터 형식)|**xsd:double**|  
|**DateTime 또는 DateTime Offset**|**xsd:dateTime**|  
|**Time**|**xsd:string**|  
|**Boolean**|**xsd:boolean**|  
|**String**, **Char**|**xsd:string**|  
|기타|**xsd:string**|  
  
  
##  <a name="XMLSpecificRenderingRules"></a> XML 관련 렌더링 규칙  
 다음 섹션에서는 XML 렌더링 확장 프로그램을 통해 보고서 내의 항목이 어떻게 해석되는지 설명합니다.  
  
### <a name="report-body"></a>보고서 본문  
 보고서는 XML 문서의 루트 요소로 렌더링됩니다. 요소의 이름은 속성 창에 설정된 DataElementName 속성을 따릅니다.  
  
 XML 네임스페이스 정의와 스키마 참조 특성도 보고서 요소에 포함됩니다. 변수는 굵은 글꼴로 표시됩니다.  
  
 <**Report** xmlns="**SchemaName**" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" xsi:**schemaLocation**="**SchemaNameReportURL**&amp;rc%3aSchema=true" Name="ReportName">  
  
 변수의 값은 다음과 같습니다.  
  
|속성|값|  
|----------|-----------|  
|보고서|Report.DataElementName|  
|ReportURL|서버의 보고서를 가리키는 URL 인코딩된 절대 URL|  
|SchemaName|Report.SchemaName. Null인 경우 Report.Name입니다. Report.Name이 사용되는 경우 먼저 XmlConvert.EncodeLocalName으로 인코딩됩니다.|  
|ReportName|보고서의 이름|  
  
### <a name="text-boxes"></a>입력란  
 입력란은 DataElementStyle RDL 속성에 따라 요소나 특성으로 렌더링됩니다. 요소 또는 특성의 이름은 TextBox.DataElementName RDL 속성을 따릅니다.  
  
### <a name="charts-data-bars-and-sparklines"></a>차트, 데이터 막대 및 스파크라인  
 차트, 데이터 막대 및 스파크라인은 XML로 렌더링됩니다. 데이터는 구조화됩니다.  
  
### <a name="gauges-and-indicators"></a>계기 및 표시기  
 계기 및 표시기는 XML로 렌더링됩니다. 데이터는 구조화됩니다.  
  
### <a name="subreports"></a>하위 보고서  
 하위 보고서는 요소로 렌더링됩니다. 요소의 이름은 DataElementName RDL 속성을 따릅니다. 하위 보고서의 TextBoxesAsElements 속성 설정 대신 보고서의 해당 속성 설정이 적용됩니다. 네임스페이스 및 XSLT 특성은 하위 보고서 요소에 추가되지 않습니다.  
  
### <a name="rectangles"></a>사각형  
 사각형은 요소로 렌더링됩니다. 요소의 이름은 DataElementName RDL 속성을 따릅니다.  
  
### <a name="custom-report-items"></a>사용자 지정 보고서 항목  
 CustomReportItems(CRI)는 렌더링 확장 프로그램에 표시되지 않습니다. 보고서에 사용자 지정 보고서 항목이 있는 경우 렌더링 확장 프로그램에서는 이를 일반적인 보고서 항목으로 렌더링합니다.  
  
### <a name="images"></a>이미지  
 이미지는 렌더링되지 않습니다.  
  
### <a name="lines"></a>선  
 선은 렌더링되지 않습니다.  
  
  
### <a name="tables-matrices-and-lists"></a>테이블, 행렬 및 목록  
 테이블, 행렬 및 목록은 요소로 렌더링됩니다. 요소의 이름은 테이블릭스 DataElementName RDL 속성을 따릅니다.  
  
#### <a name="rows-and-columns"></a>행 및 열  
 열은 행 안에 렌더링됩니다.  
  
#### <a name="tablix-corner"></a>테이블릭스 모퉁이  
 모퉁이는 렌더링되지 않습니다. 모퉁이의 내용만 렌더링됩니다.  
  
#### <a name="tablix-cells"></a>테이블릭스 셀  
 테이블릭스 셀은 요소로 렌더링됩니다. 요소의 이름은 셀의 DataElementName RDL 속성을 따릅니다.  
  
#### <a name="automatic-subtotals"></a>자동 부분합  
 테이블릭스 자동 부분합은 렌더링되지 않습니다.  
  
#### <a name="row-and-column-items-that-do-not-repeat-with-a-group"></a>그룹과 함께 반복되지 않는 행 및 열 항목  
 그룹과 함께 반복되지 않는 레이블, 부분합, 합계 등의 항목은 요소로 렌더링됩니다. 요소의 이름은 TablixMember.DataElementName RDL 속성을 따릅니다.  
  
 TablixMember.DataElementOutput RDL 속성은 반복되지 않는 항목을 렌더링할지 여부를 제어합니다.  
  
 테이블릭스 멤버의 DataElementName 속성을 지정하지 않은 경우 반복되지 않는 항목의 이름은 다음 형식에 따라 동적으로 생성됩니다.  
  
 RowX - 반복되지 않는 행의 경우. 여기에서 X는 현재 부모 내에서 0부터 시작하는 행 인덱스입니다.  
  
 ColumnY - 반복되지 않는 열의 경우. 여기에서 Y는 현재 부모 내에서 0부터 시작하는 열 인덱스입니다.  
  
 반복되지 않는 머리글은 그룹과 함께 반복되지 않는 행 또는 열의 자식으로 렌더링됩니다.  
  
 반복되지 않는 멤버에 상응하는 테이블릭스 셀이 없으면 해당 멤버가 렌더링되지 않습니다. 테이블릭스 셀이 여러 개의 열에 걸쳐 있는 경우 등이 여기에 해당할 수 있습니다.  
  
#### <a name="rows-and-columns-that-repeat-with-a-group"></a>그룹과 함께 반복되는 행 및 열  
 그룹 내에서 반복되는 행과 열은 Tablix.DataElementOutput 규칙에 따라 렌더링됩니다. 요소의 이름은 DataElementName 속성을 따릅니다.  
  
 그룹 내의 고유한 값은 각각 그룹의 자식 요소로 렌더링됩니다. 요소의 이름은 Group.DataElementName 속성을 따릅니다.  
  
 DataElementOutput 속성 값이 Output이면 반복되는 항목의 머리글이 세부 정보 요소의 자식으로 렌더링됩니다.  
  
  
##  <a name="CustomFormatsXSLTransformations"></a> 사용자 지정 형식 및 XSL 변환  
 XML 렌더링 확장 프로그램에서 만든 XML 파일은 XSLT(XSL 변환)를 사용하여 거의 모든 형식으로 변환할 수 있습니다. 이 기능을 사용하면 기존 렌더링 확장 프로그램에서 지원하지 않는 형식으로도 데이터를 만들 수 있습니다. 사용자 고유의 렌더링 확장 프로그램을 만들기 전에 XML 렌더링 확장 프로그램과 XSLT 사용을 고려해 보십시오.  
  
  
##  <a name="DuplicateName"></a> 중복 이름  
 동일한 범위 내에 데이터 요소 이름이 중복되어 있으면 렌더러를 실행할 때 오류 메시지가 나타납니다.  
  
  
##  <a name="XSLTTransformations"></a> XSLT 변환  
 XML 렌더러로 서버 쪽 XSLT 변환을 원래 XML 데이터에 적용할 수 있습니다. XSLT를 적용하는 경우 렌더러에서는 원래 XML 데이터 대신 변환된 내용을 출력합니다. 변환은 클라이언트가 아니라 서버 쪽에서 진행됩니다.  
  
 출력에 적용할 XSLT는 보고서의 DataTransform 속성을 사용하여 보고서 정의 파일에 정의하거나 XSLT *DeviceInfo* 매개 변수를 사용하여 정의합니다. 이러한 값 중 하나를 설정하면 XML 렌더러를 사용할 때마다 변환이 일어납니다. 구독을 사용하는 경우에는 RDL DataTransform 속성에 XSLT를 정의해야 합니다.  
  
 DataTransform 정의 속성과 디바이스 정보 설정을 모두 사용하여 XSLT 파일을 지정한 경우에는 DataTransform에 지정한 XSLT가 먼저 진행된 다음 디바이스 정보 설정을 통해 설정한 XSLT가 적용됩니다.  
  
  
###  <a name="DeviceInfo"></a> 디바이스 정보 설정  
 디바이스 정보 설정을 변경하여 이 렌더러의 다음과 같은 일부 기본 설정을 변경할 수 있습니다.  
  
-   XML에 적용할 변환(XSLT)  
  
-   XML 문서의 MIME 형식  
  
-   데이터에 형식 문자열 적용 여부  
  
-   XML 출력에 대한 들여쓰기 여부  
  
-   XML 스키마 이름 포함 여부  
  
-   XML 문서 인코딩  
  
-   XML 문서의 파일 확장명  
  
 자세한 내용은 [XML Device Information Settings](../../reporting-services/xml-device-information-settings.md)을 참조하세요.  
  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [여러 보고서 렌더링 확장 프로그램의 대화형 기능&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [보고서 항목 렌더링&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
