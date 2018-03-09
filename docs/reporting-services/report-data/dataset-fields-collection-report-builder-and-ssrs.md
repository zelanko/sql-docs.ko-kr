---
title: "데이터 집합 필드 컬렉션(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b3884576-1f7e-4d40-bb7d-168312333bb3
caps.latest.revision: "13"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 93e0f3ac2c38d3fa61ec63c65c3a5ceb664bc4d8
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="dataset-fields-collection-report-builder-and-ssrs"></a>데이터 집합 필드 컬렉션(보고서 작성기 및 SSRS)
  데이터 집합 필드는 데이터 연결의 데이터를 나타냅니다. 필드는 숫자 데이터나 숫자가 아닌 데이터를 나타낼 수 있습니다. 예로는 판매액, 총 판매액, 고객 이름, 데이터베이스 식별자, URL, 이미지, 공간 데이터, 전자 메일 주소 등이 있습니다. 디자인 화면에서 필드는 입력란, 테이블 및 차트와 같은 보고서 항목에서 식으로 나타납니다.  
  
 보고서에는 데이터 집합 필드, 데이터 집합 계산 필드 및 기본 제공 필드 등 세 가지 유형의 필드가 있고 보고서 데이터 창에 표시됩니다.  
  
-   **데이터 집합 필드.** 데이터 집합 쿼리가 데이터 원본에 대해 실행될 때 반환될 필드의 컬렉션을 나타내는 메타데이터입니다.  
  
-   **데이터 집합 계산 필드.** 데이터 집합에 대해 만드는 추가 필드입니다. 각 계산 필드는 사용자가 정의하는 식을 계산하여 만들어집니다.  
  
-   **기본 제공 필드.** 보고서를 처리할 때 보고서 이름 또는 시간과 같은 보고서 정보를 제공하는 보고서 작성기에서 제공하는 필드의 컬렉션을 나타내는 메타데이터입니다. 자세한 내용은 [기본 제공 Globals 및 Users 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)를 참조하세요.  
  
 데이터 집합 필드 이름은 보고서 데이터 집합 정의의 일부로 저장됩니다. 자세한 내용은 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Fields"></a> 데이터 집합 필드 및 쿼리  
 데이터 집합 필드는 데이터 집합 쿼리 명령 및 사용자가 정의하는 계산 필드로 지정됩니다. 보고서에 표시되는 필드의 컬렉션은 사용하는 데이터 집합의 유형에 따라 다릅니다.  
  
-   **공유 데이터 집합.** 필드 컬렉션은 보고서에 공유 데이터 집합을 직접 추가했을 때나 공유 데이터 집합이 포함된 보고서 파트를 추가했을 때 공유 데이터 집합 정의의 쿼리에 대한 필드의 목록입니다. 공유 데이터 집합 정의가 보고서 서버에서 변경될 때 로컬 필드 컬렉션은 변경되지 않습니다. 로컬 필드 컬렉션을 업데이트하려면 로컬 공유 데이터 집합의 목록을 새로 고쳐야 합니다.  
  
-   **포함된 데이터 집합.** 필드 컬렉션은 데이터 원본에 대해 현재 쿼리를 실행할 때 반환되는 필드의 목록입니다.  
  
 자세한 내용은 [보고서 데이터 창에서 필드 추가, 편집, 새로 고침&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)을 참조하세요.  
  
  
### <a name="calculated-fields"></a>계산 필드  
 식을 만들어 계산 필드를 직접 지정합니다. 계산 필드를 사용하면 데이터 원본에 없는 새 값을 만들 수 있습니다. 예를 들어 계산 필드는 새 값, 필드 값 집합에 대한 사용자 지정 정렬 순서 또는 다른 데이터 형식으로 변환되는 기존 필드를 나타낼 수 있습니다.  
  
 계산 필드는 보고서에 로컬이며 공유 데이터 집합의 일부로 저장될 수 없습니다.  
  
 자세한 내용은 [보고서 데이터 창에서 필드 추가, 편집, 새로 고침&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)을 참조하세요.  
  
  
### <a name="entities-and-entity-fields"></a>엔터티 및 엔터티 필드  
 보고서 모델 데이터 원본으로 작업하는 경우 엔터티 및 엔터티 필드를 보고서 데이터로 지정합니다. 보고서 모델의 쿼리 디자이너에서 대화형으로 관련 엔터티를 탐색 및 선택하고 보고서 데이터 집합에 포함할 필드를 선택할 수 있습니다. 쿼리 디자인을 마친 후 보고서 데이터 창에서 엔터티 식별자와 엔터티 필드의 컬렉션을 볼 수 있습니다. 엔터티 식별자는 보고서 모델에서 자동으로 생성되며 일반적으로 최종 사용자에게 표시되지 않습니다.  
  
