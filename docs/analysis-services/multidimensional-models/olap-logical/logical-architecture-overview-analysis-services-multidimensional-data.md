---
title: 논리적 아키텍처 개요 (Analysis Services-다차원 데이터) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c17be4bb01b5ff3b3a0ea04a99ac94ad311cc3d3
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="logical-architecture-overview-analysis-services---multidimensional-data"></a>논리 아키텍처 개요(Analysis Services - 다차원 데이터)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services는 여러 가지 유형의 Analysis Services 모델에 사용되는 메모리 아키텍처 및 런타임 환경을 결정하는 서버 배포 모드에서 작동합니다. 서버 모드는 설치 중에 결정됩니다. **다차원 및 데이터 마이닝 모드** 기존 OLAP 및 데이터 마이닝을 지원 합니다. **테이블 형식 모드** 테이블 형식 모델을 지원 합니다. **SharePoint 통합된 모드** 로 설치 된 Analysis Services의 인스턴스를 참조 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] SharePoint에 로드 하 고 Excel 쿼리 사용 또는 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 통합 문서 데이터 모델입니다.  
  
 이 항목에서는 다차원 및 데이터 마이닝 모드에서 작업할 때의 기본 Analysis Services 아키텍처에 대해 설명합니다. 다른 모드에 대 한 자세한 내용은 참조 [테이블 형식 모델링 ](../../../analysis-services/tabular-models/tabular-models-ssas.md) 및 [비교 테이블 형식 및 다차원 솔루션 ](../../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)합니다.  
  
## <a name="basic-architecture"></a>기본 아키텍처  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에는 여러 데이터베이스가 있을 수 있으며, 데이터베이스에는 OLAP 개체와 데이터 마이닝 개체가 동시에 있을 수 있습니다. 응용 프로그램은 지정된 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스와 지정된 데이터베이스에 연결합니다. 서버 컴퓨터는 여러 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스를 호스팅할 수 있습니다. 인스턴스 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 관계로 명명 됩니다 "\<서버 이름 >\\< InstanceName\>"입니다. 다음 그림 언급 된 모든 관계를 보여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체입니다.  
  
 ![AMO 실행 개체 관계](../../../analysis-services/multidimensional-models/olap-logical/media/amo-runningobjects.gif "AMO 실행 개체 관계")  
  
 기본 클래스는 큐브를 만드는 데 필요한 최소 개체 집합입니다. 이 최소 개체 집합은 차원, 측정값 그룹 및 파티션입니다. 집계는 선택 사항입니다.  
  
 차원은 특성과 계층으로 만들어집니다. 계층은 순서가 지정된 특성 집합으로 만들어집니다. 여기서 각 특성은 계층의 수준에 해당합니다.  
  
 큐브는 차원과 측정값 그룹으로 만들어집니다. 큐브의 차원 컬렉션에 있는 차원은 데이터베이스의 차원 컬렉션에 속합니다. 측정값 그룹은 동일한 데이터 원본 뷰를 가지며 큐브에서 동일한 차원 하위 집합을 갖는 측정값의 컬렉션입니다. 측정값 그룹에는 실제 데이터를 관리하는 하나 이상의 파티션이 있으며, 기본 집계 디자인이 있을 수도 있습니다. 기본 집계 디자인은 측정 그룹의 모든 파티션에서 사용될 수 있으며, 각 파티션에는 자체 집계 디자인이 있을 수 있습니다.  
  
 Server 개체  
 각 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스는 AMO에 별개의 서버 개체로 표시되므로 서로 다른 연결을 사용하여 <xref:Microsoft.AnalysisServices.Server> 개체에 연결됩니다. 각 서버 개체에는 어셈블리 및 보안 역할과 함께 하나 이상의 데이터 원본, 데이터 원본 뷰 및 데이터베이스 개체가 포함되어 있습니다.  
  
 차원 개체  
 각 데이터베이스 개체에는 여러 차원 개체가 포함되어 있고, 각 차원 개체에는 계층으로 구성되는 하나 이상의 특성이 포함되어 있습니다.  
  
 큐브 개체  
 각 데이터베이스 개체에는 하나 이상의 큐브 개체가 포함되어 있습니다. 큐브는 해당 측정값과 차원에 의해 정의됩니다. 큐브의 측정값과 차원은 큐브의 기반이 되고 측정값과 차원 정의에서 생성된 데이터 원본 뷰에 있는 테이블과 뷰에서 파생됩니다.  
  
