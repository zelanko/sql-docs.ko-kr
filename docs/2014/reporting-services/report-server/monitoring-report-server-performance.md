---
title: 보고서 서버 성능 모니터링 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- report servers [Reporting Services], performance
- counters [Reporting Services]
- monitoring performance [Reporting Services]
- SQL Server Reporting Services, performance
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: c1bc13d4-8297-4daf-bb19-4c1e5ba292a6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f020dd812b53e531a3f4634ccba0d2cba980b89e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66103794"
---
# <a name="monitoring-report-server-performance"></a>보고서 서버 성능 모니터링
  성능 모니터링 도구를 통해 보고서 서버 성능을 모니터링하여 서버 작업을 평가하고, 추세를 살피고, 시스템 병목 현상을 진단하고, 현재 시스템 구성이 충분한지 여부를 결정하는 데 도움이 되는 데이터를 수집할 수 있습니다. 서버 성능을 튜닝하기 위해 보고서 서버 애플리케이션 도메인의 재활용 빈도를 지정할 수 있습니다. 자세한 내용은 [보고서 서버 애플리케이션을 위한 사용 가능한 메모리 구성](../report-server/configure-available-memory-for-report-server-applications.md)을 참조하세요.  
  
## <a name="sources-of-performance-data"></a>성능 데이터의 원본  
 기술과 도구를 함께 사용하여 시스템 수행 방법에 대한 포괄적인 정보를 얻을 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Server 운영 체제는 다음 도구를 통해 성능 정보를 제공합니다.  
  
-   작업 관리자  
  
-   이벤트 뷰어  
  
-   성능 콘솔  
  
 작업 관리자는 컴퓨터에서 실행되는 프로그램 및 프로세스에 대한 정보를 제공합니다. 작업 관리자를 사용하여 보고서 서버의 성능을 나타내는 주요 표시기를 모니터링할 수 있습니다. 또한 실행 중인 프로세스의 활동을 평가하고 CPU 및 메모리 사용량에 대한 그래프와 데이터를 볼 수 있습니다. 작업 관리자를 사용하는 방법은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 제품 설명서를 참조하십시오.  
  
 성능 콘솔과 이벤트 뷰어를 사용하여 보고서 처리 및 리소스 소비량에 대한 로그와 경고를 만들 수 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 생성된 Windows 이벤트에 대한 자세한 내용은 [Windows 애플리케이션 로그](windows-application-log.md)를 참조하세요. 성능 콘솔에 대한 자세한 내용은 이 항목 뒷부분에서 "Windows 성능 카운터"를 참조하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티는 캐싱 및 세션 관리에 사용되는 보고서 서버 데이터베이스 및 임시 데이터베이스에 대한 정보를 제공합니다.  
  
## <a name="windows-performance-counters"></a>Windows 성능 카운터  
 특정 성능 카운터를 모니터링하여 다음을 수행할 수 있습니다.  
  
-   예측 작업을 지원하는 데 필요한 시스템 요구 사항을 추정합니다.  
  
-   구성 변경 또는 애플리케이션 업그레이드의 영향을 측정하기 위한 성능 기준을 만듭니다.  
  
-   실제 또는 인위적으로 생성된 특정 로드 하의 애플리케이션 성능을 모니터링합니다.  
  
-   하드웨어 업그레이드를 통해 원하는 성능 효과를 얻었는지 확인합니다.  
  
-   시스템 구성 변경을 통해 원하는 성능 효과를 얻었는지 확인합니다.  
  
## <a name="reporting-services-performance-objects"></a>Reporting Services 성능 개체  
 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 에는 다음과 같은 성능 개체가 포함됩니다.  
  
-   **MSRS 2011 웹 서비스** 및 `MSRS 2011 SharePoint Mode Web Service` 보고서 서버 성능을 모니터링 합니다. 이러한 성능 개체에는 일반적으로 대화형 보고서 보기 작업을 통해 시작된 보고서 서버 처리를 추적하는 데 사용되는 카운터 모음이 들어 있습니다. 이러한 카운터는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 이 보고서 서버 웹 서비스를 중지할 때마다 다시 설정됩니다.  
  
