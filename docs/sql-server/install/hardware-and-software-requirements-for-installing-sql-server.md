---
title: SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항 | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2018
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
manager: craigg
ms.openlocfilehash: 093a70a8e9651271aa2a8df4641f6f1e568fc2a7
ms.sourcegitcommit: c0b3b3d969af668d19b1bba04fa0c153cc8970fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/11/2019
ms.locfileid: "57756738"
---
# <a name="hardware-and-software-requirements-for-installing-sql-server"></a>SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 Windows 운영 체제에서 [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] 설치 및 실행을 위한 최소 하드웨어 및 소프트웨어 요구 사항을 나열합니다. 

[!INCLUDE[sscurrent](../../includes/sssqlv14-md.md)]에서는 [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] Linux에 대한 지원 기능을 제공합니다. 자세한 내용은 [Linux에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 위한 하드웨어 및 소프트웨어 요구 사항](../../linux/sql-server-linux-setup.md#system)을 참조하세요. 

> 이 문서는 [!INCLUDE[ss2016](../../includes/sssql15-md.md)] 이상에 적용됩니다. 
  
**사용해보기:**  
  
-   [**Evaluation Center**](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)에서 SQL Server를 다운로드하세요. 
  
-   [**SQL Server 2016**](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)이 이미 설치된 가상 컴퓨터 실행  
  
**다음은 모든 버전에 적용되는 고려 사항입니다.**  
  
-   [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 는 NTFS 또는 ReFS 파일 형식을 사용하는 컴퓨터에서 실행하는 것이 좋습니다. FAT32 파일 시스템을 사용하는 컴퓨터에 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 를 설치할 수는 있지만 NTFS 또는 ReFS 파일 시스템보다 안전하지 않으므로 권장하지는 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 읽기 전용, 매핑 또는 압축된 드라이브로의 설치를 차단합니다.  
  
-   미디어가 RDC 클라이언트의 로컬 리소스에 있는 상태에서 원격 데스크톱 연결을 통해 설치를 시작하면 설치에 실패합니다. 원격으로 설치하려면 미디어가 네트워크 공유에 있거나 물리적 또는 가상 머신의 로컬이어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어는 네트워크 공유, 매핑된 드라이브, 로컬 드라이브에 있거나 가상 머신에 대한 ISO로 표시될 수 있습니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 설치하려면 필수 조건으로 .NET 4.6.1을 설치해야 합니다. .NET 4.6.1은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을(를) 선택하면 설치 프로그램에 의해 자동으로 설치됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 제품에 필요한 다음 소프트웨어 구성 요소를 설치합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 지원 파일  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 에 [!INCLUDE[win8](../../includes/win8-md.md)]를 설치하기 위한 최소 버전 요구 사항은 [Windows Server 2012 또는 Windows 8에 SQL Server 설치](https://support.microsoft.com/kb/2681562)(https://support.microsoft.com/kb/2681562))를 참조하십시오.  
  
##  <a name="hwswr"></a> 하드웨어 및 소프트웨어 요구 사항  
다음은 모든 설치에 적용되는 요구 사항입니다.  
  
|구성 요소|요구 사항|  
|---------------|-----------------|  
|.NET Framework|[!INCLUDE[sql2016](../../includes/sssql15-md.md)] RC1 및 이후 버전을 사용하려면 데이터베이스 엔진, Master Data Services 또는 복제에 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6이 필요합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 설치 프로그램이 자동으로 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]를 설치합니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Windows용 Microsoft .NET Framework 4.6웹 설치 관리자 [에서 수동으로](https://support.microsoft.com/kb/3045560)를 설치할 수도 있습니다.<br/><br/>[!INCLUDE[sql2019](../../includes/sssqlv15-md.md)]에는 .NET Framework 4.6.2가 필요합니다. [다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53344)에서 제공됩니다.<br/><br/> [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6에 대한 자세한 내용, 권장 사항 및 지침은 [개발자를 위한 .NET Framework 배포 가이드](https://msdn.microsoft.com/library/ee942965\(v=vs.110\).aspx)를 참조하세요.<br/><br/>[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6을 설치하기 전에 [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)] 및 [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)]에 [KB2919355](https://support.microsoft.com/kb/2919355)가 필요합니다.|  
|네트워크 소프트웨어|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 에 대해 지원되는 운영 체제에는 기본 제공 네트워크 소프트웨어가 포함되어 있습니다. 독립 실행형 설치의 명명된 인스턴스 및 기본 인스턴스는 다음 네트워크 프로토콜을 지원합니다. 공유 메모리, 명명된 파이프, TCP/IP 및 VIA.<br/><br/> **참고:** VIA 프로토콜은 장애 조치(failover) 클러스터에서 지원되지 않습니다. SQL Server 인스턴스와 동일한 장애 조치(failover) 클러스터 노드에서 실행 중인 클라이언트 또는 애플리케이션은 공유 메모리 프로토콜을 사용하여 로컬 파이프 주소를 통해 SQL Server에 연결할 수 있습니다. 그러나 이러한 연결은 클러스터에서 인식되지 않으며 인스턴스 장애 조치(failover) 이후에 실패합니다. 따라서 이 연결은 권장되지 않으며 아주 특별한 경우에만 사용해야 합니다.<br/><br/> **중요:** VIA 프로토콜은 더 이상 사용되지 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br/><br/> 네트워크 프로토콜 및 네트워크 라이브러리에 대한 자세한 내용은 [Network Protocols and Network Libraries](../../sql-server/install/network-protocols-and-network-libraries.md)를 참조하십시오.|  
|하드 디스크|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 에는 최소 6GB의 사용 가능한 하드 디스크 공간이 필요합니다.<br/><br/> 디스크 공간 요구 사항은 설치하는 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 구성 요소에 따라 다릅니다. 자세한 내용은 이 문서의 뒷부분에 있는 [하드 디스크 공간 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace)을 참조하세요. 데이터 파일에 대해 지원되는 스토리지 유형에 대한 자세한 내용은 [Storage Types for Data Files](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)을 참조하십시오.|  
|드라이브|디스크에서 설치하려면 경우에 따라 DVD 드라이브가 필요합니다.|  
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
|메모리\*|**최소:**<br/><br/> Express Edition: 512MB<br/><br/> 기타 모든 버전: 1GB<br/><br/> **권장:**<br/><br/> Express Edition: 1GB<br/><br/> 기타 모든 버전: 최소 4GB가 필요하며 데이터베이스 크기가 늘어남에 따라 메모리 크기를 늘려 성능을 최대화해야 합니다.|  
|프로세서 속도|**최소:** x64 프로세서: 1.4GHz<br/><br/> **권장:** 2.0GHz 이상|  
|프로세서 유형|x64 프로세서: AMD Opteron, AMD Athlon 64, Intel EM64T를 지원하는 Intel Xeon, Intel EM64T를 지원하는 Intel Pentium IV|  
  
> [!NOTE]  
> [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 설치는 x64 프로세서에서만 지원됩니다. x86 프로세서에서는 더 이상 지원되지 않습니다.  
  
 \* [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)](DQS)에 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 구성 요소를 설치하는 데 필요한 최소 메모리는 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 최소 메모리 요구 사항과 달리 2GB RAM입니다. DQS 설치에 대한 자세한 내용은 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)를 참조하십시오.  
  
 **WOW64 지원:**  
  
 WOW64(Windows 32-bit on Windows 64-bit)는 32비트 애플리케이션을 32비트 모드로 실행할 수 있게 해주는 Windows 64비트 버전의 기능입니다. 기본 운영 체제가 64비트 운영 체제이더라도 애플리케이션은 32비트 모드로 작동합니다. WOW64는 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 설치에 대해 지원되지 않습니다. 그러나 관리 도구는 WOW64에서 지원됩니다.  
  
 **운영 체제 지원:**  
  
 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 버전은 다음과 같이 분류됩니다.  
  
-   [주 버전](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#TOP_Principal)  
  
-   [확장형 버전](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#TOP_Breadth)  
  
> [!NOTE]  
> 이 섹션에서 설명하는 운영 체제 지원에 대한 예외는 Windows Server 2008 R2 SP1 이상에 설치할 수 있는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이하용 다음 비즈니스 인텔리전스 기능입니다.  
>  
>-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint  
> 
>-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능(SharePoint 제품용)  

**Server Core 지원:**

 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]는 현재 Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 및 Windows Server 2019의 Server Core 설치에서 지원됩니다. 

Server Core 모드에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 설치하는 것은 다음 버전의 Windows Server에서 지원됩니다.

|                              |                                |
| :------------------------    | :------------------------------|
| Windows Server 2019 Standard | Windows Server 2019 Datacenter |
| Windows Server 2016 Standard | Windows Server 2016 Datacenter |
| Windows Server 2012 R2 Standard | Windows Server 2012 R2 데이터 센터|
| Windows Server 2012 Standard | Windows Server 2012 데이터 센터 |
| Windows Server 2008 R2 SP1 Standard | Windows Server 2008 R2 SP1 데이터 센터 |
| Windows Server 2008 R2 SP1 Enterprise | Windows Server 2008 R2 SP1 웹|
   | &nbsp; | &nbsp; |

Server Core에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 설치하는 방법에 대한 자세한 내용은 [Server Core에 SQL Server 설치](../../database-engine/install-windows/install-sql-server-on-server-core.md)를 참조하세요.  

  
### <a name="features-supported-on-32-bit-client-operating-systems"></a>32비트 클라이언트 운영 체제에서 지원되는 기능  
 Windows 클라이언트 운영 체제, 예를 들어 Windows 10 및 Windows 8.1은 32비트 또는 64비트 아키텍처로 사용할 수 있습니다.   모든 SQL Server 기능은 64비트 클라이언트 운영 체제에서 지원됩니다. 지원되는 32비트 클라이언트 운영 체제에서 Microsoft는 다음과 같은 기능을 지원합니다.  
  
-   Data Quality 클라이언트  
  
-   클라이언트 도구 연결  
  
-   Integration Services  
  
-   클라이언트 도구 이전 버전과의 호환성  
  
-   클라이언트 도구 SDK  
  
-   설명서 구성 요소  
  
-   Distributed Replay 구성 요소  
  
-   Distributed  Replay  Controller  
  
-   Distributed  Replay  Client  
  
-   SQL 클라이언트 연결 SDK  
  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 및 이후 서버 운영 체제는 32비트 아키텍처로 사용할 수 없습니다. 모든 지원되는 서버 운영 체제는 64비트로만 사용할 수 있습니다. 모든 기능은 64비트 서버 운영 체제에서 지원됩니다.  
  
###  <a name="TOP_Principal"></a> [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]의 주 버전  
 다음 표에서는 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]의 주 버전에 대한 운영 체제 요구 사항을 보여 줍니다.  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전|지원되는 운영 체제|  
|---------------------------------------|--------------------------------|  
|[!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2019_essentials_md](../../includes/winserver2019-essentials-md.md)] <br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)] <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  
|[!INCLUDE[ssStandard](../../includes/ssstandard-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2019_essentials_md](../../includes/winserver2019-essentials-md.md)] <br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)] <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>Windows 10 IoT Enterprise<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
|[!INCLUDE[ssWeb](../../includes/ssweb-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2019_essentials_md](../../includes/winserver2019-essentials-md.md)] <br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)] <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  

  
###  <a name="TOP_Breadth"></a> [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]의 확장형 버전  
 다음 표에서는 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]의 확장형 버전에 대한 운영 체제 요구 사항을 보여 줍니다.  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전|지원되는 운영 체제|  
