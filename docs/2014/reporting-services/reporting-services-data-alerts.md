---
title: Reporting Services 데이터 경고 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 8c234077-b670-45c0-803f-51c5a5e0866e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6478be669b53cd4d1a919ff6142be834de187dcc
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177133"
---
# <a name="reporting-services-data-alerts"></a>Reporting Services 데이터 경고
  
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 데이터 경고는 사용자가 관심을 가지고 있거나 사용자에게 중요한 보고서 데이터에 대한 정보를 적절한 시간에 받아 볼 수 있게 해주는 데이터 기반의 경고 솔루션입니다. 데이터 경고를 사용하면 정보를 자동으로 받아 볼 수 있으므로 더 이상 정보를 직접 찾을 필요가 없습니다.

 데이터 경고 메시지는 전자 메일로 전송됩니다. 정보의 중요도에 따라 메시지를 자주 보내거나 가끔 보내도록 선택하고 결과가 변경될 경우에만 메시지를 보내도록 선택할 수 있습니다. 전자 메일 받는 사람을 여러 명 지정하고 다른 사람들에게도 정보를 알려 효율성 및 협업을 향상시킬 수 있습니다.

||
|-|
|**[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 모드|

##  <a name="AlertingWF"></a>데이터 경고 아키텍처 및 워크플로
 다음은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 데이터 경고의 주요 영역을 요약한 것입니다.

-   **데이터 경고 정의 정의 및 저장**-보고서를 실행 하 고, 흥미로운 데이터 값을 식별 하는 규칙을 만들고, 데이터 경고 메시지를 보내는 되풀이 패턴을 정의 하 고, 경고 메시지의 받는 사람을 지정 합니다.

-   **데이터 경고 정의 실행**-경고 서비스는 예약 된 시간에 경고 정의를 처리 하 고, 보고서 데이터를 검색 하 고, 경고 정의의 규칙을 기반으로 데이터 경고 인스턴스를 만듭니다.

-   **받는 사람에 게 데이터 경고 메시지 배달**-경고 서비스는 경고 인스턴스를 만들고 받는 사람에 게 전자 메일로 경고 메시지를 보냅니다.

 또한 데이터 경고 소유자는 자신의 데이터 경고에 대한 정보를 확인하고 해당 데이터 경고 정의를 삭제 및 편집할 수 있습니다. 경고에는 한 명의 소유자(경고를 만든 사용자)가 있습니다.

 경고 관리자(SharePoint 경고 관리 권한이 있는 사용자)는 사이트 수준에서 데이터 경고를 관리할 수 있습니다. 이러한 사용자는 각 사이트 사용자별로 경고 목록을 보고 경고를 삭제할 수 있습니다.

 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 데이터 경고는 SharePoint 경고와 다릅니다. 보고서를 포함하여 모든 문서 유형에 따라 SharePoint 경고를 정의할 수 있습니다. 문서가 변경되면 SharePoint 경고가 전송됩니다. 예를 들어 보고서의 테이블에 열을 추가할 수 있습니다. 하지만 데이터 경고는 보고서에 표시된 데이터가 경고 정의의 규칙을 만족할 때 전송됩니다. 규칙은 일반적으로 보고서에 표시되는 데이터를 참조합니다.

 보고서에 대해 데이터 경고를 만들면 보고서 데이터의 변경 내용을 모니터링하고, 자신 및 다른 사용자가 관심을 가지고 있는 데이터를 정의하는 규칙을 보고서 데이터가 따를 경우 비즈니스 요구에 맞는 간격에 따라 전자 메일로 데이터 경고 메시지를 보낼 수 있습니다. 또한 요청 시 데이터 경고를 실행할 수 있습니다. SharePoint 경고 만들기 권한이 있으면 보기 권한이 있는 모든 보고서에 대해 경고를 만들 수 있습니다. 사용자가 보고서에 여러 개의 경고를 만들 수 있으며, 여러 사용자가 보고서에서 동일한 경고 또는 서로 다른 경고를 만들 수 있습니다. 다른 사용자와의 공동 작업을 위해 자신이 만드는 데이터 경고 정의에 있는 경고 메시지의 받는 사람으로 다른 사용자를 지정할 수 있습니다.

 다음 다이어그램에서는 데이터 경고 정의를 생성 및 저장하고, 데이터 경고 인스턴스 처리를 시작할 SQL 에이전트 작업을 만들고, 경고를 트리거한 보고서 데이터가 포함된 데이터 경고 메시지를 하나 이상의 받는 사람에게 전자 메일로 보내는 작업에 대한 워크플로를 보여 줍니다.

 ![Reporting Services 경고의 워크플로](media/rs-alertingworkflow.gif "Reporting Services 경고의 워크플로")

### <a name="reports-supported-by-data-alerts"></a>데이터 경고가 지원되는 보고서
 RDL(Report Definition Language)로 작성되고 보고서 디자이너 또는 보고서 작성기에서 만든 모든 전문적인 유형의 보고서에서 데이터 경고를 만들 수 있습니다. 여기에는 테이블 및 차트와 같은 데이터 영역이 포함된 보고서, 하위 보고서가 포함된 보고서, 여러 병렬 열 그룹 및 중첩된 데이터 영역이 들어 있는 복잡한 보고서가 포함됩니다. 단, 보고서에 하나 이상의 데이터 영역 유형을 포함하고 보고서 데이터 원본이 저장된 자격 증명을 사용하거나 자격 증명을 아예 사용하지 않도록 구성해야 합니다. 보고서에 데이터 영역이 없으면 보고서에 대해 경고를 만들 수 없습니다.

 
  [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]로 만든 보고서에서는 데이터 경고를 만들 수 없습니다.

 기본 모드 또는 SharePoint 모드로 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 를 설치하거나 보고서 작성기의 독립 실행형 버전을 사용하는 경우 보고서를 보고서 서버, 자신의 컴퓨터 또는 SharePoint 라이브러리에 저장할 수 있습니다. 보고서에 대해 데이터 경고를 만들려면 보고서를 SharePoint 라이브러리에 업로드하거나 저장해야 합니다. 즉, 기본 모드로 보고서 서버에 저장되거나 자신의 컴퓨터에 저장된 보고서에 대해서는 경고를 만들 수 없습니다. 또한 사용자 지정 애플리케이션에 포함된 경고는 만들 수 없습니다.

 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 는 보고서의 다양한 자격 증명 유형을 지원합니다. 저장된 자격 증명을 사용하거나 자격 증명을 아예 사용하지 않도록 구성된 데이터 원본이 포함된 보고서에 대해 데이터 경고를 만들 수 있습니다. 통합 보안 자격 증명을 사용하거나 자격 증명을 요청하도록 구성된 보고서에 대해서는 경고를 만들 수 없습니다. 보고서는 경고 정의를 처리하는 중에 실행되며 자격 증명이 없으면 처리가 실패합니다. 자세한 내용은 

-   [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](report-data/specify-credential-and-connection-information-for-report-data-sources.md)

-   [역할 및 권한&#40;Reporting Services&#41;](security/roles-and-permissions-reporting-services.md)

-   [보고서 서버 인증](security/authentication-with-the-report-server.md)

### <a name="run-reports"></a>보고서 실행
 데이터 경고 정의를 만드는 첫 번째 단계는 원하는 보고서를 SharePoint 라이브러리에서 찾은 다음 해당 보고서를 실행하는 것입니다. 실행 중에 보고서에 데이터가 포함되지 않은 경우에는 해당 보고서에 대해 경고를 만들 수 없습니다.

 보고서에 매개 변수가 있으면 보고서 실행 시 사용할 매개 변수 값을 지정해야 합니다. 매개 변수 값은 보고서에 대해 만드는 데이터 경고 정의에 저장됩니다. 이러한 값은 데이터 경고 정의 처리 단계의 일환으로 보고서를 다시 실행할 때 사용됩니다. 매개 변수 값을 변경하려는 경우 해당 매개 변수 값을 사용하여 보고서를 다시 실행하고 해당 보고서 버전에 대해 경고 정의를 만들어야 합니다.

### <a name="create-data-alert-definitions"></a>데이터 경고 정의 만들기
 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 데이터 경고 기능에는 데이터 경고 정의를 만드는 데 사용하는 데이터 경고 디자이너가 포함되어 있습니다.

 데이터 경고 정의를 만들려면 보고서를 실행한 다음 SharePoint 보고서 뷰어의 **동작** 메뉴에서 데이터 경고 디자이너를 엽니다. 보고서에 대한 보고서 데이터 피드가 생성되고 데이터 피드의 처음 100개 행이 데이터 경고 디자이너에서 데이터 미리 보기 테이블에 표시됩니다. 보고서의 모든 데이터 피드는 사용자가 데이터 경고 디자이너에서 경고 정의를 작업 중인 한 캐시됩니다. 캐시 기능을 사용하면 데이터 피드 간에 빠르게 전환할 수 있습니다. 경고 정의를 데이터 경고 디자이너에서 다시 열면 데이터 피드가 새로 고쳐집니다.

 데이터 경고 정의는 데이터 경고 메시지를 트리거하기 위해 보고서 데이터가 만족해야 하는 규칙 및 절, 경고 메시지를 보낼 빈도를 정의하는 일정, 경고 메시지 보내기를 시작 및 중지할 날짜(옵션), 경고 메시지에 포함할 제목 줄과 설명 등의 정보, 메시지를 받는 사람으로 구성됩니다. 경고 정의를 만든 후에는 SQL Server 경고 데이터베이스에 저장합니다.

### <a name="save-data-alert-definitions-and-alerting-metadata"></a>데이터 경고 정의 및 경고 메타데이터 저장
 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 를 SharePoint 모드로 설치한 경우 SQL Server 경고 데이터베이스가 자동으로 생성됩니다.

 데이터 경고 정의 및 경고 메타데이터는 경고 데이터베이스에 저장됩니다. 기본적으로 이 데이터베이스 이름은 ReportingServices\<GUID>_Alerting으로 지정됩니다.

 데이터 경고 정의를 저장하면 경고 정의에 대한 SQL Server 에이전트 작업이 생성됩니다. 작업에는 작업 일정이 포함됩니다. 일정은 사용자가 경고 정의에 지정하는 되풀이 패턴을 기반으로 합니다. 작업을 실행하면 데이터 경고 정의에 대한 처리가 시작됩니다.

### <a name="process-data-alert-definitions"></a>데이터 경고 정의 처리
 SQL Server 에이전트 작업의 일정에 따라 경고 정의 처리가 시작되면 보고서가 실행되어 보고서 데이터 피드가 새로 고쳐집니다. 경고 서비스는 데이터 피드를 읽고 데이터 경고 정의로 지정되는 규칙을 데이터 값에 적용합니다. 하나 이상의 데이터 값이 규칙을 만족하면 데이터 경고 인스턴스가 생성되고 경고 결과가 포함된 데이터 경고 메시지가 모든 받는 사람에게 전자 메일로 전송됩니다. 결과는 경고 인스턴스가 생성된 시점에 모든 규칙을 만족한 보고서 데이터의 행입니다. 동일한 결과가 포함된 경고 메시지를 여러 번 받지 않으려면 결과가 변경될 때만 메시지가 전송되도록 지정합니다. 이 경우 경고 인스턴스가 생성되어 경고 데이터베이스에 저장되지만 경고 메시지는 생성되지 않습니다. 오류가 발생할 경우에도 경고 인스턴스가 경고 데이터베이스에 저장되고 오류 정보가 포함된 경고 메시지가 받는 사람에게 전송됩니다. 로깅 및 문제 해결에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 진단 및 로깅 섹션을 참조하세요.

### <a name="send-data-alert-messages"></a>데이터 경고 메시지 보내기
 데이터 경고 메시지는 전자 메일로 전송됩니다.

 
  **보낸 사람** 줄에는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 전자 메일 배달 구성으로 제공된 값이 포함됩니다. 
  **받는 사람** 줄에는 데이터 경고 디자이너에서 경고를 만들 때 지정한 받는 사람이 나열됩니다.

 데이터 경고 메시지에는 데이터 경고 디자이너에서 지정하는 전자 메일 제목 줄뿐만 아니라 다음과 같은 정보가 포함됩니다.

-   데이터 경고 정의를 만든 사용자의 이름

-   경고 정의에 설명을 지정한 경우 설명이 전자 메일 텍스트의 맨 위에 표시됨

-   경고 결과(경고 정의에 지정된 규칙을 만족하는 보고서 데이터 피드의 행으로 구성됨)

-   경고 정의 작성 시 사용된 보고서에 대한 링크

-   경고 정의의 규칙

-   보고서를 실행하는 데 사용한 매개 변수 및 값

-   보고서 데이터 영역 밖에 있는 보고서 항목의 컨텍스트 값

 데이터 경고 인스턴스 또는 데이터 경고 메시지를 만들 수 없으면 오류 메시지가 모든 받는 사람에게 전송됩니다. 메시지에는 경고 결과 대신 오류 설명이 포함됩니다.

 자세한 내용은 [Data Alert Messages](../../2014/reporting-services/data-alert-messages.md)을 참조하세요.

##  <a name="InstallAlerting"></a>데이터 경고 설치
 데이터 경고 기능은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 가 SharePoint 모드로 설치된 경우에만 사용할 수 있습니다. 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 를 SharePoint 모드로 설치하면 데이터 경고 정보 및 경고 메타데이터를 저장하는 경고 데이터베이스와 경고 관리를 위한 두 개의 SharePoint 페이지가 자동으로 생성되고 SharePoint 사이트에 데이터 경고 디자이너가 추가됩니다. 수행할 특수 단계 또는 설치 중 경고에 대해 설정할 옵션이 없습니다.

 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]를 SharePoint 모드로 설치하는 방법과 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서 새로 도입된 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 공유 서비스 및 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능을 사용하기 전에 만들고 구성해야 하는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션에 대한 자세한 내용은 MSDN Library의 [SharePoint 2010용 Reporting Services SharePoint 모드 설치](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)를 참조하세요.

 이 항목 앞부분의 다이어그램에 나와 있는 것처럼 데이터 경고에는 SQL Server 에이전트 작업이 사용됩니다. 작업을 만들려면 SQL Server 에이전트가 실행되고 있어야 합니다. 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]를 설치할 때 SQL Server 에이전트가 자동으로 시작되도록 구성했을 수 있습니다. 그렇지 않은 경우 SQL Server 에이전트를 수동으로 시작할 수 있습니다. 자세한 내용은 [SQL Server 에이전트 구성](../ssms/agent/configure-sql-server-agent.md) 및 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)을 참조하세요.

 SharePoint 중앙 관리의 **구독 및 경고 프로비전** 페이지를 사용하여 SQL Server 에이전트가 실행되고 있는지 알아보고, SQL Server 에이전트에 대한 사용 권한을 부여하기 위해 실행할 사용자 지정 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트를 만들고 다운로드할 수 있습니다. PowerShell을 사용하여 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트를 생성할 수도 있습니다. 자세한 내용은 [SSRS 서비스 애플리케이션에 대한 구독 및 경고 프로비전](install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)을 참조하세요.

