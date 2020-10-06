---
title: SQL Server 설치 가이드
description: 설치 마법사, 명령 프롬프트, sysprep 같은 옵션을 사용하여 SQL Server 및 관련 구성 요소를 설치하는 데 도움이 되는 콘텐츠의 인덱스입니다.
ms.custom: ''
ms.date: 11/14/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- AdventureWorks sample database
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: c981154462ec6b544d8dd877d1b6a41a6fa0ac2c
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670596"
---
# <a name="sql-server-installation-guide"></a>SQL Server 설치 가이드

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

이 문서는 Windows에 SQL Server를 설치하기 위한 지침을 제공하는 콘텐츠 인덱스입니다.

기타 배포 시나리오는 다음을 참조하세요.

- [Linux](../../linux/sql-server-linux-setup.md)
- [Docker 컨테이너](../../linux/sql-server-linux-docker-container-deployment.md)
- [Kubernetes - 빅 데이터 클러스터](../../big-data-cluster/deploy-get-started.md)

[!INCLUDE[sssql15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]는 64비트 애플리케이션으로만 사용할 수 있습니다. 다음은 SQL Server 다운로드 및 설치 방법에 대한 중요한 세부 정보입니다.

## <a name="getting-started"></a>시작
  
* **버전 및 기능**: 여러 SQL Server 버전에서 지원되는 기능을 검토하여 비즈니스 요구에 가장 적합한 버전을 확인합니다. 
    - [[!INCLUDE[ss2019](../../includes/sssqlv15-md.md)]](~/sql-server/editions-and-components-of-sql-server-version-15.md)를 참조하세요.  
    - [[!INCLUDE[ss2017](../../includes/sssqlv14-md.md)]](~/sql-server/editions-and-components-of-sql-server-2017.md)를 참조하세요.  
    - [[!INCLUDE[ss2016](../../includes/sssql15-md.md)]](~/sql-server/editions-and-components-of-sql-server-2016.md)를 참조하세요.  
    - [[!INCLUDE[ss2014](../../includes/sssql14-md.md)]](https://docs.microsoft.com/previous-versions/sql/2014/getting-started/features-supported-by-the-editions-of-sql-server-2014)

*  **요구 사항**: [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)에서 [SQL Server 2016 및 2017](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md), [SQL Server 2019](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md) 또는 [SQL Server on Linux](../../linux/sql-server-linux-setup.md)의 하드웨어 및 소프트웨어 설치 요구 사항, 시스템 구성 검사 및 보안 고려 사항을 검토합니다. 


  
* **샘플 데이터베이스 및 샘플 코드**: 
    * 기본적으로 SQL Server 설치의 일부로 설치되지 않지만 찾을 수 있습니다. 
    * 비 Express 버전의 SQL Server에서 설치하려면 [샘플 위치](../../samples/sql-samples-where-are.md)를 참조하세요.
    

## <a name="installation-media"></a>설치 미디어

[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 다운로드 위치는 버전에 따라 다릅니다.

* **SQL Server Enterprise, Standard 및 Express Edition** 은 프로덕션 사용이 허가되었습니다. Enterprise 및 Standard Edition의 경우 설치 미디어를 얻으려면 소프트웨어 공급업체에 문의하세요. 구매 정보 및 Microsoft 파트너 디렉터리는 [Microsoft 라이선싱 페이지](https://www.microsoft.com/licensing/product-licensing/sql-server)에서 확인할 수 있습니다.
* [무료 버전 - 최신](https://www.microsoft.com/sql-server/sql-server-downloads)
* [무료 버전 - 기타](https://www.microsoft.com/evalcenter/evaluate-sql-server)


다른 SQL Server 구성 요소는 다음 위치에서 찾을 수 있습니다. 

* [모든 누적 업데이트](https://sqlserverbuilds.blogspot.com/)
* [SQL Server Reporting Services](https://www.microsoft.com/download/details.aspx?id=100122) 
* [SQL Server Management Studio](https://aka.ms/ssmsfullsetup)
* [Azure Data Studio](https://go.microsoft.com/fwlink/?linkid=2109256)


## <a name="considerations"></a>고려 사항

-   미디어가 RDC 클라이언트의 로컬 리소스에 있는 상태에서 원격 데스크톱 연결을 통해 설치를 시작하면 설치에 실패합니다. 원격으로 설치하려면 미디어가 네트워크 공유에 있거나 물리적 또는 가상 머신의 로컬이어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어는 네트워크 공유, 매핑된 드라이브, 로컬 드라이브에 있거나 가상 머신에 대한 ISO로 표시될 수 있습니다.  
  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 제품에 필요한 다음 소프트웨어 구성 요소를 설치합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client    
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 지원 파일  

## <a name="sql-server-installation"></a>SQL Server 설치


|아티클|Description|  
|-----------|-----------------|  
|[설치 마법사](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)|setup.exe 설치 미디어에서 시작된 설치 마법사 GUI를 사용하여 SQL Server를 설치합니다. |  
|[명령 프롬프트](./install-sql-server-from-the-command-prompt.md)|명령 프롬프트에서 SQL Server 설치를 실행하기 위한 샘플 구문 및 설치 매개 변수입니다. | 
|[Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md)|Windows Server Core에 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]를 설치합니다.|  
|[시스템 구성 검사기의 검사 매개 변수](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|SCC(시스템 구성 검사기)의 기능에 대해 설명합니다.|   
|[구성 파일](./install-sql-server-using-a-configuration-file.md)|구성 파일을 통해 설치 프로그램을 실행하기 위한 샘플 구문 및 설치 매개 변수입니다.|  
|[SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md)|SysPrep을 통해 설치 프로그램을 실행하기 위한 샘플 구문 및 설치 매개 변수입니다.|
|[인스턴스에 기능 추가](./add-features-to-an-instance-of-sql-server-setup.md)|기존 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 인스턴스의 구성 요소를 업데이트합니다.|  
|[SQL Server 장애 조치(Failover) 클러스터 설치](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)| SQL Server 장애 조치(failover) 클러스터 인스턴스를 설치합니다.  | 
|[실패한 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 설치 복구](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)|손상된 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 설치를 복구합니다.|  
|[SQL Server를 사용하여 컴퓨터 이름 바꾸기](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|SQL Server 독립 실행형 인스턴스를 호스트하는 컴퓨터의 호스트 이름을 바꾼 후에는 sys.servers에 저장된 시스템 메타데이터를 업데이트합니다. |  
|[[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 서비스 업데이트 설치](../../database-engine/install-windows/install-sql-server-servicing-updates.md)|[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 업데이트를 설치합니다.|  
|[설치 로그 파일](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)| SQL Server 설치 로그 파일에서 오류를 확인하고 읽습니다. |  
|[설치 유효성 검사](../../database-engine/install-windows/validate-a-sql-server-installation.md)|SQL 검색 보고서 사용 방법을 검토하여 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 버전 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 확인합니다.|  
  
  
## <a name="individual-component-installation"></a>개별 구성 요소 설치 
  
|아티클|Description|  
|-----------|-----------------|  
|[SQL Server 데이터베이스 엔진](../../database-engine/install-windows/install-sql-server-database-engine.md)|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]를 설치하고 구성합니다.|  
|[SQL Server 복제](../../database-engine/install-windows/install-sql-server-replication.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제를 설치하고 구성합니다.|  
|[Distributed Replay](../../tools/distributed-replay/install-distributed-replay-overview.md)|Distributed Replay 기능을 설치하는 아티클을 나열합니다.|  
|[SSMS를 사용하는 SQL Server 관리 도구](../../ssms/download-sql-server-management-studio-ssms.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 도구를 설치하고 구성합니다.|  
|[SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 구성 요소 설치 시 고려할 사항입니다.|  
  

## <a name="sql-server-configuration"></a>SQL Server 구성 
  
|아티클|Description|  
|-----------|-----------------|  
|[Windows 방화벽 구성(SQL Server)](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|방화벽 구성 및 SQL Server 액세스를 허용하도록 Windows 방화벽을 구성하는 방법의 개요입니다.|  
|[Windows 방화벽 구성(SSAS)](/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 액세스를 허용하도록 포트 및 방화벽 설정을 모두 구성합니다.|  
|[다중 홈 컴퓨터 구성](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|다중 홈 환경에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 네트워크 연결을 위해 제공할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 고급 보안이 포함된 Windows 방화벽을 구성합니다.|  

 
## <a name="see-also"></a>참고 항목  

[[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)   
[[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 제거](../../sql-server/install/uninstall-sql-server.md)   
[SSRS(SQL Server Reporting Services) 설치](../../reporting-services/install-windows/install-reporting-services.md)   
[SSAS(SQL Server Analysis Services) 설치](/analysis-services/instances/install-windows/install-analysis-services)   
[[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Business Intelligence 기능 설치](../../sql-server/install/install-sql-server-business-intelligence-features.md)   
[고가용성 솔루션&#40;SQL Server&#41;](../sql-server-business-continuity-dr.md)