|---------------------------------------|--------------------------------|  
|[!INCLUDE[ssDeveloper](../../includes/ssdeveloper-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2019_essentials_md](../../includes/winserver2019-essentials-md.md)] <br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)] <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>Windows 10 IoT Enterprise<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2019_essentials_md](../../includes/winserver2019-essentials-md.md)] <br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)] <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>Windows 10 IoT Enterprise<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  

  
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
  
##  <a name="StorageTypes"></a> 데이터 파일 스토리지 유형  
 데이터 파일에 대해 지원되는 스토리지 유형은 다음과 같습니다.  
  
-   로컬 디스크  
    > [!WARNING]  
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 설치에서는 tempdb 파일 설치에 대해서만 로컬 디스크를 지원합니다. tempdb 데이터 및 로그 파일에 대해 지정된 경로가 모든 클러스터 노드에서 올바른지 확인하십시오. 장애 조치(failover) 중에 장애 조치 대상 노드에서 tempdb 디렉터리를 사용할 수 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스가 온라인이 될 수 없습니다.

    > [!IMPORTANT]
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 현재 512바이트 및 4KB의 표준 기본 섹터 크기를 가진 디스크 드라이브를 지원합니다.  섹터 크기가 4KB를 초과하는 하드 디스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일을 저장하라고 할 때 오류가 발생할 수 있습니다.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 하드 디스크 섹터 크기 지원에 대한 자세한 내용은 [SQL Server의 하드 디스크 드라이브 섹터 크기 지원 경계](https://support.microsoft.com/kb/926930)를 참조하세요.
  
-   공유 스토리지  

-   [S2D\(스토리지 공간 다이렉트\)](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)
  
-   SMB 파일 공유  
  
    > [!NOTE]  
    > SMB 스토리지는 독립형 설치 또는 클러스터형 설치에 대한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 파일에 지원되지 않습니다. 대신 직접 연결 스토리지, SAN(스토리지 영역 네트워크) 또는 S2D를 사용합니다.  
  
    > [!IMPORTANT]  
    > SMB 스토리지는 Windows 파일 서버 또는 타사 SMB 스토리지 장치에서 호스팅할 수 있습니다. Windows 파일 서버가 사용되는 경우 Windows 파일 서버 버전이 2008 이상이어야 합니다. 스토리지 옵션으로 SMB 파일 공유를 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 대한 자세한 내용은 [SMB fileshare 기능이 있는 SQL Server를 스토리지 옵션으로 설치](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
  
  
  
##  <a name="DC_support"></a> FAT32 파일 시스템을 사용하는 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치  
 보안상의 이유로 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 는 도메인 컨트롤러에 설치하지 않는 것이 좋습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 도메인 컨트롤러 컴퓨터에 설치하는 것을 차단하지는 않지만 다음과 같은 제한 사항을 적용합니다.  
  
-   도메인 컨트롤러에서는 로컬 서비스 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 실행할 수 없습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 컴퓨터에 설치한 후에는 도메인 멤버에서 도메인 컨트롤러로 컴퓨터를 변경할 수 없습니다. 호스트 컴퓨터를 도메인 컨트롤러로 변경하려면 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 제거해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 컴퓨터에 설치한 후에는 도메인 컨트롤러에서 도메인 멤버로 컴퓨터를 변경할 수 없습니다. 호스트 컴퓨터를 도메인 멤버로 변경하려면 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 제거해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스는 클러스터 노드가 도메인 컨트롤러인 경우 지원되지 않습니다.  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 읽기 전용 도메인 컨트롤러에서 지원되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 읽기 전용 도메인 컨트롤러에서 보안 그룹을 만들거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정을 프로비전할 수 없습니다. 이 경우 설치 프로그램에서 오류가 발생합니다.  

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스는 읽기 전용 도메인 컨트롤러만 액세스할 수 있는 환경에서 지원되지 않습니다. 
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)   
 [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [SQL Server 2016 제품 사양](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)  
  
  
