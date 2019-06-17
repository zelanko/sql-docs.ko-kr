---
title: 다차원 모델용 Power View 이해 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d0558cae-8209-4242-80c5-2c95981b88b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 70ccd24e72671255ea0c929b19110794e1c0412a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072665"
---
# <a name="understanding-power-view-for-multidimensional-models"></a>다차원 모델용 파워 뷰 이해
  이 문서에서는 Microsoft SQL Server 2014의 다차원 모델용 Power View 기능에 대해 설명하고, 조직에서 다차원 모델용 Power View를 구현하려고 하는 BI 전문가 및 관리자에게 중요한 정보를 제공합니다.  
  
 다차원 모델은 업계 최고의 OLAP 데이터 모델링, 스토리지 및 분석 솔루션을 제공합니다. SQL Server 2014의 다차원 모델은 Microsoft Power View를 사용하여 임시 데이터 분석, 탐색 및 시각화를 지원합니다.  
  
 Power View는 SharePoint 라이브러리의 공유 보고서 데이터 원본 파일(.rsds)로부터 브라우저에서 실행되는 씬 웹 클라이언트입니다. 보고서 데이터 원본은 클라이언트와 백 엔드 데이터 원본 간을 연결하는 역할을 합니다. 백 엔드 데이터 원본은 SharePoint의 PowerPivot 통합 문서, 테이블 형식 모드에서 실행되는 Analysis Services 서버의 테이블 형식 모델 또는 다차원 모드에서 실행되는 Analysis Services 서버의 다차원 모델일 수 있습니다. 파워 뷰 보고서는 SharePoint 라이브러리 또는 갤러리에 저장할 수 있으며 조직의 다른 구성원과 공유할 수 있습니다.  
  
 **다차원 모델용 파워 뷰 아키텍처**  
  
 ![파워 뷰 다차원 모델 아키텍처용](../media/daxmd-architecture.gif "파워 뷰 다차원 모델 아키텍처용")  
  
## <a name="prerequisites"></a>필수 구성 요소  
 **서버 요구 사항**  
  
-   다차원 모드에서 실행하는 Analysis Service와 SQL Server 2014 Enterprise 또는 Business Intelligence Edition.  
  
-   Microsoft SharePoint Server 2010 또는 2013 Enterprise Edition용 SQL Server 2014 Reporting Services 추가 기능.  
  
 **클라이언트 요구 사항**  
  
