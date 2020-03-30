---
title: SSRS(SQL Server Reporting Services)의 보고서 데이터 소개
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.custom: seodec18
ms.date: 11/18/2019
ms.openlocfilehash: 6317e8161871d7094486ed8b6178847549d8ab96
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74190730"
---
# <a name="intro-to-report-data-in-sql-server-reporting-services-ssrs"></a>SSRS(SQL Server Reporting Services)의 보고서 데이터 소개

  보고서 데이터는 조직의 다양한 데이터 원본에서 가져올 수 있습니다. 보고서 디자인의 첫 단계는 기본 보고서 데이터를 나타내는 데이터 원본 및 데이터 세트를 만드는 것입니다. 각 데이터 원본은 데이터 연결 정보를 포함합니다. 각 데이터 세트는 데이터 원본의 데이터로 사용할 필드 세트를 정의하는 쿼리 명령을 포함합니다. 각 데이터 세트의 데이터를 시각화하려면 테이블, 행렬, 차트 및 지도와 같은 데이터 영역을 추가합니다. 보고서를 처리하면 데이터 원본에 대한 쿼리가 실행되고 각 데이터 영역이 필요에 따라 확장되어 데이터 세트에 대한 쿼리 결과를 표시합니다.  

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

## <a name="data-in-ssrbnoversion"></a>다음의 데이터 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]  
 ![rs_DataSourcesStory](../../reporting-services/report-data/media/rs-datasourcesstory.gif "rs_DataSourcesStory")  
  
1.  **보고서 데이터 창의 데이터 원본** 포함된 데이터 원본을 만들거나 공유 데이터 원본을 추가하면 데이터 원본이 보고서 데이터 창에 표시됩니다.  
  
2.  **연결 대화 상자** 연결 대화 상자를 사용하여 연결 문자열을 작성하거나 붙여 넣습니다.  
  
3.  **데이터 연결 정보** 연결 문자열은 데이터 확장 프로그램에 전달됩니다.  
  
4.  **자격 증명** 자격 증명은 연결 문자열과 별도로 관리됩니다.  
  
5.  **데이터 확장 프로그램/데이터 공급자** 여러 데이터 액세스 계층을 통해 데이터에 연결할 수 있습니다.  
  
6.  **외부 데이터 원본** 관계형 데이터베이스, SharePoint 목록 또는 웹 서비스에서 데이터를 검색합니다.  


##  <a name="defining-terms"></a><a name="BkMk_ReportDataTerms"></a> 용어 정의  
  
- **데이터 연결** *데이터 원본*이라고도 합니다. 데이터 연결에는 연결 형식에 따라 달라지는 이름 및 연결 속성이 포함되어 있습니다. 기본적으로 데이터 연결에는 자격 증명이 포함되지 않습니다. 데이터 연결은 외부 데이터 원본에서 어떤 데이터를 검색할 것인지 지정하지 않습니다. 이렇게 하려면 데이터 세트를 만들 때 쿼리를 지정합니다.  
  
- **데이터 원본 정의.** 보고서 데이터 원본의 XML 표현을 포함하는 파일입니다. 보고서를 게시할 때 해당 데이터 원본은 보고서 정의와는 별도로 보고서 서버 또는 SharePoint 사이트에 데이터 원본 정의로 저장됩니다. 예를 들어 보고서 서버 관리자가 연결 문자열이나 자격 증명을 업데이트할 수 있습니다. 기본 보고서 서버의 파일 형식은 .rds입니다. SharePoint 사이트의 파일 형식은 .rsds입니다.  
  
- **연결 문자열.** 연결 문자열은 데이터 원본에 연결하는 데 필요한 연결 속성의 문자열 버전입니다. 연결 속성은 데이터 연결 형식에 따라 다릅니다. 예를 들어 [데이터 연결 문자열 만들기 - 보고서 작성기 및 SSRS](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)를 참조하세요.  
  
- **공유 데이터 원본.** 여러 보고서에서 사용할 수 있도록 보고서 서버 또는 SharePoint 사이트에 제공되는 데이터 원본입니다.  
  
- **포함된 데이터 원본.** *보고서별 데이터 원본*이라고도 합니다. 보고서에서 정의되어 해당 보고서에서만 사용되는 데이터 원본입니다.  
  
- **자격 증명.** 자격 증명은 외부 데이터 액세스를 위해 제공해야 하는 인증 정보입니다.  
  