##  <a name="ConfigAlert"></a>데이터 경고 구성
 
  [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 부터 데이터 경고를 비롯한 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능에 대한 설정이 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 를 SharePoint 모드로 설치할 때마다 보고서 서버 구성 파일(rsreportserver.config)과 SharePoint 구성 데이터베이스 간에 배포됩니다. 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]설치 및 구성 단계의 일환으로 서비스 애플리케이션을 만들면 SharePoint 구성 데이터베이스가 자동으로 생성됩니다. 자세한 내용은 [Rsreportserver.config 구성 파일](report-server/rsreportserver-config-configuration-file.md) 및 [Reporting Services 구성 파일](report-server/reporting-services-configuration-files.md)을 참조 하세요.

 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 데이터 경고에 대한 설정에는 경고 데이터 및 메타데이터를 정리하는 간격과 데이터 경고 메시지를 전자 메일로 보낼 때의 다시 시도 횟수가 포함됩니다. 구성 파일 및 구성 데이터베이스를 업데이트하여 데이터 경고 설정에 다른 값을 사용할 수 있습니다.

 보고서 서버 구성 파일은 직접 업데이트하고, SharePoint 구성 데이터베이스는 Windows PowerShell cmdlet을 사용하여 업데이트합니다.

 다음 표에서는 데이터 경고에 대한 구성 요소, 해당 기본값, 설명 및 위치를 보여 줍니다.

