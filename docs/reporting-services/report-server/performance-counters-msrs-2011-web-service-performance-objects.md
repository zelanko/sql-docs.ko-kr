---
title: 성능 카운터 MSRS 2011 웹 서비스, 성능 개체 | Microsoft Docs
description: MSRS 2011 웹 서비스 및 MSRS 2011 Windows 서비스 성능 개체용 성능 카운터에 대해 알아봅니다.
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- Report Server Web service, performance counters
- Reporting Services performance object
- RS Web Service performance object
- counters [Reporting Services]
- performance [Reporting Services]
ms.assetid: c642fc4f-8734-4626-a194-42ac9cd8e2ef
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016'
ms.openlocfilehash: 655c0a2fdcd36c7b93b87d3d8979751fcd757e8b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97424742"
---
# <a name="performance-counters-msrs-2011-web-service-performance-objects"></a>성능 카운터 MSRS 2011 웹 서비스, 성능 개체
  이 항목에서는 **MSRS 2011 Web Service** 및 **MSRS 2011 Windows Service** 성능 개체에 대한 성능 카운터에 대해 설명합니다. 이 개체는 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 기본 코드 배포의 일부입니다.  
  
> [!NOTE]  
>  이 성능 개체는 로컬 보고서 서버의 이벤트를 모니터링합니다. 스케일 아웃 배포에서 보고서 서버를 실행 중이면 개수는 현재 서버에만 적용되고 스케일 아웃 배포에는 적용되지 않습니다.  
  
 성능 개체는 Windows 성능 모니터(**Perfmon.exe**)에서 제공됩니다. 자세한 내용은 Windows 설명서 [런타임 프로파일링](/dotnet/framework/debug-trace-profile/runtime-profiling)(https://msdn.microsoft.com/library/w4bz2147.aspx) 을 참조하세요.  
  
 SharePoint 모드 성능 카운터와 관련된 내용은 [MSRS 2011 웹 서비스 SharePoint 모드 및 MSRS 2011 Windows 서비스 SharePoint 모드 성능 개체에 대한 성능 카운터&#40;SharePoint 모드&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)를 참조하세요.  
  
 이 항목의 내용:  
  
-   [MSRS 2011 웹 서비스 성능 카운터](#bkmk_webservice)  
  
-   [MSRS 2011 Windows 서비스 성능 카운터](#bkmk_windowsservice)  
  
-   [PowerShell Cmdlet을 사용하여 목록 반환](#bkmk_powershell)  
  
##  <a name="msrs-2011-web-service-performance-counters"></a><a name="bkmk_webservice"></a> MSRS 2011 웹 서비스 성능 카운터  
 **MSRS 2011 Web Service** 성능 개체는 보고서 서버 성능을 모니터링합니다. 이 성능 개체에는 일반적으로 대화형 보고서 보기 작업을 통해 시작된 보고서 서버 처리를 추적하는 데 사용되는 카운터 모음이 들어 있습니다. 이 카운터를 설정하면 모든 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스에 카운터를 적용하거나 특정 인스턴스를 선택할 수 있습니다. 이러한 카운터는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 이 보고서 서버 웹 서비스를 중지할 때마다 다시 설정됩니다.  
  
 다음 표에서는 **MSRS 2011 Web Service** 성능 개체와 함께 제공되는 카운터를 나열합니다.  
  
|카운터|설명|  
|-------------|-----------------|  
|**Active Sessions**|활성 세션 수입니다. 이 카운터는 활성 상태인지 여부에 관계없이 보고서 실행에서 생성된 모든 브라우저 세션의 누적 개수를 제공합니다.<br /><br /> 이 카운터는 세션 레코드를 제거하면 감소합니다. 기본적으로 10분 동안 활동이 없으면 세션이 제거됩니다.|  
|**Cache Hits/Sec**|캐시된 보고서에 대한 초당 요청 수입니다. 이러한 요청은 다시 렌더링된 보고서에 대한 것이며 캐시에서 직접 처리된 보고서에 대한 요청은 아닙니다. (이 항목 뒷부분에 나오는 **Total Cache Hits** 참조)|  
|**Cache Hits/Sec (Semantic Models)**|캐시된 모델에 대한 초당 요청 수입니다. 다시 렌더링된 보고서에 대한 요청이며 캐시에서 직접 처리된 보고서에 대한 요청은 아닙니다.|  
|**Cache Misses/Sec**|캐시에서 보고서를 반환하지 못한 초당 요청 수입니다. 캐싱(디스크 또는 메모리)에 사용된 리소스가 충분한지 여부를 확인할 때 이 카운터를 사용합니다.|  
|**Cache Misses/Sec (Semantic Models)**|캐시에서 모델을 반환하지 못한 초당 요청 수입니다. 캐싱(디스크 또는 메모리)에 사용된 리소스가 충분한지 여부를 확인할 때 이 카운터를 사용합니다.|  
|**First Session Requests/Sec**|매 초마다 보고서 서버 캐시에서 시작된 새 사용자 세션 수입니다.|  
|**Memory Cache Hits/Sec**|메모리 내 캐시에서 보고서가 검색된 초당 횟수입니다. *메모리 내 캐시* 는 캐시 중 CPU 메모리에 보고서를 저장하는 부분입니다. 메모리 내 캐시가 사용되면 보고서 서버는 캐시된 내용에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 쿼리하지 않습니다.|  
|**Memory Cache Misses/Sec**|메모리 내 캐시에서 보고서를 검색하지 못한 초당 횟수입니다.|  
|**Next Session Requests/Sec**|기존 세션에서 열려 있는 보고서(예: 세션 스냅샷에서 렌더링된 보고서)에 대한 초당 요청 수입니다.|  
|**Report Requests**|현재 활성 상태이며 보고서 서버에서 관리되는 보고서 수입니다.|  
|**Reports Executed/Sec**|초당 성공적으로 실행된 보고서 수입니다. 이 카운터는 보고서 볼륨에 대한 통계를 제공합니다. 캐시에서 반환할 수 있는 보고서 요청과 보고서 실행을 비교하기 위해 **Request/Sec** 카운터와 이 카운터를 함께 사용합니다.|  
|**Requests/Sec**|보고서 서버에 대한 초당 요청 수입니다. 이 카운터는 보고서 서버에서 관리하는 모든 종류의 요청을 추적합니다.|  
|**Total Cache Hits**|서비스 시작 이후 캐시에서 보고서를 요청한 총 수입니다. 이 카운터는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 이 보고서 서버 웹 서비스를 중지할 때마다 다시 설정됩니다.|  
|**Total Cache Hits (Semantic Models)**|서비스 시작 이후 캐시에서 모델을 요청한 총 수입니다. 이 카운터는 ASP.NET에서 보고서 서버 웹 서비스를 중지할 때마다 다시 설정됩니다.|  
|**Total Cache Misses**|서비스 시작 이후 캐시에서 보고서를 반환하지 못한 총 횟수입니다. 이 카운터는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 이 보고서 서버 웹 서비스를 중지할 때마다 다시 설정됩니다. 디스크 공간 및 메모리가 충분한지 여부를 확인할 때 이 카운터를 사용합니다.|  
|**Total Cache Misses (Semantic Models)**|서비스 시작 이후 캐시에서 모델을 반환하지 못한 총 횟수입니다. 이 카운터는 ASP.NET에서 보고서 서버 웹 서비스를 중지할 때마다 다시 설정됩니다. 디스크 공간 및 메모리가 충분한지 여부를 확인할 때 이 카운터를 사용합니다.|  
|**Total Memory Cache Hits**|서비스 시작 이후 메모리 내 캐시에서 반환한 캐시된 보고서의 총 수입니다. 이 카운터는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 이 보고서 서버 웹 서비스를 중지할 때마다 다시 설정됩니다. *메모리 내 캐시* 는 캐시 중 CPU 메모리에 보고서를 저장하는 부분입니다. 메모리 내 캐시가 사용되면 보고서 서버는 캐시된 내용에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 쿼리하지 않습니다.|  
|**Total Memory Cache Misses**|서비스 시작 이후 메모리 내 캐시에 대한 총 캐시 누락 수입니다. 이 카운터는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 이 보고서 서버 웹 서비스를 중지할 때마다 다시 설정됩니다.|  
|**Total Processing Failures**|보고서 서버 웹 서비스에 대한 요청 처리 오류 수입니다.|  
|**Total Rejected Threads**|비동기 처리에 대해 거부되고 나중에 동일한 스레드에서 동기 프로세스로 처리된 총 스레드 수입니다. 각 데이터 원본은 하나의 스레드에서 처리됩니다. 스레드 볼륨이 용량을 초과하면 스레드는 비동기 처리에는 거부되고 순차 방식으로 처리됩니다.|  
|**Total Reports Executed**|서비스 시작 이후 성공적으로 실행된 총 보고서 수입니다. 이 카운터는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 이 보고서 서버 웹 서비스를 중지할 때마다 다시 설정됩니다.|  
|**총 요청 수**|서비스 시작 이후 보고서 서버에 대한 총 요청 수입니다. 이 카운터는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 이 보고서 서버 웹 서비스를 중지할 때마다 다시 설정됩니다.|  
  
##  <a name="msrs-2011-windows-service-performance-counters"></a><a name="bkmk_windowsservice"></a> MSRS 2011 Windows 서비스 성능 카운터  
 **MSRS 2011 Windows Service** 성능 개체는 보고서 서버 Windows 서비스를 모니터링합니다. 이 성능 개체에는 예약된 작업을 통해 시작된 보고서 처리를 추적하는 데 사용되는 카운터 모음이 들어 있습니다. 예약된 작업에는 구독 및 배달, 보고서 실행 스냅샷 및 보고서 기록이 포함될 수 있습니다. 이 카운터를 설정하면 모든 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스에 카운터를 적용하거나 특정 인스턴스를 선택할 수 있습니다.  
  
 다음 표에서는 **MSRS 2011 Windows Service** 성능 개체에 포함된 카운터를 나열합니다.  
  
|카운터|설명|  
|-------------|-----------------|  
|**Active Sessions**|보고서 서버 데이터베이스에 저장된 활성 세션의 수입니다. 이 카운터는 활성 상태인지 여부에 관계없이 보고서 구독에서 생성된 사용 가능한 모든 브라우저 세션의 누적 개수를 제공합니다.|  
|**Cache Flushes/Sec**|초당 캐시 플러시 수입니다.|  
|**Cache Hits/Sec**|캐시된 보고서에 대한 초당 요청 수입니다. 이러한 요청은 다시 렌더링된 보고서에 대한 것이며 캐시에서 직접 처리된 보고서에 대한 요청은 아닙니다. (이 항목 뒷부분에 나오는 **Total Cache Hits** 참조)|  
|**Cache Hits/Sec (Semantic Models)**|캐시된 모델에 대한 초당 요청 수입니다.|  
|**Cache Misses/Sec**|캐시에서 보고서를 반환하지 못한 초당 요청 수입니다. 캐싱(디스크 또는 메모리)에 사용된 리소스가 충분한지 여부를 확인할 때 이 카운터를 사용합니다.|  
|**Cache Misses/Sec (Semantic Models)**|캐시에서 모델을 반환하지 못한 초당 요청 수입니다. 캐싱(디스크 또는 메모리)에 사용된 리소스가 충분한지 여부를 확인할 때 이 카운터를 사용합니다.|  
|**Delivers/Sec**|배달 확장 프로그램에서 초당 보고서를 배달한 수입니다.|  
|**Events/Sec**|초당 처리된 이벤트 수입니다. 모니터링된 이벤트에는 **SnapshotUpdated** 및 **TimedSubscription** 이 있습니다.|  
|**First Session Requests/Sec**|초당 만들어진 새 보고서 실행 세션 수입니다.|  
|**Memory Cache Hits/Sec**|메모리 내 캐시에서 보고서가 검색된 초당 횟수입니다. *메모리 내 캐시* 는 캐시 중 CPU 메모리에 보고서를 저장하는 부분입니다. 메모리 내 캐시가 사용되면 보고서 서버는 캐시된 내용에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 쿼리하지 않습니다.|  
|**Memory Cache Misses/Sec**|메모리 내 캐시에서 보고서를 검색하지 못한 초당 횟수입니다.|  
|**Next Session Requests/Sec**|기존 세션에서 열려 있는 보고서(예: 세션 스냅샷에서 렌더링된 보고서)에 대한 초당 요청 수입니다.|  
|**Report Requests**|현재 활성 상태이며 보고서 서버에서 관리되는 보고서 수입니다. 이 카운터는 캐싱 전략을 평가하는 데 사용합니다. 생성된 보고서보다 더 많은 요청이 있을 수 있습니다.|  
|**Reports Executed/Sec**|초당 성공적으로 생성된 보고서 수입니다.|  
|**Requests/Sec**|보고서 서버 서비스가 초당 성공적으로 처리한 총 요청 수입니다.|  
|**Snapshot Updates/Sec**|초당 총 보고서 실행 스냅샷 업데이트 수입니다.|  
|**Total App Domain Recycles**|보고서 서버 Windows 서비스 시작 이후 애플리케이션 도메인의 총 재활용 횟수입니다.|  
|**Total Cache Flushes**|서비스 시작 이후 보고서 서버 캐시의 총 업데이트 수입니다. 애플리케이션 도메인을 재활용하면 이 카운터가 다시 설정됩니다. **Cache Flushes/Sec** 를 참조하세요.|  
|**Total Cache Hits**|보고서 서버 Windows 서비스 시작 이후 캐시에서 직접 처리된 보고서에 대한 총 요청 수입니다. 애플리케이션 도메인을 재활용하면 이 카운터가 다시 설정됩니다. **Cache Hits/Sec** 를 참조하세요.|  
|**Total Cache Hits (Semantic Models)**|보고서 서버 Windows 서비스 시작 이후 캐시에서 직접 처리된 모델에 대한 총 요청 수입니다. 애플리케이션 도메인을 재활용하면 이 카운터가 다시 설정됩니다. **Cache Hits/Sec** 를 참조하세요.|  
|**Total Cache Misses**|보고서 서버 Windows 서비스 시작 이후 캐시에서 보고서를 반환하지 못한 총 횟수입니다. 애플리케이션 도메인을 재활용하면 이 카운터가 다시 설정됩니다. **Cache Misses/Sec** 를 참조하세요.|  
|**Total Cache Misses (Semantic Models)**|보고서 서버 Windows 서비스 시작 이후 캐시에서 모델을 반환하지 못한 총 횟수입니다. 애플리케이션 도메인을 재활용하면 이 카운터가 다시 설정됩니다.|  
|**Total Deliveries**|모든 배달 확장 프로그램의 일정 예약 및 배달 프로세서를 통해 배달한 총 보고서 수입니다. 애플리케이션 도메인을 재활용하면 이 카운터가 다시 설정됩니다.|  
|**Total Events**|보고서 서버 Windows 서비스 시작 이후 이벤트의 총 수입니다. 애플리케이션 도메인을 재활용하면 이 카운터가 다시 설정됩니다.|  
|**Total Memory Cache Hits**|보고서 서버 Windows 서비스 시작 이후 메모리 내 캐시에서 반환된 캐시된 보고서의 총 수입니다. 애플리케이션 도메인을 재활용하면 이 카운터가 다시 설정됩니다.|  
|**Total Memory Cache Misses**|서비스 시작 이후 메모리 내 캐시에 대한 총 캐시 누락 수입니다. 애플리케이션 도메인을 재활용하면 이 카운터가 다시 설정됩니다.|  
|**Total Processing Failures**|보고서 서버 Windows 서비스의 요청 처리 오류 수입니다.|  
|**Total Rejected Threads**|비동기 처리에 대해 거부되고 나중에 동일한 스레드에서 동기 프로세스로 처리된 총 스레드 수입니다. 보통 또는 과도한 로드 상태에서 이 카운터는 계속 증가합니다.|  
|**Total Reports Executed**|실행된 총 보고서 수입니다.|  
|**총 요청 수**|서비스 시작 이후 성공적으로 실행된 총 보고서 수입니다. 애플리케이션 도메인을 재활용하면 이 카운터가 다시 설정됩니다.|  
|**Total Snapshot Updates**|보고서 실행 스냅샷에 대한 총 업데이트 수입니다.|  
  
##  <a name="use-powershell-cmdlets-to-return-lists"></a><a name="bkmk_powershell"></a> PowerShell Cmdlet을 사용하여 목록 반환  
 ![PowerShell 관련 콘텐츠](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠")다음 Windows PowerShell 스크립트는 CounterSetName이 “msr”로 시작되는 카운터 집합을 반환합니다.  
  
```  
get-counter -listset msr*  
```  
  
 다음 Windows PowerShell 스크립트는 CounterSetName의 성능 카운터 목록을 반환합니다.  
  
```  
(get-counter -listset "MSRS 2011 Windows Service").paths  
```  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 성능 모니터링](../../reporting-services/report-server/monitoring-report-server-performance.md)   
 [MSRS 2011 웹 서비스 SharePoint 모드 및 MSRS 2011 Windows 서비스 SharePoint 모드 성능 개체에 대한 성능 카운터&#40;SharePoint 모드&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)   
 [ReportServer:Service 및 ReportServerSharePoint:Service 성능 개체에 대한 성능 카운터](../../reporting-services/report-server/performance-counters-reportserver-service-performance-objects.md)  
  
