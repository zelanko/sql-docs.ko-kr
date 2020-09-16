---
description: SSRS 서비스 애플리케이션에 대한 구독 및 경고 프로비전
title: SSRS 서비스 애플리케이션에 대한 구독 및 경고 프로비전 | Microsoft Docs
ms.date: 06/03/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Shared Service
- SharePoint Mode [Reporting Services]
- SharePoint Mode
- Reporting Services Service Application
- SSRS service application
ms.assetid: d0de3f1f-4887-47fb-bacf-46aaad74c4be
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 28f69b4aa47b45708832162b2b4b8429a847bc65
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454535"
---
# <a name="provision-subscriptions-and-alerts-for-ssrs-service-applications"></a>SSRS 서비스 애플리케이션에 대한 구독 및 경고 프로비전
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독 및 데이터 경고에는 SQL Server 에이전트가 필요하며 SQL Server 에이전트에 대한 사용 권한 구성이 필요합니다. SQL Server 에이전트가 필요하고 SQL Server 에이전트 실행 확인을 나타내는 오류 메시지가 표시되는 경우 사용 권한을 업데이트하거나 확인해야 합니다. 이 항목의 범위는 SharePoint 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 이며, 이 항목에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독을 사용하여 SQL Server 에이전트의 사용 권한을 업데이트하는 세 가지 방법에 대해 설명합니다. 이 항목의 단계에 사용하는 자격 증명에는 서비스 애플리케이션, msdb 및 master 데이터베이스의 개체를 위한 RSExecRole에 실행 권한을 부여하기에 충분한 사용 권한이 있어야 합니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2016 &#124; SharePoint 2013|  
  
 ![서비스 애플리케이션 DB에 대한 SQL 에이전트 권한](../../reporting-services/install-windows/media/rs-provisionsqlagent.gif "서비스 애플리케이션 DB에 대한 SQL 에이전트 권한")  
  
||Description|  
|------|-----------------|  
|**1**|Reporting Services 서비스 애플리케이션 데이터베이스를 호스팅하는 SQL Server 데이터베이스 엔진의 인스턴스입니다.|  
|**2**|SQL 데이터베이스 엔진의 인스턴스에 대한 SQL Server 에이전트의 인스턴스입니다.|  
|**3**|Reporting Services 서비스 애플리케이션 데이터베이스입니다. 이름은 서비스 애플리케이션을 만드는 데 사용된 정보를 기반으로 합니다. 다음은 데이터베이스 이름의 예입니다.<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0_Alerting<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0TempDB|  
|**4**|SQL Server 데이터베이스 엔진 인스턴스의 마스터 및 MSDB 데이터베이스입니다.|  
  
 다음 세 가지 방법 중 하나를 사용하여 사용 권한을 업데이트합니다.  
  
1.  **구독 및 경고 프로비전** 페이지에서 자격 증명을 입력하고 **확인**을 클릭합니다.  
  
2.  구독 및 경고 프로비전 페이지에서 **스크립트 다운로드** 단추를 클릭하여 사용 권한 구성에 사용될 수 있는 Transact-SQL 스크립트를 다운로드합니다.  
  
3.  PowerShell cmdlet을 실행하여 사용 권한 구성에 사용될 수 있는 Transact-SQL 스크립트를 작성합니다.  
  
### <a name="to-update-permissions-using-the-provision-page"></a>프로비전 페이지를 사용하여 사용 권한을 업데이트하려면  
  
1.  SharePoint 중앙 관리의 **애플리케이션 관리** 그룹에서 **서비스 애플리케이션 관리**를 클릭합니다.  
  
2.  목록에서 서비스 애플리케이션을 찾고 애플리케이션 이름을 클릭하거나 **유형** 열을 클릭하여 서비스 애플리케이션을 선택하고 SharePoint 리본에서 **관리** 단추를 클릭합니다.  
  
3.  **Reporting Services 애플리케이션 관리** 페이지에서 **구독 및 경고 프로비전**을 클릭합니다.  
  
4.  SharePoint 관리자가 Master 데이터베이스 및 서비스 애플리케이션 데이터베이스에 대한 충분한 권한이 있을 경우 자격 증명을 입력합니다.  
  
5.  **확인** 단추를 클릭합니다.  
  
