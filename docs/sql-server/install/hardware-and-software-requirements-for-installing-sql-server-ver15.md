---
title: SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항 | Microsoft Docs
ms.custom: sqlfreshmay19
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Setup [SQL Server], software
- software [SQL Server]
- installing SQL Server, software
- operating systems [SQL Server], SQL Server requirements
- Setup [SQL Server], cross-language support
- operating systems [SQL Server], cross-language support
- network connections [SQL Server], requirements
- disk space [SQL Server], SQL Server installations
- WOW [SQL Server]
- Setup [SQL Server], hardware
- dependencies [SQL Server], SQL Server installations
- cluster hardware requirements [SQL Server]
- endpoints [SQL Server], SQL Server installations
- Internet [SQL Server], SQL Server installations
- hardware [SQL Server]
- Windows on Windows [SQL Server]
- installing SQL Server, hardware
- Setup Configuration Checker
- SCC [SQL Server]
- operating systems [SQL Server]
- space [SQL Server], SQL Server installations
- system configuration checker
- installing SQL Server, cross-language support
- Internet [SQL Server]
- space [SQL Server]
- extended system support [SQL Server]
- 64-bit edition [SQL Server]
- failover clustering [SQL Server]
- failover clustering [SQL Server], hardware requirements
- 32-bit edition [SQL Server]
- locales [SQL Server], SQL Server installations
- cross-language support
- disk space [SQL Server]
- localized SQL Server versions
ms.assetid: 09bcf20b-0a40-4131-907f-b61479d5e4d8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: aca31d10c030c360dcd82d6c4851df700bc3c4fe
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74319045"
---
# <a name="hardware-and-software-requirements-for-installing-sql-server"></a>SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 Windows 운영 체제에서 [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] 설치 및 실행을 위한 최소 하드웨어 및 소프트웨어 요구 사항을 나열합니다.

[!INCLUDE[sscurrent](../../includes/sssqlv14-md.md)]은 Linux에서 [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)]를 지원합니다. 자세한 내용은 [Linux에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 위한 하드웨어 및 소프트웨어 요구 사항](../../linux/sql-server-linux-setup.md#system)을 참조하세요. 

**사용해보기:**  
  
- [**Evaluation Center**](https://www.microsoft.com/evalcenter/evaluate-sql-server-2019-rc)에서 SQL Server를 다운로드하세요. 
  
<!-- 
- Spin up a Virtual Machine with [**SQL Server 2017**](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) already installed.  
-->
  
**다음은 모든 버전에 적용되는 고려 사항입니다.**  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 읽기 전용, 매핑 또는 압축된 드라이브로의 설치를 차단합니다.  
  
- 미디어가 RDC 클라이언트의 로컬 리소스에 있는 상태에서 원격 데스크톱 연결을 통해 설치를 시작하면 설치에 실패합니다. 원격으로 설치하려면 미디어가 네트워크 공유에 있거나 물리적 또는 가상 머신의 로컬이어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어는 네트워크 공유, 매핑된 드라이브, 로컬 드라이브에 있거나 가상 머신에 대한 ISO로 표시될 수 있습니다.
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 제품에 필요한 다음 소프트웨어 구성 요소를 설치합니다.  
  
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 지원 파일  

##  <a name="hwswr"></a> 하드웨어 및 소프트웨어 요구 사항  
다음은 모든 설치에 적용되는 요구 사항입니다.  
  
|구성 요소|요구 사항|  
|---------------|-----------------|  
|운영 체제|Windows 10 TH1 1507 이상<br/><br>Windows Server 2016 이상<br/><br/>
|.NET Framework|최소 운영 체제에는 최소 .NET 프레임워크가 포함됩니다.|  
|네트워크 소프트웨어|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 에 대해 지원되는 운영 체제에는 기본 제공 네트워크 소프트웨어가 포함되어 있습니다. 독립 실행형 설치의 명명된 인스턴스 및 기본 인스턴스는 다음 네트워크 프로토콜을 지원합니다. 공유 메모리, 명명된 파이프 및 TCP/IP.<br/><br/> |  
|하드 디스크|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 에는 최소 6GB의 사용 가능한 하드 디스크 공간이 필요합니다.<br/><br/> 디스크 공간 요구 사항은 설치하는 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 구성 요소에 따라 다릅니다. 자세한 내용은 이 문서의 뒷부분에 있는 [하드 디스크 공간 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace)을 참조하세요. 데이터 파일에 대해 지원되는 스토리지 유형에 대한 자세한 내용은 [Storage Types for Data Files](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)을 참조하십시오.|  
|모니터|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 에는 Super-VGA(800x600) 이상 해상도의 모니터가 필요합니다.|  
|인터넷|인터넷 기능을 사용하려면 인터넷에 액세스해야 합니다(요금이 부과될 수 있음).|  

> [!NOTE]
> 가상 머신에서 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]를 실행하면 가상화에 따른 오버헤드로 인해 기본적인 실행 방식보다 속도가 느립니다.  

> [!IMPORTANT]
> PolyBase 기능에 대한 추가 하드웨어 및 소프트웨어 요구 사항이 있습니다. 자세한 내용은 [PolyBase 시작](../../relational-databases/polybase/get-started-with-polybase.md)을 참조하세요.  
  
##  <a name="pmosr"></a> 프로세서, 메모리 및 운영 체제 요구 사항  
 모든 버전의 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]에는 다음과 같은 메모리 및 프로세서 요구 사항이 적용됩니다.  
  
