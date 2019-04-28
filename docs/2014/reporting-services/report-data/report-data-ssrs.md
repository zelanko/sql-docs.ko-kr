---
title: 보고서 데이터
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: reporting-services-2014, sql-server-2014
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 8c0a6ef25f33b5396ecea36edfd57ac3c42e8f5b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721409"
---
# <a name="report-data-in-sql-server-reporting-services-ssrs"></a>SSRS(SQL Server Reporting Services)의 보고서 데이터

  보고서 데이터는 조직의 다양한 데이터 원본에서 가져올 수 있습니다. 보고서 디자인의 첫 단계는 기본 보고서 데이터를 나타내는 데이터 원본 및 데이터 세트를 만드는 것입니다. 각 데이터 원본은 데이터 연결 정보를 포함합니다. 각 데이터 세트는 데이터 원본의 데이터로 사용할 필드 세트를 정의하는 쿼리 명령을 포함합니다. 각 데이터 세트의 데이터를 시각화하려면 테이블, 행렬, 차트 및 지도와 같은 데이터 영역을 추가합니다. 보고서를 처리하면 데이터 원본에 대한 쿼리가 실행되고 각 데이터 영역이 필요에 따라 확장되어 데이터 세트에 대한 쿼리 결과를 표시합니다.  
  
##  <a name="BkMk_ReportDataTerms"></a> 용어

 경우에 잘 알고 있다면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 개념에 다음 사용 약관을 검토 [Reporting Services 개념 &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md): *데이터 연결*, *포함 된 데이터 원본*, *공유 데이터 원본을*를 *포함 된 데이터 집합*를 *공유 데이터 집합*를 *데이터 집합 쿼리* 하십시오 *보고서 파트*, 및 *데이터 경고*합니다.  
  
##  <a name="BkMk_ReportDataTips"></a> 보고서 데이터 지정 시 유용한 정보

 다음 정보를 사용하여 보고서 데이터 전략을 설계하십시오.  
  
- **데이터 원본** 보고서 서버 또는 SharePoint 사이트에 있는 보고서와 별도로 데이터 원본을 게시 및 관리할 수 있습니다. 각 데이터 원본의 경우 개발자나 데이터베이스 소유자가 한 장소에서 연결 정보를 관리할 수 있습니다. 데이터 원본 자격 증명은 보고서 서버에 안전하게 저장됩니다. 연결 문자열에 암호를 포함하지 마십시오. 데이터 원본을 테스트 서버에서 프로덕션 서버로 리디렉션할 수 있습니다. 데이터 원본을 비활성화하여 해당 데이터 원본을 사용하는 모든 보고서를 일시 중지할 수 있습니다. 지원 되는 데이터 원본의 목록을 보려면 참조 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)합니다.  
  
- **데이터 집합** 기반이 되는 공유 데이터 원본 또는 보고서와 별도로 데이터 집합을 게시 및 관리할 수 있습니다. 개발자 또는 데이터베이스 소유자는 보고서 작성자가 사용할 최적화된 쿼리를 제공할 수 있습니다. 쿼리를 변경하면 공유 데이터 세트를 사용하는 모든 보고서에 업데이트된 쿼리가 사용됩니다. 성능 향상을 위해 데이터 세트 캐싱을 활성화할 수 있습니다. 특정 시간 동안 쿼리 캐싱 일정을 예약하거나 공유 일정을 사용할 수 있습니다.  
  
- **보고서 파트에 사용되는 데이터** 보고서 파트는 기반이 되는 데이터를 포함할 수 있습니다. 보고서 파트에 대한 자세한 내용은 [보고서 디자이너의 보고서 파트&#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md)를 참조하세요.  
  
- **데이터 필터링** 쿼리 또는 보고서의 보고서 데이터를 필터링할 수 있습니다. 데이터 세트 및 쿼리 변수를 사용하여 연계 매개 변수를 만들고, 사용자에게 수천 가지의 선택권을 좀 더 관리 가능한 수치로 좁히는 기능을 제공할 수 있습니다. 매개 변수 값이나 지정하는 기타 값을 기반으로 테이블 또는 차트의 데이터를 필터링할 수 있습니다.  
  
- **매개 변수** 쿼리 변수를 포함하는 데이터 집합 쿼리 명령은 일치하는 보고서 매개 변수를 자동으로 만듭니다. 매개 변수를 직접 만들 수도 있습니다. 보고서를 볼 때 보고서 도구 모음에 매개 변수가 표시됩니다. 사용자는 보고서 데이터 또는 보고서 모양을 제어하는 값을 선택할 수 있습니다. 특정 대상을 위해 보고서 데이터를 사용자 지정하려면 동일한 보고서 정의에 다양한 기본값이 연결된 보고서 매개 변수 집합을 만들거나 기본 제공 `UserID` 필드를 사용할 수 있습니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../report-design/report-parameters-report-builder-and-report-designer.md) 및 [식의 기본 제공 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md)을 참조하세요.  
  
- **데이터 경고** 보고서가 게시된 후 보고서 데이터를 기반으로 경고를 만들어 지정한 규칙에 부합하는 경우 전자 메일 메시지를 수신할 수 있습니다.  
  
