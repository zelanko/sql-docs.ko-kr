---
title: 서버 속성(고급 페이지) - Reporting Services | Microsoft Docs
author: markingmyname
ms.author: maghan
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.suite: reporting-services
ms.topic: conceptual
ms.date: 08/16/2018
ms.openlocfilehash: c0fef28c07244e220aab90873dd80226f9a3cddd
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43266271"
---
# <a name="server-properties-advanced-page---reporting-services"></a>서버 속성(고급 페이지) - Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

이 페이지를 사용하여 보고서 서버의 시스템 속성을 설정할 수 있습니다. 시스템 속성을 설정하는 데에는 여러 가지 방법이 있습니다. 이 도구는 그래픽 사용자 인터페이스를 제공하므로 코드를 작성하지 않고도 속성을 설정할 수 있습니다.

이 페이지를 열려면 SQL Server Management Studio를 시작하고, 보고서 서버 인스턴스에 연결한 다음, 보고서 서버 이름을 마우스 오른쪽 단추로 클릭하고, **속성**을 선택합니다. **고급**을 선택하여 이 페이지를 엽니다.

## <a name="options"></a>Options

**EnableMyReports**  
내 보고서 기능이 설정되어 있는지 여부를 나타냅니다. **true** 값은 이 기능이 설정되어 있음을 나타냅니다.  

**MyReportsRole**  
사용자의 내 보고서 폴더에서 보안 정책을 만들 때 사용된 역할의 이름입니다. 기본값은 **My Reports Role**입니다.  

**EnableClientPrinting**  
보고서 서버에서 RSClientPrint ActiveX 컨트롤을 다운로드할 수 있는지 여부를 지정합니다. 유효한 값은 **true** 및 **false**입니다. 기본값은 **true**입니다. 이 컨트롤에 필요한 추가 설정에 대한 자세한 내용은 [Reporting Services에 대해 클라이언트 쪽 인쇄 사용 및 사용 안 함](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)을 참조하세요.  

**EnableExecutionLogging**  
보고서 실행 로깅이 설정되어 있는지 여부를 나타냅니다. 기본값은 **true**입니다. 보고서 서버 실행 로그에 대한 자세한 내용은 [보고서 서버 ExecutionLog 및 ExecutionLog3 뷰](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)를 참조하세요.  

**ExecutionLogDaysKept**  
실행 로그에 보고서 실행 정보를 보관하는 일 수입니다. 이 속성에 유효한 값은 **-1** 부터 **2**,**147**,**483**,**647**입니다. 값이 **-1** 이면 실행 로그 테이블에서 항목이 삭제되지 않습니다. 기본값은 **60**입니다.  

> [!NOTE]
> 값을 **0**으로 설정하면 모든 항목이 실행 로그에서 *삭제*됩니다. 값이 **-1**이면 실행 로그의 항목을 유지하고 삭제하지는 않습니다.

**RDLXReportTimetout** 보고서 서버 네임스페이스에서 관리되는 모든 보고서에 대한 RDLX 보고서 *(SharePoint Server의 파워 뷰 보고서)* 처리 제한 시간 값(초)입니다. 이 값은 보고서 수준에서 무시할 수 있습니다. 이 속성을 설정하면 지정된 시간이 만료될 경우 보고서 서버가 보고서 처리를 중지합니다. 유효한 값은 **-1** 에서 **2**까지,**147**,**483**,**647**입니다. 값이 **-1**이면 네임스페이스의 보고서 처리 중 시간 제한으로 인한 중지가 발생하지 않습니다. 기본값은 **1800**입니다.

**SessionTimeout** 세션이 활성 상태로 유지되는 시간(초)입니다. 기본값은 **600**입니다.  

**SharePointIntegratedMode**  
이 읽기 전용 속성은 서버 모드를 나타냅니다. 이 값이 False이면 보고서 서버는 기본 모드로 실행됩니다.  

**SiteName**  
웹 포털의 페이지 제목에 표시되는 보고서 서버 사이트의 이름입니다. 기본값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]입니다. 이 속성은 빈 문자열일 수 있습니다. 최대 길이는 8,000자입니다.  

**StoredParametersLifetime** 저장된 매개 변수를 저장할 수 있는 최대 일 수를 지정합니다. 유효한 값은 **-1**, **+1** 에서 **2,147,483,647**까지입니다. 기본값은 **180** 일입니다.  

**StoredParametersThreshold**  
보고서 서버에서 저장할 수 있는 매개 변수 값의 최대 일 수를 지정합니다. 유효한 값은 **-1**, **+1** 에서 **2,147,483,647**까지입니다. 기본값은 **1500**입니다.  

