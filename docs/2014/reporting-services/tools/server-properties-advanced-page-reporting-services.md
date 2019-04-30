---
title: 서버 속성(고급 페이지) - Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.advanced.f1
ms.assetid: 07b78a84-a6aa-4502-861d-349720ef790e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a4123ea79502821026b80254db4fba7a61e5f565
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63158768"
---
# <a name="server-properties-advanced-page---reporting-services"></a>서버 속성(고급 페이지) - Reporting Services
  이 페이지를 사용하여 보고서 서버의 시스템 속성을 설정할 수 있습니다. 시스템 속성을 설정하는 데에는 여러 가지 방법이 있습니다. 이 도구는 그래픽 사용자 인터페이스를 제공하므로 코드를 작성하지 않고도 속성을 설정할 수 있습니다.  
  
 이 페이지를 열려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 시작하고 보고서 서버 인스턴스에 연결한 다음 보고서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **고급** 을 클릭하여 이 페이지를 엽니다.  
  
## <a name="options"></a>변수  
 **EnableMyReports**  
 내 보고서 기능이 설정되어 있는지 여부를 나타냅니다. `true` 값은 이 기능이 설정되어 있음을 나타냅니다.  
  
 **MyReportsRole**  
 사용자의 내 보고서 폴더에서 보안 정책을 만들 때 사용된 역할의 이름입니다. 기본값은 `My Reports Role`입니다.  
  
 **EnableClientPrinting**  
 보고서 서버에서 RSClientPrint ActiveX 컨트롤을 다운로드할 수 있는지 여부를 지정합니다. 유효한 값은 `true` 및 `false`입니다. 기본값은 `true`입니다. 이 컨트롤에 필요한 추가 설정에 대한 자세한 내용은 [Reporting Services에 대해 클라이언트 쪽 인쇄 사용 및 사용 안 함](../report-server/enable-and-disable-client-side-printing-for-reporting-services.md)을 참조하세요.  
  
 **EnableExecutionLogging**  
 보고서 실행 로깅이 설정되어 있는지 여부를 나타냅니다. 기본값은 `true`입니다. 보고서 서버 실행 로그에 대 한 자세한 내용은 참조 하세요. [보고서 서버 실행 로그 및 ExecutionLog3 뷰](../report-server/report-server-executionlog-and-the-executionlog3-view.md)합니다.  
  
 **ExecutionLogDaysKept**  
 실행 로그에 보고서 실행 정보를 보관하는 일 수입니다. 이 속성에 유효한 값은 `-1`부터 `2`,`147`,`483`,`647`까지입니다. 값이 `-1`이면 실행 로그 테이블에서 항목이 삭제되지 않습니다. 기본값은 `60`입니다.  
  
 **SessionTimeout**  
 세션이 활성 상태로 유지되는 시간(초)입니다. 기본값은 `600`입니다.  
  
 **SharePointIntegratedMode**  
 서버 모드를 나타내는 읽기 전용 속성입니다. 이 값이 False이면 보고서 서버는 기본 모드로 실행됩니다.  
  
 **SiteName**  
 보고서 관리자의 페이지 제목에 표시되는 보고서 서버 사이트의 이름입니다. 기본값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]입니다. 이 속성은 빈 문자열일 수 있습니다. 최대 길이는 8,000자입니다.  
  
 **StoredParametersLifetime**  
 저장된 매개 변수를 저장할 수 있는 최대 일 수를 지정합니다. 유효한 값은 `-1`, `+1`부터 `2,147,483,647`까지입니다. 기본값은 `180`일입니다.  
  
 **StoredParametersThreshold**  
 보고서 서버에서 저장할 수 있는 매개 변수 값의 최대 수를 지정합니다. 유효한 값은 `-1`, `+1`부터 `2,147,483,647`까지입니다. 기본값은 `1500`입니다.  
  
 **UseSessionCookies**  
 보고서 서버에서 클라이언트 브라우저와 통신할 때 세션 쿠키를 사용해야 하는지 여부를 나타냅니다. 기본값은 `true`입니다.  
  
 **ExternalImagesTimeout**  
 외부 이미지 파일을 검색해야 하는 시간을 지정합니다. 이 시간을 넘기면 연결 시간이 초과된 것으로 처리됩니다. 기본값은 `600` 시간 (초)입니다.  
  
 **SnapshotCompression**  
 스냅숏의 압축 방식을 정의합니다. 기본값은 `SQL`입니다. 유효한 값은 다음과 같습니다.  
  
 **SQL =** 보고서 서버 데이터베이스에 저장될 때 스냅숏이 압축됩니다. 이것은 현재 동작입니다.  
  
 **None =** 스냅숏이 압축되지 않습니다.  
  
 **All =** 보고서 서버 데이터베이스, 파일 시스템을 포함한 모든 스토리지 옵션에 대해 스냅숏이 압축됩니다.  
  
 **SystemReportTimeout**  
 보고서 서버 네임스페이스에서 관리되는 모든 보고서에 대한 기본 보고서 처리 제한 시간 값(초)입니다. 이 값은 보고서 수준에서 무시할 수 있습니다. 이 속성을 설정하면 지정된 시간이 만료될 경우 보고서 서버가 보고서 처리를 중지합니다. 유효한 값은 `-1`부터 `2`,`147`,`483`,`647`까지입니다. 값이 `-1`이면 네임스페이스의 보고서 처리 중 시간 제한으로 인한 중지가 발생하지 않습니다. 기본값은 `1800`입니다.  
  
 **SystemSnapshotLimit**  
 하나의 보고서에 대해 저장되는 최대 스냅숏 수입니다. 유효한 값은 `-1`부터 `2`,`147`,`483`,`647`까지입니다. 값이 `-1`이면 스냅숏 제한이 없습니다.  
  
 **EnableIntegratedSecurity**  
 보고서 데이터 원본 연결에 Windows 통합 보안이 지원되는지 여부를 지정합니다. 기본값은 `True`입니다. 유효한 값은 다음과 같습니다.  
  
 `True` = Windows 통합 보안이 사용됩니다.  
  
 `False` = Windows 통합 보안이 사용되지 않습니다. Windows 통합 보안을 사용하도록 구성된 보고서 데이터 원본은 실행되지 않습니다.  
  
 `EnableLoadReportDefinition`  
 이 옵션을 선택하면 사용자가 보고서 작성기 보고서에서 임시 보고서 실행을 수행할 수 있는지 여부를 지정할 수 있습니다. 이 옵션 설정에 따라 보고서 서버의 `EnableLoadReportDefinition` 속성 값이 결정됩니다.  
  
 이 옵션의 선택을 취소하면 속성은 False로 설정되며 보고서 모델을 데이터 원본으로 사용하는 보고서에 대해 보고서 서버가 클릭 광고 보고서를 생성하지 않습니다. LoadReportDefinition 메서드에 대한 모든 호출은 차단됩니다.  
  
 이 옵션을 끄면 악의적인 사용자가 LoadReportDefinition 요청으로 보고서 서버에 오버로드를 가하여 서비스 거부 공격을 실행할 수 있는 위협이 완화됩니다.  
  
 **EnableRemoteErrors**  
 원격 컴퓨터에서 보고서를 요청하는 사용자에 대해 반환되는 오류 메시지에 외부 오류 정보(예: 보고서 데이터 원본에 대한 오류 정보)를 포함합니다. 유효한 값은 `true` 및 `false`입니다. 기본값은 `false`입니다. 자세한 내용은 [원격 오류 사용&#40;Reporting Services&#41;](../report-server/enable-remote-errors-reporting-services.md)을 참조하세요.  
  
 **EnableReportDesignClientDownload**  
 보고서 서버에서 보고서 작성기 설치 패키지를 다운로드할 수 있는지 여부를 지정합니다. 이 설정을 해제하면 보고서 작성기에 대한 URL이 작동하지 않습니다. 자세한 내용은 [보고서 작성기 액세스 구성](../report-server/configure-report-builder-access.md)을 참조하세요.  
  
 **EditSessionCacheLimit**  
 보고서 편집 세션에서 활성화될 수 있는 데이터 캐시 항목 수를 지정합니다. 기본값은 5입니다.  
  
 **EditSessionTimeout**  
 보고서 편집 세션이 시간 초과될 때까지 걸리는 시간(초)을 지정합니다. 기본값은 7200초(2시간)입니다.  
  
 **EnableTestConnectionDetailedErrors**  
 사용자가 보고서 서버를 사용하여 데이터 원본 연결을 테스트할 때 클라이언트 컴퓨터로 자세한 오류 메시지를 보낼지 여부를 나타냅니다. 기본값은 `true`입니다. 이 옵션이 `false`로 설정되어 있으면 일반 오류 메시지만 보냅니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 속성 설정&#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Management Studio에서 보고서 서버에 연결](connect-to-a-report-server-in-management-studio.md)   
 [Reporting Services 속성](../report-server-web-service/net-framework/reporting-services-properties.md)   
 [Management Studio의 보고서 서버 F1 도움말](report-server-in-management-studio-f1-help.md)   
 [보고서 서버 시스템 속성](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
 [배포 및 관리 태스크 스크립팅](script-deployment-and-administrative-tasks.md)   
 [내 보고서 설정 및 해제](../report-server/enable-and-disable-my-reports.md)  
  
  
