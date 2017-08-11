---
title: "서버 속성(고급 페이지) - Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.serverproperties.advanced.f1
ms.assetid: 07b78a84-a6aa-4502-861d-349720ef790e
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: 5baf0e5c9dcc3b9c70fce06024e5bba957c48f65
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---

# <a name="server-properties-advanced-page---reporting-services"></a>서버 속성(고급 페이지) - Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

이 페이지를 사용하여 보고서 서버의 시스템 속성을 설정할 수 있습니다. 시스템 속성을 설정하는 데에는 여러 가지 방법이 있습니다. 이 도구는 그래픽 사용자 인터페이스를 제공하므로 코드를 작성하지 않고도 속성을 설정할 수 있습니다.

이 페이지를 열려면 SQL Server Management Studio를 시작, 보고서 서버 인스턴스에 연결, 보고서 서버 이름 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다. 선택 **고급** 이 페이지를 엽니다.

## <a name="options"></a>옵션

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
> 값을 **0**으로 설정하면 모든 항목이 실행 로그에서 *삭제*됩니다. 값이 **-1**이면 실행 로그 항목이 유지되며 삭제되지 않습니다.

**SessionTimeout**  
세션이 활성 상태로 유지되는 시간(초)입니다. 기본값은 **600**입니다.  

**SharePointIntegratedMode**  
서버 모드를 나타내는 읽기 전용 속성입니다. 이 값이 False이면 보고서 서버는 기본 모드로 실행됩니다.  

**SiteName**  
웹 포털의 페이지 제목에 표시되는 보고서 서버 사이트의 이름입니다. 기본값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]입니다. 이 속성은 빈 문자열일 수 있습니다. 최대 길이는 8,000자입니다.  

**StoredParametersLifetime**  
저장된 매개 변수를 저장할 수 있는 최대 일 수를 지정합니다. 유효한 값은 **-1**, **+1** 에서 **2,147,483,647**까지입니다. 기본값은 **180** 일입니다.  

**StoredParametersThreshold**  
보고서 서버에서 저장할 수 있는 매개 변수 값의 최대 일 수를 지정합니다. 유효한 값은 **-1**, **+1** 에서 **2,147,483,647**까지입니다. 기본값은 **1500**입니다.  

**UseSessionCookies**  
보고서 서버에서 클라이언트 브라우저와 통신할 때 세션 쿠키를 사용해야 하는지 여부를 나타냅니다. 기본값은 **true**입니다.  

**ExternalImagesTimeout**  
외부 이미지 파일을 검색해야 하는 시간을 지정합니다. 이 시간을 넘기면 연결 시간이 초과된 것으로 처리됩니다. 기본값은 **600** 초입니다.  

**SnapshotCompression**  
스냅숏의 압축 방식을 정의합니다. 기본값은 **SQL**입니다. 유효한 값은 다음과 같습니다.

|값|Description|
|---------|---------|
|**SQL**|보고서 서버 데이터베이스에 저장 될 때 스냅숏이 압축 됩니다. 이것은 현재 동작입니다.|
|**없음**|스냅숏이 압축 되지 않습니다.|
|**모두**|보고서 서버 데이터베이스 또는 파일 시스템을 포함 하는 모든 저장소 옵션에 대해 스냅숏이 압축 됩니다.|

**SystemReportTimeout**  
보고서 서버 네임스페이스에서 관리되는 모든 보고서에 대한 기본 보고서 처리 제한 시간 값(초)입니다. 이 값은 보고서 수준에서 무시할 수 있습니다. 이 속성을 설정하면 지정된 시간이 만료될 경우 보고서 서버가 보고서 처리를 중지합니다. 유효한 값은 **-1** 에서 **2**까지,**147**,**483**,**647**입니다. 값이 **-1**이면 네임스페이스의 보고서 처리 중 시간 제한으로 인한 중지가 발생하지 않습니다. 기본값은 **1800**입니다.  

**SystemSnapshotLimit**  
하나의 보고서에 대해 저장되는 최대 스냅숏 수입니다. 유효한 값은 **-1** 에서 **2**까지,**147**,**483**,**647**입니다. 값이 **-1**이면 스냅숏 제한이 없습니다.  