**UseSessionCookies**  
보고서 서버에서 클라이언트 브라우저와 통신할 때 세션 쿠키를 사용해야 하는지 여부를 나타냅니다. 기본값은 **true**입니다.  

**ExternalImagesTimeout**  
외부 이미지 파일을 검색해야 하는 시간을 지정합니다. 이 시간을 넘기면 연결 시간이 초과된 것으로 처리됩니다. 기본값은 **600** 초입니다.  

**SnapshotCompression** 해당 시점의 보고서 서버의 스냅숏입니다.

**SnapshotCompression**  
스냅숏의 압축 방식을 정의합니다. 기본값은 **SQL**입니다. 유효한 값은 다음과 같습니다.

|값|설명|
|---------|---------|
|**SQL**|보고서 서버 데이터베이스에 저장될 때 스냅숏이 압축됩니다. 이 압축은 현재 동작입니다.|
|**없음**|스냅숏이 압축되지 않습니다.|
|**모두**|보고서 서버 데이터베이스, 파일 시스템을 포함한 모든 저장소 옵션에 대해 스냅숏이 압축됩니다.|

**SystemReportTimeout**  
보고서 서버 네임스페이스에서 관리되는 모든 보고서에 대한 기본 보고서 처리 제한 시간 값(초)입니다. 이 값은 보고서 수준에서 무시할 수 있습니다. 이 속성을 설정하면 지정된 시간이 만료될 경우 보고서 서버가 보고서 처리를 중지합니다. 유효한 값은 **-1** 에서 **2**까지,**147**,**483**,**647**입니다. 값이 **-1**이면 네임스페이스의 보고서 처리 중 시간 제한으로 인한 중지가 발생하지 않습니다. 기본값은 **1800**입니다.  

**SystemSnapshotLimit**  
하나의 보고서에 대해 저장되는 최대 스냅숏 수입니다. 유효한 값은 **-1** 에서 **2**까지,**147**,**483**,**647**입니다. 값이 **-1**이면 스냅숏 제한이 없습니다.  

**EnableIntegratedSecurity**  
보고서 데이터 원본 연결에 Windows 통합 보안이 지원되는지 여부를 지정합니다. 기본값은 **True**입니다. 유효한 값은 다음과 같습니다.

|값|설명|
|---------|---------|
|**True**|Windows 통합 보안이 사용됩니다.|
|**False**|Windows 통합 보안이 사용되지 않습니다. Windows 통합 보안을 사용하도록 구성된 보고서 데이터 원본은 실행되지 않습니다.|

**EnableLoadReportDefinition**  
이 옵션을 선택하면 사용자가 보고서 작성기 보고서에서 계획되지 않은 보고서 실행을 수행할 수 있는지 여부를 지정할 수 있습니다. 이 옵션 설정에 따라 보고서 서버의 **EnableLoadReportDefinition** 속성 값이 결정됩니다.  

이 옵션의 선택을 취소하면 속성이 False로 설정됩니다. 보고서 서버는 보고서 모델을 데이터 원본으로 사용하는 보고서에 대해 클릭 방문 보고서를 생성하지 않습니다. LoadReportDefinition 메서드에 대한 모든 호출은 차단됩니다.  

이 옵션을 끄면 악의적인 사용자가 LoadReportDefinition 요청으로 보고서 서버에 오버로드를 가하여 서비스 거부 공격을 실행할 수 있는 위협이 완화됩니다.  