|설정|기본값|Description|위치|
|-------------|-------------------|-----------------|--------------|
|AlertingCleanupCycleMinutes|20|정리 주기가 시작되는 지점 간의 간격(분)입니다.|보고서 서버 구성 파일|
|AlertingExecutionLogCleanupMinutes|10080|실행 로그 항목이 유지되는 시간(분)입니다.|보고서 서버 구성 파일|
|AlertingDataCleanupMinutes|360|임시 데이터가 유지되는 시간(분)입니다.|보고서 서버 구성 파일|
|AlertingMaxDataRetentionDays|180|경고 실행 메타데이터, 경고 인스턴스 및 실행 결과가 삭제될 때까지의 기간(일 수)입니다.|보고서 서버 구성 파일|
|MaxRetries|3|데이터 경고 처리를 다시 시도하는 횟수입니다.|서비스 구성 데이터베이스|
|SecondsBeforeRetry|900|작업을 다시 시도하기 전마다 기다릴 시간(초)입니다.|서비스 구성 데이터베이스|

 기본적으로 MaxRetries 및 SecondsBeforeRetry 설정은 데이터 경고가 발생시키는 모든 이벤트에 적용됩니다. 다시 시도 및 다시 시도 간격을 더 세부적으로 제어하려면 다른 MaxRetries 및 SecondsBeforeRetry 값을 지정하는 임의의 이벤트 처리기 및 모든 이벤트 처리기에 대한 요소를 추가합니다.

