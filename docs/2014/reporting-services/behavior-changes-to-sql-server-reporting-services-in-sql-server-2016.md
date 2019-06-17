---
title: SQL Server 2014에서에서 SQL Server Reporting Services 동작 변경 내용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- rows [Reporting Services], heights
- leading blanks
- installing Reporting Services, behavior changes with release
- cryptography [Reporting Services]
- Setup [Reporting Services], behavior changes with release
- DefaultValueQueryBased property
- encryption [Reporting Services]
- decryption [Reporting Services]
- blank characters [SQL Server]
- initializing installations [Reporting Services]
- behavior changes [Reporting Services]
ms.assetid: 2a767f0f-84f2-4099-8784-1e37790f858e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 91fa7a66981f3e36c7e25babffbf73dc2519a0c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109935"
---
# <a name="behavior-changes-to-sql-server-reporting-services--in-sql-server-2014"></a>SQL Server 2014에서 SQL Server Reporting Services의 동작 변경 내용
  이 항목에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 동작 변경 내용에 대해 설명합니다. 동작 변경 내용은 이전 버전의 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 와 비교해서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 기능이 작동하고 상호 작용하는 방법에 영향을 줍니다.  
  
 항목 내용  
  
-   [SQL Server 2014 Reporting Services Behavior Changes](#bkmk_sql14)  
  
-   [SQL Server 2012 Reporting Services Behavior Changes](#bkmk_rc0)  
  
-   [SQL Server 2008 R2 Reporting Services Behavior Changes](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Reporting Services 동작 변경 내용  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]기능에는 동작 변경 내용이 없습니다.  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Reporting Services 동작 변경 내용  
 이 섹션에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드의 동작 변경 내용에 대해 설명합니다.  
  
### <a name="view-items-permission-will-not-download-shared-datasets-sharepoint-mode"></a>항목 보기 권한으로 공유 데이터 집합 다운로드 불가(SharePoint 모드)  
 **새 동작:** SharePoint "항목 보기" 권한이 있는 사용자는 Reporting Services 공유 데이터 집합의 콘텐츠를 다운로드 더 이상 수 없습니다. 이 동작 변경은 보고서, 데이터 원본 및 모델에 대 한 "항목 보기" 권한이 있는 일치 됩니다. "항목 보기" 권한이 있는 사용자 보기를 업데이트 하 고 보고서, 데이터 원본 및 모델을 실행할 수 있지만 해당 콘텐츠를 다운로드 하지 못하는 합니다.  
  
 **이전 동작:** SharePoint "항목 보기" 권한이 있는 사용자는 Reporting Services 공유 데이터 집합의 콘텐츠를 다운로드 수 없습니다.  
  
 SharePoint 권한 수준에 대한 자세한 내용은 [사용자 권한 및 사용 권한 수준](https://technet.microsoft.com/library/cc721640.aspx)을 참조하세요.  
  
### <a name="report-server-trace-logs-are-in-a-new-location-for-sharepoint-mode-sharepoint-mode"></a>SharePoint 모드에서 보고서 서버 추적 로그가 새 위치에 있음(SharePoint 모드)  
 **새 동작:** SharePoint 모드로 설치 된 보고서 서버의 경우 보고서 서버 추적 로그가 %Programfiles%\Common Files\Microsoft Shared\Web Server Extensions\14\Web Services\ReportServer\LogFiles 아래 됩니다.  
  
 **이전 동작:** 보고서 서버 추적 로그가 다음과 비슷한 경로 아래에서 찾을 수 없습니다: SQL Server %Programfilesdir%\Microsoft\\< RS_instance > services\logfiles  
  
### <a name="getserverconfiginfo-soap-api-is-no-longer-supported-sharepoint-mode"></a>GetServerConfigInfo SOAP API가 더 이상 지원되지 않음(SharePoint 모드)  
 **새 동작**: PowerShell cmdlet "Get-sprsserviceapplicationservers"를 사용 합니다.  
  
 **이전 동작:** 고객이 SOAP 클라이언트 코드와 직접 통신할 수를 개발할 수는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 끝점 및 GetReportServerConfigInfo() 호출 합니다.  
  
### <a name="report-server-configuration-and-management-tools"></a>보고서 서버 구성 및 관리 도구  
  
#### <a name="configuration-manager-is-not-used-for-sharepoint-mode"></a>구성 관리자가 SharePoint 모드에서 사용되지 않음  
 **새 동작:** [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Configuration Manager에는 더 이상 SharePoint 모드 보고서 서버만 지원 합니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드 구성을 이제 SharePoint 중앙 관리를 사용하여 완료할 수 있으므로 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구성 관리자가 더 이상 SharePoint 모드를 지원하지 않습니다. 구성 관리자는 이제 기본 모드 보고서 서버에만 사용됩니다.  
  
#### <a name="you-cannot-change-the-server-from-one-mode-to-another"></a>서버를 한 모드에서 다른 모드로 변경할 수 없음  
 **새 동작:** 서버 모드를 변경할 수 없습니다. 보고서 서버를 기본 모드로 설치하는 경우 이것을 SharePoint 모드로 변경하거나 다시 구성할 수 없습니다. SharePoint 모드로 설치하는 경우 보고서 서버를 기본 모드로 변경할 수 있습니다.  
  
 **이전 동작:** 고객 설치는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드의 보고서 서버. 고객이 보고서 서버를 기본 모드로 전환하려는 경우 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구성 관리자를 열어 새 기본 모드 데이터베이스를 만들거나 기존 기본 모드 데이터베이스에 연결하여 기본 모드로 전환할 수 있었습니다. 또한 고객은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 SharePoint 모드에서 기본 모드로 전환할 수 있었습니다.  
  
##  <a name="bkmk_kj"></a> SQL Server 2008 R2 Reporting Services 동작 변경 내용  
 이 섹션에서는 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 동작 변경 내용에 대해 설명합니다.  
  
> [!NOTE]  
>  SQL Server 2008 R2는 SQL Server 2008의 부 버전 업그레이드이므로 SQL Server 2008 섹션의 내용도 검토하는 것이 좋습니다.  
  
### <a name="secureconnectionlevel-property-in-the-reporting-services-wmi-provider-library"></a>Reporting Services WMI 공급자 라이브러리의 SecureConnectionLevel 속성  
 용 WMI 공급자 라이브러리에서 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], **SecureConnectionLevel** 속성의 값을 사용 하면 `0`를`1`,`2`를`3`를 사용 하 여 `0` 보안 소켓 레이어 (SSL) 웹 서비스 메서드 중 하나에 대 한 필수 임을 나타내는 `3` SSL은 모든 웹 서비스 메서드에 대 한 필수 항목 임을 나타내는 및 `1` 고 `2` 웹 서비스 메서드의 하위 집합을 나타내는 SSL이 필요 합니다. [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 이러한 값은 단 두 가지 의미를 갖습니다.  
  
-   `0`은 웹 서비스에 메서드에 SSL이 필요하지 않음을 나타냅니다.  
  
-   양의 정수는 모든 웹 서비스에 메서드에 SSL이 필요함을 나타냅니다.  
  
 이 변경 내용은 보고서 서버에서 웹 서비스 호출에 응답하는 방식을 결정합니다. 예를 들어 <xref:ReportService2005.ReportingService2005.ListSecureMethods%2A> 이제 아무 것도 반환 하는 경우 **SecureConnectionLevel** 의 모든 메서드 및 0으로 설정 됩니다 <xref:ReportService2005.ReportingService2005> 하는 경우 **SecureConnectionLevel** 로 설정 된 `1`를 `2`, 또는 `3`합니다.  
  
## <a name="see-also"></a>관련 항목  
 [새로운 &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [SQL Server 2014에서에서 SQL Server Reporting Services에서 사용 되지 않는 기능](deprecated-features-in-sql-server-reporting-services-ssrs.md)   
 [SQL Server 2014에서에서 SQL Server Reporting Services에 지원 되지 않는 기능](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)   
 [SQL Server 2014에서 SQL Server Reporting Services의 주요 변경 내용](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)  
  
  
