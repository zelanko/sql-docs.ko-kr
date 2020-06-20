---
title: SQL Server 2014 설치 Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- sql12.portal.Installation.f1
helpviewer_keywords:
- installing SQL Server, initial installation
- installation [SQL Server]
- initial installation [SQL Server]
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6dafb1e971b85adfee2ecb3579ac20b83906b9dd
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932379"
---
# <a name="installation-for-sql-server-2014"></a>SQL Server 2014 설치
 ## <a name="download-sql-server-2014-express"></a>[SQL Server 2014 Express 다운로드](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  **모든 설치 관리자 패키지 링크를 한 곳에서 수집 하기 위해 [Scott Hanselman](http://www.hanselman.com/) 주셔서 감사 합니다.**
  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 설치하는 하나의 기능 트리를 제공합니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
  
-   관리 도구  
  
-   연결 구성 요소  
  
 각 구성 요소를 개별적으로 설치하거나 위에 나열된 구성 요소 조합을 선택할 수 있습니다. 에서 사용할 수 있는 버전과 구성 요소 중에서 가장 적합 한 항목을 선택 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server 2014의 버전 및 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md) 및 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조 하세요. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]는 32비트 및 64비트 버전으로 제공됩니다.
 
 **사용해 보기:**  
  
-   Azure 계정이 있으세요?  그런 다음 **[여기](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2016RTMEnterpriseWindowsServer2012R2)** 로 이동 하 여 SQL SERVER 2014 SP1 (서비스 팩 1)이 이미 설치 되어 있는 가상 머신을 실행 합니다. SQL Server 2014 (SP1)에 대 한 자세한 내용은 [SQL Server 2014 서비스 팩 1 릴리스 정보](https://support.microsoft.com/kb/3058865)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사와 명령 프롬프트 중 어느 쪽을 사용하는지에 관계없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치에는 다음 단계가 포함됩니다.  
  
 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)  
 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치를 준비하는 방법에 대해 설명합니다.  
  
-   하드웨어 및 소프트웨어 요구 사항  
  
-   시스템 구성 검사기 요구 사항 및 차단 문제  
  
-   보안 고려 사항  
  
 [SQL Server 2014 설치](install-sql-server.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치 옵션에 대해 설명합니다.  
  
 [SQL Server 2014로 업그레이드](upgrade-sql-server.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드하기 위한 옵션에 대해 설명합니다.  
  
 [SQL Server 2014 제거](../../sql-server/install/uninstall-sql-server.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]를 제거하는 절차에 대해 설명합니다.  
  
 [SQL Server 장애 조치(Failover) 클러스터 설치](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 설명서 중 이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터를 설치 및 구성하는 방법에 대해 설명합니다.  
  
 [SQL Server 2014 BI 기능 설치](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능(Microsoft BI 플랫폼에 속함)에는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]및 분석 데이터를 만들거나 사용하는 데 사용되는 일부 클라이언트 애플리케이션이 포함됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 설명서 중 이 섹션에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]설치 방법에 대해 설명합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [설치 방법 도움말 항목](../../sql-server/install/installation-how-to-topics.md)  
 설치 마법사, 명령 프롬프트, 구성 파일 사용 및 SysPrep 사용 등의 방법으로 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 설치하는 절차 항목에 대한 링크를 제공합니다.  
  
 [SharePoint &#40;PowerPivot 및 Reporting Services를 사용 하 여 SQL Server BI 기능 설치&#41;](../../sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)  
 이 섹션에서는 SharePoint 환경에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 설치하는 방법에 대해 설명합니다. 여기에서는 SharePoint의 특정 버전 및 에디션에서 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 설명하고 SharePoint용 PowerPivot 및 SharePoint 모드의 Reporting Services에 대한 설치 지침을 제공합니다.  
  
 [SQL Server 예제 및 예제 데이터베이스 설치](https://sqlserversamples.codeplex.com/)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 예제 및 예제 데이터베이스를 설치 및 구성하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 설치의 새로운 기능](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
 [SQL Server 2014 설치에 대한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
