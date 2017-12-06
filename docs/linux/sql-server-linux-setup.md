---
title: "SQL Server 2017 linux 설치 | Microsoft Docs"
description: "설치, 업데이트 및 Linux에서 SQL Server를 제거 합니다. 이 항목에서는 온라인, 오프 라인 및 무인 시나리오에 설명 합니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/26/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.workload: Active
ms.openlocfilehash: 65835ac1faf75664ecdbac8907c74906ccc4175e
ms.sourcegitcommit: 085dd05d56afecbb454206ed8402cfbaa597cfbe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>Linux에서 SQL Server에 대 한 설치 지침

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 항목에서는 설치, 업데이트 및 SQL Server 2017 Linux에서 제거 하는 방법에 설명 합니다. SQL Server 2017 Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES), 및 Ubuntu에서 지원 됩니다. Linux 또는 Docker에 대 한 Windows/Mac. Docker 엔진에서 실행할 수 있는 Docker 이미지 형식으로 제공 됩니다.

> [!TIP]
> 빠르게 시작 하려면 하나에 대 한 빠른 시작 자습서로 이동할 [RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), [Ubuntu](quickstart-install-connect-ubuntu.md), 또는 [Docker](quickstart-install-connect-docker.md)합니다.

## <a id="supportedplatforms"></a>지원 되는 플랫폼

SQL Server 2017 Linux 다음 플랫폼에서 사용할 수 있습니다.

