---
title: Reporting Services 구독 모니터링 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], inactive
- subscriptions [Reporting Services], status
- monitoring [Reporting Services], subscriptions
- status information [Reporting Services]
- inactive subscriptions [Reporting Services]
ms.assetid: 054c4a87-60bf-4556-9a8c-8b2d77a534e6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dad31c0742cfa71a3a5f38659adab9bea220ee0e
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56289642"
---
# <a name="monitor-reporting-services-subscriptions"></a>Reporting Services 구독 모니터링
  사용자 인터페이스, Windows PowerShell 또는 로그 파일을 통해 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독을 모니터링할 수 있습니다. 모니터링에 사용할 수 있는 옵션은 실행 중인 보고서 서버의 모드에 따라 달라집니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드|  
  
 **항목 내용**  
  
-   [기본 모드 사용자 인터페이스](#bkmk_native_mode)  
  
-   [SharePoint 모드](#bkmk_sharepoint_mode)  
  
-   [PowerShell을 사용한 구독 모니터링](#bkmk_use_powershell)  
  
-   [비활성 구독 관리](#bkmk_manage_inactive)  
  
##  <a name="bkmk_native_mode"></a> 기본 모드 사용자 인터페이스  
 개별 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 사용자는 보고서 관리자의 **내 구독** 페이지 또는 **구독** 탭을 사용하여 구독 상태를 모니터링할 수 있습니다. 구독 페이지에는 구독이 마지막으로 실행된 시간과 구독 상태를 나타내는 열이 있습니다. 구독을 처리하도록 예약하면 상태 메시지가 업데이트됩니다. 트리거가 발생하지 않으면(예: 보고서 실행 스냅숏이 새로 고쳐지지 않거나 일정이 실행되지 않는 경우) 상태 메시지가 업데이트되지 않습니다.  
  
 다음 표에서는 **상태** 열에 사용할 수 있는 값에 대해 설명합니다.  
  
|상태|설명|  
|------------|-----------------|  
|새 구독|구독을 처음 만들 때 나타납니다.|  
|비활성|구독을 처리할 수 없을 때 나타납니다. 자세한 내용은 이 항목의 뒷부분에 있는 "비활성 구독 관리"를 참고하십시오.|  
|완료: 총 \<*number*>개 중 \<*number*>개가 처리되었으며 \<*number*>개의 오류가 발생했습니다.|데이터 기반 구독 실행 상태를 나타냅니다. 이 메시지는 일정 예약 및 배달 프로세서에서 제공합니다.|  
|\<*number*>개가 처리됨|일정 예약 및 배달 프로세서에서 성공적으로 배달했거나 더 이상 배달하지 않는 알림의 수입니다. 데이터 기반 배달이 완료되면 처리된 알림 수가 생성된 알림의 총 수와 같아야 합니다.|  
|총 \<*number*>개|구독의 마지막 배달에 대해 생성된 알림의 총 수입니다.|  
|\<*number*>개의 오류|일정 예약 및 배달 프로세서에서 배달하지 못했거나 더 이상 배달하지 않는 알림의 수입니다.|  
|메일 전송 실패: 서버에 연결하지 못해 전송하지 못했습니다.|보고서 서버가 메일 서버에 연결하지 못했음을 나타냅니다. 이 메시지는 전자 메일 배달 확장 프로그램에서 제공합니다.|  
|\<*filename*> 파일을 \<path>에 썼습니다.|파일 공유 위치에 성공적으로 배달했음을 나타냅니다. 이 메시지는 파일 공유 배달 확장 프로그램에서 제공합니다.|  
|파일에 쓰는 동안 알 수 없는 오류가 발생했습니다.|파일 공유 위치에 배달하지 못했음을 나타냅니다. 이 메시지는 파일 공유 배달 확장 프로그램에서 제공합니다.|  
|대상 폴더 \<path>에 연결하지 못했습니다. 대상 폴더가 있거나 파일이 공유되어 있는지 확인하십시오.|지정한 폴더를 찾을 수 없음을 나타냅니다. 이 메시지는 파일 공유 배달 확장 프로그램에서 제공합니다.|  
|\<filename> 파일을 \<path>에 쓸 수 없습니다. 다시 시도하는 중입니다.|파일을 새 버전으로 업데이트할 수 없음을 나타냅니다. 이 메시지는 파일 공유 배달 확장 프로그램에서 제공합니다.|  
|\<filename>: \<message> 파일에 쓰지 못했습니다.|파일 공유 위치에 배달하지 못했음을 나타냅니다. 이 메시지는 파일 공유 배달 확장 프로그램에서 제공합니다.|  
|\<custom status messages>|배달 확장 프로그램에서 제공하는 배달 성공 및 실패에 대한 상태 메시지입니다. 타사 또는 사용자 지정 배달 확장 프로그램을 사용할 경우 추가 상태 메시지가 제공될 수 있습니다.|  
  
 또한, 보고서 서버 관리자는 현재 처리 중인 표준 구독을 모니터링할 수 있습니다. 데이터 기반 구독은 모니터링할 수 없습니다. 자세한 내용은 [실행 중인 프로세스 관리](../../reporting-services/subscriptions/manage-a-running-process.md)를 참조하세요.  
  
 구독을 배달할 수 없는 경우(예: 메일 서버를 사용할 수 없는 경우) 배달 확장 프로그램에서 배달을 다시 시도합니다. 구성 설정에 따라 시도할 횟수가 지정됩니다. 기본값은 다시 시도 안 함입니다. 보고서가 데이터 없이 처리되는 경우(예: 데이터 원본이 오프라인 상태인 경우)도 있습니다. 이런 경우 해당 사실을 나타내는 텍스트가 메시지 본문에 제공됩니다.  
  
### <a name="native-mode-log-files"></a>기본 모드 로그 파일  
 배달 중에 오류가 발생하면 보고서 서버 추적 로그에 항목이 하나 생성됩니다.  
  
 보고서 서버 관리자는 **reportserverservice_\*.log** 파일을 검토하여 구독 배달 상태를 확인할 수 있습니다. 전자 메일 배달의 경우 보고서 서버 로그 파일에 처리 및 특정 전자 메일 계정으로 배달 레코드가 포함됩니다. 다음은 로그 파일의 기본 위치입니다.  
  
 `C:\Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\LogFiles`  
  
 다음은 로그 파일 이름의 예입니다.  
  
 `ReportServerService__05_21_2014_00_05_07.log`  
  
 다음은 구독과 관련된 추적 로그 파일 예제 오류 메시지입니다.  
  
-   library!WindowsService_7!b60!05/20/2014-22:34:36:: i INFO: Initializing EnableExecutionLogging to 'True'  as specified in Server system properties.emailextension!WindowsService_7!b60!05/20/2014-22:34:41:: e ERROR: **메일을 보내는 중 오류가 발생했습니다**. 예외:  System.Net.Mail.SmtpException: SMTP 서버에 보안 연결이 필요하거나 클라이언트가 인증되지 않았습니다. 서버 응답: 5.7.1 System.Net.Mail.MailCommand.CheckResponse(SmtpStatusCode statusCode, 문자열 응답)에서 클라이언트가 인증되지 않았습니다.  
  
 로그 파일에는 보고서를 열었는지 여부 또는 배달이 실제로 성공했는지 여부에 대한 정보가 없습니다. 성공적인 배달은 일정 예약 및 배달 프로세서에서 오류가 발생하지 않고 보고서 서버가 메일 서버에 연결되었음을 의미합니다. 사용자의 사서함에 전자 메일을 배달할 수 없다는 메시지 오류가 표시될 경우 해당 정보는 로그 파일에 포함되지 않습니다. 로그 파일에 대한 자세한 내용은 [Reporting Services 로그 파일 및 소스](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)를 참조하세요.  
  
##  <a name="bkmk_sharepoint_mode"></a> SharePoint 모드  
 SharePoint 모드에서 구독 모니터링: 구독 상태는 **구독 관리** 페이지에서 모니터링할 수 있습니다.  
  
1.  보고서가 있는 문서 라이브러리로 이동합니다.  
  
2.  보고서의 상황에 맞는 메뉴를 엽니다(**...**).  
  
3.  확장된 메뉴 옵션을 선택합니다(**...**).  
  
4.  **구독 관리**를 선택합니다.  
  
### <a name="sharepoint-uls-log-files"></a>SharePoint ULS 로그 파일  
 구독 관련 정보는 SharePoint ULS 로그에 기록됩니다. ULS 로그에 대한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 이벤트를 구성하는 방법에 대한 자세한 내용은 [SharePoint 추적 로그에 대한 Reporting Services 이벤트 설정&#40;ULS&#41;](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)를 참조하세요.  다음은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독과 관련된 ULS 로그 항목의 예입니다.  
  
||||||||  
|-|-|-|-|-|-|-|  
|date|처리|영역|범주|Level|Correlation|메시지|  
|5/21/2014 14:34:06:15|응용 프로그램 풀: a0ba039332294f40bc4a81544afde01d|SQL Server Reporting Services|보고서 서버 전자 메일 확장 프로그램|예기치 않은 오류|( 비어 있음)|**메일을 보내는 중 오류가 발생했습니다.** 예외:  System.Net.Mail.SmtpException: 사서함을 사용할 수 없습니다. 서버 응답: 5.7.1 클라이언트가 Microsoft.ReportingServices.EmailDeliveryProvider.EmailProvider.Deliver(Notification 알림)의 System.Net.Mail.DataStopCommand.Send(SmtpConnection conn)  at System.Net.Mail.SmtpClient.Send(MailMessage 메시지)의 System.Net.Mail.DataStopCommand.CheckResponse(SmtpStatusCode statusCode, 문자열 serverResponse)에서 이 보낸 사람으로 보낼 수 있는 권한이 없습니다.|  
  
##  <a name="bkmk_use_powershell"></a> PowerShell을 사용한 구독 모니터링  
 기본 모드나 SharePoint 모드 구독의 상태를 확인하는 데 사용할 수 있는 PowerShell 스크립트 예가 필요하면 [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)을 참조하세요.  
  
##  <a name="bkmk_manage_inactive"></a> 비활성 구독 관리  
 구독이 비활성 상태가 되면 구독이 처리되지 못하게 하는 기본 조건을 해결하여 구독을 다시 활성화하거나 해당 구독을 삭제해야 합니다. 처리할 수 없게 하는 조건이 발생하면 구독이 비활성화될 수 있습니다. 이러한 조건은 다음과 같습니다.  
  
-   구독에 지정된 배달 확장 프로그램이 제거된 경우  
  
-   자격 증명 설정을 저장된 값에서 통합된 값이나 프롬프트된 값으로 변경한 경우  
  
-   보고서 정의에서 매개 변수 이름 또는 데이터 형식을 변경한 다음 보고서를 다시 게시한 경우. 구독에 더 이상 유효하지 않은 매개 변수가 포함되어 있으면 해당 구독이 비활성화됩니다.  
  
-   보고서의 실행 모드를 변경한 경우(예: 보고서 실행 스냅숏으로 실행하도록 요청 시 실행 보고서를 수정한 경우). 자세한 내용은 [보고서 처리 속성 설정](../../reporting-services/report-server/set-report-processing-properties.md)을 참조하세요.  
  
 비활성 구독은 구독 자체에 메시지로 표시됩니다. 이 메시지에는 해당 원인과 구독을 다시 활성화하는 단계에 대한 정보가 포함되어 있습니다.  
  
 여러 조건으로 인해 구독이 비활성화되면 보고서 서버가 구독을 실행할 때 해당 사실이 구독에 반영됩니다. 구독을 매주 금요일 오전 2시에 배달하도록 예약되어 있을 때 배달 확장 프로그램이 월요일 오전 9시에 제거되었다면 금요일 오전 2시까지는 구독에 비활성 상태가 반영되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [기존_기본 모드 보고서 서버 구독 만들기 및 관리](https://msdn.microsoft.com/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)   
 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
  
  
