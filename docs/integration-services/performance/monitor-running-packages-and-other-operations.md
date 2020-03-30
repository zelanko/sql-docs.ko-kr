---
title: 실행 중인 패키지 및 기타 작업 모니터링 | Microsoft Docs
ms.custom: supportability
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isoperations.executions.f1
- sql13.ssis.ssms.isoperations.general.f1
ms.assetid: cbbcd79f-ab9b-46ec-84cb-4821c1d16b99
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d7fd62f4f2f82e6dcc3921db7099b4f052db27b3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79287847"
---
# <a name="monitor-running-packages-and-other-operations"></a>실행 중인 패키지 및 기타 작업 모니터링

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  다음 도구 중 하나 이상을 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 실행, 프로젝트 유효성 검사 및 기타 작업을 모니터링할 수 있습니다. 데이터 탭과 같은 일부 도구는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포된 프로젝트에 대해서만 사용할 수 있습니다.  
  
-   로그  
  
     자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
-   보고서  
  
     자세한 내용은 [Reports for the Integration Services Server](#reports)을(를) 참조하세요.  
  
-   뷰  
  
     자세한 내용은 [뷰&#40;Integration Services 카탈로그&#41;](../../integration-services/system-views/views-integration-services-catalog.md)를 참조하세요.  
  
-   성능 카운터  
  
     자세한 내용은 [성능 카운터](../../integration-services/performance/performance-counters.md)를 참조하세요.  
  
-   데이터 탭  

> [!NOTE]
> 이 문서에서는 SSIS 패키지 실행을 일반적으로 모니터링하는 방법 및 온-프레미스에서 패키지 실행을 모니터링하는 방법을 설명합니다. 또한 Azure SQL Database에서 SSIS 패키지를 실행 및 모니터링할 수도 있습니다. 자세한 내용은 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)를 참조하세요.
>
> Linux에서 SSIS 패키지를 실행할 수 있더라도 Linux에서 모니터링 도구가 제공되지 않습니다. 자세한 내용은 [Linux에서 SSIS를 사용하여 데이터 추출, 변환 및 로드](../../linux/sql-server-linux-migrate-ssis.md)를 참조하세요.

## <a name="operation-types"></a>작업 유형  
 여러 유형의 작업이 **서버의** SSISDB [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에서 모니터링됩니다. 각 작업과 연관된 메시지가 여러 개 있을 수 있습니다. 각 메시지는 여러 가지 유형 중 하나로 분류될 수 있습니다. 예를 들어 정보, 경고 또는 오류 메시지일 수 있습니다. 메시지 유형에 대한 전체 목록은 Transact-SQL [catalog.operation_messages&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md) 뷰를 참조하세요. 작업 유형에 대한 전체 목록은 [catalog.operations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)를 참조하세요.  
  
 한 작업의 상태를 나타내기 위해 9가지 상태 유형이 사용됩니다. 상태 유형에 대한 전체 목록은 [catalog.operations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 뷰를 참조하세요.  

## <a name="active-operations-dialog-box"></a><a name="active_ops"></a> 활성 작업 대화 상자
  **활성 작업** 대화 상자를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서 현재 실행 중인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 작업(예: 배포, 유효성 검사 및 패키지 실행)의 상태를 볼 수 있습니다. 이 데이터는 SSISDB 카탈로그에 저장됩니다.  
  
 관련된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 뷰에 대한 자세한 내용은 [catalog.operations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md), [catalog.validations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md) 및 [catalog.executions&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)를 참조하세요.  
  
###  <a name="open-the-active-operations-dialog-box"></a><a name="open_dialog"></a> 활성 작업 대화 상자 열기  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]열기  
  
2.  Microsoft SQL Server 데이터베이스 엔진 연결  
  
3.  개체 탐색기에서 **Integration Services** 노드를 확장하고 **SSISDB**를 마우스 오른쪽 단추로 클릭한 다음 **활성 작업**을 클릭합니다.  
  
### <a name="configure-the-options"></a>옵션 구성  
  
 **형식**  
 작업 유형을 지정합니다. 다음은 **유형** 필드의 가능한 값과 Transact-SQL **catalog.operations** 뷰의 operations_type 열에 표시되는 해당 값입니다.  
  
|||  
|-|-|  
|Integration Services 초기화|1|  
|작업 정리(SQL 에이전트 작업)|2|  
|프로젝트 버전 정리(SQL 에이전트 작업)|3|  
|프로젝트 배포|101|  
|프로젝트 복원|106|  
|패키지 실행 생성 및 시작|200|  
|작업 중지(유효성 검사 또는 실행 중지)|202|  
|프로젝트 유효성 검사|300|  
|패키지 유효성 검사|301|  
|카탈로그 구성|1000|  
  
 **중지**  
 현재 실행 중인 작업을 중지하려면 클릭합니다.  

## <a name="viewing-and-stopping-packages-running-on-the-integration-services-server"></a>Integration Services 서버에서 실행 중인 패키지 보기 및 중지
  **SSISDB** 데이터베이스는 사용자에게 표시되지 않는 내부 테이블에 실행 기록을 저장합니다. 그러나 공용 뷰 쿼리를 통해 이 데이터베이스에서 필요한 정보를 얻을 수 있습니다. 또한 이 데이터베이스는 패키지와 관련된 일반적인 태스크를 수행하기 위해 호출할 수 있는 저장 프로시저를 제공합니다.  
  
 일반적으로 서버의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 관리합니다. 그러나 데이터베이스 뷰를 쿼리하고 저장 프로시저를 직접 호출하거나 관리되는 API를 호출하는 사용자 지정 코드를 작성할 수도 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 관리되는 API는 뷰를 쿼리하고 저장 프로시저를 호출하여 많은 태스크를 수행합니다. 예를 들어 서버에서 현재 실행 중인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 목록을 보고 필요한 경우 패키지를 중지하도록 요청할 수 있습니다.  
  
### <a name="viewing-the-list-of-running-packages"></a>실행 중인 패키지 목록 보기  
 서버에서 현재 실행 중인 패키지 목록을 **활성 작업** 대화 상자에서 볼 수 있습니다. 자세한 내용은 [Active Operations Dialog Box](#active_ops)를 참조하세요.  
  
 실행 중인 패키지 목록을 보는 데 사용할 수 있는 다른 방법은 다음 항목을 참조하십시오.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스  
 서버에서 실행 중인 패키지 목록을 보려면 상태가 2인 패키지에 대해 [catalog.executions&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md) 뷰를 쿼리합니다.  
  
 관리되는 API를 통해 프로그래밍 방식으로 액세스  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스 및 해당 클래스를 참조하세요.  
  
### <a name="stopping-a-running-package"></a>실행 중인 패키지 중지  
 **활성 작업** 대화 상자에서 실행 중인 패키지를 중지하도록 요청할 수 있습니다. 자세한 내용은 [Active Operations Dialog Box](#active_ops)를 참조하세요.  
  
 실행 중인 패키지를 중지하는 데 사용할 수 있는 다른 방법은 다음 항목을 참조하십시오.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스  
 서버에서 실행 중인 패키지를 중지하려면 [catalog.stop_operation&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md) 저장 프로시저를 호출합니다.  
  
 관리되는 API를 통해 프로그래밍 방식으로 액세스  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스 및 해당 클래스를 참조하세요.  
  
### <a name="viewing-the-history-of-packages-that-have-run"></a>실행된 패키지 기록 보기  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 실행된 패키지의 기록을 보려면 **모든 실행** 보고서를 사용합니다. **모든 실행** 보고서 및 다른 표준 보고서에 대한 자세한 내용은 [Integration Services 서버를 위한 보고서](#reports)를 참조하세요.  
  
 실행 중인 패키지의 기록을 보는 데 사용할 수 있는 다른 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스  
 실행된 패키지에 대한 정보를 보려면 [catalog.executions&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md) 뷰를 쿼리합니다.  
  
 관리되는 API를 통해 프로그래밍 방식으로 액세스  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스 및 해당 클래스를 참조하세요.  

## <a name="reports-for-the-integration-services-server"></a><a name="reports"></a> Reports for the Integration Services Server
  현재 릴리스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 서버에 배포된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 모니터링하는 데 도움이 되는 표준 보고서를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 사용할 수 있습니다. 이러한 보고서는 패키지 상태 및 기록을 보고 필요한 경우 패키지 실행 실패 원인을 파악하는 데 도움이 됩니다.  
  
 각 보고서 페이지의 위쪽에서 뒤로 아이콘을 클릭하면 확인한 이전 페이지로 이동하고, 새로 고침 아이콘을 클릭하면 페이지에 표시된 정보가 새로 고쳐지며, 인쇄 아이콘을 사용하면 현재 페이지를 인쇄할 수 있습니다.  
  
 패키지를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포하는 방법은 [Integration Services(SSIS) 프로젝트 및 패키지 배포](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)를 참조하세요.  
  
### <a name="integration-services-dashboard"></a>통합 서비스 대시보드  
 **Integration Services 대시보드** 보고서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 패키지 실행에 대한 개요를 제공합니다. 대시보드에서는 서버에서 실행된 각 패키지를 "확대"하여 발생했을 수 있는 패키지 실행 오류에 대한 특정 세부 정보를 찾을 수 있습니다.  
  
 보고서에는 다음과 같은 정보 섹션이 표시됩니다.  
  
|섹션|Description|  
|-------------|-----------------|  
|**실행 정보**|지난 24시간 동안 서로 다른 상태의 여러 실행 개수를 보여 줍니다(실패, 실행 중, 성공 등).|  
|**패키지 정보**|지난 24시간 동안 실행된 총 패키지 수를 보여 줍니다.|  
|**연결 정보**|지난 24시간 동안 실패한 실행에 사용된 연결을 보여 줍니다.|  
|**패키지 세부 정보**|지난 24시간 동안 발생한 완료된 실행에 대한 세부 정보를 보여 줍니다. 예를 들어 이 섹션에서는 실패한 실행 수, 총 실행 수, 실행 기간(초), 과거 3개월 동안의 평균 실행 기간을 보여 줍니다.<br /><br /> **개요**, **모든 메시지**및 **실행 성능**을 클릭하면 패키지에 대한 추가 정보를 볼 수 있습니다.<br /><br /> **실행 성능** 보고서에서는 마지막 실행 인스턴스의 기간뿐 아니라 시각 및 종료 시간과 적용된 환경도 보여 줍니다.<br /><br /> **실행 성능** 보고서에 포함된 차트 및 연결된 테이블에서는 지난 10개의 성공한 패키지 실행 기간을 보여 줍니다. 또한 이 테이블에서는 3개월 동안의 평균 실행 기간도 보여 줍니다. 이러한 10개의 성공한 패키지 실행에는 런타임에 서로 다른 환경 및 리터럴 값이 적용되었을 수 있습니다.<br /><br /> 끝으로 **실행 성능** 보고서에는 패키지 데이터 흐름 구성 요소의 활성 시간 및 총 시간이 표시됩니다. 활성 시간은 모든 단계에서 구성 요소가 실행하는 데 걸린 총 시간을 의미하고, 총 시간은 구성 요소에 대해 경과된 총 시간을 의미합니다. 이 보고서에는 마지막 패키지 실행의 로깅 수준이 성능 또는 자세히로 설정된 경우 패키지 구성 요소에 대해 이 정보만 표시됩니다.<br /><br /> **개요** 보고서에는 패키지 태스크의 상태가 표시됩니다. **메시지** 보고서에는 패키지 및 태스크(예: 시작 및 종료 시간과 작성된 행 수 보고)에 대한 모든 이벤트 메시지 및 오류 메시지가 표시됩니다.<br /><br /> **개요** 보고서에서 **메시지 보기** 를 클릭하여 **메시지** 보고서로 이동할 수도 있습니다. **메시지** 보고서에서 **개요 보기** 를 클릭하여 **개요** 보고서로 이동할 수도 있습니다.|  
  
 **필터** 를 클릭한 다음 **필터 설정** 대화 상자에서 조건을 선택하여 페이지에 표시되는 테이블을 필터링할 수 있습니다. 사용 가능한 필터 조건은 표시되고 있는 데이터에 따라 달라집니다. **필터 설정** 대화 상자에서 정렬 아이콘을 클릭하여 보고서의 정렬 순서를 변경할 수 있습니다.  
  
### <a name="all-executions-report"></a>모든 실행 보고서  
 **모든 실행 보고서** 에는 서버에서 수행된 모든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 실행에 대한 요약 내용이 표시됩니다. 동일한 패키지의 실행이 여러 개 있을 수 있습니다. **Integration Services 대시보드** 보고서와 달리 특정 날짜 범위 동안 시작된 실행을 표시하도록 **모든 실행** 보고서를 구성할 수 있습니다. 날짜 범위는 수 일, 수 개월 또는 수 년으로 지정할 수 있습니다.  
  
 보고서에는 다음과 같은 정보 섹션이 표시됩니다.  
  
|섹션|Description|  
|-------------|-----------------|  
|Assert|보고서에 적용된 현재 필터(예: 시작 시간 범위)를 보여 줍니다.|  
|실행 정보|각 패키지 실행의 시작 시간, 종료 시간 및 기간을 보여 줍니다. 패키지 실행 태스크를 사용하여 자식 패키지에 전달된 값과 같이 패키지 실행과 함께 사용된 매개 변수 값의 목록을 볼 수도 있습니다. 매개 변수 목록을 보려면 개요를 클릭합니다.|  
  
 패키지 실행 태스크를 사용하여 자식 패키지에 값을 제공하는 방법에 대한 자세한 내용은 [Execute Package Task](../../integration-services/control-flow/execute-package-task.md)를 참조하십시오.  
  
 매개 변수에 대한 자세한 내용은 [Integration Services(SSIS) 패키지 및 프로젝트 매개 변수](../../integration-services/integration-services-ssis-package-and-project-parameters.md)를 참조하세요.  
  
### <a name="all-connections"></a>모든 연결  
 **모든 연결** 보고서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 발생한 실행 및 실패한 연결에 대해 다음 정보를 제공합니다.  
  
 보고서에는 다음과 같은 정보 섹션이 표시됩니다.  
  
|섹션|Description|  
|-------------|-----------------|  
|Assert|보고서에 적용된 현재 필터(예: 지정된 문자열이 있는 연결 및 **마지막으로 실패한 시간** 범위)를 보여 줍니다.<br /><br /> **마지막으로 실패한 시간** 범위를 설정하면 특정 날짜 범위 동안 발생한 연결 실패만 표시됩니다. 날짜 범위는 수 일, 수 개월 또는 수 년으로 지정할 수 있습니다.|  
|세부 정보|연결 문자열, 연결 실패 기간 동안의 실행 수 및 연결이 마지막으로 실패한 날짜를 보여 줍니다.|  
  
### <a name="all-operations-report"></a>모든 작업 보고서  
 **모든 작업 보고서** 에는 패키지 배포, 유효성 검사 및 실행과 기타 관리 작업을 비롯하여 서버에서 수행된 모든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 작업에 대한 요약이 표시됩니다. Integration Services 대시보드를 사용하는 경우와 마찬가지로 테이블에 필터를 적용하여 표시되는 정보를 좁힐 수 있습니다.  
  
### <a name="all-validations-report"></a>모든 유효성 검사 보고서  
 **모든 유효성 검사 보고서** 에는 서버에서 수행된 모든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 유효성 검사에 대한 요약 내용이 표시됩니다. 요약 내용으로는 상태, 시작 시간 및 종료 시간과 같은 각 유효성 검사에 대한 정보가 표시됩니다. 각 요약 항목에는 유효성 검사 중 생성된 메시지에 대한 링크가 포함됩니다. Integration Services 대시보드를 사용하는 경우와 마찬가지로 테이블에 필터를 적용하여 표시되는 정보를 좁힐 수 있습니다.  
  
### <a name="custom-reports"></a>사용자 지정 보고서  
 **Integration Services 카탈로그** 노드 아래의 **SSISDB**[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]카탈로그 노드에 사용자 지정 보고서(.rdl 파일)를 추가할 수 있습니다. 보고서를 추가하기 전에 세 부분으로 이루어진 명명 규칙을 사용하여 원본 테이블과 같은 참조 개체를 정규화하고 있는지 확인합니다. 그렇지 않으면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 오류를 표시합니다. 명명 규칙은 \<데이터베이스>.\<소유자>.\<개체>입니다. 일례로 SSISDB.internal.executions를 들 수 있습니다.  
  
> [!NOTE]  
>  **데이터베이스** 노드 아래의 **SSISDB** 노드에 사용자 지정 보고서를 추가한 경우에는 SSISDB 접두사가 필요하지 않습니다.  
  
 사용자 지정 보고서를 만들고 추가하는 방법은 [Add a Custom Report to Management Studio](../../ssms/object/add-a-custom-report-to-management-studio.md)를 참조하십시오.  

## <a name="view-reports-for-the-integration-services-server"></a>Integration Services 서버용 보고서 보기
  현재 릴리스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 서버에 배포된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 모니터링하는 데 도움이 되는 표준 보고서를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 사용할 수 있습니다.  보고서에 대한 자세한 내용은 [Integration Services 서버를 위한 보고서](#reports)를 참조하세요.  
  
### <a name="to-view-reports-for-the-integration-services-server"></a>Integration Services 서버용 보고서를 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **Integration Services 카탈로그** 노드를 확장합니다.  
  
2.  **SSISDB**를 마우스 오른쪽 단추로 클릭하고 **보고서**, **표준 보고서**를 차례로 클릭합니다.  
  
3.  보고서를 보려면 다음 중 하나 이상을 클릭합니다.  
  
    -   **통합 서비스 대시보드**  
  
    -   **모든 실행**  
  
    -   **모든 유효성 검사**  
  
    -   **모든 작업**  
  
    -   **모든 연결**  

## <a name="see-also"></a>참고 항목  
 [프로젝트 및 패키지 실행](../packages/deploy-integration-services-ssis-projects-and-packages.md)   
 [패키지 실행 문제 해결 보고서](../troubleshooting/troubleshooting-reports-for-package-execution.md)  