## <a name="object-inheritance"></a>개체 상속  
 ASSL 개체 모델에는 많은 반복 요소 그룹이 포함되어 있습니다. 예를 들어 요소 그룹 "**차원** 포함 **계층**,"는 요소의 차원 계층을 정의 합니다. 둘 다 **큐브** 및 **MeasureGroups** 는 요소 그룹 "**차원** 포함 **계층**."  
  
 명시적으로 재정의되지 않는 한 요소는 상위 수준에서 이러한 반복 요소 그룹의 정보를 상속합니다. 예를 들어는 **번역** 에 대 한는 **CubeDimension** 동일는 **번역** 해당 상위 항목 요소에 대 한 **큐브**합니다.  
  
 상위 수준 개체에서 상속된 속성을 명시적으로 재정의하려는 경우 개체는 상위 수준 개체의 전체 구조와 속성을 명시적으로 반복하지 않아도 되며, 재정의하려는 속성만 명시적으로 표시하면 됩니다. 예를 들어 한 **CubeDimension** 만 표시할 수 있습니다 **계층** 에서 해제 해야 하는 **큐브**, 표시 유형을 변경 해야 할를 나 또는 일부 **수준** 세부 정보에 제공 되지 않은 **차원** 수준입니다.  
  
 개체에 지정된 일부 속성은 자식 또는 하위 항목 개체의 동일한 속성에 기본값을 제공합니다. 예를 들어 **Cube.StorageMode** 에 대 한 기본값을 제공 **Partition.StorageMode**합니다. 상속된 기본값의 경우 ASSL은 상속된 기본값에 대한 이러한 규칙을 적용합니다.  
  
-   XML에서 자식 개체의 속성이 null이면 기본적으로 속성의 기본값이 상속된 값으로 설정됩니다. 그러나 서버의 값을 쿼리하는 경우 서버가 XML 요소의 null 값을 반환합니다.  
  
-   자식 개체의 속성이 자식 개체에 직접 설정되었는지 또는 상속되었는지 여부를 프로그래밍 방식으로 확인할 수는 없습니다.  
  
## <a name="example"></a>예제  
 Packages와 Last라는 두 개의 측정값과 Route, Source, Time이라는 세 개의 관련 차원이 있는 Imports 큐브가 있다고 가정합니다.  
  
 ![큐브 예 1](../../../analysis-services/multidimensional-models/olap-logical/media/cubeintro1.gif "큐브 예 1")  
  
 큐브 주위의 더 작은 영숫자 값이 차원의 멤버입니다. 예제 멤버는 ground(Route 차원의 멤버), Africa(Source 차원의 멤버) 및 1st quarter(Time 차원의 멤버)입니다.  
  
### <a name="measures"></a>큐브 구조  
 큐브 셀 내의 값은 Packages와 Last라는 두 가지 측정값을 나타냅니다. Packages 측정값은 수입한 패키지 수를 나타내며 및 **Sum** 함수 팩트 집계에 사용 됩니다. Last 측정값은 수령한 날짜를 나타내는 및 **최대** 함수 팩트 집계에 사용 됩니다.  
  
### <a name="dimensions"></a>차원  
 Route 차원은 수입품이 목적지에 도착하는 방법을 나타냅니다. 이 차원의 멤버에는 ground, nonground, air, sea, road 또는 rail이 있습니다. Source 차원은 수입품이 생산되는 Africa 또는 Asia 등의 지역을 나타냅니다. Time 차원은 단일 연도의 분기와 반기를 나타냅니다.  
  
### <a name="aggregates"></a>집계  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 필요에 따라 상위 수준의 값을 집계하므로 차원 내 멤버의 수준에 관계없이 큐브의 비즈니스 사용자가 모든 차원의 각 멤버에 대한 측정값을 결정할 수 있습니다. 예를 들어 위 그림의 측정값은 다음 다이어그램에서와 같이 Time 차원 내의 Calendar Time 계층을 사용하여 표준 달력 계층에 따라 집계될 수 있습니다.  
  
 ![시간 차원에 따라 구성 된 측정값 다이어그램](../../../analysis-services/multidimensional-models/olap-logical/media/cubeintro2.gif "시간 차원에 따라 구성 된 측정값 다이어그램")  
  
 단일 차원을 사용하여 측정값을 집계하는 것 외에도 다른 차원의 멤버를 조합하여 측정값을 집계할 수 있습니다. 이렇게 하면 비즈니스 사용자가 동시에 여러 차원에서 측정값을 평가할 수 있습니다. 예를 들어 비즈니스 사용자가 Eastern Hemisphere와 Western Hemisphere에서 항공편으로 도착한 분기별 수입품을 분석하려는 경우 큐브에 대해 쿼리를 실행하여 다음과 같은 데이터 집합을 검색할 수 있습니다.  
  