| 플랫폼 | 지원 되는 버전 | 가져오기
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3 또는 7.4 | [7.4 RHEL 가져오기](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2 | [SLES v12 SP2 받기](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [Ubuntu 16.04 가져오기](http://www.ubuntu.com/download/server)
| **Docker 엔진** | 1.8+ | [Docker 가져오기](http://www.docker.com/products/overview)

## <a id="system"></a>시스템 요구 사항

SQL Server 2017 Linux에 대 한 다음과 같은 시스템 요구 사항에 있습니다.

|||
|-----|-----|
| **메모리** | 2GB |
| **파일 시스템** | **XFS** 또는 **EXT4** (예: 다른 파일 시스템, **BTRFS**, 지원 되지 않습니다) |
| **디스크 공간** | 6GB |
| **프로세서 속도** | 2 GHz |
| **프로세서 코어** | 2 코어 |
| **프로세서 유형** | x64 호환만 |

사용 하는 경우 **네트워크 파일 시스템 (NFS)** 프로덕션 환경에서 원격 공유에는 다음과 같은 지원 요구 사항을 확인 하세요.

- 사용 하 여 NFS 버전 **4.2 이상**합니다. 이전 버전의 NFS fallocate, 최신 파일 시스템에 공통 스파스 파일 만들기 등 필수 기능을 지원 하지 않습니다.
- 만 찾습니다는 **/var/opt/mssql** NFS 탑재 디렉터리입니다. SQL Server 시스템 이진 파일 등의 기타 파일 지원 되지 않습니다.
- 원격 공유 마운트할 때 NFS 클라이언트 'nolock' 옵션을 사용 하도록 확인 합니다.

## <a id="platforms"></a> SQL Server 설치

명령줄에서 Linux에서 SQL Server를 설치할 수 있습니다. 자세한 내용은 다음 빠른 시작 자습서 중 하나를 참조 하십시오.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-docker.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

## <a id="upgrade"></a>SQL Server를 업데이트 합니다.

업데이트 하는 **mssql 서버** 을 최신 릴리스로 해당 플랫폼에 따라 다음 명령 중 하나를 사용 합니다.

| 플랫폼 | 패키지 업데이트 명령 |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

이 명령은 최신 패키지를 다운로드 하 고 아래에 있는 이진 파일을 대체 `/opt/mssql/`합니다. 사용자가 생성 한 데이터베이스 및 시스템 데이터베이스는이 작업에 영향을 받지 않습니다.

## <a id="rollback"></a>SQL Server 롤백

롤백 또는 SQL Server 이전 버전으로 다운 그레이드 하려면 다음 단계를 사용 합니다.

1. 으로 다운 그레이드 하려면 SQL Server 패키지에 대 한 버전 번호를 식별 합니다. 목록이 패키지 번호에 대 한 참조는 [릴리스 정보](sql-server-linux-release-notes.md)합니다.

1. SQL Server의 이전 버전으로 다운 그레이드 합니다. 다음 명령에서 대체 `<version_number>` 을 1 단계에서 식별 된 SQL Server 버전 번호입니다.

   | 플랫폼 | 패키지 업데이트 명령 |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> SQL Server 2017 같은 같은 주 버전 내에서 릴리스를 다운 그레이드 하 에서만 지원 됩니다.

## <a id="versioncheck"></a>설치 된 SQL Server 버전 확인

현재 버전 및 Linux에서 SQL Server 버전을 확인 하려면 다음 절차를 따릅니다.

1. 아직 설치 하지 하는 경우 설치는 [SQL Server 명령줄 도구](sql-server-linux-setup-tools.md)합니다.

1. 사용 하 여 **sqlcmd** SQL Server 버전 및 버전을 표시 하는 Transact SQL 명령을 실행할 수 있습니다.

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a>SQL Server 제거

제거 하는 **mssql 서버** linux 플랫폼에 따라 다음 명령 중 하나를 사용 합니다.

| 플랫폼 | 패키지 제거 명령 |
|-----|-----|
| RHEL | `sudo yum remove mssql-server` |
| SLES | `sudo zypper remove mssql-server` |
| Ubuntu | `sudo apt-get remove mssql-server` |

패키지를 제거 하는 경우에 생성 된 데이터베이스 파일이 삭제 되지 않습니다. 데이터베이스 파일을 삭제 하려면 다음 명령을 사용 합니다.

```bash
sudo rm -rf /var/opt/mssql/
```

## <a id="repositories"></a>소스 저장소 구성

를 설치 하거나 SQL Server를 업그레이드 하는 경우 구성 된 Microsoft 리포지토리에서 SQL Server의 최신 버전을 가져옵니다.

### <a name="repository-options"></a>저장소 옵션

같은 두 가지 유형의 각 배포에 대 한 저장소는

- **CU (누적 업데이트)**: The CU (누적 업데이트) 저장소 해당 릴리스 이후 기본 SQL Server 릴리스 및 버그 수정 또는 향상 된 기능에 대 한 패키지를 포함 합니다. 누적 업데이트는 SQL Server 2017 등의 릴리스 버전에 고유 합니다. 일반 주기로 릴리스되는 합니다.

- **GDR**: The GDR 리포지토리 해당 릴리스 이후는 기본 SQL Server 릴리스만 주요 수정 프로그램 및 보안 업데이트에 대 한 패키지를 포함 합니다. 이러한 업데이트는 다음 CU 릴리스로 추가 됩니다.

각 CU 및 GDR 릴리스에 전체 SQL Server 패키지 및 해당 저장소에 대 한 모든 이전 업데이트를 포함합니다. CU 릴리스에 GDR 릴리스의 업데이트는 SQL Server에 대 한 구성된 저장소를 변경 하 여 지원 됩니다. 수도 있습니다 [다운 그레이드](#rollback) 주요 버전 내에서 모든 릴리스를 (예: 2017). 업데이트 CU에서 릴리스를 GDR 릴리스 지원 되지 않습니다.

### <a name="check-your-configured-repository"></a>구성 된 저장소를 확인 합니다.

어떤 저장소 구성 되어 있는지 확인 하려는 경우 다음 플랫폼에 종속 된 기술을 사용 합니다.

| 플랫폼 | 절차 |
|-----|-----|
| RHEL | 1. 파일을 볼는 **/etc/yum.repos.d** 디렉터리:`sudo ls /etc/yum.repos.d`<br/>2. 와 같은 SQL Server 디렉터리를 구성 하는 파일을 찾도록 **mssql server.repo**합니다.<br/>3. 파일의 내용을 출력.`sudo cat /etc/yum.repos.d/mssql-server.repo`<br/>4. **이름** 속성은 구성된 저장소입니다.|
| SLES | 1. `sudo zypper info mssql-server` 명령을 실행합니다.<br/>2. **리포지토리** 속성은 구성된 저장소입니다. |
| Ubuntu | 1. `sudo cat /etc/apt/sources.list` 명령을 실행합니다.<br/>2. Mssql 서버에 대 한 패키지 URL을 검사 합니다. |

리포지토리 URL의 끝을 저장소 유형을 확인합니다.

- **mssql 서버**: 미리 보기 저장소입니다.
- **mssql-서버-2017**: CU 저장소입니다.
- **mssql 서버-2017 gdr**: GDR 저장소입니다.

### <a name="change-the-source-repository"></a>소스 저장소 변경

CU 또는 GDR 저장소를 구성 하려면 다음 단계를 사용 합니다.

> [!NOTE]
> [빠른 시작 자습서](#platforms) CU 리포지토리를 구성 합니다. 이러한 자습서를 수행 하는 경우 다음 단계를 사용 하 여 CU 저장소를 사용 하 여 계속 필요가 없습니다. 이러한 단계는만 구성 된 저장소를 변경 하는 데 필요 합니다.

1. 필요한 경우 이전에 구성 된 저장소를 제거 합니다.

   | 플랫폼 | 리포지토리 | 저장소 제거 명령 |
   |---|---|---|
   | RHEL | **모두** | `sudo rm -rf /etc/yum.repos.d/mssql-server.repo` |
   | SLES | **CTP** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
   | | **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
   | | **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|
   | Ubuntu | **CTP** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` 
   | | **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
   | | **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

1. 에 대 한 **Ubuntu만**, 공용 리포지토리 GPG 키를 가져옵니다.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 새 저장소를 구성 합니다.

   | 플랫폼 | 리포지토리 | Command |
   |-----|-----|-----|
   | RHEL | CU | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
   | RHEL | GDR | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |
   | SLES | CU  | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
   | SLES | GDR | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |
   | Ubuntu | CU | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)" && sudo apt-get update` |
   | Ubuntu | GDR | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)" && sudo apt-get update` |

1. [설치](#platforms) 또는 [업데이트](#upgrade) 새 저장소에서 SQL Server 및 모든 관련 패키지 합니다.

   > [!IMPORTANT]
   > 와 같은 설치 자습서 중 하나를 사용 하기로 선택한 경우이 시점에서 [빠른 시작 자습서](#platforms), 대상 저장소 방금 구성한 기억 합니다. 이 자습서에서 해당 단계를 반복 하지 않습니다. 이 빠른 시작 자습서 CU 리포지토리를 사용 하기 때문에 GDR 저장소를 구성 하는 경우에 특히 그렇습니다.

## <a id="unattended"></a>무인된 설치

다음과 같은 방식으로 무인된 설치를 수행할 수 있습니다.

- 초기 단계에서 수행 된 [빠른 시작 자습서](#platforms) 리포지토리를 등록 및 SQL Server를 설치 합니다.
- 실행 하는 경우 `mssql-conf setup`설정, [환경 변수](sql-server-linux-configure-environment-variables.md) 사용 하는 `-n` (메시지 표시) 옵션입니다.

다음 예제에서는 구성 사용 하 여 SQL server Developer edition에서 **MSSQL_PID** 환경 변수입니다. EULA 받기도 (**ACCEPT_EULA**) SA 사용자 암호를 설정 하 고 (**MSSQL_SA_PASSWORD**). `-n` 매개 변수는 구성 값 환경 변수에서 찾아볼 수 있는 unprompted 설치 수행 합니다.

```bash
sudo MSSQL_PID=Developer ACCEPT_EULA=Y MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' /opt/mssql/bin/mssql-conf -n setup
```

또한 다른 동작을 수행 하는 스크립트를 만들 수 있습니다. 예를 들어 다른 SQL Server 패키지를 설치할 수 있습니다.

더 자세한 예제 스크립트를 다음 예제를 참조 하세요.

- [Red Hat 무인된 설치 스크립트](sample-unattended-install-redhat.md)
- [SUSE 무인된 설치 스크립트](sample-unattended-install-suse.md)
- [Ubuntu 무인된 설치 스크립트](sample-unattended-install-ubuntu.md)

## <a id="offline"></a>오프 라인 설치

Linux 컴퓨터에 없는 경우 액세스에 사용 되는 온라인 저장소에는 [빠른 시작](#platforms), 패키지 파일을 직접 다운로드할 수 있습니다. 이러한 패키지는 Microsoft 리포지토리([https://packages.microsoft.com](https://packages.microsoft.com))에 있습니다.

> [!TIP]
> 빠른 시작의 단계와 성공적으로 설치를 다운로드 하거나 아래 패키지를 수동으로 설치할 필요가 없습니다. 이 섹션은 오프 라인 시나리오에 대해서만 합니다.

1. **사용 중인 플랫폼에 대 한 데이터베이스 엔진 패키지 다운로드**합니다. 패키지 세부 정보 구역에서 패키지 다운로드 링크를 찾습니다는 [릴리스 정보](sql-server-linux-release-notes.md)합니다.

1. **Linux 컴퓨터에 다운로드 한 패키지를 이동**합니다. Linux 컴퓨터에 패키지를 이동 하는 한 가지 방법은와 다른 컴퓨터를 사용 하 여 패키지를 다운로드 하도록 하는 경우는 **scp** 명령입니다.

1. **데이터베이스 엔진 패키지 설치**합니다. 해당 플랫폼에 따라 다음 명령 중 하나를 사용 합니다. 이 예제 패키지 파일 이름을 다운로드 한 정확한 이름으로 바꿉니다.

   | 플랫폼 | 패키지 제거 명령 |
   |-----|-----|
   | RHEL | `sudo yum localinstall mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `sudo zypper install mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `sudo dpkg -i mssql-server_versionnumber_amd64.deb` |

    > [!NOTE]
    > 와 (RHEL 및 SLES) RPM 패키지를 설치할 수도 있습니다는 `rpm -ivh` 명령을 하지만 앞의 표에서 명령을 자동으로 종속성 승인한 경우 설치할에서 사용할 수 있는 저장소입니다.

1. **누락 된 종속성 해결**: 누락 된 종속성이 시점에서 할 수 있습니다. 그렇지 않은 경우이 단계를 건너뛸 수 있습니다. Ubuntu, 해당 종속성을 포함 하는 승인 된 저장소에 액세스할 수 있는 경우 가장 쉬운 방법은 사용 하 여 `apt-get -f install` 명령입니다. 또한이 명령은 SQL Server 설치를 완료합니다. 종속성을 수동으로 조사 하는 다음 명령을 사용 합니다.

   | 플랫폼 | 종속성 목록 표시 명령 |
   |-----|-----|
   | RHEL | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `dpkg -I mssql-server_versionnumber_amd64.deb` |

   누락 된 종속성을 해결 한 후 mssql 서버 패키지를 다시 설치 하려고 합니다.

1. **SQL Server 설치를 완료**합니다. 사용 하 여 **mssql conf** SQL Server 설치를 완료 하려면:

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

## <a name="next-steps"></a>다음 단계

설치 후 다른 선택적 SQL Server 패키지를 설치할 수 있습니다.

- [SQL Server 명령줄 도구](sql-server-linux-setup-tools.md)
- [SQL Server 에이전트](sql-server-linux-setup-sql-agent.md)
- [SQL Server 전체 텍스트 검색](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services (Ubuntu)](sql-server-linux-setup-ssis.md)

데이터베이스 만들기 및 관리를 시작 하 여 SQL Server 인스턴스에 연결 합니다. 시작 하려면 빠른 시작 자습서를 참조 합니다.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