**EnableRemoteErrors**  
원격 컴퓨터에서 보고서를 요청하는 사용자에 대해 반환되는 오류 메시지에 외부 오류 정보(예: 보고서 데이터 원본에 대한 오류 정보)를 포함합니다. 유효한 값은 **true** 및 **false**입니다. 기본 값은 **false**입니다. 자세한 내용은 [원격 오류 사용&#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md)을 참조하세요.  

**AccessControlAllowCredentials**  
'자격 증명' 플래그가 true로 설정되면 클라이언트 요청에 대한 응답이 노출될 수 있는지를 나타냅니다. 기본 값은 **false**입니다.

**AccessControlAllowHeaders** 클라이언트가 요청하면 서버에서 허용하는 헤더의 쉼표로 구분된 목록입니다. 이 속성은 빈 문자열일 수 있고 *를 지정하면 모든 헤더를 허용합니다.

**AccessControlAllowMethods** 클라이언트가 요청하면 서버에서 허용하는 HTTP 메서드의 쉼표로 구분된 목록입니다. 기본값은 (GET, PUT, POST, PATCH, DELETE)이며 *를 지정하면 모든 메서드를 허용합니다.

**AccessControlAllowOrigin** 클라이언트가 요청하면 서버에서 허용하는 원본의 쉼표로 구분된 목록입니다. 기본값이 비어 있어서 모든 요청을 방지하며, *를 지정하면 자격 증명이 설정되지 않은 경우 모든 원본을 허용합니다. 자격 증명이 지정된 경우 원본의 자세한 목록을 지정해야 합니다.

**AccessControlExposeHeaders** 서버가 클라이언트에 노출하는 헤더의 쉼표로 구분된 목록입니다. 기본값은 공백입니다.

**AccessControlMaxAge** 실행 전 요청 결과를 캐시할 수 있는 시간(초)을 지정합니다. 기본값은 600초(10분)입니다.

**EditSessionCacheLimit**  
보고서 편집 세션에서 활성화될 수 있는 데이터 캐시 항목 수를 지정합니다. 기본값은 5입니다.  

**EditSessionTimeout**  
보고서 편집 세션이 시간 초과될 때까지 걸리는 시간(초)을 지정합니다. 기본값은 7200초(2시간)입니다.  

**EnableCustomVisuals** ***(Power BI Report Server 전용)*** Power BI 사용자 지정 시각적 개체의 표시를 사용하려면 값은 true/false입니다. *기본값은 True입니다.*  

**ExecutionLogLevel** 실행 로그를 수준을 설정합니다. *기본값은 보통입니다.*

**InterProcessTimeoutMinutes** 프로세스 시간 제한(분)을 설정합니다. *기본값은 30입니다.*

**MaxFileSizeMb** 보고서의 최대 파일 크기를 MB 단위로 설정합니다. *기본값은 1000입니다.  최댓값은 2000입니다.*

**ModelCleanupCycleminutes** 모델 정리 주기(분)를 설정합니다. *기본값은 15입니다.*

**OfficeAccessTokenExpirationSeconds** ***(Power BI Report Server 전용)*** office 액세스 토큰이 만료되는 시간(초)을 설정합니다. *기본값은 60입니다.*

**OfficeOnlineDiscoveryURL** ***(Power BI Report Server 전용)*** Excel 통합 문서를 볼 수 있도록 Office Online Server 인스턴스의 주소를 설정합니다.

**RequireIntune** Intune이 Power BI 모바일 앱을 통해 조직의 보고서에 액세스하도록 요구합니다. *기본값은 false입니다.*

**ScheduleRefreshTimeoutMinutes** ***(Power BI Report Server 전용)*** 일정 새로 고침 제한 시간을 설정합니다. *기본값은 120입니다.*

**ShowDownloadMenu** 클라이언트 도구 다운로드 메뉴를 사용하도록 설정합니다. *기본값은 true입니다.*

**TimeInitialDelaySeconds** 초기 시간을 지연할 시간(초)을 설정합니다. *기본값은 60입니다.*

**TrustedFileFormat** Reporting Services 포털 사이트의 브라우저 내에서 열리는 모든 외부 파일 형식을 설정합니다. 나열되지 않은 외부 파일 형식의 경우 브라우저에서 옵션을 다운로드하라는 메시지가 표시됩니다. 기본값은 jpg, jpeg, jpe, wav, bmp, pdf, img, gif, json, mp4, web, png입니다.

**EnablePowerBIReportExportData** ***(Power BI Report Server 전용)***  
Power BI 시각적 개체에서 Power BI Report Server 데이터 내보내기를 사용하도록 설정합니다. 사용 가능한 값은 True 또는 False입니다.  기본값은 True입니다.  

**ScheduleRefreshTimeoutMinutes** ***(Power BI Report Server 전용)***  
포함된 AS 모델을 사용하여 Power BI 보고서에 예약된 새로 고침의 데이터 새로 고침 제한 시간(분)입니다. 기본값은 120분입니다.

**EnableTestConnectionDetailedErrors**  
사용자가 보고서 서버를 사용하여 데이터 원본 연결을 테스트할 때 클라이언트 컴퓨터로 자세한 오류 메시지를 보낼지 여부를 나타냅니다. 기본값은 **true**입니다. 이 옵션이 **false**로 설정되어 있으면 일반 오류 메시지만 보냅니다.

## <a name="see-also"></a>참고 항목

[보고서 서버 속성 설정&#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Management Studio에서 보고서 서버에 연결](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Reporting Services 속성](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Management Studio의 보고서 서버 F1 도움말](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[보고서 서버 시스템 속성](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[배포 및 관리 태스크 스크립팅](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[내 보고서 사용 및 사용 안 함 설정](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