### <a name="event-handlers-and-retry"></a>이벤트 처리기 및 다시 시도
 이벤트 처리기는 다음과 같습니다.

|이벤트 처리기|Description|
|-------------------|-----------------|
|FireAlert|데이터 경고 관리자에서 **실행**  을 클릭하여 경고 정의 처리를 즉시 시작합니다.|
|FireSchedule|SQL Server 에이전트에서 경고 정의에 대한 작업 일정이 시작됩니다.|
|CreateSchedule|사용자가 데이터 경고 정의를 만들면 경고 정의에 지정된 빈도 간격을 기반으로 SQL Server 에이전트 작업 일정이 생성됩니다.|
|UpdateSchedule|사용자가 데이터 경고 정의의 빈도 간격을 업데이트하면 SQL Server 에이전트 작업 일정이 업데이트됩니다.|
|DeleteSchedule|사용자가 데이터 경고 정의를 삭제하면 해당 SQL Server 에이전트 작업이 삭제됩니다.|
|GenerateAlert|경고 런타임에서 보고서 데이터 피드가 처리되고, 데이터 경고 정의에 지정된 규칙이 적용되고, 데이터 경고 인스턴스의 생성 여부가 결정되고, 필요한 경우 데이터 경고 인스턴스가 생성됩니다.|
|DeliverAlert|런타임에서 데이터 경고 메시지가 생성되고 모든 받는 사람에게 전자 메일로 전송됩니다.|

 다음 표에는 이벤트 처리기 및 재시도 발생 시기가 요약되어 있습니다.

