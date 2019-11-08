---
title: SQL Server on Linux 설치 지침
titleSuffix: SQL Server
description: SQL Server on Linux를 설치, 업데이트 및 제거합니다. 이 문서에서는 온라인, 오프라인 및 무인 시나리오를 설명합니다.
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.openlocfilehash: a6cd31b1f67d37f1316db9db5d4356bbb5e31d3b
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593663"
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>SQL Server on Linux 설치 지침

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux에서 SQL Server 2017 및 SQL Server 2019를 설치, 업데이트, 제거하는 방법을 설명합니다.

기타 배포 시나리오는 다음을 참조하세요.

- [창](../database-engine/install-windows/install-sql-server.md)
- [Docker 컨테이너](../linux/sql-server-linux-configure-docker.md)
- [Kubernetes-빅 데이터 클러스터](../big-data-cluster/deploy-get-started.md)

> [!TIP]
> 이 가이드에서는 몇 가지 배포 시나리오를 설명합니다. 단계별 설치 지침만 보려면 다음 빠른 시작 중 하나로 이동합니다.
> - [RHEL 빠른 시작](quickstart-install-connect-red-hat.md)
> - [SLES 빠른 시작](quickstart-install-connect-suse.md)
> - [Ubuntu 빠른 시작](quickstart-install-connect-ubuntu.md)
> - [Docker 빠른 시작](quickstart-install-connect-docker.md)

질문과 대답은 [SQL Server on Linux FAQ](../linux/sql-server-linux-faq.md)를 참조하세요.

## <a id="supportedplatforms"></a> 지원되는 플랫폼