||||패키지|||마지막|||  
|-|-|-|--------------|-|-|----------|-|-|  
||||All Sources|Eastern Hemisphere|Western Hemisphere|All Sources|Eastern Hemisphere|Western Hemisphere|  
|All Time|||25110|6547|18563|Dec-29-99|Dec-22-99|Dec-29-99|  
||1st half||11173|2977|8196|Jun-28-99|6 월-20-99|Jun-28-99|  
|||1st quarter|5108|1452|3656|Mar-30-99|3 월-19-99|Mar-30-99|  
|||2nd quarter|6065|1525|4540|Jun-28-99|6 월-20-99|Jun-28-99|  
||2nd half||13937|3570|10367|Dec-29-99|Dec-22-99|Dec-29-99|  
|||3rd quarter|6119|1444|4675|Sep-30-99|9 월-18-99|Sep-30-99|  
|||4th quarter|7818|2126|5692|Dec-29-99|Dec-22-99|Dec-29-99|  
  
 큐브를 정의한 다음에는 새 집계를 만들거나, 집계를 처리하는 동안 미리 계산할 것인지 또는 쿼리 시 계산할 것인지와 같은 옵션을 설정하기 위해 기존 집계를 변경할 수 있습니다. **관련된 항목:**[집계 및 집계 디자인](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)합니다.  
  
### <a name="mapping-measures-attributes-and-hierarchies"></a>측정값, 특성 및 계층 매핑  
 이 예제 큐브의 측정값, 특성 및 계층은 큐브의 팩트 및 차원 테이블의 다음 열에서 파생됩니다.  
  
|측정값 또는 특성(수준)|멤버|원본 테이블|원본 열|열 값의 예|  
|------------------------------------|-------------|------------------|-------------------|-------------------------|  
|Packages 측정값|해당 사항 없음|ImportsFactTable|패키지|12|  
|Last 측정값|해당 사항 없음|ImportsFactTable|마지막|May-03-99|  
|Route 차원의 Route Category 수준|nonground,ground|RouteDimensionTable|Route_Category|Nonground|  
|Route 차원의 Route 특성|air,sea,road,rail|RouteDimensionTable|경로|Sea|  
|Source 차원의 Hemisphere 특성|Eastern Hemisphere,Western Hemisphere|SourceDimensionTable|Hemisphere|Eastern Hemisphere|  
|Source 차원의 Continent 특성|Africa,Asia,AustraliaEurope,N. America,S. America|SourceDimensionTable|Continent|Europe|  
|Time 차원의 Half 특성|1st half,2nd half|TimeDimensionTable|Half|2nd half|  
|Time 차원의 Quarter 특성|1st quarter,2nd quarter,3rd quarter,4th quarter|TimeDimensionTable|Quarter|3rd quarter|  
  
 단일 큐브 셀의 데이터는 일반적으로 팩트 테이블의 여러 행에서 파생됩니다. 예를 들어 air 멤버, Africa 멤버 및 1st quarter 멤버가 교차 하는 지점의 큐브 셀의 다음 행을 집계 하 여 파생 값이 포함 되어는 **i m p** 팩트 테이블입니다.  
  
|||||||  
|-|-|-|-|-|-|  
|Import_ReceiptKey|RouteKey|SourceKey|TimeKey|패키지|마지막|  
|3516987|1.|6|1.|15|1 월-10-99|  
|3554790|1.|6|1.|40|1 월-19-99|  
|3572673|1.|6|1.|34|Jan-27-99|  
|3600974|1.|6|1.|45|Feb-02-99|  
|3645541|1.|6|1.|20|Feb-09-99|  
|3674906|1.|6|1.|36|Feb-17-99|  
  
 이전 테이블의 각 행에 동일한 값에 대 한는 **RouteKey**, **SourceKey**, 및 **TimeKey** 이러한 행은 동일한 큐브 셀을 발생할 수 있음을 나타내는 열입니다.  
  
 여기에 제시된 예는 큐브에 단일 측정값 그룹이 있으며 모든 차원 테이블이 별모양 스키마로 팩트 테이블에 조인된다는 점에서 매우 단순한 큐브를 나타냅니다. 팩트 테이블에 직접 조인되는 것이 아니라 또 다른 차원 테이블에 하나 이상의 차원 테이블이 조인되는 눈송이 스키마도 많이 사용됩니다. **관련된 항목:**[차원 &#40;Analysis Services-다차원 데이터&#41;](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)합니다.  
  
 여기에 제시된 예에는 단일 팩트 테이블만 있습니다. 큐브에 팩트 테이블이 여러 개 있는 경우 각 팩트 테이블의 측정값은 측정값 그룹으로 구성되고 측정값 그룹은 정의된 차원 관계에 따라 특정 차원 집합에 연결됩니다. 이러한 관계는 참여하는 테이블을 데이터 원본 뷰에 지정하고 관계의 세분성을 지정하여 정의됩니다. **관련된 항목:**[차원 관계](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델 데이터베이스 ](../../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