-   예약된 작업 및 보고서 배달을 모니터링하기 위한 `MSRS 2011 Windows Service` 및 `MSRS 2011 Windows Service SharePoint Mode`. 이러한 성능 개체에는 예약된 작업을 통해 시작된 보고서 처리를 추적하는 데 사용되는 카운터 모음이 들어 있습니다. 예약된 작업에는 구독 및 배달, 보고서 실행 스냅샷 및 보고서 기록이 포함됩니다.  
  
-   HTTP 관련 이벤트 및 메모리 관리를 모니터링하기 위한 `ReportServer:Service` 및 `ReportServerSharePoint:Service`. 이러한 카운터는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 한정되며 요청, 연결 및 로그온 시도와 같은 보고서 서버에 대한 HTTP 관련 이벤트를 추적합니다. 이 성능 개체에는 메모리 관리 관련 카운터도 들어 있습니다.  
  
 한 시스템에 보고서 서버 인스턴스가 여러 개 있을 경우 인스턴스를 함께 모니터링하거나 별도로 모니터링할 수 있습니다. 카운터 추가 시 포함할 인스턴스를 선택합니다. 성능 콘솔(perfmon.msc) 사용 및 카운터를 추가하는 방법은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 제품 설명서를 참조하세요.  
  
## <a name="other-performance-counters"></a>기타 성능 카운터  
 사용자 지정 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 성능 카운터는 `MSRS 2008 Web Service`, `MSRS 2008 Windows Service` 및 `ReportServer:Service`에 대해서만 제공됩니다. 다음 성능 개체는 보고서 서버에 대한 추가 성능 모니터링 데이터를 제공합니다.  
  
|성능 개체|메모|  
|------------------------|-----------|  
|`.NET CLR Data` 및 `.NET CLR Memory`|보고서 관리자는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 성능 카운터를 사용합니다. 자세한 내용은 MSDN에서 "Improving .NET Application Performance and Scalability"를 참조하십시오.|  
|`Process`|ReportingServicesService 인스턴스에 대한 `Elapsed Time` 및 `ID Process` 성능 카운터를 추가하여 프로세스 ID별로 프로세스 작동 시간을 추적합니다.|  
  
## <a name="sharepoint-events"></a>SharePoint 이벤트  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 성능 개체 이외에도 SharePoint 통합 모드로 보고서 서버를 실행하고 SharePoint 제품을 사용하도록 보고 환경을 구성한 경우 SharePoint 이벤트를 구성할 수도 있습니다. 이 섹션에서는 SharePoint 통합 모드의 보고서 서버 이벤트를 사용하여 보고 환경이 SharePoint와 통합되는 경우에 유용한 정보를 제공할 수 있는 진단 이벤트를 검토합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [MSRS 2014 웹 서비스 및 MSRS 2014 Windows 서비스 성능 개체에 대 한 성능 카운터는 기본 모드 &#40;&#41;](performance-counters-msrs-2011-web-service-performance-objects.md)  
 보고서 서버 웹 서비스에 사용된 성능 카운터를 설명합니다.  
  
 [SharePoint 모드 &#40;MSRS 2014 웹 서비스 SharePoint 모드 및 MSRS 2014 Windows 서비스 SharePoint 모드 성능 개체에 대 한 성능 카운터&#41;](performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)  
 보고서 서버 Windows 서비스에 사용된 성능 카운터를 설명합니다.  
  
 [ReportServer:Service 및 ReportServerSharePoint:Service 성능 개체에 대한 성능 카운터](performance-counters-reportserver-service-performance-objects.md)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 HTTP 관련 성능 카운터 및 메모리 관련 성능 카운터를 설명합니다.  
  
 SharePoint 통합 모드의 보고서 서버 이벤트  
 SharePoint 제품을 사용하여 보고 환경을 실행할 때 기록할 유용한 진단 이벤트를 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 애플리케이션을 위한 사용 가능한 메모리 구성](../report-server/configure-available-memory-for-report-server-applications.md)   
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](reporting-services-report-server-native-mode.md)   
 [Reporting Services 도구](../tools/reporting-services-tools.md)  
  
  