### <a name="using-extended-field-properties"></a>확장 필드 속성 사용  
 다차원 쿼리를 지원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]와 같은 데이터 원본은 필드의 필드 속성을 지원합니다. 필드 속성은 쿼리의 결과 집합에 나타나지만 **보고서 데이터** 창에 표시되지 않습니다. 보고서에서 이 필드 속성을 계속 사용할 수 있습니다. 필드의 속성을 참조하려면 필드를 보고서로 끌고 기본 속성 **Value** 를 원하는 속성의 필드 이름으로 변경합니다. 예를 들어 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브에서 큐브 셀의 값에 대한 서식을 정의할 수 있습니다. 서식이 지정된 값은 필드 속성 **FormattedValue**를 통해 사용할 수 있습니다. 값을 사용하고 입력란의 서식 속성을 설정하는 대신 값을 직접 사용하려면 필드를 입력란으로 끌고 기본 식 `=Fields!FieldName.Value` 를 `=Fields!FieldName.FormattedValue`로 변경합니다.  
  
> [!NOTE]  
>  모든 데이터 원본에 대해 모든 **Field** 속성을 사용할 수 있는 것은 아닙니다. **Value** 및 **IsMissing** 속성은 모든 데이터 원본에 대해 정의됩니다. 미리 정의된 다른 속성(다차원 데이터 원본에 대한 **Key**, **UniqueName**및 **ParentUniqueName** )은 데이터 원본에서 제공하는 경우에만 지원됩니다. 일부 데이터 공급자는 사용자 지정 속성을 지원합니다. 자세한 내용은 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)를 참조하세요. 예를 들어, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본에 대한 자세한 내용은 [Analysis Services 데이터베이스에 대한 확장 필드 속성&#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)을 참조하세요.  
  
  
##  <a name="Defaults"></a> 필드에 대한 기본 식 이해  
 입력란은 보고서 본문의 입력란 보고서 항목 또는 테이블릭스 데이터 영역에 있는 셀의 입력란일 수 있습니다. 입력란에 필드를 연결할 때 입력란 위치에서 필드 참조에 대한 기본 식을 결정합니다. 보고서 본문에서 입력란 값 식은 집계 및 데이터 집합을 지정해야 합니다. 보고서에 하나의 데이터 집합만 존재하는 경우 이 기본 식이 생성됩니다. 숫자 값을 나타내는 필드의 경우 기본 집계 함수는 Sum입니다. 숫자가 아닌 값을 나타내는 필드의 경우 기본 집계는 First입니다.  
  
 테이블릭스 데이터 영역에서 기본 필드 식은 필드를 추가하는 입력란의 행 및 그룹 멤버 자격에 따라 다릅니다. 테이블의 정보 행에 있는 입력란에 추가되는 Sales 필드에 대한 필드 식은 `[Sales]`입니다. 동일한 필드를 그룹 머리글의 입력란에 추가하는 경우 그룹 머리글에서 정보 값이 아닌 그룹에 대한 요약 값을 표시하므로 기본 식은 `(Sum[Sales])`입니다. 보고서가 실행되면 보고서 처리기에서 각 식을 계산하고 보고서의 결과를 대체합니다.  
  
 식에 대한 자세한 내용은 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
  
##  <a name="DataTypes"></a> 필드 데이터 형식  
 데이터 집합을 만들 때 데이터 원본의 필드 데이터 형식이 보고서에서 사용하는 데이터 형식과 정확하게 일치하지 않을 수 있습니다. 데이터 형식이 하나 또는 두 개의 매핑 계층을 거칠 수 있습니다. 데이터 처리 확장 프로그램 또는 데이터 공급자는 데이터 원본의 데이터 형식을 CLR(공용 언어 런타임) 데이터 형식으로 매핑할 수 있습니다. 데이터 처리 확장 프로그램에서 반환하는 데이터 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에서 CLR(공용 언어 런타임) 데이터 형식의 하위 집합으로 매핑됩니다.  
  
 데이터 원본에서 데이터는 데이터 원본에서 지원하는 데이터 형식으로 저장됩니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nvarchar **또는** datetime **과 같이 지원되는**데이터 형식 중 하나여야 합니다. 데이터 원본에서 데이터를 검색하는 경우 데이터는 데이터 원본 유형과 연결된 데이터 처리 확장 프로그램 또는 데이터 공급자를 통과합니다. 데이터 처리 확장 프로그램에 따라 데이터가 데이터 원본에서 사용되는 데이터 형식에서 데이터 처리 확장 프로그램에서 지원하는 데이터 형식으로 변환될 수 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]와 함께 설치된 CLR(공용 언어 런타임)에서 지원하는 데이터 형식을 사용합니다. 데이터 공급자는 결과 집합의 각 열을 네이티브 데이터 형식에서 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 데이터 형식으로 매핑합니다.  
  
 각 단계에서 데이터는 다음 목록에서 설명하는 데이터 형식으로 표현됩니다.  
  