##  <a name="tips-for-specifying-report-data"></a><a name="BkMk_ReportDataTips"></a> 보고서 데이터 지정 시 유용한 정보

 다음 정보를 사용하여 보고서 데이터 전략을 설계하십시오.  
  
- **데이터 원본** 보고서 서버 또는 SharePoint 사이트에 있는 보고서와 별도로 데이터 원본을 게시 및 관리할 수 있습니다. 각 데이터 원본의 경우 개발자나 데이터베이스 소유자가 한 장소에서 연결 정보를 관리할 수 있습니다. 데이터 원본 자격 증명은 보고서 서버에 안전하게 저장됩니다. 연결 문자열에 암호를 포함하지 마십시오. 데이터 원본을 테스트 서버에서 프로덕션 서버로 리디렉션할 수 있습니다. 데이터 원본을 비활성화하여 해당 데이터 원본을 사용하는 모든 보고서를 일시 중지할 수 있습니다.  
  
- **데이터 세트** 기반이 되는 공유 데이터 원본 또는 보고서와 별도로 데이터 세트를 게시 및 관리할 수 있습니다. 개발자 또는 데이터베이스 소유자는 보고서 작성자가 사용할 최적화된 쿼리를 제공할 수 있습니다. 쿼리를 변경하면 공유 데이터 세트를 사용하는 모든 보고서에 업데이트된 쿼리가 사용됩니다. 성능 향상을 위해 데이터 세트 캐싱을 활성화할 수 있습니다. 특정 시간 동안 쿼리 캐싱 일정을 예약하거나 공유 일정을 사용할 수 있습니다.  
  
- **보고서 파트에 사용되는 데이터** 보고서 파트는 기반이 되는 데이터를 포함할 수 있습니다. 보고서 파트에 대한 자세한 내용은 [보고서 디자이너의 보고서 파트&#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)를 참조하세요.  
  
- **데이터 필터링** 쿼리 또는 보고서의 보고서 데이터를 필터링할 수 있습니다. 데이터 세트 및 쿼리 변수를 사용하여 연계 매개 변수를 만들 수 있습니다. 사용자는 연계 매개 변수를 사용하여 수천 개의 선택 항목을 더 쉽게 관리할 수 있는 개수로 좁힐 수 있습니다. 매개 변수 값이나 지정하는 기타 값을 기반으로 테이블 또는 차트의 데이터를 필터링할 수 있습니다.  
  
- **매개 변수** 쿼리 변수를 포함하는 데이터 세트 쿼리 명령은 일치하는 보고서 매개 변수를 자동으로 만듭니다. 매개 변수를 직접 만들 수도 있습니다. 보고서를 볼 때 보고서 도구 모음에 매개 변수가 표시됩니다. 사용자는 보고서 데이터 또는 보고서 모양을 제어하는 값을 선택할 수 있습니다. 특정 대상을 위해 보고서 데이터를 사용자 지정하려면 동일한 보고서 정의에 다양한 기본값이 연결된 보고서 매개 변수 집합을 만들 수 있습니다. 기본 제공 **UserID** 필드를 사용하여 다른 대상 사용자를 위해 데이터를 사용자 지정할 수도 있습니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md) 및 [식의 기본 제공 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)을 참조하세요.  
  
- **데이터 경고** 보고서를 게시한 후 보고서 데이터를 기반으로 경고를 만들 수 있습니다. 그런 다음 사용자가 지정하는 규칙이 충족될 경우 이메일 메시지를 받습니다.  
  
- **데이터 그룹화 및 집계** 쿼리 또는 보고서의 보고서 데이터를 그룹화하고 집계할 수 있습니다. 쿼리의 값을 집계하는 경우 계속해서 유의미한 값 제약 조건 내에서 보고서에 값을 결합할 수 있습니다.  자세한 내용은 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) 및 [집계 함수&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-function.md)를 참조하세요.  
  
- **데이터 정렬** 쿼리 또는 보고서의 보고서 데이터를 정렬할 수 있습니다. 테이블에는 사용자가 정렬 순서를 제어할 수 있도록 대화형 정렬 단추를 추가할 수도 있습니다.  
  
- **식 기반 데이터** 대부분의 보고서 속성은 식 기반일 수 있고 식에는 데이터 세트 필드 및 보고서 매개 변수에 대한 참조를 포함할 수 있기 때문에 보고서 데이터 및 모양을 제어하는 강력한 식을 작성할 수 있습니다. 매개 변수 정의를 통해 표시할 데이터를 제어하는 기능을 사용자에게 제공할 수 있습니다.  
  
