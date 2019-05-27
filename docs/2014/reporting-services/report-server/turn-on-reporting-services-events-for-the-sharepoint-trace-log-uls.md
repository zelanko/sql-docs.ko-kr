---
title: SharePoint 추적 로그에 대한 Reporting Services 이벤트 설정(ULS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 81110ef6-4289-405c-a931-e7e9f49e69ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b292805f0cf24a220223adc3a1996b3e5effe54c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66103155"
---
# <a name="turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls"></a>SharePoint 추적 로그에 대한 Reporting Services 이벤트 설정(ULS)
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]부터 SharePoint 모드의 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 서버는 SharePoint ULS(통합 로깅 서비스) 추적 로그에 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 이벤트를 기록할 수 있습니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 관련 범주는 SharePoint 중앙 관리의 모니터링 페이지에서 사용할 수 있습니다.  
  
 항목 내용  
  
-   [일반 ULS 로그 권장 사항](#bkmk_general)  
  
-   [Reporting Services 범주에서 Reporting Services 이벤트를 설정 및 해제하려면](#bkmk_turnon)  
  
-   [권장 구성](#bkmk_recommended)  
  
-   [로그 항목 읽기](#bkmk_readentries)  
  
-   [SQL Server Reporting Services 이벤트 목록](#bkmk_list)  
  
-   [PowerShell에서 로그 파일 보기](#bkmk_powershell)  
  
-   [추적 로그 위치](#bkmk_trace)  
  
##  <a name="bkmk_general"></a> 일반 ULS 로그 권장 사항  
 다음 표에서는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 환경을 모니터링하는 데 권장되는 이벤트 범주 및 수준을 나열합니다. 이벤트를 기록하면 각 항목에 이벤트 기록 시간, 프로세스 이름 및 스레드 ID가 포함됩니다.  
  
|범주|Level|Description|  
|--------------|-----------|-----------------|  
|데이터베이스|자세히|데이터베이스 액세스를 포함하는 이벤트를 기록합니다.|  
|일반|자세히|다음 항목에 대한 액세스를 포함하는 이벤트를 기록합니다.<br /><br /> [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 웹 페이지<br /><br /> 보고서 뷰어 HTTP 처리기<br /><br /> 보고서 액세스 파일(.rdl)<br /><br /> 데이터 원본 파일(.rsds)<br /><br /> SharePoint 사이트의 URL(.smdl 파일)|  
|Office Server 일반|Exception|로그온 실패를 기록합니다.|  
|토폴로지|Verbose|현재 사용자 정보를 기록합니다.|  
|웹 파트|자세히|보고서 뷰어 웹 파트에 대한 액세스를 포함하는 이벤트를 기록합니다.|  
  
##  <a name="bkmk_turnon"></a> Reporting Services 범주에서 Reporting Services 이벤트를 설정 및 해제하려면  
  
1.  SharePoint 중앙 관리에서  
  
2.  **모니터링**을 클릭합니다.  
  
3.  **보고** 그룹에서 **진단 로깅 구성** 을 클릭합니다.  
  
4.  범주 목록에서 **SQL Server Reporting Services** 를 찾습니다.  
  
5.  더하기 기호(+)를 클릭하여 **SQL Server Reporting Services**의 하위 범주를 확장합니다.  
  
6.  추적 로그에 추가할 하위 범주를 선택합니다.  
  
7.  범주 목록 아래쪽에서 **추적 로그에 보고할 최소 중요 이벤트**에 대한 이벤트 수준을 선택합니다. **없음** 을 선택하여 추적을 해제합니다.  
  
> [!NOTE]  
>  **이벤트 로그에 보고할 최소 중요 이벤트** 옵션은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 지원되지 않으므로 무시됩니다.  
  
##  <a name="bkmk_recommended"></a> 권장 구성  
 다음 로깅 옵션을 표준 구성으로 사용하는 것이 좋습니다.  
  
-   **HTTP 리디렉터**  
  
-   **SOAP 클라이언트 프록시**  
  
-   구성에 문제가 있으면 **구성 페이지**를 추가합니다.  
  
 다음 PowerShell cmdlet을 사용하여 모든 현재 팜 진단 로그 설정을 검토할 수 있습니다.  
  
```  
Get-SPDiagnosticConfig  
```  
  
##  <a name="bkmk_readentries"></a> 로그 항목 읽기  
 로그에서 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 항목의 서식은 다음과 같은 방법으로 지정됩니다.  
  
1.  **제품: SQL Server Reporting Services**  
  
2.  **범주:** 서버와 관련 된 이벤트 이름 시작 부분에 "Report Server" 라는 문자가 있습니다. 예: "Report Server Alerting Runtime" 이러한 이벤트는 보고서 서버 로그 파일에도 기록됩니다.  
  
3.  **범주:** 이벤트와 관련 된 나 웹 프런트 엔드 구성 요소 로부터 전달 되는 "Report Server"를 포함 되지 않습니다. 예 "Service Application Proxy" Report Server Alerting Runtime" WFE 항목은 CorrelationID를 포함하지만 서버 항목은 CorrelationID를 포함하지 않습니다.  
  
##  <a name="bkmk_list"></a> SQL Server Reporting Services 이벤트 목록  
 다음 표에는 SQL Server Reporting Services 범주의 이벤트 목록이 나와 있습니다.  
  
|영역 이름|설명 또는 샘플 항목|  
|---------------|-----------------------------------|  
|구성 페이지||  
|HTTP 리디렉터||  
|로컬 모드 처리||  
|로컬 모드 렌더링||  
|SOAP 클라이언트 프록시||  
|UI 페이지||  
|파워 뷰|**LogClientTraceEvents** API에 쓴 로그 항목입니다. 다음 항목의 출처는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]Enterprise Edition용 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 추가 기능의 기능인 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 을 포함하는 클라이언트 애플리케이션입니다.<br /><br /> LogClientTraceEvents API의 모든 로그 항목은 "SQL Server Reporting Services" 및 "파워 뷰" **영역**의 **범주**에 기록됩니다.<br /><br /> "파워 뷰" 영역으로 기록된 항목의 내용은 클라이언트 애플리케이션에 의해 결정됩니다.|  
|보고서 서버 경고 런타임||  
|보고서 서버 응용 프로그램 도메인 관리자||  
|보고서 서버 버퍼링 응답||  
|보고서 서버 캐시||  
|보고서 서버 카탈로그||  
|보고서 서버 청크||  
|보고서 서버 정리||  
|보고서 서버 구성 관리자|샘플 항목:<br /><br /> MediumUsing 보고서 서버 내부 url http://localhost:80/ReportServer.<br /><br /> UnexpectedMissing 또는 잘못된 ExtendedProtectionLevel 설정|  
|보고서 서버 암호화||  
|보고서 서버 데이터 확장 프로그램||  
|보고서 서버 DB 폴링||  
|보고서 서버 기본값||  
|보고서 서버 전자 메일 확장 프로그램||  
|보고서 서버 Excel 렌더러||  
|보고서 서버 확장 프로그램 팩터리||  
|보고서 서버 HTTP 런타임||  
|보고서 서버 이미지 렌더러||  
|보고서 서버 메모리 모니터링||  
|보고서 서버 알림||  
|보고서 서버 처리||  
|보고서 서버 공급자||  
|보고서 서버 렌더링||  
|보고서 서버 보고서 미리 보기||  
|보고서 서버 리소스 유틸리티|샘플 항목:<br /><br /> MediumReporting 서비스 시작 SKU: Evaluation<br /><br /> MediumEvaluation 복사: 180 일 남음|  
|보고서 서버 실행 작업||  
|보고서 서버 실행 요청||  
|보고서 서버 예약||  
|보고서 서버 보안||  
|보고서 서버 서비스 컨트롤러||  
|보고서 서버 세션||  
|보고서 서버 구독||  
|보고서 서버 WCF 런타임||  
|보고서 서버 웹 서버||  
|서비스 애플리케이션 프록시||  
|공유 서비스|샘플 항목:<br /><br /> MediumUpdating ReportingWebServiceApplication<br /><br /> 콘텐츠 데이터베이스에 대한 MediumGranting 액세스입니다.<br /><br /> ReportingWebServiceApplication의 MediumProvisioning 인스턴스<br /><br /> ReportingWebServiceApplication에 대한 MediumProcessing 서비스 계정 변경 내용<br /><br /> MediumSetting 데이터베이스 사용 권한입니다.|  
  
##  <a name="bkmk_powershell"></a> PowerShell에서 로그 파일 보기  
 ![PowerShell 관련 내용](../media/rs-powershellicon.jpg "PowerShell 관련 내용")PowerShell을 사용하여 ULS 로그 파일에서 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 관련 이벤트 목록을 반환할 수 있습니다. ULS 로그 파일 UESQL11SPOINT-20110606-1530.log 파일에서 "**sql server reporting services**"가 포함된 필터링된 행 목록을 반환하려면 SharePoint 2010 관리 셸에서 다음 명령을 입력합니다.  
  
```  
Get-content -path "C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\LOGS\UESQL11SPOINT-20110606-1530.log" | select-string "sql server reporting services"  
```  
  
 ULS 로그를 읽는 데 사용할 수 있는 다운로드 가능한 많은 도구가 있습니다. 예를 들어 [SharePoint LogViewer](http://sharepointlogviewer.codeplex.com/) 또는 [SharePoint ULS 로그 뷰어](http://ulsviewer.codeplex.com/workitem/list/basic)를 다운로드할 수 있습니다. 이 두 도구는 Codeplex에서 다운로드할 수 있습니다.  
  
 PowerShell을 사용하여 로그 데이터를 보는 방법에 대한 자세한 내용은 [진단 로그 보기(SharePoint Server 2010)](https://technet.microsoft.com/library/ff463595.aspx)를 참조하세요.  
  
##  <a name="bkmk_trace"></a> 추적 로그 위치  
 추적 로그 파일은 일반적으로 **c:\Program Files\Common files\Microsoft Shared\Web Server Extensions\14\logs** 폴더에 있지만 SharePoint 중앙 관리의 **진단 로깅** 페이지에서 경로를 확인하거나 변경할 수 있습니다.  
  
 SharePoint 2010 중앙 관리에서 SharePoint 서버에 대해 진단 로깅을 구성하는 방법 및 단계는 [진단 로깅 설정 구성(Windows SharePoint Services)](https://go.microsoft.com/fwlink/?LinkID=114423)을 참조하세요.  
  
  