-   **데이터 원본** 연결하는 데이터 원본 유형 버전에서 지원하는 데이터 형식입니다.  
  
     예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본에 대한 일반적인 데이터 형식에는 **int**, **datetime**및 **varchar**가 있습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 에서 새로 도입된 데이터 형식으로 **date**, **time**, **datetimetz**및 **datetime2**에 대한 지원을 추가했습니다. 자세한 내용은 [데이터 형식(Transact-SQL)](http://go.microsoft.com/fwlink/?linkid=98362)을 참조하세요.  
  
-   **데이터 공급자 또는 데이터 처리 확장 프로그램** 데이터 원본에 연결할 때 선택하는 데이터 처리 확장 프로그램의 데이터 공급자 버전에서 지원하는 데이터 형식입니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 를 기반으로 하는 데이터 공급자는 CLR에서 지원하는 데이터 형식을 사용합니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자 데이터 형식 지원에 대한 자세한 내용은 MSDN의 [데이터 형식 매핑(ADO.NET)](http://go.microsoft.com/fwlink/?LinkId=112178) 및 [기본 형식 사용](http://go.microsoft.com/fwlink/?LinkId=112177) 을 참조하세요.  
  
     예를 들어 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 에서 지원하는 일반적인 데이터 형식에는 **Int32** 및 **String**이 있습니다. 달력 날짜 및 시간은 **DateTime** 구조에서 지원합니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 서비스 팩 1은 표준 시간대 오프셋이 있는 날짜에 대한 **DateTimeOffset** 구조를 새로 지원합니다.  
  
    > [!NOTE]  
    >  보고서 서버는 보고서 서버에 설치되고 구성되는 데이터 공급자를 사용합니다. 미리 보기 모드의 보고서 제작 클라이언트는 클라이언트 컴퓨터에 설치되고 구성된 데이터 처리 확장 프로그램을 사용합니다. 보고서를 보고서 클라이언트 환경과 보고서 서버 환경 모두에서 테스트해야 합니다.  
  
-   **보고서 처리기** 데이터 형식은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 설치할 때 설치된 CLR 버전을 기반으로 합니다.  
  
     예를 들어 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 에서 새로 도입된 새 날짜 및 시간 유형에 대해 보고서 처리기가 사용하는 데이터 형식이 다음 표에 표시됩니다.  
  
    |SQL 데이터 형식|CLR 데이터 형식|Description|  
    |-------------------|-------------------|-----------------|  
    |**날짜**|**DateTime**|날짜만|  
    |**Time**|**TimeSpan**|시간만|  
    |**DateTimeTZ**|**DateTimeOffset**|표준 시간대 오프셋을 포함하는 날짜 및 시간|  
    |**DateTime2**|**DateTime**|소수 자릿수 밀리초를 포함하는 날짜 및 시간|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 형식에 대한 자세한 내용은 [데이터 형식(데이터베이스 엔진)](http://go.microsoft.com/fwlink/?linkid=98362) 및 [날짜 및 시간 데이터 형식 및 함수(Transact-SQL)](http://go.microsoft.com/fwlink/?linkid=98360)를 참조하세요.  
  
 식에서 데이터 집합 필드에 대한 참조를 포함하는 방법은 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
  
##  <a name="MissingFields"></a> 런타임에 누락된 필드 검색  
 보고서가 처리될 때 해당 열이 더 이상 데이터 원본에 존재하지 않아 데이터 집합에 대한 결과 집합에서 지정된 일부 열에 대한 값이 누락될 수 있습니다. 필드 속성 IsMissing을 사용하여 필드에 대한 값이 런타임에 반환되었는지를 검색할 수 있습니다. 자세한 내용은 [데이터 집합 필드 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-dataset-fields-collection-references-report-builder.md)를 참조하세요.  
  
  
## <a name="see-also"></a>참고 항목  
 [데이터 집합 속성 대화 상자, 필드&#40;보고서 작성기&#41;](http://msdn.microsoft.com/library/75c7e54a-3d20-4c9a-88da-ab36dce2ce42)   
 [보고서 작성기의 보고서 파트 및 데이터 집합](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