SQL Server는 RHEL(Red Hat Enterprise Linux), SLES(SUSE Linux Enterprise Server) 및 Ubuntu에서 지원됩니다. Linux Docker 엔진 또는 Windows/Mac용 Docker에서 실행할 수 있는 Docker 이미지로도 지원됩니다.

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| 플랫폼 | 지원되는 버전 | 가져오기
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3, 7.4, 7.5, 7.6 | [RHEL 7.6 다운로드](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2 | [SLES v12 SP2 다운로드](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [Ubuntu 16.04 다운로드](http://releases.ubuntu.com/xenial/)
| **Docker 엔진** | 1.8 이상 | [Docker 다운로드](https://www.docker.com/get-started)

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| 플랫폼 | 지원되는 버전 | 가져오기
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3, 7.4, 7.5, 7.6 | [RHEL 7.6 다운로드](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2, SP3, SP4 | [SLES v12 가져오기](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [Ubuntu 16.04 다운로드](http://releases.ubuntu.com/xenial/)
| **Docker 엔진** | 1.8 이상 | [Docker 다운로드](https://www.docker.com/get-started)

::: moniker-end

Microsoft는 OpenShift와 Kubernetes를 사용하여 SQL Server 컨테이너의 배포 및 관리도 지원합니다.

> [!NOTE]
> SQL Server는 앞에 나열된 배포에 대해 Linux에서 테스트되었으며 지원됩니다. 지원되지 않는 운영 체제에서 SQL Server를 설치하려는 경우 [Microsoft SQL Server 기술 지원 정책](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)의 **지원 정책** 섹션을 검토하여 지원 관련 영향을 파악하세요.

## <a id="system"></a> 시스템 요구 사항

SQL Server에 대한 Linux의 시스템 요구 사항은 다음과 같습니다.

|||
|-----|-----|
| **메모리** | 2GB |
| **파일 시스템** | **XFS** 또는 **EXT4**(**BTRFS** 등의 다른 파일 시스템은 지원되지 않음) |
| **디스크 공간** | 6GB |
| **프로세서 속도** | 2GHz |
| **프로세서 코어** | 코어 2개 |
| **프로세서 유형** | x64 호환 전용 |

프로덕션에서 **NFS(네트워크 파일 시스템)** 원격 공유를 사용하는 경우 다음과 같은 지원 요구 사항을 확인합니다.

- NFS 버전 **4.2 이상**을 사용합니다. 이전 버전의 NFS는 최신 파일 시스템에서 일반적으로 필요한 기능(예: fallocate, 스파스 파일 만들기)을 지원하지 않습니다.
- NFS 탑재에 **/var/opt/mssql** 디렉터리만 배치합니다. SQL Server 시스템 이진 파일 등의 다른 파일은 지원되지 않습니다.
- NFS 클라이언트가 원격 공유를 탑재할 때 ‘nolock’ 옵션을 사용하는지 확인합니다.

## <a id="repositories"></a> 원본 리포지토리 구성

SQL Server를 설치하거나 업그레이드하는 경우 구성된 Microsoft 리포지토리에서 최신 버전의 SQL Server를 다운로드합니다. 이 빠른 시작에서는 SQL Server용 누적 업데이트 **CU** 리포지토리를 사용합니다. 그러나 **GDR** 리포지토리를 대신 구성할 수 있습니다. 리포지토리 및 구성 방법에 대한 자세한 내용은 [SQL Server on Linux용 리포지토리 구성](sql-server-linux-change-repo.md)을 참조하세요.

## <a id="platforms"></a> SQL Server 설치

명령줄을 통해 Linux에 SQL Server 2017 또는 SQL Server 2019을 설치할 수 있습니다. 단계별 지침은 다음 빠른 시작 중 하나를 참조하세요.

| 플랫폼 | 설치 빠른 시작 |
|---|---|
| RHEL(Red Hat Enterprise Linux) | [2017](quickstart-install-connect-red-hat.md?view=sql-server-2017) \| [2019](quickstart-install-connect-red-hat.md?view=sql-server-linux-ver15) |
| SLES(SUSE Linux Enterprise Server) | [2017](quickstart-install-connect-suse.md?view=sql-server-2017) \| [2019](quickstart-install-connect-suse.md?view=sql-server-linux-ver15) |
| Ubuntu | [2017](quickstart-install-connect-ubuntu.md?view=sql-server-2017) \| [2019](quickstart-install-connect-ubuntu.md?view=sql-server-linux-ver15) |
| Docker | [2017](quickstart-install-connect-docker.md?view=sql-server-2017) \| [2019](quickstart-install-connect-docker.md?view=sql-server-linux-ver15) |

Azure 가상 머신에서도 SQL Server on Linux를 실행할 수 있습니다. 자세한 내용은 [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)을 참조하세요.

설치 후에 성능을 최적화하기 위해 몇 가지 구성을 추가로 변경하는 것이 좋습니다. 자세한 내용은 [SQL Server on Linux의 성능 모범 사례 및 구성 지침](sql-server-linux-performance-best-practices.md)을 참조하세요.

## <a id="upgrade"></a> SQL Server 설치 또는 업그레이드

**mssql-server** 패키지를 최신 릴리스로 업데이트하려면 해당 플랫폼에 따라 다음 명령 중 하나를 사용합니다.

| 플랫폼 | 패키지 업데이트 명령 |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

이 명령은 최신 패키지를 다운로드하고 `/opt/mssql/` 아래에 있는 이진 파일을 바꿉니다. 사용자가 생성한 데이터베이스와 시스템 데이터베이스는 이 작업의 영향을 받지 않습니다.

SQL Server를 업그레이드하려면 먼저 [구성된 리포지토리를 원하는 SQL Server 버전으로 변경](sql-server-linux-change-repo.md)합니다. 그런 다음 동일한 **업데이트** 명령을 사용하여 SQL Server 버전을 업그레이드합니다. 이 작업은 두 리포지토리 간에 업그레이드 경로가 지원되는 경우에만 가능합니다.

## <a id="rollback"></a> SQL Server 롤백

SQL Server를 이전 릴리스로 롤백 또는 다운그레이드하려면 다음 단계를 사용합니다.

1. 다운그레이드하려는 SQL Server 패키지의 버전 번호를 확인합니다. 패키지 번호 목록은 [릴리스 정보](../linux/sql-server-linux-release-notes.md)를 참조하세요.

1. 이전 버전의 SQL Server로 다운그레이드 다음 명령에서 `<version_number>`를 1단계에서 확인한 SQL Server 버전 번호로 바꿉니다.

   | 플랫폼 | 패키지 업데이트 명령 |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> SQL Server 2019과 같은 동일한 주 버전 내의 릴리스로만 다운그레이드할 수 있습니다.

## <a id="versioncheck"></a> 설치된 SQL Server 버전 확인

SQL Server on Linux의 현재 버전을 확인하려면 다음 절차를 사용합니다.

1. [SQL Server 명령줄 도구](sql-server-linux-setup-tools.md)를 아직 설치하지 않은 경우 지금 설치합니다.

1. **sqlcmd**를 사용하여 SQL Server 버전을 표시하는 Transact-SQL 명령을 실행합니다.

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a> SQL Server 제거

Linux에서 **mssql-server** 패키지를 제거하려면 해당 플랫폼에 따라 다음 명령 중 하나를 사용합니다.

| 플랫폼 | 패키지 제거 명령 |
|-----|-----|
| RHEL | `sudo yum remove mssql-server` |
| SLES | `sudo zypper remove mssql-server` |
| Ubuntu | `sudo apt-get remove mssql-server` |

패키지를 제거해도 생성된 데이터베이스 파일은 삭제되지 않습니다. 데이터베이스 파일을 삭제하려면 다음 명령을 사용합니다.

```bash
sudo rm -rf /var/opt/mssql/
```

## <a id="unattended"></a> 무인 설치

다음과 같은 방법으로 무인 설치를 수행할 수 있습니다.

- [빠른 시작](#platforms)의 초기 단계를 수행하여 리포지토리를 등록하고 SQL Server를 설치합니다.
- `mssql-conf setup`을 실행하는 경우 [환경 변수](sql-server-linux-configure-environment-variables.md)를 설정하고 `-n`(프롬프트 없음) 옵션을 사용합니다.

다음 예제에서는 **MSSQL_PID** 환경 변수를 사용하여 SQL Server Developer Edition을 구성합니다. 또한 EULA(**ACCEPT_EULA**)에 동의하고 SA 사용자 암호(**MSSQL_SA_PASSWORD**)를 설정합니다. `-n` 매개 변수는 환경 변수에서 구성 값을 끌어오는 메시지가 표시되지 않는 설치를 수행합니다.

```bash
sudo MSSQL_PID=Developer ACCEPT_EULA=Y MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' /opt/mssql/bin/mssql-conf -n setup
```

다른 작업을 수행하는 스크립트를 만들 수도 있습니다. 예를 들어 다른 SQL Server 패키지를 설치할 수 있습니다.

자세한 샘플 스크립트는 다음 예제를 참조하세요.

- [Red Hat 무인 설치 스크립트](sample-unattended-install-redhat.md)
- [SUSE 무인 설치 스크립트](sample-unattended-install-suse.md)
- [Ubuntu 무인 설치 스크립트](sample-unattended-install-ubuntu.md)

## <a id="offline"></a> 오프라인 설치

Linux 머신에 [빠른 시작](#platforms)에서 사용된 온라인 리포지토리에 대한 액세스 권한이 없는 경우 패키지 파일을 직접 다운로드할 수 있습니다. 이 패키지는 Microsoft 리포지토리 [https://packages.microsoft.com](https://packages.microsoft.com)에 있습니다.

> [!TIP]
> 빠른 시작의 단계를 사용하여 설치에 성공한 경우에는 SQL Server 패키지를 다운로드하거나 수동으로 설치할 필요가 없습니다. 이 섹션은 오프라인 시나리오에만 해당됩니다.

1. **해당 플랫폼용 데이터베이스 엔진 패키지를 다운로드합니다**. [릴리스 정보](../linux/sql-server-linux-release-notes.md)의 패키지 정보 섹션에서 패키지 다운로드 링크를 찾습니다.

1. **다운로드한 패키지를 Linux 머신으로 이동**합니다. 다른 머신을 사용하여 패키지를 다운로드한 경우 패키지를 Linux 머신으로 이동하는 한 가지 방법은 **scp** 명령을 사용하는 것입니다.

1. **데이터베이스 엔진 패키지를 설치합니다**. 해당 플랫폼에 따라 다음 명령 중 하나를 사용합니다. 이 예제의 패키지 파일 이름을 다운로드한 정확한 이름으로 바꿉니다.

   | 플랫폼 | 패키지 설치 명령 |
   |-----|-----|
   | RHEL | `sudo yum localinstall mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `sudo zypper install mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `sudo dpkg -i mssql-server_versionnumber_amd64.deb` |

    > [!NOTE]
    > `rpm -ivh` 명령을 사용하여 RPM 패키지(RHEL 및 SLES)를 설치할 수도 있지만, 위 표의 명령은 승인된 리포지토리에서 사용할 수 있는 경우 자동으로 종속성을 설치합니다.

1. **누락된 종속성을 해결합니다**. 이때 누락된 종속성이 있을 수 있습니다. 누락된 종속성이 없으면 이 단계를 건너뛰어도 됩니다. Ubuntu에서 해당 종속성을 포함하는 승인된 리포지토리에 액세스할 수 있는 경우 가장 간편한 해결 방법은 `apt-get -f install` 명령을 사용하는 것입니다. 이 명령은 SQL Server 설치도 완료합니다. 종속성을 수동으로 검사하려면 다음 명령을 사용합니다.

   | 플랫폼 | 종속성 나열 명령 |
   |-----|-----|
   | RHEL | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `dpkg -I mssql-server_versionnumber_amd64.deb` |

   누락된 종속성을 해결한 후에 mssql-server 패키지 설치를 다시 시도합니다.

1. **SQL Server 설치를 완료합니다**. **mssql-conf**를 사용하여 SQL Server 설치를 완료합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

## <a name="licensing-and-pricing"></a>라이선스 및 가격 책정

SQL Server는 Linux와 Windows에 대해 동일하게 사용이 허가됩니다. SQL Server 라이선스 및 가격 책정에 대한 자세한 내용은 [SQL Server 라이선스 획득 방법](https://www.microsoft.com/sql-server/sql-server-2017-pricing)을 참조하세요.

## <a name="optional-sql-server-features"></a>선택적 SQL Server 기능

설치 후에 선택적 SQL Server 기능을 설치하거나 사용하도록 설정할 수도 있습니다.

- [SQL Server 명령줄 도구](sql-server-linux-setup-tools.md)
- [SQL Server 에이전트](sql-server-linux-setup-sql-agent.md)
- [SQL Server 전체 텍스트 검색](sql-server-linux-setup-full-text-search.md)
- [Machine Learning Services(R, Python)](sql-server-linux-setup-machine-learning.md)
- [SQL Server Integration Services](sql-server-linux-setup-ssis.md)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

> [!TIP]
> 질문과 대답은 [SQL Server on Linux FAQ](sql-server-linux-faq.md)를 참조하세요.
