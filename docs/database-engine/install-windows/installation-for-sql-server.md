---
title: "SQL Server 설치 | Microsoft Docs"
ms.custom: 
ms.date: 07/17/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.portal.Installation.f1
helpviewer_keywords:
- installing SQL Server, initial installation
- installation [SQL Server]
- initial installation [SQL Server]
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f3053d9238af0112dfb41be2eb0f2972f24a34ce
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="installation-for-sql-server"></a>SQL Server 설치

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 설치하는 하나의 기능 트리를 제공합니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
-   연결 구성 요소  
  
[!INCLUDE[ss2016](../../includes/sssql15-md.md)]부터 SQL Server 관리 도구는 주 기능 트리에서 더 이상 설치되지 않습니다. 자세한 내용은 [SSMS(SQL Server Management Studio) 다운로드](../../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요.  
  
각 구성 요소를 개별적으로 설치하거나 위에 나열된 구성 요소 조합을 선택할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 수 있는 버전과 구성 요소 중에서 가장 적합한 항목을 선택하려면 사용 중인 SQL Server 버전에서 지원되는 기능을 참조합니다.

- [[!INCLUDE[ss2017](../../includes/sssqlv14-md.md)]의 버전 및 지원하는 기능](~/sql-server/editions-and-components-of-sql-server-2017.md)  
- [[!INCLUDE[ss2016](../../includes/sssql15-md.md)]의 버전 및 지원하는 기능](~/sql-server/editions-and-components-of-sql-server-2016.md)  
- [[!INCLUDE[ss2014](../../includes/sssql14-md.md)] 버전에서 지원하는 기능](http://technet.microsoft.com/library/cc645993(v=sql.120).aspx)
  
## <a name="in-this-section"></a>섹션 내용  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사와 명령 프롬프트 중 어느 쪽을 사용하는지에 관계없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치에는 다음 단계가 포함됩니다.  
  
[SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)  
컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치를 준비하는 방법에 대해 설명합니다.  
  
-   하드웨어 및 소프트웨어 요구 사항  
-   시스템 구성 검사기 요구 사항 및 차단 문제  
-   보안 고려 사항  
  
[SQL Server 설치](../../database-engine/install-windows/install-sql-server.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치 옵션에 대해 설명합니다.  
  
[SQL Server 설치 사용자 인터페이스 참조](http://msdn.microsoft.com/library/183b5cdd-962e-41ca-8064-ea44f622c77d)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사에서 제공되는 설치 옵션에 대해 설명합니다.  
  
[SQL Server 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드하기 위한 옵션에 대해 설명합니다.  
  
[SQL Server 제거](../../sql-server/install/uninstall-sql-server.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]를 제거하는 절차에 대해 설명합니다.  
  
[SQL Server 장애 조치(Failover) 클러스터 설치](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 설명서 중 이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터를 설치 및 구성하는 방법에 대해 설명합니다.  
  
[SQL Server Business Intelligence 기능 설치](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능(Microsoft BI 플랫폼에 속함)에는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]및 분석 데이터를 만들거나 사용하는 데 사용되는 일부 클라이언트 응용 프로그램이 포함됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 설명서 중 이 섹션에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]설치 방법에 대해 설명합니다.  
  
## <a name="more-information"></a>자세한 정보
[SharePoint와 함께 SQL Server BI 기능 설치&#40;파워 피벗 및 Reporting Services&#41;](http://msdn.microsoft.com/library/3166107c-30c2-468e-bb1b-bb42b79b37c3)  
 이 섹션에서는 SharePoint 환경에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 설치하는 방법에 대해 설명합니다. 여기에서는 SharePoint의 특정 버전 및 에디션에서 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 설명하고 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 및 SharePoint 모드의 Reporting Services에 대한 설치 지침을 제공합니다.  
  
![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) 새 샘플 데이터베이스 [Wide World Importers](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx)를 설치합니다. 
  
[추가 SQL Server 예제 및 예제 데이터베이스 설치](http://sqlserversamples.codeplex.com/)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 예제 및 예제 데이터베이스를 설치 및 구성하는 방법에 대해 설명합니다.  
  
[의 모든 버전을 지원하는 링크 및 자세한 내용은](https://msdn.microsoft.com/library/ff803383.aspx) SQL Server 업데이트 센터 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 설치의 새로운 기능](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
[SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