**EnableIntegratedSecurity**  
보고서 데이터 원본 연결에 Windows 통합 보안이 지원되는지 여부를 지정합니다. 기본값은 **True**입니다. 유효한 값은 다음과 같습니다.

|값|Description|
|---------|---------|
|**True**|Windows 통합된 보안이 사용 됩니다.|
|**False**|Windows 통합된 보안 사용 되지 않습니다. Windows 통합 보안을 사용하도록 구성된 보고서 데이터 원본은 실행되지 않습니다.|

**EnableLoadReportDefinition**  
이 옵션을 선택하면 사용자가 보고서 작성기 보고서에서 임시 보고서 실행을 수행할 수 있는지 여부를 지정할 수 있습니다. 이 옵션 설정에 따라 보고서 서버의 **EnableLoadReportDefinition** 속성 값이 결정됩니다.  

이 옵션의 선택을 취소하면 속성은 False로 설정되며 보고서 모델을 데이터 원본으로 사용하는 보고서에 대해 보고서 서버가 클릭 광고 보고서를 생성하지 않습니다. LoadReportDefinition 메서드에 대한 모든 호출은 차단됩니다.  

이 옵션을 끄면 악의적인 사용자가 LoadReportDefinition 요청으로 보고서 서버에 오버로드를 가하여 서비스 거부 공격을 실행할 수 있는 위협이 완화됩니다.  

**EnableRemoteErrors**  
원격 컴퓨터에서 보고서를 요청하는 사용자에 대해 반환되는 오류 메시지에 외부 오류 정보(예: 보고서 데이터 원본에 대한 오류 정보)를 포함합니다. 유효한 값은 **true** 및 **false**입니다. 기본값은 **false**입니다. 자세한 내용은 [원격 오류 사용&#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md)을 참조하세요.  

**EnableReportDesignClientDownload**  
보고서 서버에서 보고서 작성기 설치 패키지를 다운로드할 수 있는지 여부를 지정합니다. 이 설정을 해제하면 보고서 작성기에 대한 URL이 작동하지 않습니다. 자세한 내용은 [보고서 작성기 액세스 구성](../../reporting-services/report-server/configure-report-builder-access.md)을 참조하세요.  

**EditSessionCacheLimit**  
보고서 편집 세션에서 활성화될 수 있는 데이터 캐시 항목 수를 지정합니다. 기본값은 5입니다.  

**EditSessionTimeout**  
보고서 편집 세션이 시간 초과될 때까지 걸리는 시간(초)을 지정합니다. 기본값은 7200초(2시간)입니다.  

**EnableCustomVisuals** ***(Power BI 보고서 서버 전용)***  
PowerBI ReportServer PowerBI 사용자 지정 시각적 개체의 표시를 사용 해야 합니다. 값은 True, false를 반환 합니다.  기본값은 True입니다.  

**EnablePowerBIReportExportData** ***(Power BI 보고서 서버 전용)***  
PowerBI ReportServer PowerBI 시각적 개체에서 데이터 내보내기 사용 하도록 설정 해야 합니다. 값은 True, false를 반환 합니다.  기본값은 True입니다.  

**EnableTestConnectionDetailedErrors**  
사용자가 보고서 서버를 사용하여 데이터 원본 연결을 테스트할 때 클라이언트 컴퓨터로 자세한 오류 메시지를 보낼지 여부를 나타냅니다. 기본값은 **true**입니다. 이 옵션이 **false**로 설정되어 있으면 일반 오류 메시지만 보냅니다.

## <a name="see-also"></a>관련 항목:

[보고서 서버 속성 &#40; 설정 합니다. Management studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Management Studio에서 보고서 서버에 연결](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Reporting Services 속성](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Management Studio의 보고서 서버 F1 도움말](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[보고서 서버 시스템 속성](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[배포 및 관리 태스크 스크립팅](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[내 보고서 사용 및 사용 안 함 설정](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)
