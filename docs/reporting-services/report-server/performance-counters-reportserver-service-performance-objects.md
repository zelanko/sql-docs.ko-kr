---
title: 성능 카운터 - ReportServer 서비스 성능 개체 | Microsoft Docs
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- Report Server service, performance counters
ms.assetid: 2bcacab2-3a4f-4aae-b123-19d756b9b9ed
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: f86af60001deb0991983fe17c3cf1cf9ba3f2552
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893447"
---
# <a name="performance-counters---reportserver-service--performance-objects"></a>성능 카운터 - ReportServer 서비스 성능 개체
  이 항목에서는 **배포에 포함된** ReportServer:Service **및** ReportServerSharePoint:Service [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 성능 개체의 성능 카운터에 대해 설명합니다.  
  
> [!NOTE]  
>  이 성능 개체는 로컬 보고서 서버의 이벤트를 모니터링하는 데 사용됩니다. 스케일 아웃 배포에서 보고서 서버를 실행 중이면 카운터는 현재 서버에만 적용되고 스케일 아웃 배포 전체에는 적용되지 않습니다.  
  
 성능 개체는 Windows 성능 모니터(**Perfmon.exe**)에서 제공됩니다. 자세한 내용은 Windows 설명서를 참조하십시오. [런타임 프로파일링](https://msdn.microsoft.com/library/w4bz2147.aspx)(https://msdn.microsoft.com/library/w4bz2147.aspx).  
  
 항목 내용  
  
-   [ReportServer:Service 성능 카운터(기본 모드 보고서 서버)](#bkmk_ReportServer)  
  
-   [ReportServerSharePoint:Service(SharePoint 모드 보고서 서버)](#bkmk_ReportServerSharePoint)  
  
-   [PowerShell Cmdlet을 사용하여 목록 반환](#bkmk_powershell)  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
##  <a name="bkmk_ReportServer"></a> ReportServer:Service 성능 카운터(기본 모드 보고서 서버)  
 **ReportServer:Service** 성능 개체에는 보고서 서버 인스턴스에 대한 HTTP 관련 이벤트 및 메모리 관련 이벤트를 추적하는 카운터 모음이 들어 있습니다. 이 성능 개체는 컴퓨터의 각 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스마다 한 번씩 나타나며 사용자는 각 인스턴스에 대한 성능 카운터에서 카운터를 추가하거나 제거할 수 있습니다. 기본 인스턴스의 카운터는 **ReportServer:Service**형식으로 나타납니다. 명명된 인스턴스의 카운터는 **ReportServer$\<***instance_name***>:Service** 형식으로 나타납니다.  
  
 **ReportServer:Service** 성능 개체는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 새로 도입되었으며 이전 버전의 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 에서 IIS(인터넷 정보 서비스) 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]과 함께 제공된 카운터의 하위 집합을 제공합니다. 이러한 새 카운터는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 한정되며 요청, 연결 및 로그온 시도와 같은 보고서 서버에 대한 HTTP 관련 이벤트를 추적합니다. 또한 이 성능 개체에는 메모리 관리 이벤트를 추적하는 카운터가 포함됩니다.  
  
 다음 표에서는 **ReportServer:Service** 성능 개체에 포함된 카운터를 나열합니다.  
  
 ![PowerShell 관련 콘텐츠](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠") 다음 Windows PowerShell 스크립트는 CounterSetName의 성능 카운터 목록을 반환합니다.  
  
```  
(get-counter -listset "ReportServer:Service").paths  
```  
  
|카운터|설명|  
|-------------|-----------------|  
|**Active connections**|서버에서 현재 활성화된 연결 수입니다.|  
|**Bytes Received Total**|서버가 받은 바이트 수입니다. 이 카운터는 보고서 관리자와 보고서 서버가 받은 총 원시 바이트를 계산합니다.|  
|**Bytes Received/sec**|서버가 받은 초당 바이트 수입니다. 이 카운터는 전송이 완료된 경우에만 업데이트됩니다. 즉 카운터는 0을 유지하며 전송이 완료된 후 이 값이 증가합니다.|  
|**Bytes Sent Total**|서버가 보낸 바이트 수입니다. 이 카운터는 보고서 관리자와 보고서 서버가 보낸 총 원시 바이트를 계산합니다.|  
|**Bytes Sent/sec**|서버가 보낸 초당 바이트 수입니다. 이 카운터는 전송이 완료된 경우에만 업데이트됩니다. 즉 카운터는 0을 유지하며 전송이 완료된 후 이 값이 증가합니다.|  
|**Errors Total**|HTTP 요청을 처리하는 동안 발생한 총 오류 수입니다. 이 오류에는 400s 및 500s의 HTTP 상태 코드가 있습니다.|  
|**Errors/sec**|HTTP 요청을 처리하는 동안 발생한 초당 총 오류 수입니다. 이 오류에는 400s 및 500s의 HTTP 상태 코드가 있습니다.|  
|**Logon Attempts Total**|RSWindows 인증 유형에서 로그온을 시도한 횟수입니다. RSWindows 인증 유형에는 RSWindowsNegotiate, RSWindowsNTLM, RSWindowsKerberos 및 RSWindowsBasic이 있습니다. 값 0은 사용자 지정 인증을 나타냅니다.|  
|**Logon Attempts/sec**|로그온 시도 비율입니다.|  
|**Logon Successes Total**|RSWindows 인증 유형에 대해 로그온에 성공한 횟수입니다. RSWindows 인증 유형에는 RSWindowsNegotiate, RSWindowsNTLM, RSWindowsKerberos 및 RSWindowsBasic이 있습니다. 값 0은 사용자 지정 인증을 나타냅니다.|  
|**Logon Successes/sec**|성공한 로그온 비율입니다.|  
|**Memory Pressure State**|서버의 현재 메모리 상태를 나타내는 다음 값(1-5) 중 하나입니다.<br /><br /> 1: 가중 없음<br /><br /> 2: 낮은 가중<br /><br /> 3: 보통 가중<br /><br /> 4: 높은 가중<br /><br /> 5: 초과 가중|  
|**Memory Shrink Amount**|사용 중인 메모리를 줄이기 위해 서버에서 요청한 바이트 수입니다.|  
|**Memory Shrink Notifications/sec**|사용 중인 메모리를 줄이기 위해 마지막 1초에 서버에서 발행한 알림 수입니다. 이 값은 서버에서 메모리 가중을 경험하는 횟수를 나타냅니다.|  
|**Requests Disconnected**|통신 오류로 인해 연결이 끊어진 요청 수입니다.|  
|**Requests Executing**|현재 처리 중인 요청 수입니다.|  
|**Requests Not Authorized**|실패한 요청 수입니다(HTTP 401 상태 코드).|  
|**Requests Rejected**|서버 리소스 부족으로 인해 처리되지 않은 총 요청 수입니다. 이 카운터는 서버가 사용 중임을 나타내는 HTTP 503 상태 코드를 반환하는 요청 수를 나타냅니다.|  
|**Requests Total**|시작 후 보고서 서버 서비스에서 받은 총 요청 수입니다. 이 카운터는 보고서 관리자에 보낸 요청 수와 보고서 관리자가 보고서 서버로 보낸 요청 수를 계산합니다.|  
|**Requests/sec**|초당 처리된 요청 수입니다. 이 값은 애플리케이션 현재 처리량을 나타냅니다.|  
|**Tasks Queued**|스레드를 사용할 수 있을 때까지 기다리는 태스크 수입니다. 보고서 서버에 대한 각 요청은 하나 이상의 태스크에 해당합니다. 이 카운터는 처리할 준비가 된 태스크의 수만 나타내며 현재 실행 중인 태스크 수는 포함하지 않습니다.|  
  
##  <a name="bkmk_ReportServerSharePoint"></a> ReportServerSharePoint:Service(SharePoint 모드 보고서 서버)  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 **ReportServerSharePoint:Service** 성능 개체가 추가되었습니다.  
  
 ![PowerShell 관련 콘텐츠](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠") 다음 Windows PowerShell 스크립트는 CounterSetName의 성능 카운터 목록을 반환합니다.  
  
```  
(get-counter -listset "ReportServerSharePoint:Service").paths  
```  
  
|카운터|설명|  
|-------------|-----------------|  
|**Memory Pressure State**||  
|**Memory Shrink Amount**||  
|**Memory Shrink Notifications/Sec**||  
  
##  <a name="bkmk_powershell"></a> PowerShell Cmdlet을 사용하여 목록 반환  
 ![PowerShell 관련 콘텐츠](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠") 다음 Windows PowerShell 스크립트는 CounterSetName "ReportServerSharePoint:Service"의 성능 카운터 목록을 반환합니다.  
  
```  
(get-counter -listset "ReportServerSharePoint:Service").paths  
```  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 성능 모니터링](../../reporting-services/report-server/monitoring-report-server-performance.md)   
 [MSRS 2011 웹 서비스 및 MSRS 2011 Windows 서비스 성능 개체에 대한 성능 카운터&#40;기본 모드&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-web-service-performance-objects.md)   
 [MSRS 2011 웹 서비스 SharePoint 모드 및 MSRS 2011 Windows 서비스 SharePoint 모드 성능 개체에 대한 성능 카운터&#40;SharePoint 모드&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)  
  
  
