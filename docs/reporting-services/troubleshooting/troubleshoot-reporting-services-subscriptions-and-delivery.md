---
title: Reporting Services 구독 및 배달 문제 해결 | Microsoft Docs
ms.custom: ''
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: troubleshooting
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ae1775f7-9919-48ca-8bd7-cc16df274e2c
caps.latest.revision: 16
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3065ee61d14d51caf67b9a62bb88621f9f5beaf6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="troubleshoot-reporting-services-subscriptions-and-delivery"></a>Reporting Services 구독 및 배달 문제 해결
  
    
이 항목의 정보를 참조하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] 보고서 구독, 예약 및 배달 작업 시 발생하는 문제를 해결할 수 있습니다.  
## <a name="log-information"></a>로그 정보
 
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 의 구독 페이지에는 구독의 상태가 포함되지만 구독에 문제가 있는 경우 세부 정보는 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 로그에 있습니다. 
![ssrs_tutorial_datadriven_subscription_status_ReportManager](../../reporting-services/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.png)

**추적 로그:** 추적 로그는 다음 위치에 기록된 텍스트 파일입니다. `\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`

다음은 로그 항목의 예입니다.

```
   subscription WindowsService_10   4c7c    05/24/2016-01:05:06  e ERROR     Failure writing file \\ServerName\SalesReports\so71949.xls : Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider+NetworkErrorException: An impersonation error occurred using the security context of the current user. ---> System.ArgumentException: Value does not fall within the expected range.  05/24/2016
```
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 추적 로그에 대한 자세한 내용은 다음을 참조하세요. 
+ [보고서 서버 추적 로그](../../reporting-services/report-server/report-server-service-trace-log.md)
+ [Reporting Services 로그 파일](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)

**실행 로그 뷰:**

실행 로그는 ReportServer SQL database의 뷰입니다. [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 에 대한 자세한 내용은 [Reporting Services ExecutionLog 및 ExecutionLog3 뷰](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)를 참조하세요.  

----------
## <a name="unable-to-send-reports-using-e-mail-with-windows-server-2003-and-pop3"></a>Windows Server 2003 및 POP3에서 전자 메일을 사용하여 보고서를 보낼 수 없습니다.  
Microsoft Windows Server 2003에서 POP3(Post Office Protocol 버전 3)을 사용하여 전자 메일 응용 프로그램을 실행 중이면 로컬 POP3 서버를 통해 보고서를 보내지 못할 수 있습니다. 로컬 POP3 서버를 통해 전자 메일을 보내도록 보고서 서버를 구성하고 보고서를 보내는 구독을 만든 경우 다음과 같은 오류 메시지가 표시될 수 있습니다.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Failure sending mail: <error message>`  
  
여기서 \<error message>는 CDO(Collaboration Data Objects)에서 반환된 추가 오류 메시지로 바뀝니다.  
  
### <a name="to-resolve-this-problem"></a>이 문제를 해결하려면  
* `SendUsing` Rsreportserver.config **파일에서** 요소의 값을 1로 설정합니다.  
* `SMTPServer` 속성이 비어 있도록 해당 값을 지웁니다. `SMTPServerPickupDirectory` 속성에 대한 값도 제공해야 합니다.   
  
로컬 SMTP 서비스를 사용하여 보고서를 전자 메일로 배달하는 방법에 대한 자세한 내용은 전자 메일 배달을 위한 보고서 서버 구성을 참조하세요.  
  
## <a name="failure-sending-mail-the-server-rejected-the-sender-address-the-server-response-was-454-573-client-does-not-have-permission-to-submit-mail-to-this-server"></a>메일을 보내지 못했습니다. 서버가 보낸 사람 주소를 거부했습니다. 서버 응답: 454 5.7.3 클라이언트가 이 서버에 메일을 제출할 권한이 없습니다.  
이 오류는 SMTP 서버의 보안 정책 설정에 의해 인증된 사용자만 배달할 메일을 제출할 수 있는 경우 발생합니다. SMTP 서버에서 익명 사용자의 전자 메일 제출을 허용하지 않는 경우 시스템 관리자에게 해당 서버 사용 권한을 얻는 방법을 문의하십시오.  
> 이 오류는 Exchange Server 이름을 SMTPServer로 지정한 경우에도 발생할 수 있습니다. 전자 메일 배달에 Exchange 서버를 사용하려면 해당 Exchange 서버에 대해 구성된 SMTP 게이트웨이의 이름을 지정해야 합니다. 이 정보는 Exchange 관리자에게 문의하십시오.  
  
## <a name="subscriptions-are-not-processing"></a>구독이 처리되지 않습니다.  
다음과 같은 상황에서는 구독이 실패할 수 있습니다.   
* 보고서를 트리거하는 데 사용되는 일정이 만료된 경우. 보고서 스냅숏 업데이트를 트리거하는 구독의 경우 스냅숏을 새로 고치는 데 사용되는 일정이 만료될 수 있습니다.  
  
* 보고서 서버, SQL Server 에이전트 또는 전자 메일 서버 응용 프로그램이 실행되고 있지 않습니다.  
* 보고서를 배달할 수 없는 경우(예: 너무 커서 배달하지 못한 경우) 보고서가 너무 커서 배달에 실패하는지 여부를 확인하려면 보고서를 파일로 저장한 뒤 전자 메일로 보내 보십시오. 반드시 구독 시에 지정한 것과 동일한 렌더링 형식을 선택해야 합니다. 배달 오류가 생길 경우 보고서 서버 전자 메일을 사용하는 대신 파일 공유 배달 확장 프로그램을 사용하십시오.  
* 파일 공유 배달에 사용되는 컴퓨터가 실행 중이지 않거나 파일 공유가 읽기 전용 액세스로 구성된 경우  
* 구독에 지정된 배달 확장 프로그램이 설치되지 않았거나 사용할 수 없는 경우  
* 자격 증명 설정을 저장 값에서 통합 값이나 사용자 입력 값으로 변경한 경우  
* 보고서 정의의 매개 변수 이름이나 데이터 형식이 변경되고 보고서가 다시 게시된 경우. 구독에 더 이상 유효하지 않은 매개 변수가 포함되어 있으면 해당 구독이 비활성화됩니다.  
  
자세한 내용은 TechNet Wiki [Troubleshoot issues and errors with Reporting Services(Reporting Services 문제 및 오류 해결)](http://social.technet.microsoft.com/wiki/contents/articles/1633.ssrs-troubleshoot-issues-and-errors-with-reporting-services.aspx)를 참조하세요.  
  
  
    
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]