|구성 요소|요구 사항|  
|---------------|-----------------|  
|메모리\*|**최소:**<br/><br/> Express Edition: 512MB<br/><br/> 기타 모든 버전: 1 GB<br/><br/> **권장:**<br/><br/> Express Edition: 1 GB<br/><br/> 기타 모든 버전: 최소 4GB가 필요하며 데이터베이스 크기가 늘어남에 따라 메모리 크기를 늘려 성능을 최대화해야 합니다.|  
|프로세서 속도|**최소:** x64 프로세서: 1.4GHz<br/><br/> **권장:** 2.0GHz 이상|  
|프로세서 유형|x64 프로세서: AMD Opteron, AMD Athlon 64, Intel EM64T를 지원하는 Intel Xeon, Intel EM64T를 지원하는 Intel Pentium IV|  
  
> [!NOTE]  
> [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 설치는 x64 프로세서에서만 지원됩니다. x86 프로세서에서는 더 이상 지원되지 않습니다.  
  
 \*[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)](DQS)에 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 구성 요소를 설치하는 데 필요한 최소 메모리는 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 최소 메모리 요구 사항과 달리 2GB RAM입니다. DQS 설치에 대한 자세한 내용은 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)를 참조하십시오.  

**Server Core 지원:**

Server Core 모드에서 SQL Server 2019를 설치하는 것은 다음 버전의 Windows Server에서 지원됩니다.

|                              |
| :------------------------  |
| Windows Server 2019 Core | 
| Windows Server 2016 Core |
| &nbsp; | 

Server Core에 SQL Server를 설치하는 방법에 대한 자세한 내용은 [Server Core에 SQL Server 설치](../../database-engine/install-windows/install-sql-server-on-server-core.md)를 참조하세요.  

###  <a name="TOP_Principal"></a> OS 호환성   

다음 표에서는 어떤 SQL Server 2019 버전이 어떤 Windows 버전과 호환되는지 설명합니다.  
  

| SQL Server 버전:               | Enterprise | Developer | Standard | 웹 | Express |  
| :------------------------         | :--------- | :-------- | :------- | :-- | :------ | 
| Windows Server 2019 Datacenter    |    yes     |    yes    |    yes   | yes |   yes   |
| Windows Server 2019 Standard      |    yes     |    yes    |    yes   | yes |   yes   |
| Windows Server 2019 Essentials    |    yes     |    yes    |    yes   | yes |   yes   |
| Windows Server 2016 Datacenter    |    yes     |    yes    |    yes   | yes |   yes   |
| Windows Server 2016 Standard      |    yes     |    yes    |    yes   | yes |   yes   |
| Windows Server 2016 Essentials    |    yes     |    yes    |    yes   | yes |   yes   |
| Windows 10 Enterprise             |    예      |    yes    |    yes   | 예  |   yes   |
| Windows 10 Professional           |    예      |    yes    |    yes   | 예  |   yes   |
| Windows 10 Home                   |    예      |    yes    |    yes   | 예  |   yes   |
| &nbsp; | &nbsp; |


##  <a name="CrossLanguageSupport"></a> 언어 간 호환성 지원  
 지역화된 언어로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치하기 위한 언어 간 호환성 지원 및 고려 사항에 대한 자세한 내용은 [SQL Server의 로컬 언어 버전](../../sql-server/install/local-language-versions-in-sql-server.md)을 참조하세요.  
  
##  <a name="HardDiskSpace"></a> 하드 디스크 공간 요구 사항  
 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]를 설치하는 동안 Windows Installer는 시스템 드라이브에 임시 파일을 만듭니다. 설치 프로그램을 실행하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하거나 업그레이드하기 전에 먼저 시스템 드라이브에 이 파일을 저장할 디스크 공간(최소 6GB)이 있는지 확인합니다. 이 요구 사항은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 기본 드라이브가 아닌 곳에 설치하는 경우에도 적용됩니다.  
  
 실제 하드 디스크 공간 요구 사항은 시스템 구성과 설치할 기능에 따라 달라집니다. 다음 표에서는 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 구성 요소에 대한 디스크 공간 요구 사항을 보여 줍니다.  
  