- **데이터 세트의 데이터 표시** 데이터 세트의 데이터는 일반적으로 테이블 및 차트와 같은 하나 이상의 데이터 영역에 표시됩니다.  
  
- **여러 데이터 세트의 데이터 표시**  데이터 영역에서 단일 데이터 세트를 기반으로 값을 조회하거나 다른 데이터 세트로 집계하는 식을 작성할 수 있습니다. 테이블에 단일 데이터 세트를 기반으로 하며 다양한 데이터 원본의 데이터를 표시하는 하위 보고서를 포함할 수 있습니다.  
  
 다음 목록을 사용하여 보고서의 데이터 원본을 정의할 수 있습니다.  
  
- 포함된 데이터 원본 및 데이터 세트를 사용할지 공유 데이터 원본 및 데이터 세트를 사용할지 고려합니다. 데이터 원본 소유자와 공동으로 작업하여 조직에 적합한 인증 및 권한 부여 기술을 구현하여 사용하십시오.  
  
- 소프트웨어 데이터 계층 아키텍처 및 데이터 형식에서 발생할 수 있는 문제에 대해 이해합니다. 데이터 확장 프로그램 및 데이터 처리 확장 프로그램이 쿼리 결과에 어떤 영향을 미치는지 이해합니다. 데이터 형식은 데이터 원본, 데이터 제공자, 보고서 정의 파일(.rdl)에 저장된 데이터 형식 사이에 서로 다릅니다.  
  
- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 클라이언트/서버 아키텍처 및 도구를 이해합니다. 예를 들어 보고서 디자이너에서 기본 제공 데이터 원본 유형을 사용하는 클라이언트 컴퓨터에 보고서를 작성합니다. 보고서를 게시하는 경우 데이터 원본 유형이 보고서 서버 또는 SharePoint 사이트에서 지원되어야 합니다.  자세한 내용은 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)을 참조하세요.  
  
- 데이터 원본 및 데이터 세트는 보고서에 작성되고 클라이언트 제작 도구에서 보고서 서버 또는 SharePoint 사이트로 게시됩니다. 데이터 원본을 보고서 서버에서 직접 만들 수 있습니다. 게시 후에는 보고서 서버에서 자격 증명 및 기타 속성을 구성할 수 있습니다. 자세한 내용은 [데이터 연결 문자열 만들기 - 보고서 작성기 및 SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 및 [Reporting Services 도구](../../reporting-services/tools/reporting-services-tools.md)를 참조하세요.  
  
- 사용할 수 있는 데이터 원본은 설치된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 확장 프로그램에 따라 다릅니다. 데이터 원본에 대한 지원은 클라이언트 제작 도구, 보고서 서버 버전 및 보고서 서버 플랫폼에 따라 다를 수 있습니다. 자세한 내용은 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)을 참조하세요.  
  
- 데이터 원본 자격 증명은 데이터 원본 유형별로 다르며 보고서를 클라이언트에서 보는지 아니면 보고서 서버 또는 SharePoint 사이트에서 보는지에 따라 다릅니다. 자세한 내용은 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md), [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) 및 [Reporting Services 도구](../../reporting-services/tools/reporting-services-tools.md)의 각 도구에 지정된 자격 증명 정보를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업

 데이터 연결 만들기, 외부 원본과 데이터 세트 및 쿼리에서 가져온 데이터 추가 등과 관련된 태스크입니다.  
  
|||  
|-|-|  
|**일반 태스크**|**연결**|  
|데이터 연결 만들기|[데이터 연결 문자열 만들기 - 보고서 작성기 및 SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)|  
|데이터 세트 및 쿼리 만들기|[보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|  
|게시 후 데이터 원본 관리|[보고서 데이터 원본 관리](../../reporting-services/report-data/manage-report-data-sources.md)|  
|게시 후 공유 데이터 세트 관리|[공유 데이터 세트 관리](../../reporting-services/report-data/manage-shared-datasets.md)|  
|데이터 경고 만들기 및 관리|[Reporting Services 데이터 경고](../../reporting-services/reporting-services-data-alerts.md)|  
|공유 데이터 세트 캐시|[공유 데이터 세트 캐시&#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)|  
|캐시를 미리 로드하도록 공유 데이터 세트 일정 예약|[일정](../../reporting-services/subscriptions/schedules.md)|  
|데이터 확장 프로그램 추가|[데이터 처리 확장 프로그램 구현](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)|