---
title: 장애 조치(Failover) 클러스터 문제 해결 | Microsoft 문서
description: 오류 복구, 일반적인 문제 해결, 확장 저장 프로시저/COM 개체 사용을 비롯하여 장애 조치(failover) 클러스터 문제 해결에 대해 알아봅니다.
ms.custom: ''
ms.date: 10/21/2015
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- troublshooting, failover clustering
- failover clustering, troubleshooting
- cluster troubleshooting
ms.assetid: 84012320-5a7b-45b0-8feb-325bf0e21324
author: cawrites
ms.author: chadam
ms.openlocfilehash: 75090ce180ff6e71796c9363e39768f09ec3f91b
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96121098"
---
# <a name="failover-cluster-troubleshooting"></a>장애 조치(Failover) 클러스터 문제 해결
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  이 항목에는 다음 문제에 대한 정보가 있습니다.  
  
-   기본 문제 해결 단계  
  
-   장애 조치(Failover) 클러스터 오류 복구  
  
-   일반적인 장애 조치(Failover) 클러스터링 문제 해결  
  
-   확장 저장 프로시저 및 COM 개체 사용  
  
## <a name="basic-troubleshooting-steps"></a>기본 문제 해결 단계  
 첫 번째 진단 단계는 새로운 클러스터 유효성 검사 확인을 실행하는 것입니다. 유효성 검사에 대한 자세한 내용은 [장애 조치(failover) 클러스터 단계별 가이드: 장애 조치(failover) 클러스터에 대한 하드웨어 유효성 검사](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732035(v=ws.10))를 참조하세요.  이 작업은 어떠한 온라인 클러스터 리소스에도 영향을 주지 않으므로 중단 없이 완료할 수 있습니다. 장애 조치(failover) 클러스터링 기능이 설치되었으면 클러스터가 배포되기 전, 클러스터 생성 중, 클러스터가 실행되는 동안을 포함하여 언제든지 유효성 검사를 실행할 수 있습니다. 실제로 클러스터가 사용 중이면 고가용성 워크로드를 위해 모범 사례를 따르고 있는지 확인하는 추가 테스트를 실행합니다. 이러한 수십 가지 테스트 중에 일부만 실행 중인 클러스터 워크로드에 영향을 주며 모두 스토리지 범주 내에 있으므로 이 전체 범주를 건너뛰면 테스트 중단을 쉽게 피할 수 있습니다.  
장애 조치(failover) 클러스터링에는 유효성 검사 중에 스토리지 테스트를 실행할 때 실수로 인한 중단 시간을 방지하기 위해 기본 제공 보호 기능이 함께 제공됩니다. 유효성 검사가 시작될 때 클러스터에 온라인 그룹이 있는 경우 스토리지 테스트가 선택된 상태로 있으면 모든 테스트를 실행할지(중단 시간 발생) 중단 시간을 피하기 위해 온라인 그룹 디스크의 테스트를 건너뛸지 묻는 메시지가 사용자에게 표시됩니다. 전체 스토리지 범주가 테스트에서 제외된 경우 이 메시지는 표시되지 않습니다. 이렇게 하면 중단 시간 없이 클러스터 유효성 검사가 가능합니다.  
  
#### <a name="how-to-revalidate-your-cluster"></a>클러스터의 유효성을 다시 검사하는 방법  
  
1.  장애 조치(failover) 클러스터 스냅인의 콘솔 트리에서 **장애 조치(failover) 클러스터 관리** 가 선택되어 있는지 확인하고 **관리** 아래에서 **구성 유효성 검사** 를 클릭합니다.  
  
2.  마법사의 지침에 따라 서버 및 테스트를 지정하고 테스트를 실행합니다. 테스트가 실행된 후 **요약** 페이지가 나타납니다.  
  
3.  **요약** 페이지에 있는 동안 **보고서 보기** 를 클릭하여 테스트 결과를 봅니다.  
  
     마법사를 닫은 후 테스트 결과를 보려면 **%SystemRoot%\Cluster\Reports\Validation Report date and time.html** 을 확인합니다. 여기서 **%SystemRoot%** 는 운영 체제가 설치된 폴더입니다(예: **C:\Windows**).  
  