- **데이터 그룹화 및 집계** 쿼리 또는 보고서의 보고서 데이터를 그룹화하고 집계할 수 있습니다. 쿼리의 값을 집계하는 경우 계속해서 유의미한 값 제약 조건 내에서 보고서에 값을 결합할 수 있습니다.  자세한 내용은 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) 및 [집계 함수&#40;보고서 작성기 및 SSRS&#41;](../report-design/report-builder-functions-aggregate-function.md)를 참조하세요.  
  
- **데이터 정렬** 쿼리 또는 보고서의 보고서 데이터를 정렬할 수 있습니다. 테이블에는 사용자가 정렬 순서를 제어할 수 있도록 대화형 정렬 단추를 추가할 수도 있습니다.  
  
- **식 기반 데이터** 대부분의 보고서 속성은 식 기반일 수 있고 식에는 데이터 집합 필드 및 보고서 매개 변수에 대한 참조를 포함할 수 있기 때문에 보고서 데이터 및 모양을 제어하는 강력한 식을 작성할 수 있습니다. 매개 변수 정의를 통해 표시할 데이터를 제어하는 기능을 사용자에게 제공할 수 있습니다.  
  
- **데이터 집합의 데이터 표시** 데이터 집합의 데이터는 일반적으로 테이블 및 차트와 같은 하나 이상의 데이터 영역에 표시됩니다.  
  
- **여러 데이터 집합의 데이터 표시**  데이터 영역에서 단일 데이터 집합을 기반으로 값을 조회하거나 다른 데이터 집합으로 집계하는 식을 작성할 수 있습니다. 테이블에 단일 데이터 세트를 기반으로 하며 다양한 데이터 원본의 데이터를 표시하는 하위 보고서를 포함할 수 있습니다.  
  
## <a name="data-connections-data-sources-and-datasets"></a>데이터 연결, 데이터 원본 및 데이터 세트

 다음 목록을 사용하여 보고서의 데이터 원본을 정의할 수 있습니다.  
  
- 포함된 데이터 원본 및 데이터 세트를 사용할지 공유 데이터 원본 및 데이터 세트를 사용할지 고려합니다. 데이터 원본 소유자와 공동으로 작업하여 조직에 적합한 인증 및 권한 부여 기술을 구현하여 사용하십시오.  
  
- 소프트웨어 데이터 계층 아키텍처 및 데이터 형식에서 발생할 수 있는 문제에 대해 이해합니다. 데이터 확장 프로그램 및 데이터 처리 확장 프로그램이 쿼리 결과에 어떤 영향을 미치는지 이해합니다. 데이터 형식은 데이터 원본, 데이터 제공자, 보고서 정의 파일(.rdl)에 저장된 데이터 형식 사이에 서로 다릅니다.  
  
- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 클라이언트/서버 아키텍처 및 도구를 이해합니다. 예를 들어 보고서 디자이너에서 기본 제공 데이터 원본 유형을 사용하는 클라이언트 컴퓨터에 보고서를 작성합니다. 보고서를 게시하는 경우 데이터 원본 유형이 보고서 서버 또는 SharePoint 사이트에서 지원되어야 합니다.  자세한 내용은 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../create-deploy-and-manage-mobile-and-paginated-reports.md)을 참조하세요.  
  
- 데이터 원본 및 데이터 세트는 보고서에 작성되고 클라이언트 제작 도구에서 보고서 서버 또는 SharePoint 사이트로 게시됩니다. 데이터 원본을 보고서 서버에서 직접 만들 수 있습니다. 게시 후에는 보고서 서버에서 자격 증명 및 기타 속성을 구성할 수 있습니다. 자세한 내용은 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) 하 고 [Reporting Services 도구](../tools/reporting-services-tools.md)합니다.  
  
- 사용할 수 있는 데이터 원본은 설치된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 확장 프로그램에 따라 다릅니다. 데이터 원본에 대한 지원은 클라이언트 제작 도구, 보고서 서버 버전 및 보고서 서버 플랫폼에 따라 다를 수 있습니다. 자세한 내용은 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../create-deploy-and-manage-mobile-and-paginated-reports.md)을 참조하세요.  
  
- 데이터 원본 자격 증명은 데이터 원본 유형별로 다르며 보고서를 클라이언트에서 보는지 아니면 보고서 서버 또는 SharePoint 사이트에서 보는지에 따라 다릅니다. 자세한 내용은 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../security/set-permissions-for-report-server-items-on-a-sharepoint-site.md), [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../integration-services/connection-manager/data-sources.md) 및 [Reporting Services 도구](../tools/reporting-services-tools.md)의 각 도구에 지정된 자격 증명 정보를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업

 데이터 연결 만들기, 외부 원본과 데이터 세트 및 쿼리에서 가져온 데이터 추가 등과 관련된 태스크입니다.  
  
|||  
|-|-|  
|**일반 태스크**|**링크**|  
|데이터 연결 만들기|[보고서 서비스의 데이터 연결, 데이터 원본 및 연결 문자열](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|데이터 세트 및 쿼리 만들기|[보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|  
|게시 후 데이터 원본 관리|[보고서 데이터 원본 관리](manage-report-data-sources.md)|  
|게시 후 공유 데이터 세트 관리|[공유 데이터 집합 관리](manage-shared-datasets.md)|  
|데이터 경고 만들기 및 관리|[Reporting Services 데이터 경고](../tutorial-creating-a-basic-table-report-report-builder.md)|  
|공유 데이터 세트 캐시|[공유 데이터 세트 캐시&amp;#40;SSRS&amp;#41;](../report-server/cache-shared-datasets-ssrs.md)|  
|캐시를 미리 로드하도록 공유 데이터 세트 일정 예약|[일정](../subscriptions/schedules.md)|  
|데이터 확장 프로그램 추가|[데이터 처리 확장 프로그램 구현](../extensions/data-processing/implementing-a-data-processing-extension.md)|