|오류 범주|<|\<|이벤트 유형||>|>|>|
|--------------------|--------|--------|----------------|-|--------|--------|--------|
||**FireAlert**|**FireSchedule**|**CreateSchedule**|**UpdateSchedule**|**DeleteSchedule**|**GenerateAlert**|**DeliverAlert**|
|메모리가 부족합니다.|X|X|X|X|X|X|X|
|스레드 중단|X|X|X|X|X|X|X|
|SQL 에이전트가 실행되고 있지 않습니다.|X||X|X|X|||
|임시 상태입니다. 대부분 연결, 제한 시간 및 잠금 문제일 수 있습니다.|X|X|X|X|X|X|X|
|IOException|||||||X|
|WebException|||||||X|
|SocketException|||||||X|
|System.net.mail.smtpexception **(\*)**|||||||X|

 **(\*)** 다시 시도를 트리거하는 SMTP 오류:

-   SmtpStatusCode.ServiceNotAvailable

-   SmtpStatusCode.MailboxBusy

-   SmtpStatusCode.MailboxUnavailable

###  <a name="bkmk_disablealerts"></a>데이터 경고 사용 안 함
 데이터 경고 기능을 사용하지 않으려면 구성 파일의 Service 섹션을 업데이트합니다. 다음 코드에서는 구성 파일의 Service 섹션을 보여 줍니다.

 `<Service>`

 `<IsSchedulingService>True</IsSchedulingService>`

 `<IsNotificationService>True</IsNotificationService>`

 `<IsEventService>True</IsEventService>`

 `<IsAlertingService>True</IsAlertingService>`

 `...`

 `</Service>`

 경고를 사용하지 않으려면 `<IsAlertingService>True</IsAlertingService>`에서 True를 False로 바꿉니다.

##  <a name="Permissions"></a>데이터 경고에 대 한 사용 권한
 보고서에 대해 데이터 경고를 만들려면 SharePoint 사이트에서 보고서를 실행하고 경고를 만들 수 있는 권한이 있어야 합니다. 보고서 사용 권한에 대한 자세한 내용은 다음 항목을 참조하세요.

-   [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)

-   [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)

 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]데이터 경고는 정보 근로자 및 경고 관리자의 두 가지 권한 수준을 지원 합니다. 다음 표에서는 관련된 SharePoint 사용 권한 및 사용자 태스크가 나열됩니다.

|사용자 유형|SharePoint 사용 권한|태스크 설명|
|---------------|---------------------------|----------------------|
|정보 근로자|항목 보기<br /><br /> 경고 만들기|보고서와 같은 항목을 보고 보고서에 대한 데이터 경고를 만듭니다. 경고를 편집 및 삭제합니다.|
|경고 관리자|알림 관리|SharePoint 사이트에 저장된 모든 데이터 경고 목록을 보고 경고를 삭제합니다.|

##  <a name="DiagnosticsLogging"></a>진단 및 로깅
 데이터 경고를 사용하면 경고 내역 및 경고가 실패한 이유를 확인하고, 관리자가 로그를 사용하여 전송할 경고와 전송 대상자, 경고 인스턴스 수 등을 확인하는 등 여러 가지 방법으로 정보 근로자와 관리자의 업무에 도움을 줄 수 있습니다.