4.  결과를 해석하는 데 도움이 되는 도움말 항목을 보려면 **클러스터 유효성 검사 테스트에 대한 추가 정보** 를 클릭합니다.  
  
 마법사를 닫은 후 클러스터 유효성 검사에 대한 도움말 항목을 보려면 장애 조치(failover) 클러스터 스냅인에서 **도움말**, **도움말 항목**, **목차** 탭을 차례로 클릭하고 장애 조치(failover) 클러스터 도움말에 대한 내용을 확장한 후 **장애 조치(failover) 클러스터 구성 유효성 검사** 를 클릭합니다.  유효성 검사 마법사를 완료하면 **요약 보고서** 에 결과가 표시됩니다. 녹색 확인 표시 또는 경우에 따라 노란색 삼각형(경고)와 함께 모든 테스트를 통과해야 합니다. 테스트 결과를 요약하는 보고서의 일부에서 문제 영역(빨간색 X 또는 노란색 물음표)을 찾을 때는 개별 테스트를 클릭하여 세부 정보를 검토합니다. 모든 빨간색 X 문제는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 문제를 해결하기 전에 해결해야 합니다.  
  
 **업데이트 설치**  
  
 업데이트 설치는 시스템에서 문제를 피하기 위한 중요한 부분입니다. 유용한 링크:  
  
