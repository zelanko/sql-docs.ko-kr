---
title: SysPrep을 사용하여 SQL Server 설치 | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 11f4ed8a-aaa9-417b-bdd5-204f551c6bb6
caps.latest.revision: 29
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 3b8678535c387a6ca1117d4e2851c57632573da1
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40405825"
---
# <a name="install-sql-server-with-sysprep"></a>SysPrep을 사용하여 SQL Server 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep 관련 설치 동작에 액세스할 수 있습니다. **설치 센터**의 **고급** 페이지에는 **독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이미지 준비**와 **독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 준비 인스턴스의 이미지 완료**라는 두 옵션이 있습니다. [준비](#prepare) 및 [완료](#complete) 섹션에서는 설치 프로세스에 대해 자세히 설명합니다. 자세한 내용은 [Considerations for Installing SQL Server Using SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)을 참조하세요. 
  
명령 프롬프트 또는 구성 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 준비하고 완료할 수도 있습니다. 참조 항목:  
  
- [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
- [구성 파일을 사용하여 SQL Server 설치](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)  
  
## <a name="prerequisites"></a>사전 요구 사항  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하기 전에 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)의 문서를 검토합니다. 
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전과 하드웨어 및 소프트웨어 요구 사항에 대한 자세한 내용은 [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요. 
    
##  <a name="sysprep"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep 클러스터 지원  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 SysPrep은 명령줄에서 클러스터형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 설치를 지원합니다. 자세한 내용은 [Sysprep이란?](http://msdn.microsoft.com/library/cc721940\(v=WS.10\).aspx)을 참조하십시오. 
  
### <a name="to-prepare-a-includessnoversionincludesssnoversion-mdmd-failover-cluster-unattended"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 준비하려면  
  
1. 이미지를 준비하고( [SysPrep을 사용하여 SQL Server 설치 시 고려 사항](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)참조) SysPrep Generalization을 통해 Windows 이미지를 캡처합니다. 다음 예에서는 이미지를 준비합니다.  
  
    ```  
    Setup.exe /q /ACTION=PrepareImage l /FEATURES=SQLEngine /InstanceID =<MYINST> /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     Windows SysPrep Generalization을 실행합니다. 
  
2. Windows SysPrep Specialize를 실행하여 이미지를 배포합니다. 
  
3. Windows 장애 조치(Failover) 클러스터를 만듭니다. 
  
4. 모든 노드에서 **/ACTION=PrepareFailoverCluster** 를 사용하여 setup.exe를 실행합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
    ```  
    setup.exe /q /ACTION=PrepareFailoverCluster /InstanceName=<InstanceName> /Features=SQLEngine  /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx"  /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
### <a name="complete-a-includessnoversionincludesssnoversion-mdmd-failover-cluster-unattended"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 완료(무인)  
  
1. 사용 가능한 저장소 그룹을 소유한 노드에서 **/ACTION=CompleteFailoverCluster** 를 사용하여 setup.exe를 실행합니다.  
  
    ```  
    setup.exe /q /ACTION=CompleteFailoverCluster /InstanceName=<InstanceName>  /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'>:" /FAILOVERCLUSTERNETWORKNAME="<Insert FOI Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
    ```  
  
### <a name="adding-a-node-to-an-existing-includessnoversionincludesssnoversion-mdmd-failover-cluster-unattended"></a>기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 노드 추가(무인)  
  
1. Windows SysPrep Specialize를 실행하여 이미지를 배포합니다. 
  
2. Windows 장애 조치(Failover) 클러스터에 참가합니다. 
  
3. 모든 노드에서 **/ACTION=AddNode** 를 사용하여 setup.exe를 실행합니다.  
  
    ```  
    setup.exe /q /ACTION=AddNode /InstanceName=<InstanceName> /Features=SQLEngine  /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx"  /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
##  <a name="prepare"></a> 이미지 준비  
  
### <a name="prepare-a-stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 준비 
  
1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 폴더에서 Setup.exe를 두 번 클릭합니다. 네트워크 공유에서 설치하려면 공유에서 루트 폴더를 찾은 다음 Setup.exe를 두 번 클릭합니다. 
  
2. 설치 마법사가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터를 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 준비하려면 **고급** 페이지에서 **독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이미지 준비**를 클릭합니다. 
  
3. 시스템 구성 검사기가 컴퓨터에서 검색 작업을 실행합니다. 계속하려면 **확인**을 클릭합니다. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다. 
  
4. 제품 업데이트 페이지에는 사용 가능한 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 업데이트가 표시됩니다. 업데이트를 포함하지 않으려면 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 업데이트 포함** 확인란의 선택을 취소합니다. 제품 업데이트가 검색되지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 이 페이지가 표시되지 않으며 **설치 파일 설치** 페이지로 자동으로 진행됩니다. 
  
5. 설치 프로그램에서 설치 파일 설치 페이지에는 설치 파일의 다운로드, 추출 및 설치 진행률이 표시됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에 대한 업데이트가 발견되고 이러한 업데이트가 포함되도록 지정된 경우 해당 업데이트도 함께 설치됩니다. 
  
6. 시스템 구성 검사기가 설치를 계속하기 전에 컴퓨터의 시스템 상태를 확인합니다. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다. 
  
7. **이미지 유형 준비** 페이지에서 **새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 준비**를 선택합니다. 
  
     컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 구성되지 않은 기존 준비 인스턴스가 있는 경우에만 **이미지 유형 준비** 페이지가 표시됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 새 인스턴스를 준비하거나, 컴퓨터에 이미 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 준비 인스턴스에 sys prep 지원 기능을 추가하도록 선택할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 준비 인스턴스에 기능을 추가하는 방법은 [준비 인스턴스에 기능 추가](#AddFeatures)를 참조하십시오. 
  
8. **사용 조건** 페이지에서 사용권 계약을 읽은 다음 사용 조건과 계약 조건에 동의하면 해당 확인란을 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 개선을 돕기 위해 기능 사용 옵션을 사용하도록 설정하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)]로 보고서를 보낼 수도 있습니다. 
  
9. **기능 선택** 페이지에서 설치할 구성 요소를 선택합니다.  
  
    |||  
    |-|-|  
    |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SysPrep|[!INCLUDE[ssDE](../../includes/ssde-md.md)]<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제<br /><br /> 전체 텍스트 기능<br /><br /> 데이터베이스 엔진 서비스<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 다음 네이티브 모드:<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]<br /><br /> 재배포 가능 기능<br /><br /> 공유 기능|  
  
     기능 이름을 선택하여 강조하면 오른쪽 창에 각 구성 요소 그룹에 대한 설명이 나타납니다. 확인란을 자유롭게 조합하여 선택할 수 있습니다. 자세한 내용은 [SQL Server의 버전과 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)을 참조하세요. 
  
     선택한 기능의 필수 구성 요소가 오른쪽 창에 표시됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서는 이미 설치되어 있지 않은 필수 구성 요소가 있는 경우 이 절차의 뒷부분에 설명된 설치 단계에서 이를 설치합니다. 
  
10. **이미지 준비 규칙** 페이지에서 시스템 구성 검사기가 설치를 계속하기 전에 컴퓨터의 시스템 상태를 확인합니다. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다. 
  
11. 인스턴스 구성 페이지에서 해당 인스턴스의 인스턴스 ID를 지정합니다. 계속하려면 **다음** 을 클릭합니다. 
  
     **인스턴스 ID** — 인스턴스 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 설치 디렉터리 및 레지스트리 키를 식별하는 데 사용됩니다. 이는 기본 인스턴스와 명명된 인스턴스에 모두 해당됩니다. 준비 인스턴스가 완료 단계 중에 기본 인스턴스로 완료되면 MSSQLSERVER가 인스턴스 이름을 덮어쓰고 인스턴스 ID는 지정한 대로 유지됩니다. 
  
     **인스턴스 루트 디렉터리** — 기본적으로 인스턴스 루트 디렉터리는 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]입니다. 기본 위치가 아닌 루트 디렉터리를 지정하려면 제공된 필드를 사용하거나 **찾아보기** 를 클릭하여 설치 폴더를 찾습니다. 준비 단계에서 지정된 디렉터리는 완료 단계의 구성 작업에 사용됩니다. 
  
     모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 팩 및 업그레이드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 구성 요소에 적용됩니다. 
  
     **설치된 인스턴스** — 설치 프로그램을 실행 중인 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 표 형식으로 표시됩니다. 
  
12. **디스크 공간 요구 사항** 페이지에서는 지정한 기능에 필요한 디스크 공간을 계산합니다. 그런 다음 사용 가능한 디스크 공간과 필요한 디스크 공간을 비교합니다. 
  
13. 시스템 구성 검사기는 사용자가 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능에 따라 컴퓨터 구성의 유효성을 검사하기 위해 이미지 준비 규칙을 실행합니다. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다. 
  
14. **이미지 준비 작업 준비** 페이지에 설치 중에 지정한 설치 옵션이 트리 뷰 형태로 표시됩니다. 설치 프로그램의 이 페이지에서는 제품 업데이트 기능이 사용하도록 설정되었는지 여부와 최종 업데이트 버전이 표시됩니다. 계속하려면 **준비**를 클릭합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 선택한 기능에 대한 필수 구성 요소를 먼저 설치하고 그 다음에 기능을 설치합니다. 
  
15. 설치하는 동안 **이미지 준비 진행률** 페이지에 상태 정보가 제공되므로 설치 진행률을 모니터링할 수 있습니다. 
  
16. 설치가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 **완료** 페이지에 제공됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 과정을 완료하려면 **닫기**를 클릭합니다. 
  
17. 컴퓨터를 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 자세한 내용은 [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)을 참조하세요. 
  
18. 준비 단계가 끝났습니다. [Considerations for Installing SQL Server Using SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)에 설명한 대로 이미지를 완료하거나 준비 이미지를 배포할 수 있습니다. 
  
##  <a name="complete"></a> 이미지 완료  
  
### <a name="complete-a-prepared-instance-of-includessnoversionincludesssnoversion-mdmd"></a>다음 준비 인스턴스 완료: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 준비 인스턴스가 컴퓨터의 이미지에 포함되어 있으면 시작 메뉴에 바로 가기가 나타납니다. 설치 센터를 시작하고 **고급** 페이지에서 **독립 실행형 준비 인스턴스의 이미지 완료** 를 클릭할 수도 있습니다. 
  
2. 시스템 구성 검사기가 컴퓨터에서 검색 작업을 실행합니다. 계속하려면 **확인**을 클릭합니다. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다. 
  
3. **설치 지원 파일** 페이지에서 **설치** 를 클릭하여 설치 지원 파일을 설치합니다. 
  
4. 시스템 구성 검사기가 설치를 계속하기 전에 컴퓨터의 시스템 상태를 확인합니다. 검사가 완료되면 **다음** 을 클릭하여 작업을 계속 진행합니다. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다. 
  
5. **제품 키** 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]무료 버전을 설치할지 아니면 PID 키가 있는 제품의 프로덕션 버전을 설치할지를 나타내는 옵션 단추를 선택합니다. 자세한 내용은 [SQL Server의 버전과 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)을 참조하세요. Evaluation Edition을 설치하는 경우 이 단계를 완료하면 180일의 무료 사용 기간이 시작됩니다. 
  
6. **사용 조건** 페이지에서 사용권 계약을 읽은 다음 사용 조건과 계약 조건에 동의하면 해당 확인란을 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 개선을 돕기 위해 기능 사용 옵션을 사용하도록 설정하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)]로 보고서를 보낼 수도 있습니다. 
  
7. **준비 인스턴스 선택** 페이지의 드롭다운 상자에서 완료할 준비 인스턴스를 선택합니다. **인스턴스 ID** 목록에서 구성되지 않은 인스턴스를 선택합니다. 
  
     **설치된 인스턴스:** 준비 인스턴스를 포함하여 이 컴퓨터에 설치되어 있는 모든 인스턴스가 표시됩니다. 
  
8. 준비 단계에서 설치에 포함하도록 선택한 기능 및 구성 요소가 **기능 검토** 페이지에 표시됩니다. 준비 인스턴스에 포함되지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 다른 기능을 더 추가하려면 먼저 이 단계를 완료하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 완료한 다음, **설치 센터** 의 **기능 추가**에서 기능을 추가해야 합니다. 
  
    > [!NOTE]  
    >  설치하는 제품 버전에 사용할 수 있는 기능을 추가할 수 있습니다. 자세한 내용은 [SQL Server의 버전과 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)을 참조하세요.  
  
9. 인스턴스 구성 페이지에서 준비 인스턴스의 인스턴스 이름을 지정합니다. 이것은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]구성을 완료한 인스턴스의 이름입니다. 계속하려면 **다음** 을 클릭합니다. 
  
     **인스턴스 ID** — 인스턴스 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 설치 디렉터리 및 레지스트리 키를 식별하는 데 사용됩니다. 이는 기본 인스턴스와 명명된 인스턴스에 모두 해당됩니다. 준비 인스턴스가 완료 단계 중에 기본 인스턴스로 완료되면 MSSQLSERVER가 인스턴스 이름을 덮어쓰고 인스턴스 ID는 준비 단계에서 지정한 대로 유지됩니다. 
  
     **인스턴스 루트 디렉터리** — 준비 단계에서 지정한 디렉터리가 사용되고 이 단계에서 수정할 수 없습니다. 
  
     모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 팩 및 업그레이드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 구성 요소에 적용됩니다. 
  
     **설치된 인스턴스** — 설치 프로그램을 실행 중인 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 표 형식으로 표시됩니다. 
  
10. 이 문서의 나머지 부분에 대한 워크플로는 준비 단계에서 선택한 기능에 따라 달라집니다. 선택 항목에 따라 일부 페이지가 표시되지 않을 수도 있습니다. 
  
11. **서버 구성** - 서비스 계정 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대한 로그인 계정을 지정합니다. 이 페이지에 구성된 실제 서비스는 사용자가 설치하도록 선택한 기능에 따라 달라집니다. 
  
     모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 동일한 로그인 계정을 할당하거나 각 서비스 계정을 따로 구성할 수 있습니다. 서비스 시작 유형을 자동 또는 수동으로 지정하거나 서비스의 해제 여부도 지정할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 서비스 계정을 개별적으로 구성하여 각 서비스에 대해 최소한의 권한만 제공할 것을 권장합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에서 태스크를 완료하는 데 필요한 최소한의 권한만 부여할 수 있습니다. 자세한 내용은 [서버 구성 - 서비스 계정](http://msdn.microsoft.com/library/c283702d-ab20-4bfa-9272-f0c53c31cb9f) 및 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요. 
  
     이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 서비스 계정에 대해 동일한 로그온 계정을 지정하려면 페이지 맨 아래에 있는 필드에 자격 증명을 입력합니다. 
  
     **보안 정보** [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대한 로그인 정보 지정을 완료하면 **다음**을 클릭합니다. 
  
12. **서버 구성 - 데이터 정렬** 탭을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 기본이 아닌 데이터 정렬을 지정합니다. 자세한 내용은 [서버 구성 - 데이터 정렬](http://msdn.microsoft.com/library/e3986870-5be4-458b-b671-5ff12a27b022)을 참조하세요. 
  
13. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성 - 계정 프로비전 페이지를 사용하여 다음을 지정합니다.  
  
    - 보안 모드 — [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대해 Windows 인증 또는 혼합 모드 인증을 선택합니다. 혼합 모드 인증을 선택할 경우 기본 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자 계정에 강력한 암호를 제공해야 합니다. 
  
         장치가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 성공적으로 연결되면 Windows 인증 및 혼합 모드에 모두 동일한 보안 메커니즘이 적용됩니다. 자세한 내용은 [데이터베이스 엔진 구성 - 서버 구성](http://msdn.microsoft.com/library/834b26bc-49de-4033-88d5-6aa7b1609720)을 참조하세요. 
  
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 시스템 관리자를 한 명 이상 지정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하는 계정을 추가하려면 **현재 사용자 추가**를 클릭합니다. 시스템 관리자 목록에 계정을 추가하거나 목록의 계정을 제거하려면 **추가** 또는 **제거**를 클릭한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 관리자 권한을 가질 사용자, 그룹 또는 컴퓨터 목록을 편집합니다. 자세한 내용은 [데이터베이스 엔진 구성 - 서버 구성](http://msdn.microsoft.com/library/834b26bc-49de-4033-88d5-6aa7b1609720)을 참조하세요. 
  
     목록 편집을 마쳤으면 **확인**을 클릭합니다. 구성 대화 상자에서 관리자 목록을 확인합니다. 목록 구성을 완료했으면 **다음**을 클릭합니다. 
  
14. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성 - 데이터 디렉터리 페이지를 사용하여 기본이 아닌 설치 디렉터리를 지정합니다. 기본 디렉터리에 설치하려면 **다음**을 클릭합니다. 
  
    > [!IMPORTANT]  
    >  기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대해 고유한지 확인해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. 
  
     자세한 내용은 [데이터베이스 엔진 구성 - 데이터 디렉터리](http://msdn.microsoft.com/library/9b1fa0fc-623b-479a-afc3-4f13bd850487)를 참조하세요. 
  
15. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성 - FILESTREAM 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 FILESTREAM을 설정합니다. 자세한 내용은 [데이터베이스 엔진 구성 - Filestream](http://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02)을 참조하세요. 
  
16. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 페이지를 사용하여 만들 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 유형을 지정할 수 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 모드에 대한 자세한 내용은 [Reporting Services 구성 옵션&#40;SSRS&#41;](http://msdn.microsoft.com/library/e4561f6c-bc7f-467e-821a-cde8e5cd7391)을 참조하세요. 
  
17. **오류 보고** 페이지에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 개선에 도움이 되도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 보낼 정보를 지정할 수 있습니다. 오류 보고 옵션은 기본적으로 사용됩니다. 
  
18. **이미지 완료 규칙** 페이지에서 시스템 구성 검사기는 사용자가 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성에 따라 컴퓨터 구성의 유효성을 검사하기 위해 이미지 완료 규칙을 실행합니다. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다. 
  
19. **이미지 완료 준비** 페이지에 설치 중에 지정한 설치 옵션이 트리 뷰 형태로 표시됩니다. 계속하려면 **설치**를 클릭합니다. 
  
20. 설치하는 동안 **이미지 완료 진행률** 페이지에 상태 정보가 제공되므로 설치 진행률을 모니터링할 수 있습니다. 
  
21. 설치가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 **완료** 페이지에 제공됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 과정을 완료하려면 **닫기**를 클릭합니다. 
  
22. 컴퓨터를 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 자세한 내용은 [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)을 참조하세요. 
  
23. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 준비 인스턴스 구성이 끝나고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치를 완료했습니다. 
  
##  <a name="AddFeatures"></a> Add Features to a Prepared Instance  
  
### <a name="add-features-to-a-prepared-instance-of-includessnoversionincludesssnoversion-mdmd"></a>다음 준비 인스턴스에 기능 추가: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 폴더에서 Setup.exe를 두 번 클릭합니다. 네트워크 공유에서 설치하려면 공유에서 루트 폴더를 찾은 다음 Setup.exe를 두 번 클릭합니다. 
  
2. 설치 마법사가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터를 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 준비 인스턴스에 기능을 추가하려면 **고급** 페이지에서 **독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이미지 준비**를 클릭합니다. 
  
3. 시스템 구성 검사기가 컴퓨터에서 검색 작업을 실행합니다. 계속하려면 **확인**을 클릭합니다. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다. 
  
4. 설치 지원 파일 페이지에서 **설치** 를 클릭하여 설치 지원 파일을 설치합니다. 
  
5. **이미지 유형 준비** 페이지에서 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기존 준비 인스턴스에 기능 추가** 옵션을 선택합니다. 사용 가능한 준비 인스턴스가 포함된 드롭다운 목록에서 기능을 추가할 특정 준비 인스턴스를 선택합니다. 
  
6. **기능 선택** 페이지가 나타나면 이전 단계에서 선택한 준비 인스턴스에 추가할 기능을 지정합니다. 
  
     선택한 기능의 필수 구성 요소가 오른쪽 창에 표시됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서는 이미 설치되어 있지 않은 필수 구성 요소가 있는 경우 이 절차의 뒷부분에 설명된 설치 단계에서 이를 설치합니다. 
  
7. **이미지 준비 규칙** 페이지에서 시스템 구성 검사기가 설치를 계속하기 전에 컴퓨터의 시스템 상태를 확인합니다. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다. 
  
8. 디스크 공간 요구 사항 페이지에서는 지정한 기능에 필요한 디스크 공간을 계산합니다. 그런 다음 사용 가능한 디스크 공간과 필요한 디스크 공간을 비교합니다. 
  
9. **이미지 준비 규칙** 페이지에서 시스템 구성 검사기는 사용자가 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능에 따라 컴퓨터 구성의 유효성을 검사하기 위해 이미지 준비 규칙을 실행합니다. **자세한 정보 표시**를 클릭하여 화면에 세부 정보를 표시하거나 **자세한 보고서 보기**를 클릭하여 HTML 보고서 형식으로 볼 수 있습니다. 
  
10. **이미지 준비 작업 준비** 페이지에 설치 중에 지정한 설치 옵션이 트리 뷰 형태로 표시됩니다. 계속하려면 **설치**를 클릭합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 선택한 기능에 대한 필수 구성 요소를 먼저 설치하고 그 다음에 기능을 설치합니다. 
  
11. 설치하는 동안 **이미지 준비 진행률** 페이지에 상태 정보가 제공되므로 설치 진행률을 모니터링할 수 있습니다. 
  
12. 설치가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 **완료** 페이지에 제공됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 과정을 완료하려면 **닫기**를 클릭합니다. 
  
13. 컴퓨터를 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 자세한 내용은 [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)을 참조하세요. 
  
##  <a name="RemoveFeatures"></a> 준비 인스턴스에서 기능 제거  
  
### <a name="removing-features-from-a-prepared-instance-of-includessnoversionincludesssnoversion-mdmd"></a>다음 준비 인스턴스에서 기능 제거: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1. 제거 프로세스를 시작하려면 **시작** 메뉴에서 **제어판** 을 클릭하고 **프로그램 및 기능**을 두 번 클릭합니다. 
  
2. 제거할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 두 번 클릭하고 **제거**를 클릭합니다. 
  
3. 컴퓨터 구성을 확인하기 위해 설치 지원 규칙이 실행됩니다. 계속하려면 **확인** 을 클릭합니다. 
  
4. **인스턴스 선택** 페이지에서 수정할 준비 인스턴스를 선택합니다. PreparedInstanceID 인스턴스를 선택하면 준비 인스턴스의 이름이 "구성되지 않은 PreparedInstanceID"로 표시됩니다. 
  
5. **기능 선택** 페이지가 나타나면 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 제거할 기능을 지정합니다. 계속하려면 **다음** 을 클릭합니다. 
  
6. 작업을 성공적으로 완료할 수 있는지 확인하기 위해 제거 규칙이 실행됩니다. 
  
7. **제거 준비** 페이지에서 제거할 구성 요소 및 기능 목록을 검토합니다. 
  
8. **제거 진행률** 페이지에 작업 상태가 표시됩니다. 
  
9. **완료** 페이지에서 작업 완료 상태를 검토할 수 있습니다. 설치 마법사를 끝내려면 **닫기** 를 클릭합니다. 
  
##  <a name="Uninstall"></a> 준비 인스턴스 제거  
  
### <a name="uninstall-a-prepared-instance-of-includessnoversionincludesssnoversion-mdmd"></a>다음 준비 인스턴스 제거: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1. 제거 프로세스를 시작하려면 **시작** 메뉴에서 **제어판** 을 클릭하고 **프로그램 및 기능**을 두 번 클릭합니다. 
  
2. 제거할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 두 번 클릭하고 **제거**를 클릭합니다. 
  
3. 컴퓨터 구성을 확인하기 위해 설치 지원 규칙이 실행됩니다. 계속하려면 **확인** 을 클릭합니다. 
  
4. **인스턴스 선택** 페이지에서 수정할 준비 인스턴스를 선택합니다. PreparedInstanceID 인스턴스를 선택하면 준비 인스턴스의 이름이 "구성되지 않은 PreparedInstanceID"로 표시됩니다. 
  
5. **기능 선택** 페이지가 나타나면 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 제거할 기능을 지정합니다. 계속하려면 **다음** 을 클릭합니다. 
  
6. **제거 규칙** 페이지에서 작업을 성공적으로 완료할 수 있는지 확인하기 위해 설치 프로그램이 규칙을 실행합니다. 
  
7. **제거 준비** 페이지에서 제거할 구성 요소 및 기능 목록을 검토합니다. 
  
8. **제거 진행률** 페이지에 작업 상태가 표시됩니다. 
  
9. **완료** 페이지에서 작업 완료 상태를 검토할 수 있습니다. 설치 마법사를 끝내려면 **닫기** 를 클릭합니다. 
  
10. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 모든 구성 요소가 제거될 때까지 1-9단계를 반복합니다. 
  
##  <a name="bk_Modifying_Uninstalling"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 완료된 인스턴스 수정 또는 제거 
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 완료된 인스턴스를 제거하거나 기능을 추가 또는 제거하는 작업은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 설치된 인스턴스에 대한 작업과 프로세스가 비슷합니다. 자세한 내용은 다음 문서를 참조하세요.  
  
- [SQL Server 인스턴스에 기능 추가&#40;설치 프로그램&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)  
  
- [SQL Server의 기존 인스턴스 제거&#40;설치 프로그램&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)  
  
## <a name="see-also"></a>참고 항목  
 [Sysprep이란?](http://go.microsoft.com/fwlink/?LinkId=143546)   
 [Windows Sysprep 작동 방법](http://go.microsoft.com/fwlink/?LinkId=143547)  
  
  