### <a name="data-alert-manager"></a>데이터 경고 관리자
 데이터 경고 관리자에는 정보 근로자 및 경고 관리자가 오류가 발생한 이유를 확인하는 데 도움이 되는 경고 정의 및 오류 정보가 나열됩니다. 오류에 대한 몇 가지 일반적인 원인은 다음과 같습니다.

-   변경된 보고서 데이터 피드 및 데이터 경고 정의 규칙에 사용된 열은 더 이상 데이터 피드에 포함되지 않습니다.

-   보고서에 대한 보기 권한은 취소되었습니다.

-   변경된 기본 데이터 원본의 데이터 형식 및 경고 정의는 더 이상 유효하지 않습니다.

### <a name="logs"></a>로그
 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 는 데이터 경고 정의를 처리할 때 실행되는 보고서, 생성되는 데이터 경고 인스턴스 등에 대한 정보를 얻을 수 있는 많은 로그를 제공합니다. 경고 실행 로그, 보고서 서버 실행 로그, 보고서 서버 추적 로그라는 세 로그가 특히 유용합니다.

 다른 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 로그에 대한 자세한 내용은 [Reporting Services 로그 파일 및 소스](report-server/reporting-services-log-files-and-sources.md)를 참조하세요.

#### <a name="alerting-execution-log"></a>경고 실행 로그
 경고 런타임 서비스는 경고 데이터베이스의 ExecutionLogView 테이블에 항목을 작성합니다. 테이블을 쿼리하거나 다음 저장 프로시저를 실행하여 경고 데이터베이스에 저장된 데이터 경고에 대한 보다 다양한 진단 정보를 얻을 수 있습니다.

-   ReadAlertData

-   ReadAlertHistory

-   ReadAlertInstances

-   ReadEventHistory

-   ReadFeedPollHistory

-   ReadFeedPools

-   ReadPollData

-   ReadSentAlerts

 SQL 에이전트를 사용하여 일정에 따라 저장 프로시저를 실행할 수 있습니다. 자세한 내용은 [SQL Server Agent](../ssms/agent/sql-server-agent.md)을 참조하세요.

#### <a name="report-server-execution-log"></a>보고서 서버 실행 로그
 보고서는 데이터 경고 정의를 작성하는 데 사용된 데이터 피드를 생성하기 위해 실행됩니다. 보고서 서버 데이터베이스의 보고서 서버 실행 로그는 보고서가 실행될 때마다 정보를 캡처합니다. 자세한 정보가 필요한 경우 데이터베이스에서 ExecutionLog2 뷰를 쿼리할 수 있습니다. 자세한 내용은 [보고서 서버 실행 로그 및 ExecutionLog3 뷰](report-server/report-server-executionlog-and-the-executionlog3-view.md)를 참조 하세요.

#### <a name="report-server-trace-log"></a>보고서 서버 추적 로그
 보고서 서버 추적 로그에는 보고서 서버 웹 서비스 및 백그라운드 처리가 수행하는 작업을 비롯하여 보고서 서버 서비스 작업에 대한 세부 정보가 들어 있습니다. 추적 로그 정보는 보고서 서버가 포함된 애플리케이션을 디버깅하거나 이벤트 로그 또는 실행 로그에 기록된 특정 문제를 조사하는 경우 유용할 수 있습니다. 자세한 내용은 [Report Server Service Trace Log](report-server/report-server-service-trace-log.md)을 참조하세요.

##  <a name="PerformanceCounters"></a>성능 카운터
 데이터 경고는 자체 성능 카운터를 제공합니다. 하나를 제외한 모든 성능 카운터가 경고 런타임 서비스에 포함된 이벤트와 관련되어 있습니다. 이벤트 큐와 관련된 성능 카운터를 보면 모든 활성 이벤트 큐의 길이를 알 수 있습니다.