-   [Windows Server 2012 R2 기반 장애 조치(Failover) 클러스터의 권장 핫픽스 및 업데이트](https://support.microsoft.com/kb/2920151)  
  
-   [Windows Server 2012 기반 장애 조치(Failover) 클러스터의 권장 핫픽스 및 업데이트](https://support.microsoft.com/kb/2784261)  
  
-   [Windows Server 2008 R2 기반 장애 조치(Failover) 클러스터의 권장 핫픽스 및 업데이트](https://support.microsoft.com/kb/980054)  
  
-   [Windows Server 2008 기반 장애 조치(Failover) 클러스터의 권장 핫픽스 및 업데이트](https://support.microsoft.com/kb/957311)  
  
## <a name="recovering-from-failover-cluster-failure"></a>장애 조치(Failover) 클러스터 오류 복구  
 대개 장애 조치(Failover) 클러스터 오류의 원인은 다음 두 가지 중 하나입니다.  
  
-   이중 노드 클러스터의 한 노드에서 발생한 하드웨어 오류. 이 하드웨어 오류는 SCSI 카드 또는 운영 체제의 오류에 의해 발생할 수 있습니다.  
  
     이 오류를 복구하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 장애 조치(Failover) 클러스터에서 실패한 노드를 제거하고 컴퓨터를 오프라인 상태로 만들어 하드웨어 오류를 해결한 다음 컴퓨터를 다시 온라인 상태로 만들고 복구한 노드를 장애 조치(Failover) 클러스터 인스턴스에 다시 추가합니다.  
  
     자세한 내용은 [새 SQL Server 장애 조치(failover) 클러스터 만들기&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md) 및 [장애 조치(failover) 클러스터 인스턴스 오류 복구](../../../sql-server/failover-clusters/windows/recover-from-failover-cluster-instance-failure.md)를 참조하세요.  
  
-   운영 체제 오류. 이 경우 노드는 오프라인이지만 복구 불능 상태는 아닙니다.  
  
     운영 체제 오류를 복구하려면 노드를 복구하고 장애 조치(Failover)를 테스트합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 장애 조치(Failover)가 제대로 수행되지 않으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 장애 조치(Failover) 클러스터에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 제거하고 필요한 복구를 수행한 다음 컴퓨터를 다시 온라인 상태로 만들고 복구한 노드를 다시 장애 조치(Failover) 클러스터 인스턴스에 추가합니다.  
  
     이 방법으로 운영 체제 오류를 복구하면 시간이 걸릴 수 있습니다. 운영 체제 오류를 쉽게 복구할 수 있다면 이 방법을 사용하지 마십시오.  
  
     자세한 내용은 [새 SQL Server 장애 조치(failover) 클러스터 만들기&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md) 및 [방법: 시나리오 2의 장애 조치(failover) 클러스터 오류 복구](recover-from-failover-cluster-instance-failure.md)를 참조하세요.  
  
## <a name="resolving-common-problems"></a>일반적인 문제 해결  
 다음 목록에서는 일반적인 사용법 문제와 그 해결 방법에 대해 설명합니다.  
  
### <a name="problem-incorrect-use-of-command-prompt-syntax-to-install-sql-server"></a>문제: SQL Server를 설치하기 위한 명령 프롬프트 구문을 잘못 사용했습니다.  
 **문제점 1:****/qn** 스위치는 모든 설치 대화 상자와 오류 메시지를 표시하지 않도록 지정하는 스위치이므로 명령 프롬프트에서 **/qn** 스위치를 사용하면 설치 문제를 진단하기가 어렵습니다. **/qn** 스위치를 지정하면 오류 메시지를 비롯한 모든 설치 메시지가 설치 로그 파일에 기록됩니다. 로그 파일에 대한 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조하세요.  
  
 **해결 방법 1**: **/qn** 스위치 대신 **/qb** 스위치를 사용합니다. **/qb** 스위치를 사용하면 오류 메시지를 포함하여 각 단계의 기본 UI가 표시됩니다.  
  
### <a name="problem-sql-server-cannot-log-on-to-the-network-after-it-migrates-to-another-node"></a>문제: SQL Server에서 다른 노드로 마이그레이션한 다음에는 네트워크에 로그온할 수 없습니다.  
 **문제 1:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정이 도메인 컨트롤러에 연결할 수 없습니다.  
  
 **해결 방법 1**: 이벤트 로그에 어댑터 오류나 DNS 문제와 같은 네트워킹 문제가 있는지 검사합니다. 도메인 컨트롤러를 ping할 수 있는지 확인합니다.  
  
 **문제 2:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정 암호가 모든 클러스터 노드에서 동일하지 않거나 실패한 노드로부터 마이그레이션한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 노드에서 다시 시작되지 않습니다.  
  
 **해결 방법 2:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정 암호를 변경합니다. 그렇지 않고 한 노드에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정 암호를 변경하면 다른 모든 노드의 암호도 변경해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자에서 이 작업을 자동으로 수행합니다.  
  
### <a name="problem-sql-server-cannot-access-the-cluster-disks"></a>문제: SQL Server에서 클러스터 디스크에 액세스할 수 없습니다.  
 **문제 1:** 일부 노드에서 펌웨어나 드라이버가 업데이트되지 않았습니다.  
  
 **해결 방법 1:** 모든 노드에서 올바른 펌웨어 버전과 동일한 드라이버 버전을 사용하고 있는지 확인합니다.  
  
 **문제점 2:** 공유 클러스터 디스크에서 다른 드라이브 문자를 사용할 경우 노드가 실패한 노드에서 마이그레이션된 클러스터 디스크를 복구할 수 없습니다.  
  
 **해결 방법 2:** 클러스터 디스크의 디스크 드라이브 문자는 두 서버에서 동일해야 합니다. 그렇지 않을 경우 운영 체제와 MSCS( [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Cluster Service)의 원래 설치를 검토하십시오.  
  
### <a name="problem-failure-of-a-sql-server-service-causes-failover"></a>문제: SQL Server 서비스 오류로 인해 장애 조치(failover)가 발생합니다.  
 **해결 방법:** 특정 서비스의 오류 때문에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 그룹에서 장애 조치(Failover)를 수행하지 않도록 하려면 Windows의 클러스터 관리자를 사용하여 다음과 같이 해당 서비스를 구성합니다.  
  
-   **전체 텍스트 속성** 대화 상자의 **고급** 탭에서 **그룹에 영향을 줌** 확인란 선택을 취소합니다. 그러나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 장애 조치(Failover)를 일으키면 전체 텍스트 검색 서비스가 다시 시작됩니다.  
  
### <a name="problem-sql-server-does-not-start-automatically"></a>문제: SQL Server가 자동으로 시작되지 않습니다.  
 **해결 방법:** MSCS의 클러스터 관리자를 사용하여 자동으로 장애 조치(failover) 클러스터를 시작합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 수동으로 시작되도록 설정해야 합니다. MSCS에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스를 시작하도록 클러스터 관리자를 구성해야 합니다. 자세한 내용은 [서비스 관리](https://msdn.microsoft.com/library/ms178096\(v=sql.105\).aspx)를 참조하세요.  
  
### <a name="problem-the-network-name-is-offline-and-you-cannot-connect-to-sql-server-using-tcpip"></a>문제: 네트워크 이름이 오프라인 상태이고 TCP/IP를 사용하여 SQL Server에 연결할 수 없습니다.  
 **문제 1:** 클러스터 리소스가 DNS를 요구하도록 설정된 상태에서 DNS가 실패합니다.  
  
 **해결 방법 1:** DNS 문제를 해결합니다.  
  
 **문제 2:** 네트워크에 중복된 이름이 있습니다.  
  
 **해결 방법 2:** NBTSTAT를 사용하여 중복된 이름을 찾은 다음 문제를 해결합니다.  
  
 **문제 3:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 명명된 파이프를 사용하여 연결하지 않습니다.  
  
 **해결 방법 3:** 명명된 파이프를 사용하여 연결하려면 SQL Server 구성 관리자를 사용하여 별칭을 만들고 적절한 컴퓨터에 연결합니다. 예를 들어 노드가 두 개(**노드 A** 및 **노드 B**)인 클러스터와 기본 인스턴스를 가진 장애 조치(failover) 클러스터 인스턴스(**Virtsql**)가 있으면 다음 단계를 수행하여 네트워크 이름 리소스가 오프라인 상태인 서버에 연결할 수 있습니다.  
  
1.  클러스터 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스가 있는 그룹이 실행 중인 노드를 확인합니다. 이 예에서는 **노드 A** 입니다.  
  
2.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] net start **를 사용하여 해당 컴퓨터에서** 서비스를 시작합니다. **net start** 를 사용하는 방법은 [SQL Server 수동 시작](https://msdn.microsoft.com/library/ms191193\(v=sql.105\).aspx)을 참조하세요.  
  
3.  **노드 A** 에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL Server 구성 관리자를 시작합니다. 서버가 수신하는 파이프 이름을 확인합니다. 파이프 이름은 \\\\.\\$$\VIRTSQL\pipe\sql\query와 비슷해야 합니다.  
  
4.  클라이언트 컴퓨터에서 SQL Server 구성 관리자를 시작합니다.  
  
5.  별칭 SQLTEST1을 만들어 명명된 파이프를 통해 이 파이프 이름에 연결합니다. 그러려면 **노드 A** 를 서버 이름으로 입력하고 파이프 이름을 \\\\.\pipe\\$$\VIRTSQL\sql\query로 편집합니다.  
  
6.  별칭 SQLTEST1을 서버 이름으로 사용하여 이 인스턴스에 연결합니다.  
  
### <a name="problem-sql-server-setup-fails-on-a-cluster-with-error-11001"></a>문제: 오류 11001이 발생하여 클러스터에 SQL Server를 설치하지 못했습니다.  
 **문제:** [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.X\Cluster]에 고아 레지스트리 키가 있습니다.  
  
 **해결 방법:** MSSQL.X 레지스트리 하이브가 현재 사용되고 있지 않은지 확인한 다음, 클러스터 키를 삭제합니다.  
  
### <a name="problem-cluster-setup-error-the-installer-has-insufficient-privileges-to-access-this-directory-drivemicrosoft-sql-server-the-installation-cannot-continue-log-on-as-an-administrator-or-contact-your-system-administrator"></a>문제: 클러스터 설치 오류: "이 디렉터리에 액세스할 수 있는 권한이 없습니다. \<drive>\Microsoft SQL Server. 설치를 계속할 수 없습니다. Administrator로 로그온하거나 시스템 관리자에게 문의하십시오."  
 **문제:** 이 오류는 SCSI 공유 드라이브의 파티션 문제로 인해 발생합니다.  
  
 **해결 방법:** 다음 단계를 수행하여 공유 디스크에 파티션 하나를 다시 만듭니다.  
  
1.  클러스터에서 디스크 리소스를 삭제합니다.  
  
2.  디스크의 모든 파티션을 삭제합니다.  
  
3.  디스크 속성에서 해당 디스크가 기본 디스크인지 확인합니다.  
  
4.  공유 디스크에 파티션 한 개를 만들고 디스크를 포맷한 다음 디스크에 드라이브 문자를 할당합니다.  
  
5.  클러스터 관리자(cluadmin)를 사용하여 클러스터에 디스크를 추가합니다.  
  
6.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행합니다.  
  
### <a name="problem-applications-fail-to-enlist-sql-server-resources-in-a-distributed-transaction"></a>문제: 애플리케이션이 SQL Server 리소스를 분산 트랜잭션에 등록하지 못했습니다.  
 **문제점:** Windows에서 MS DTC( [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Distributed Transaction Coordinator)가 완전하게 구성되지 않아서 애플리케이션에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스를 분산 트랜잭션에 등록하지 못할 수 있습니다. 이 문제는 연결된 서버, 분산 쿼리 및 분산 트랜잭션을 사용하는 원격 저장 프로시저에 영향을 미칠 수 있습니다. MS DTC를 구성하는 방법은 [Before Installing Failover Clustering](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)를 참조하십시오.  
  
 **해결 방법:** 이러한 문제를 방지하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 설치되고 MS DTC가 구성된 서버에서 MS DTC 서비스를 완전히 활성화해야 합니다.  
  
 MS DTC를 완전히 활성화하려면 다음 단계를 따르십시오.  
  
1.  제어판에서 **관리 도구** 를 열고 **컴퓨터 관리** 를 엽니다.  
  
2.  컴퓨터 관리 왼쪽 창에서 **서비스 및 애플리케이션** 을 확장한 다음 **서비스** 를 클릭합니다.  
  
3.  컴퓨터 관리 오른쪽 창에서 **Distributed Transaction Coordinator** 를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택합니다.  
  
4.  **Distributed Transaction Coordinator** 창에서 **일반** 탭을 클릭한 다음 **중지** 를 클릭하여 서비스를 중지합니다.  
  
5.  **Distributed Transaction Coordinator** 창에서 **로그온** 탭을 클릭하고 로그온 계정 NT AUTHORITY\NetworkService를 설정합니다.  
  
6.  **적용** 및 **확인** 을 클릭하여 **Distributed Transaction Coordinator** 창을 닫습니다. **컴퓨터 관리** 창을 닫습니다. **관리 도구** 창을 닫습니다.  
  
## <a name="using-extended-stored-procedures-and-com-objects"></a>확장 저장 프로시저 및 COM 개체 사용  
 장애 조치 클러스터링 구성에서 확장 저장 프로시저를 사용할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 종속적인 클러스터 디스크에 모든 확장 저장 프로시저를 설치해야 합니다. 그러면 노드에서 장애 조치(Failover)를 수행할 때 확장 저장 프로시저를 계속 사용할 수 있습니다.  
  
 확장 저장 프로시저에서 COM 구성 요소를 사용하면 관리자는 COM 구성 요소를 클러스터의 각 노드에 등록해야 합니다. COM 구성 요소의 로드 및 실행에 대한 정보는 구성 요소가 만들어지도록 액티브 노드의 레지스트리에 있어야 합니다. 그렇지 않으면 COM 구성 요소가 처음 등록된 컴퓨터의 레지스트리에 정보가 남아 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [확장 저장 프로시저 작동 원리](../../../relational-databases/extended-stored-procedures-programming/how-extended-stored-procedures-work.md)   
 [확장 저장 프로시저의 실행 특징](../../../relational-databases/extended-stored-procedures-programming/execution-characteristics-of-extended-stored-procedures.md)  
  
