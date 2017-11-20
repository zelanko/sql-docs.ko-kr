---
title: "SQL Server 설치 | Microsoft Docs"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- AdventureWorks sample database
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
caps.latest.revision: 59
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1df54edd5857ac2816fa4b164d268835d9713638
ms.openlocfilehash: eab4b7f0ac099d615df1eda831adf04dfd29a7f6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/12/2017

---
# <a name="install-sql-server"></a>SQL Server 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > 이전 버전의 SQL Server와 관련된 내용은 [SQL Server 2014 설치](https://msdn.microsoft.com/library/bb500395(SQL.120).aspx)를 참조하세요.

 [!INCLUDE[sssql15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]는 64비트 응용 프로그램으로만 사용할 수 있습니다. 다음은 SQL Server 다운로드 및 설치 방법에 대한 중요한 세부 정보입니다.

## <a name="installation-details"></a>설치 세부 정보
  
*  **옵션**: 설치 마법사, 명령 프롬프트 또는 sysprep을 통해 설치
 
*  **요구 사항**: 설치하기 전에 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md) 

* **프로세스**: 설치 프로세스에 대한 전체 지침은 [SQL Server 설치](../../database-engine/install-windows/installation-for-sql-server-2016.md) 를 참조하세요.

* **샘플 데이터베이스 및 샘플 코드**: 
    * 기본적으로 SQL Server 설치의 일부로 설치되지 않습니다. 
    * Express 버전 이외의 SQL Server 버전에 대해 설치하려면 [GitHub](http://github.com/Microsoft/sql-server-samples)를 참조하세요.
    

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="how-to-install-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 설치 방법
 
|Title|Description|  
|-----------|-----------------|  
|[Server Core에 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 설치](../../database-engine/install-windows/install-sql-server-on-server-core.md)|Windows Server Core에 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]를 설치하려면 이 항목을 검토합니다.|  
|[시스템 구성 검사기의 검사 매개 변수](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|SCC(시스템 구성 검사기)의 기능에 대해 설명합니다.|  
|[설치 마법사에서 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 설치&#40;설치 프로그램&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)|설치 마법사를 사용한 일반적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치를 설명하는 절차 항목입니다.|  
|[명령 프롬프트에서 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|무인 설치 프로그램을 실행하는 데 사용하는 예제 구문 및 설치 매개 변수를 제공하는 절차 항목입니다.|  
|[구성 파일을 사용하여 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 설치](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|구성 파일을 통해 설치 프로그램을 실행하는 데 사용하는 예제 구문 및 설치 매개 변수를 제공하는 절차 항목입니다.|  
|[SysPrep을 사용하여 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 설치](../../database-engine/install-windows/install-sql-server-using-sysprep.md)|SysPrep을 통해 설치 프로그램을 실행하는 데 사용하는 예제 구문 및 설치 매개 변수를 제공하는 절차 항목입니다.|  
|[[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 인스턴스에 기능 추가&#40;설치 프로그램&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|기존 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 인스턴스의 구성 요소를 업데이트하는 방법을 설명하는 절차 항목입니다.|  
|[실패한 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 설치 복구](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)|손상된 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 설치를 복구하는 방법을 설명하는 절차 항목입니다.|  
|[SQL Server의 독립 실행형 인스턴스를 호스트하는 컴퓨터 이름 바꾸기](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|sys.servers에 저장되어 있는 시스템 메타데이터를 업데이트하는 방법을 설명하는 절차 항목입니다.|  
|[[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 서비스 업데이트 설치](../../database-engine/install-windows/install-sql-server-servicing-updates.md)|[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]에 대한 업데이트를 설치하기 위한 절차 항목입니다.|  
|[SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)|설치 로그 파일에서 오류를 검사하는 방법을 설명하는 절차 항목입니다.|  
|[SQL Server 설치 유효성 검사](../../database-engine/install-windows/validate-a-sql-server-installation.md)|SQL 검색 보고서 사용 방법을 검토하여 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 버전 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 확인합니다.|  
  
  
## <a name="how-to-install-individual-components"></a>개별 구성 요소 설치 방법  
  
|항목|Description|  
|-----------|-----------------|  
|[SQL Server 데이터베이스 엔진 설치](../../database-engine/install-windows/install-sql-server-database-engine.md)|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 설치 및 구성하는 방법에 대해 설명합니다.|  
|[SQL Server 복제 설치](../../database-engine/install-windows/install-sql-server-replication.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제를 설치 및 구성하는 방법에 대해 설명합니다.|  
|[Distributed Replay 설치 - 개요](../../tools/distributed-replay/install-distributed-replay-overview.md)|Distributed Replay 기능 설치와 관련된 항목들을 나열합니다.|  
|[SSMS로 SQL Server 관리 도구 설치](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 도구를 설치 및 구성하는 방법에 대해 설명합니다.|  
|[SQL Server PowerShell 설치](../../database-engine/install-windows/install-sql-server-powershell.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 구성 요소 설치에 대한 고려 사항을 설명합니다.|  
  

## <a name="how-to-configure-sql-server"></a>SQL Server 구성 방법  
  
|항목|Description|  
|-----------|-----------------|  
|[SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|이 항목에서는 방화벽 구성 및 Windows 방화벽 구성 방법에 대한 개요를 제공합니다.|  
|[SQL Server 액세스를 허용하도록 다중 홈 컴퓨터 구성](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|이 항목에서는 다중 홈 환경에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 네트워크 연결을 제공하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 고급 보안이 포함된 Windows 방화벽을 구성하는 방법에 대해 설명합니다.|  
|[Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|이 항목에서 제공하는 단계를 따라 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 또는 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 에 액세스할 수 있도록 포트 및 방화벽 설정 모두를 구성할 수 있습니다.|  
  
## <a name="related-sections"></a>관련 단원  
[[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]의 버전 및 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)  
[[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Business Intelligence 기능 설치](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
  [SQL Server 장애 조치(Failover) 클러스터 설치](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 
  
## <a name="see-also"></a>참고 항목  

[SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)   
 [[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)   
 [[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 제거](../../sql-server/install/uninstall-sql-server.md)   
 [고가용성 솔루션&#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  