|이벤트 또는 이벤트 큐|성능 카운터|
|--------------------------|-------------------------|
|ALERTINGQUEUESIZE|경고: 이벤트 큐 길이|
|FireAlert|경고: 이벤트 처리됨 - FireAlert|
|FireSchedule|경고: 이벤트 처리됨 - FireSchedule|
|CreateSchedule|경고: 이벤트 처리됨 - CreateSchedule|
|UpdateSchedule|경고: 이벤트 처리됨 - UpdateSchedule|
|DeleteSchedule|경고: 이벤트 처리됨 - DeleteSchedule|
|GenerateAlert|경고: 이벤트 처리됨 - GenerateAlert|
|DeliverAlert|경고: 이벤트 처리됨 - DeliverAlert|

 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 는 기타 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능에 대한 성능 카운터를 제공합니다. 자세한 내용은 [ReportServer: service 및 ReportServerSharePoint: Service 성능 개체](report-server/performance-counters-reportserver-service-performance-objects.md)에 대 한 성능 카운터, Msrs [2014 웹 서비스 및 Msrs 2014 Windows 서비스 성능 개체에 대 한 성능 카운터 &#40;기본 모드&#41;](report-server/performance-counters-msrs-2011-web-service-performance-objects.md)및 Msrs [2014 웹 서비스 Sharepoint 모드 및 msrs 2014 Windows 서비스 sharepoint 모드 성능 개체에 대 한 성능 카운터 (sharepoint 모드&#41;&#40;](report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md))를 참조 하세요.

##  <a name="SupportForSSL"></a>SSL 지원
 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] HTTP SSL(Secure Sockets Layer) 서비스를 사용하여 보고서 서버 또는 SharePoint 사이트에 대한 암호화된 연결을 설정할 수 있습니다.

 경고 런타임 서비스와 데이터 경고 사용자 인터페이스는 SSL을 지원하며 사용자가 SSL을 사용하는지, 아니면 HTTP를 사용하는지에 관계없이 유사하게 작동하지만 약간의 차이점은 있습니다. SSL 연결을 사용하여 데이터 경고 정의를 만들면 데이터 경고 메시지에서 SharePoint 라이브러리로 다시 연결되는 URL에도 SSL이 사용됩니다. URL에 HTTP 대신 HTTPS가 사용되므로 SSL 연결을 식별할 수 있습니다. 마찬가지로, HTTP 연결을 사용하여 데이터 경고 정의를 만들면 SharePoint 사이트로 다시 연결되는 링크에 HTTP가 사용됩니다. 경고 정의가 SSL 또는 HTTP 중 어떤 것을 사용하여 생성되었는지에 상관없이 사용자 및 경고 관리자는 데이터 경고 디자이너 또는 데이터 경고 관리자에서 동일한 환경을 사용하게 됩니다. 경고 정의가 생성된 다음 업데이트 및 다시 저장된 시점 사이에 프로토콜(HTTP 또는 SSL)을 변경해야 하는 경우에는 원래 프로토콜이 유지되어 링크 URL에 사용됩니다.

 SSL을 사용하도록 구성된 SharePoint 사이트에서 데이터 경고를 만든 다음 SSL 요구 사항을 제거하면 경고가 사이트에서 계속 작동합니다. 사이트가 삭제되면 기본 영역 사이트가 대신 사용됩니다.

##  <a name="UserInterface"></a>데이터 경고 사용자 인터페이스
 데이터 경고에는 경고 관리를 위한 SharePoint 페이지와 데이터 경고 정의를 만들고 편집하기 위한 디자이너가 제공됩니다.

-   데이터 경고 **디자이너** 에서 데이터 경고 정의를 만들거나 편집할 수 있습니다. 자세한 내용은 [데이터 경고 디자이너](../../2014/reporting-services/data-alert-designer.md), [데이터 경고 디자이너에서 데이터 경고 만들기](create-a-data-alert-in-data-alert-designer.md) 및 [경고 디자이너에서 데이터 경고 편집](edit-a-data-alert-in-alert-designer.md)을 참조하세요.

-   데이터 경고 **관리자** 를 통해 데이터 경고 목록을 보고, 경고를 삭제 하 고, 경고를 열어서 편집할 수 있습니다. 데이터 경고 관리자는 두 가지 버전으로 제공됩니다. 하나는 자신이 만든 경고를 관리할 수 있는 사용자용 버전이고 다른 버전은 사이트 사용자에게 속하는 경고를 관리할 수 있는 관리자용 버전입니다.

     직접 만든 데이터 경고 관리에 대한 자세한 내용은 [SharePoint 사용자용 데이터 경고 관리자](../../2014/reporting-services/data-alert-manager-for-sharepoint-users.md) 및 [데이터 경고 관리자에서 내 데이터 경고 관리](manage-my-data-alerts-in-data-alert-manager.md)를 참조하세요.

     사이트의 모든 데이터 경고 관리에 대한 자세한 내용은 [경고 담당자를 위한 데이터 경고 관리자](../../2014/reporting-services/data-alert-manager-for-alerting-administrators.md) 및 [데이터 경고 관리자에서 SharePoint 사이트의 모든 데이터 경고 관리](manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md)를 참조하세요.

-   **구독 및 데이터 경고를 프로 비전** 하 여 Reporting Services에서 데이터 경고에 SQL Server 에이전트를 사용할 수 있는지 여부를 확인 하 고 SQL Server 에이전트에 대 한 액세스를 허용 하는 스크립트를 다운로드할 수 있습니다. 자세한 내용은 [SSRS 서비스 애플리케이션에 대한 구독 및 경고 프로비전](install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)을 참조하세요.