|**기능**|**디스크 공간 요구 사항**|  
|-----------------|--------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 데이터 파일, 복제, 전체 텍스트 검색 및 Data Quality Services|1480MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (위의 설명 참조), R Services(데이터베이스 내) 포함|2744MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (위의 설명 참조), 외부 데이터용 PolyBase 쿼리 서비스 포함|4194MB|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 데이터 파일|698MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|967MB|  
|[!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] (독립 실행형)|280MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint|1203MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능(SharePoint 제품용)|325MB|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|121MB|  
|클라이언트 도구 연결|328MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|306MB|  
|클라이언트 구성 요소( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서 구성 요소 및 Integration Services 도구 외의 기타 구성 요소)|445MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|280MB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서 구성 요소(도움말 내용을 보고 관리할 수 있음)*|27MB|  
|모든 기능|8030MB|  
  
 *다운로드한 온라인 설명서 내용에 대한 디스크 공간 요구 사항은 200MB입니다.  
  
##  <a name="StorageTypes"></a> 데이터 파일의 스토리지 유형  
 데이터 파일에 대해 지원되는 스토리지 유형은 다음과 같습니다.  
  
- 로컬 디스크 
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 현재 512바이트 및 4KB의 표준 기본 섹터 크기를 가진 디스크 드라이브를 지원합니다.  섹터 크기가 4KB를 초과하는 하드 디스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일을 저장하려 할 때 오류가 발생할 수 있습니다.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 하드 디스크 섹터 크기 지원에 대한 자세한 내용은 [SQL Server의 하드 디스크 드라이브 섹터 크기 지원 경계](https://support.microsoft.com/kb/926930)를 참조하세요. 
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 설치에서는 tempdb 파일 설치에 대해서만 로컬 디스크를 지원합니다. tempdb 데이터 및 로그 파일에 대해 지정된 경로가 모든 클러스터 노드에서 올바른지 확인하십시오. 장애 조치(failover) 중에 장애 조치 대상 노드에서 tempdb 디렉터리를 사용할 수 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스가 온라인이 될 수 없습니다.
- 공유 스토리지  
- [S2D\(스토리지 공간 다이렉트\)](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)  
- SMB 파일 공유  
    - SMB 스토리지는 독립형 설치 또는 클러스터형 설치에 대한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 파일에 지원되지 않습니다. 대신 직접 연결 스토리지, SAN(스토리지 영역 네트워크) 또는 S2D를 사용합니다. 
    - SMB 스토리지는 Windows 파일 서버 또는 타사 SMB 저장 디바이스에서 호스팅할 수 있습니다. Windows 파일 서버가 사용되는 경우 Windows 파일 서버 버전이 2008 이상이어야 합니다. 스토리지 옵션으로 SMB 파일 공유를 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 대한 자세한 내용은 [SMB fileshare 기능이 있는 SQL Server를 스토리지 옵션으로 설치](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
  
  
  
##  <a name="DC_support"></a> 도메인 컨트롤러에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치  
 보안상의 이유로 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 는 도메인 컨트롤러에 설치하지 않는 것이 좋습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 도메인 컨트롤러 컴퓨터에 설치하는 것을 차단하지는 않지만 다음과 같은 제한 사항을 적용합니다.  
  
- 도메인 컨트롤러에서는 로컬 서비스 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 실행할 수 없습니다.    
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 컴퓨터에 설치한 후에는 도메인 멤버에서 도메인 컨트롤러로 컴퓨터를 변경할 수 없습니다. 호스트 컴퓨터를 도메인 컨트롤러로 변경하려면 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 제거해야 합니다.    
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 컴퓨터에 설치한 후에는 도메인 컨트롤러에서 도메인 멤버로 컴퓨터를 변경할 수 없습니다. 호스트 컴퓨터를 도메인 멤버로 변경하려면 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 제거해야 합니다.   
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스는 클러스터 노드가 도메인 컨트롤러인 경우 지원되지 않습니다.   
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 읽기 전용 도메인 컨트롤러에서 지원되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 읽기 전용 도메인 컨트롤러에서 보안 그룹을 만들거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정을 프로비전할 수 없습니다. 이 경우 설치 프로그램에서 오류가 발생합니다. 
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스는 읽기 전용 도메인 컨트롤러만 액세스할 수 있는 환경에서 지원되지 않습니다. 
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)   
 [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   