-   파워 뷰 클라이언트 기능에는 Microsoft Silverlight 5가 필요합니다. 자세한 내용은 [Reporting Services 및 파워 뷰 브라우저 지원 계획 &#40;Reporting Services 2014&#41;](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)합니다.  
  
## <a name="features"></a>기능  
 **파워 뷰에 대한 기본 지원**  
  
 이 릴리스에서 다차원 모델은 SharePoint 모드의 파워 뷰를 사용하여 분석 및 시각화를 지원합니다. 다차원 모델에 대한 특별한 구성은 필요하지 않습니다. 하지만 Microsoft Excel 및 Microsoft PerformancePoint 등의 다른 클라이언트 도구와 비교할 때 Power View에서 다차원 모델 개체가 표시되는 방식에는 몇 가지 차이점이 있습니다. 이 릴리스에서는 Excel 2013의 Power View를 사용하여 다차원 모델의 분석 및 시각화를 지원하지 않습니다.  
  
 **DAX 쿼리에 대한 기본 지원**  
  
 이 릴리스에서 다차원 모델은 일반적인 MDX 쿼리뿐 아니라 DAX 쿼리 및 함수도 지원합니다. PATH 같은 일부 DAX 함수는 다차원 모델링에 적용할 수 없습니다. DAX에 대한 자세한 내용 및 MDX와의 차이점을 알아보려면 [Data Analysis Expressions 및 MDX](https://msdn.microsoft.com/library/ff487170\(SQL.105\).aspx)를 참조하십시오.  
  
## <a name="multidimensional-to-tabular-object-mapping"></a>다차원 개체와 테이블 형식 개체의 매핑  
 Analysis Services에서는 다차원 모델을 테이블 형식 모델 메타데이터로 표현합니다. 다차원 모델의 개체는 파워 뷰와 BI 주석이 포함된 CSDL 출력에서 테이블 형식 개체로 표현됩니다.  
  
 **개체 매핑 요약**  
  
|다차원 개체|테이블 형식 개체|  
|-----------------------------|--------------------|  
|Cube|Model|  
|큐브 차원|Table|  
|차원 특성(키, 이름)|Column|  
|측정값 그룹|Table|  
|측정값|이름|  
|측정값 그룹이 없는 측정값|Measures라는 테이블의 내부|  
|측정값 그룹 큐브 차원 관계|관계|  
|Cube|Cube|  
|KPI|KPI|  
|사용자/부모-자식 계층|계층|  
|표시 폴더|표시 폴더|  
  
## <a name="measures-measure-groups-and-kpis"></a>측정값, 측정값 그룹 및 KPI  
  
> [!NOTE]  
>  이 문서의 일부 이미지 및 텍스트는 SQL Server 2012용 Adventure Works 다차원 모델 예제 데이터베이스를 나타냅니다.  
  
 다차원 큐브의 측정값 그룹은 파워 뷰 필드 목록에서 시그마(∑) 기호가 있는 테이블로 표시됩니다.  
  
 **파워 뷰 필드 목록의 측정값 그룹**  
  
 ![필드 목록에서 Power View](../media/daxmd-powerviewfieldlist.gif "Power View에서 목록 필드")  
  
 측정값 그룹 내의 측정값은 측정값으로 나타납니다. 연결된 측정값 그룹이 없는 계산 측정값이 있을 경우 이러한 측정값은 Measures라는 특수 테이블에 그룹화됩니다.  
  
 보다 복잡한 다차원 모델을 단순화하기 쉽도록 모델 작성자는 표시 폴더에 배치할 큐브의 측정값 또는 KPI 집합을 정의할 수 있습니다. 파워 뷰에서는 표시 폴더와 그 안의 측정값 및 KPI를 표시할 수 있습니다.  
  
 **측정값 그룹의 측정값 및 KPI**  
  
 ![파워 뷰 필드 목록의 측정값 그룹과](../media/daxmd-fieldlist-group.gif "Power View 필드 목록의 측정값 그룹")  
  
### <a name="measures-as-variants"></a>variant로서의 측정값  
 다차원 모델의 측정값은 variant입니다. 즉, 이 측정값은 강력한 형식이 아니며 다른 데이터 형식일 수 있습니다. 예를 들어 아래 이미지에서 기본적으로 Financial Reporting 테이블의 Amount 측정값 통화 데이터 형식 이지만 "Statistical Accounts"를 문자열 데이터 형식인의 부분합에 대 한 문자열 값 "NA"도 있습니다. 파워 뷰에서는 일부 측정값을 variant로 인식하고 다른 시각화 유형으로 올바른 값 및 서식을 표시합니다.  
  
 **variant로서의 측정값**  
  
 ![파워 뷰의 집계할 수 없는 계층](../media/daxmd-nonaggrattrib.gif "파워 뷰의 집계할 수 없는 계층")  
  
### <a name="implicit-measures"></a>암시적 측정값  
 테이블 형식 모델에서는 사용자가 필드에 count, sum 또는 average와 같은 *암시적* 측정값을 만들 수 있습니다. 다차원 모델의 경우에는 차원 특성 데이터가 다른 방식으로 저장되므로 암시적 측정값을 쿼리하는 데 시간이 오래 걸릴 수 있습니다. 따라서 Powe View에서는 암시적 측정값을 사용할 수 없습니다.  
  
## <a name="dimensions-attributes-and-hierarchies"></a>차원, 특성 및 계층  
 큐브 차원은 테이블 형식 메타데이터에서 테이블로 표시됩니다. 파워 뷰 필드 목록에서 차원 특성은 표시 폴더 내에 열로 표시됩니다.  AttributeHierarchyEnabled 속성이 false로 설정된 차원 특성(예: Customer 차원의 Birth Date 특성)이나 AttributeHierarchyVisible 속성이 false로 설정된 차원 특성은 Power View 필드 목록에 나타나지 않습니다. 여러 수준 계층 또는 사용자 계층(예: Customer 차원의 Customer Geography)은 파워 뷰 필드 목록에서 계층으로 표시됩니다. 차원 특성의 숨겨진 UnknownMember는 DAX 쿼리와 파워 뷰에서는 표시됩니다.  
  
 **SSDT(SQL Server Data Tools) 및 파워 뷰 필드 목록의 차원, 특성 및 계층**  
  
 ![SSDT 및 파워 뷰 필드 목록의 차원을](../media/daxmd-ssdt-dimensions.gif "SSDT 및 파워 뷰 필드 목록의 차원")  
  
### <a name="dimension-attribute-type"></a>차원 특성 유형  
 다차원 모델에서는 차원 특성을 특정 차원 특성 유형과 연결할 수 있습니다. 아래 이미지에서는 City, State-Province, Country 및 Postal Code 차원 특성에 지리 유형이 연결된 Geography 차원을 보여 줍니다. 이러한 차원 특성은 테이블 형식 메타데이터에 표시됩니다. 파워 뷰에서는 메타데이터를 인식하므로 사용자가 지도 시각화를 만들 수 있습니다. 이는 파워 뷰 필드 목록에서 Geography 테이블의 City, Country, Postal Code 및 State-Province 열 옆에 지도 아이콘으로 표시됩니다.  
  
 **SSDT 및 파워 뷰 필드 목록의 차원 특성 지리 유형**  
  
 ![차원 특성 지리 유형](../media/daxmd-ssdt-attribute-geog-types.gif "차원 특성 지리 유형")  
  
### <a name="dimension-calculated-members"></a>차원 계산 멤버  
 다차원 모델에서는 단일 실제 멤버가 있는 모든 항목의 자식에 대해 계산 멤버를 지원합니다. 이러한 유형의 계산 멤버를 표시할 때의 추가 제약 조건은 다음과 같습니다.  
  
-   차원에 둘 이상의 특성이 있는 경우 단일 실제 멤버여야 합니다.  
  
-   계산 멤버를 포함하는 특성이 유일한 특성이 아닐 경우 이 특성은 차원의 키 특성일 수 없습니다.  
  
-   계산 멤버를 포함하는 특성은 부모-자식 특성일 수 없습니다.  
  
 사용자 계층의 계산 멤버는 파워 뷰에서 표시되지만, 최종 사용자는 여전히 사용자 계층의 계산 멤버를 포함하는 큐브에 연결할 수 있습니다.  
  
 아래 이미지에는 Date 차원의 "Fiscal Date Calculations" 차원 특성의 시간 인텔리전스 계산된 멤버를 포함 하는 큐브에 대 한 Power View 보고서를 보여 줍니다.  
  
 **계산 멤버가 있는 파워 뷰 보고서**  
  
 ![Power View의 계산 된 구성원](../media/daxmd-calcmembersinpowerview.gif "Power View의 계산 된 구성원")  
  
### <a name="default-members"></a>기본 멤버  
 다차원 모델에서는 차원 특성의 기본 멤버를 지원합니다. 기본 멤버는 Analysis Services에서 쿼리를 위해 데이터를 집계할 때 사용됩니다. 차원 특성의 기본 멤버는 테이블 형식 메타데이터에서 해당하는 열의 기본 값 또는 필터로 표시됩니다.  
  
 특성이 적용될 경우 파워 뷰는 Excel 피벗 테이블과 거의 동일하게 동작합니다. 사용자가 기본값을 포함하는 파워 뷰 시각화 유형(테이블, 행렬 또는 차트)에 열을 추가할 경우 해당 기본값이 적용되지 않고 사용 가능한 모든 값이 표시됩니다. 사용자가 필터에 열을 추가할 경우에는 기본값이 적용됩니다.  
  
### <a name="dimension-security"></a>차원 보안  
 다차원 모델에서는 역할을 통해 차원 및 셀 수준 보안을 지원합니다. 파워 뷰를 사용하여 큐브에 연결하는 사용자는 인증 후 적절한 사용 권한이 있는지 여부가 평가됩니다. 차원 보안이 적용된 경우에는 해당 차원 멤버가 파워 뷰에서 사용자에게 표시되지 않고, 사용자에게 일부 셀이 제한된 셀 보안 사용 권한이 정의된 경우에는 해당 사용자가 파워 뷰를 사용하여 큐브에 연결할 수 없습니다. 집계 데이터의 일부가 보안 데이터에서 계산된 경우 사용자가 집계 데이터를 볼 수 있는 경우도 있습니다.  
  
### <a name="non-aggregatable-attributeshierarchies"></a>집계할 수 없는 특성/계층  
 다차원 모델에서는 차원의 특성에 대해 IsAggregatable 속성이 false로 설정될 수 있습니다. 이는 클라이언트 애플리케이션에서 데이터를 쿼리할 때 계층 간에 데이터를 집계하지 않도록 모델 작성자가 지정했음을 의미합니다. 파워 뷰에서 이 차원 특성은 부분합을 사용할 수 없는 열로 표시됩니다. 아래 이미지에서는 집계할 수 없는 계층의 예, 즉 Accounts를 볼 수 있습니다. Accounts 부모-자식 계층의 최상위 수준은 집계할 수 없는 반면 다른 수준은 집계할 수 있습니다. Accounts 계층의 행렬 시각화(처음 두 수준)에서는 Account Level 02에 대한 부분합이 표시되지만 최상위 수준인 Account Level 01에 대한 부분합은 표시되지 않습니다.  
  
 **파워 뷰의 집계할 수 없는 계층**  
  
 ![파워 뷰의 집계할 수 없는 계층](../media/daxmd-nonaggrattrib.gif "파워 뷰의 집계할 수 없는 계층")  
  
## <a name="images"></a>이미지  
 파워 뷰에서는 이미지를 렌더링할 수 있습니다. 다차원 모델에서 파워 뷰에 이미지를 제공하는 방법 중 하나는 이미지의 URL(Uniform Resource Locator)을 포함하는 열을 표시하는 것입니다. 이 릴리스의 Analysis Services에서는 ImageURL 형식으로 차원 특성의 태그를 지정할 수 있습니다. 그런 다음 이 데이터 형식이 테이블 형식 메타데이터에 포함되어 파워 뷰에 제공됩니다. 그러면 파워 뷰는 시각화 내에서 URL에 지정된 이미지를 다운로드하여 표시할 수 있습니다.  
  
 **SSDT의 ImageURL 차원 특성 유형**  
  
 ![특성 속성을 차원](../media/daxmd-dimattribute-properties.gif "차원 특성 속성")  
  
## <a name="parent-child-hierarchies"></a>부모-자식 계층  
 다차원 모델은 부모-자식 계층을 지원하며 이 계층은 테이블 형식 메타데이터에 계층으로 표시됩니다. 부모-자식 계층의 각 수준은 숨겨진 열로 제공됩니다. 부모-자식 차원의 키 특성은 테이블 형식 메타데이터에 표시되지 않습니다.  
  
 **파워 뷰의 부모-자식 계층**  
  
 ![부모-자식 계층](../media/daxmd-ssdt-hierarchies.gif "부모-자식 계층")  
  
## <a name="perspectives-and-translations"></a>큐브 뷰 및 번역  
 큐브 뷰는 일부 차원 또는 측정값 그룹만 클라이언트 도구에 표시되는 큐브의 뷰입니다. 큐브 뷰의 이름은 큐브 연결 문자열 속성에 대한 값으로 지정할 수 있습니다. 예를 들어 다음 연결 문자열에 ' 직접 판매 '는 다차원 모델의 큐브 뷰:  
  
 `Data Source=localost;Initial Catalog=AdventureWorksDW-MD;Cube='Direct Sales'`  
  
 큐브에서는 모델 내의 다양한 언어에 대해 메타데이터 및 데이터 번역이 지정될 수 있습니다. 번역 (데이터 및 메타 데이터)를 확인 하기 위해 아래와 같이 RSDS 파일에서 연결 문자열에 선택적 "로캘 식별자" 속성을 추가 해야 합니다.  
  
 `Data Source=localost;Initial Catalog=AdventureWorksDW-MD;Cube='Adventure Works'; Locale Identifier=3084`  
  
 파워 뷰에서 로캘 ID가 있는 .rsds 파일로 다차원 모델에 연결할 때 해당 번역이 큐브에 포함되어 있으면 파워 뷰에 번역이 표시됩니다.  
  
 자세한 내용은 [Create a Report Data Source](create-a-report-data-source.md)을 참조하세요.  
  
## <a name="power-view-pinned-filters"></a>파워 뷰의 고정된 필터  
 파워 뷰 보고서에는 여러 뷰가 포함될 수 있습니다. 이 릴리스에서는 테이블 형식 모델과 다차원 모델 모두에 대해 *필터 고정* 기능을 사용하여 보고서의 모든 뷰에 적용되는 필터를 만들 수 있습니다. 아래 이미지에서는 뷰 필터에 대한 필터 고정 토글 단추를 보여 줍니다. 기본적으로 뷰 필터는 고정 해제되어 있고 해당 뷰에만 적용됩니다. 뷰 필터 고정은 모든 뷰에 적용되며, 뷰 필터를 고정 해제하면 다른 뷰에서 해당 필터가 제거됩니다.  
  
 **고정된 필터**  
  
 ![필터 고정](../media/daxmd-pinnedfilterinpowerview.gif "필터 고정")  
  
## <a name="unsupported-features"></a>지원되지 않는 기능  
 **Excel 2013의 power View** -에 연결 및 다차원 모델에 대 한 보고서 만들기를 지원 하지 않습니다. 다차원 모델용 Power View는 브라우저 기반 Power View 클라이언트만 지원합니다.  
  
 **동작** - 다차원 모델에 대한 Power View 보고서나 DAX 쿼리에서는 지원되지 않습니다.  
  
 **명명된 집합** - 다차원 모델에서는 다차원 모델에 대한 파워 뷰 또는 DAX 쿼리에서 명명된 집합이 지원되지 않습니다.  
  
> [!NOTE]  
>  동작과 명명된 집합이 지원되지 않더라도 사용자는 파워 뷰를 사용하여 다차원 모델에 연결하고 이를 탐색할 수 있습니다.  
  
 **셀 수준 보안** -Power View 보고서에서 지원 되지 않습니다.  
  
## <a name="csdlbi-annotations"></a>CSDLBI 주석  
 다차원 큐브 메타데이터는 CSDLBI(비즈니스 인텔리전스 포함 개념 스키마 정의 언어) 주석을 사용하여 EDM(엔터티 데이터 모델) 기반 개념 모델로 표시됩니다.  
  
 Analysis Services 인스턴스로 DISCOVER_CSDL_METADATA 요청이 보내질 때 다차원 메타데이터는 CSDLBI 문서, 즉 CSDL 출력에서 테이블 형식 모델 네임스페이스로 표현됩니다.  
  
 **DISCOVER_CSDL_METADATA 요청 예제**  
  
```  
<Envelopexmlns="http://schemas.xmlsoap.org/soap/envelope/">  
   <Body>  
      <Discoverxmlns="urn:schemas-microsoft-com:xml-analysis">  
         <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
              <CATALOG_NAME>"catalogname"<CATALOG_NAME>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
            <PropertyList>  
            </PropertyList>  
         </Properties>  
      </Discover>  
   </Body>  
</Envelope>  
  
```  
  
 DISCOVER_CSDL_METADATA 요청에는 다음과 같은 제한이 있습니다.  
  
|이름|필수|Description|  
|----------|--------------|-----------------|  
|CATALOG_NAME|사용자 계정 컨트롤|카탈로그\데이터베이스 이름입니다.|  
|PERSPECTIVE_NAME|큐브에 둘 이상의 큐브 뷰가 포함된 경우 필수, 큐브가 하나뿐이고 기본 큐브 뷰가 있는 경우 선택적|다차원 데이터베이스의 큐브 이름 또는 큐브 뷰 이름입니다.|  
|VERSION|사용자 계정 컨트롤|클라이언트가 요청한 CSDL 버전입니다. 다차원 기능 및 구문은 버전 2.0에서 지원됩니다.|  
  
 반환되는 CSDL 출력 문서에서는 모델을 네임스페이스, 포함 엔터티, 연결 및 속성으로 나타냅니다.  
  
 테이블 형식 모델의 CSDLBI 주석에 대 한 정보를 자세한 [csdl 용 BI 주석에 대 한 기술 참조](https://docs.microsoft.com/bi-reference/csdl/technical-reference-for-bi-annotations-to-csdl) MSDN의 및 [ \[MS-CSDLBI\]: 개념 스키마 정의 파일 형식으로 비즈니스 인텔리전스 주석 사용](https://msdn.microsoft.com/library/jj161299\(SQL.105\).aspx)합니다.  
  
## <a name="client-help-on-officecom"></a>Office.com의 클라이언트 도움말  
 Office.com에서 제공되는 다음 문서는 파워 뷰에서 다차원 모델 개체가 나타나는 방식과 예제 보고서를 만드는 방법을 배우는 데 유용합니다.  
  
 [파워 뷰의 다차원 모델 개체 이해](http://office.microsoft.com/excel-help/understanding-multidimensional-model-objects-in-power-view-HA104018589.aspx)  
  
 [파워 뷰를 사용하여 Adventure Works 다차원 모델 탐색](http://office.microsoft.com/excel-help/explore-the-adventure-works-multidimensional-model-by-using-power-view-HA104046830.aspx)  
  
  