##  <a name="to-download-the-transact-sql-script"></a><a name="bkmk_download"></a> Transact-SQL 스크립트를 다운로드하려면  
  
1.  SharePoint 중앙 관리의 **애플리케이션 관리** 그룹에서 **서비스 애플리케이션 관리**를 클릭합니다.  
  
2.  목록에서 서비스 애플리케이션을 찾고 애플리케이션 이름을 클릭하거나 **유형** 열을 클릭하여 서비스 애플리케이션을 선택하고 SharePoint 리본에서 **관리** 단추를 클릭합니다.  
  
3.  **Reporting Services 애플리케이션 관리** 페이지에서 **구독 및 경고 프로비전**을 클릭합니다.  
  
4.  **상태 보기** 영역에서 SQL Server 에이전트가 실행되고 있는지 확인하십시오.  
  
5.  **스크립트 다운로드** 를 클릭하여 SQL Server Management Studio에서 권한 부여를 위해 실행할 수 있는 Transact-SQL 스크립트를 다운로드합니다. 만들어진 스크립트 파일 이름에는 Reporting Services 서비스 애플리케이션의 이름이 포함됩니다(예: **[서비스 애플리케이션 이름]-GrantRights.sql**).  
  
### <a name="to-generate-the-transact-sql-statement-with-powershell"></a>PowerShell을 사용하여 Transact-SQL 문을 만들려면  
  
1.  SharePoint 2016 또는 SharePoint 2013 관리 셸에서 Windows PowerShell cmdlet을 사용하여 Transact-SQL 스크립트를 만들 수도 있습니다.  
  
2.  **시작** 메뉴에서 **모든 프로그램**을 클릭합니다.  
  
3.  **Microsoft SharePoint 2016 제품** 을 확장하고 **Microsoft SharePoint 2016 관리 셸**을 클릭합니다.
  
4.  보고서 서버 데이터베이스, 애플리케이션 풀 계정 및 문 경로의 이름을 바꾸어 다음 PowerShell cmdlet을 업데이트합니다.  
  
     **cmdlet 구문:** `Get-SPRSDatabaseRightsScript -DatabaseName <ReportingServices database name> -UserName <app pool account> -IsWindowsUser | Out-File <path of statement>`  
  
     **샘플 cmdlet:** `Get-SPRSDatabaseRightsScript -DatabaseName ReportingService_46fd00359f894b828907b254e3f6257c -UserName "NT AUTHORITY\NETWORK SERVICE" -IsWindowsUser | Out-File c:\SQLServerAgentrights.sql`  
  
## <a name="using-the-transact-sql-script"></a>Transact-SQL 스크립트 사용  
 프로비전 페이지의 스크립트 다운로드 또는 PowerShell을 사용하여 만든 스크립트를 사용하는 경우 다음 절차를 따릅니다.  
  
#### <a name="to-load-the-transact-sql-script-in-sql-server-management-studio"></a>SQL Server Management Studio에서 Transact-SQL 스크립트를 로드하려면  
  
1.  SQL Server Management Studio를 열려면 **시작** 메뉴에서 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] 을(를) 클릭하고 **SQL Server Management Studio**를 클릭합니다.  
  
2.  **서버에 연결** 대화 상자에서 다음 옵션을 설정합니다.  
  
    -   **서버 유형** 목록에서 **데이터베이스 엔진**을 선택합니다.  
  
    -   **서버 이름**에서 SQL Server 에이전트를 구성하려는 SQL Server 인스턴스의 이름을 입력합니다.  
  
    -   인증 모드를 선택합니다.  
  
    -   SQL Server 인증을 사용하여 연결하는 경우 로그인과 암호를 제공합니다.  
  
3.  **연결**을 클릭합니다.  
  
#### <a name="to-run-the-transact-sql-statement"></a>Transact-SQL 문을 실행하려면  
  
1.  SQL Server Management Studio의 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
2.  **파일** 메뉴에서 **열기**를 클릭한 다음 **파일**을 클릭합니다.  
  
3.  SharePoint 2016 또는 SharePoint 2013 관리 셸에서 생성한 Transact-SQL 문을 저장한 폴더로 이동합니다.  
  
4.  파일을 클릭한 다음 **열기**를 클릭합니다.  
  
     문은 쿼리 창에 추가됩니다.  
  
5.  **실행**을 클릭합니다.  
  
  