##  <a name="Globalization"></a>데이터 경고의 세계화
 아랍어 및 히브리어와 같은 특정 스크립트는 오른쪽에서 왼쪽으로 씁니다. 데이터 경고는 오른쪽에서 왼쪽으로 쓰는 스크립트뿐만 아니라 왼쪽에서 오른쪽으로 쓰는 스크립트도 지원합니다. 데이터 경고는 culture를 감지하고, 이에 따라 데이터 경고 메시지의 레이아웃과 사용자 인터페이스 모양 및 동작을 변경합니다. culture는 사용자 컴퓨터에 있는 운영 체제의 국가별 설정에서 파생됩니다. culture는 사용자가 데이터 경고 정의를 업데이트한 다음 다시 저장할 때마다 저장됩니다.

 경고 정의의 culture에 따라 데이터가 경고 정의의 규칙을 만족하는지 여부가 달라질 수 있습니다. 문자열 비교는 culture별 규칙의 영향을 가장 많이 받습니다.

 경고 정의의 culture에 따라 보고서 데이터가 경고 정의의 규칙을 만족하는지 여부를 결정하는 작업에 영향이 있을 수 있습니다. 이는 문자열에서 가장 많이 발생합니다. 예를 들어 독일어 culture를 사용하는 경고 정의에서 영어 문자 "o"와 독일어 문자 "ö"를 비교하는 규칙은 만족될 수 없습니다. 하지만 영어 culture를 사용하는 동일한 경고 정의에서는 해당 규칙이 만족될 수 있습니다.

 데이터 서식도 경고 정의의 culture를 기반으로 합니다. 예를 들어 culture에 마침표가 소수점 기호로 사용되는 경우 값은 45.67로 표시되지만, 쉼표가 소수점 기호로 사용되는 culture의 경우 45,67이 표시됩니다.

 사용하는 데이터 경고 사용자 인터페이스에 따라 오른쪽에서 왼쪽으로 쓰는 스크립트에 대한 지원이 달라집니다. 데이터 경고 디자이너는 입력란에서 오른쪽에서 왼쪽으로 쓰는 스크립트를 지원하지만 디자이너의 레이아웃은 오른쪽에서 왼쪽으로 되어 있지 않습니다. 해당 레이아웃은 다른 도구와 마찬가지로 왼쪽에서 오른쪽으로 되어 있습니다. 경고 정의를 오른쪽에서 왼쪽으로 진행되는 텍스트 방향을 사용하여 만든 다음 왼쪽에서 오른쪽으로 되어 있는 환경에서 편집하면 경고 정의를 저장할 때 오른쪽에서 왼쪽으로 진행되는 텍스트 방향이 유지됩니다. 데이터 경고 관리자는 SharePoint 페이지와 동일하게 작동합니다. 해당 레이아웃은 기타 SharePoint 페이지와 마찬가지로 오른쪽에서 왼쪽으로 되어 있습니다. 오른쪽에서 왼쪽으로 진행되는 데이터 경고 정의를 기반으로 하는 데이터 경고 메시지는 메시지 텍스트를 오른쪽에서 왼쪽으로 표시하며 메시지 레이아웃은 왼쪽에서 오른쪽으로 되어 있습니다.

##  <a name="HowTo"></a> 관련 작업

-   [SharePoint 라이브러리에 보고서 저장&#40;보고서 작성기&#41;](report-builder/save-a-report-to-a-sharepoint-library-report-builder.md)

-   [데이터 경고 디자이너에서 데이터 경고 만들기](create-a-data-alert-in-data-alert-designer.md)

-   [경고 디자이너에서 데이터 경고 편집](edit-a-data-alert-in-alert-designer.md)

-   [데이터 경고 관리자에서 내 데이터 경고 관리](manage-my-data-alerts-in-data-alert-manager.md)

-   [데이터 경고 관리자에서 SharePoint 사이트의 모든 데이터 경고 관리](manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md)

-   [사용자 및 경고 담당자에게 권한 부여](grant-permissions-to-users-and-alerting-administrators.md)

## <a name="see-also"></a>참고 항목
 [SharePoint 사용자를 위한](../../2014/reporting-services/data-alert-manager-for-sharepoint-users.md) 경고 관리자 데이터 경고 관리자 [에 대 한](../../2014/reporting-services/data-alert-manager-for-alerting-administrators.md) [데이터 경고 디자이너](../../2014/reporting-services/data-alert-designer.md) 데이터 경고 관리자


