---
title: Linux의 SQL Server에 대 한 설치 지침 | Microsoft Docs
description: 설치, 업데이트 및 Linux에서 SQL Server를 제거 합니다. 이 문서는 온라인과 오프 라인 무인 시나리오를 다룹니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/07/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.openlocfilehash: 1edc63d4dc29e05a914bbfbd891df06a4b3a7255
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63455090"
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>Linux의 SQL Server에 대 한 설치 지침

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 설치, 업데이트 및 SQL Server 2017 및 Linux에서 SQL Server 2019 미리 보기 제거에 대 한 지침을 제공 합니다.

> [!TIP]
> 이 가이드는 몇 가지 배포 시나리오를 coves입니다. 단계별 설치 지침에 대해서만 하려는 경우 빠른 시작 중 하나로 이동:
> - [RHEL 빠른 시작](quickstart-install-connect-red-hat.md)
> - [SLES 빠른 시작](quickstart-install-connect-suse.md)
> - [Ubuntu 빠른 시작](quickstart-install-connect-ubuntu.md)
> - [Docker 빠른 시작](quickstart-install-connect-docker.md)

자주 묻는 질문에 대한 답변은, [SQL Server on Linux FAQ](../linux/sql-server-linux-faq.md)를 참조하세요.

## <a id="supportedplatforms"></a> 지원 되는 플랫폼

SQL Server 2017은 Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server SLES () 및 Ubuntu에서 지원 됩니다. Linux에서 Docker에 대 한 Windows/Mac. Docker 엔진에서 실행할 수 있는 Docker 이미지로 에서도 지원 됩니다.

| 플랫폼 | 지원 되는 버전 | 가져오기
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3, 7.4, 7.5, 7.6 | [RHEL 7.6 가져오기](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2 | [SLES v12 SP2 받기](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [Ubuntu 16.04를 가져오기](https://www.ubuntu.com/download/server)
| **Docker 엔진** | 1.8+ | [Docker 가져오기](https://www.docker.com/products/overview)

Microsoft 배포와 OpenShift 및 Kubernetes를 사용 하 여 SQL Server 컨테이너 관리를 지원 합니다.

> [!NOTE]
> SQL Server는 테스트 하 고 앞에 나열 된 배포에 대 한 Linux 지원 합니다. 지원 되지 않는 운영 체제에서 SQL Server를 설치 하려는 경우 살펴보시기를 **지원 정책** 섹션을 [Microsoft SQL Server에 대 한 기술 지원 정책](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) 지원을 이해 하 영향을 줍니다.

## <a id="system"></a> 시스템 요구 사항

SQL Server 2017 Linux에 대 한 다음 시스템 요구 사항에 있습니다.

|||
|-----|-----|
| **메모리** | 2GB |
| **파일 시스템** | **XFS** 나 **EXT4** (같은 다른 파일 시스템을 **BTRFS**, 지원 되지 않습니다) |
| **디스크 공간** | 6GB |
| **프로세서 속도** | 2ghz |
| **프로세서 코어** | 2 코어 |
| **프로세서 유형** | x64 호환만 |

사용 하는 경우 **네트워크 파일 시스템 (NFS)** 프로덕션 환경에서 원격 공유 다음 지원 요구 사항을 note 합니다.

- 사용 하 여 NFS 버전 **4.2 이상**합니다. 이전 버전의 NFS fallocate 및 스파스 파일 만들기, 최신 파일 시스템에 공통적으로 적용 등 필수 기능을 지원 하지 않습니다.
- 만 찾습니다 합니다 **/var/opt/mssql** NFS 탑재 디렉터리입니다. SQL Server 시스템 이진 파일을 같은 다른 파일을 사용할 수 없습니다.
- 된 NFS 클라이언트 원격 공유를 탑재 하는 경우 'nolock' 옵션을 사용 하는 것을 확인 합니다.

## <a id="repositories"></a> 소스 리포지토리 구성

를 설치 하거나 SQL Server를 업그레이드 하는 경우에 구성 된 Microsoft 리포지토리에서 최신 버전을의 SQL Server를 가져옵니다. SQL Server 2017 누적 업데이트를 사용 하 여 퀵 스타트 **CU** 리포지토리. 하지만 대신 구성할 수 있습니다 합니다 **GDR** 리포지토리 또는 **미리 보기 (vNext)** 리포지토리. 리포지토리 및 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [Linux의 SQL Server에 대 한 리포지토리를 구성](sql-server-linux-change-repo.md)합니다.

> [!IMPORTANT]
> CTP 또는 SQL Server 2017의 RC 버전을 이전에 설치한 경우 미리 보기 저장소를 제거 하 고는 GA (일반 공급) 하나를 등록 합니다. 자세한 내용은 [Linux의 SQL Server에 대 한 리포지토리를 구성](sql-server-linux-change-repo.md)합니다.

## <a id="platforms"></a> SQL Server 2017 설치

명령줄에서 Linux의 SQL Server 2017을 설치할 수 있습니다. 단계별 지침은 다음 빠른 시작 중 하나를 참조 하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-docker.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

## <a id="sqlvnext"></a> SQL Server 2019 미리 보기 설치

이전 섹션에는 동일한 빠른 시작 링크를 사용 하 여 Linux에서 SQL Server 2019 미리 보기를 설치할 수 있습니다. 그러나 등록 해야 합니다는 **미리 보기 (vNext)** 리포지토리 대신 합니다 **CU** 리포지토리. 빠른 시작이 작업을 수행 하는 방법에 지침을 제공 합니다.  

를 설치한 후 최적의 성능에 대 한 추가 구성을 변경 하는 것이 좋습니다. 자세한 내용은 [성능 모범 사례 및 Linux의 SQL Server에 대 한 구성 지침](sql-server-linux-performance-best-practices.md)합니다.

## <a id="upgrade"></a> SQL Server 업데이트

업데이트 하는 **mssql server** 패키지 최신 릴리스를 플랫폼에 따라 다음 명령 중 하나를 사용 합니다.

| 플랫폼 | 패키지 업데이트 명령 |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

이 명령은 최신 패키지를 다운로드 하 고 아래에 있는 이진 파일을 대체 `/opt/mssql/`합니다. 사용자 데이터베이스를 생성 하 고 시스템 데이터베이스는이 작업이 영향을 받지 않습니다.

> [!TIP]
> 경우 있습니다 첫 번째 [구성 된 리포지토리에 변경](sql-server-linux-change-repo.md), 있기 합니다 **업데이트** SQL Server의 버전을 업그레이드 하는 명령입니다. 업그레이드 경로 두 저장소 간에 지원 되는 경우 대/소문자만입니다.

## <a id="rollback"></a> 롤백 SQL Server

롤백 또는 SQL Server 이전 버전으로 다운 그레이드 하려면 다음 단계를 사용 합니다.

1. 다운 그레이드 하려는 SQL Server 패키지의 버전 번호를 식별 합니다. 패키지 번호의 목록을 보려면 참조는 [릴리스](../linux/sql-server-linux-release-notes.md)합니다.

1. SQL Server의 이전 버전으로 다운 그레이드 합니다. 다음 명령에서 대체 `<version_number>` 1 단계에서 확인 된 SQL Server 버전 번호를 사용 하 여 합니다.

   | 플랫폼 | 패키지 업데이트 명령 |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> SQL Server 2017 같은 동일한 주 버전 내에서 릴리스 다운 그레이드 하 에서만 지원 됩니다.

## <a id="versioncheck"></a> 설치 된 SQL Server 버전을 확인

Linux의 SQL Server 버전을 확인 하 고 현재 버전을 확인 하려면 다음 절차를 따르십시오.

1. 아직 설치 하지 않았으면를 설치 합니다 [SQL Server 명령줄 도구](sql-server-linux-setup-tools.md)합니다.

1. 사용 하 여 **sqlcmd** SQL Server 버전 및 버전을 표시 하는 TRANSACT-SQL 명령을 실행 합니다.

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a> SQL Server 제거

제거할 합니다 **mssql server** 플랫폼에 따라 다음 명령 중 하나를 사용 하 여, linux 패키지:

| 플랫폼 | 패키지 제거 명령 |
|-----|-----|
| RHEL | `sudo yum remove mssql-server` |
| SLES | `sudo zypper remove mssql-server` |
| Ubuntu | `sudo apt-get remove mssql-server` |

패키지를 제거 하는 경우에 생성 된 데이터베이스 파일이 삭제 되지 않습니다. 데이터베이스 파일을 삭제 하려는 경우 다음 명령을 사용 합니다.

```bash
sudo rm -rf /var/opt/mssql/
```

## <a id="unattended"></a> 무인된 설치

다음과 같이 무인된 설치를 수행할 수 있습니다.

- 초기 단계에 따라 합니다 [퀵 스타트](#platforms) 리포지토리를 등록 하 여 SQL Server를 설치 합니다.
- 실행 하는 경우 `mssql-conf setup`설정 [환경 변수](sql-server-linux-configure-environment-variables.md) 사용 하는 `-n` (메시지 표시) 옵션입니다.

다음 예제에서는 사용 하 여 SQL server Developer edition을 구성 합니다 **MSSQL_PID** 환경 변수입니다. EULA도 받습니다 (**ACCEPT_EULA**) SA 사용자 암호를 설정 하 고 (**MSSQL_SA_PASSWORD**). `-n` 매개 변수는 환경 변수에서 구성 값을 가져온 위치 메시지가 표시 되지 않는 설치를 수행 합니다.

```bash
sudo MSSQL_PID=Developer ACCEPT_EULA=Y MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' /opt/mssql/bin/mssql-conf -n setup
```

또한 다른 작업을 수행 하는 스크립트를 만들 수 있습니다. 예를 들어, 다른 SQL Server 패키지를 설치할 수 있습니다.

자세한 샘플 스크립트를 다음 예제를 참조 하세요.

- [Red Hat 무인된 설치 스크립트](sample-unattended-install-redhat.md)
- [SUSE 무인된 설치 스크립트](sample-unattended-install-suse.md)
- [Ubuntu 무인된 설치 스크립트](sample-unattended-install-ubuntu.md)

## <a id="offline"></a> 오프 라인 설치

Linux 컴퓨터에 없으면 액세스에 사용 된 온라인 리포지토리에 합니다 [빠른 시작](#platforms), 패키지 파일을 직접 다운로드할 수 있습니다. 이러한 패키지는 Microsoft 리포지토리를에 위치한 [ https://packages.microsoft.com ](https://packages.microsoft.com)합니다.

> [!TIP]
> 빠른 시작의 단계를 사용 하 여 성공적으로 설치 하는 경우를 다운로드 하거나 SQL Server 패키지를 수동으로 설치할 필요가 없습니다. 이 섹션에서는 오프 라인 시나리오만입니다.

1. **플랫폼에 대 한 데이터베이스 엔진 패키지 다운로드**합니다. 패키지 세부 정보 구역에서 패키지 다운로드 링크를 찾을 합니다 [릴리스](../linux/sql-server-linux-release-notes.md)합니다.

1. **Linux 컴퓨터에 다운로드 한 패키지를 이동**합니다. Linux 컴퓨터에 패키지를 이동 하는 한 가지 방법은 된 다른 컴퓨터를 사용 하 여 패키지를 다운로드 하는 경우는 **scp** 명령입니다.

1. **데이터베이스 엔진 패키지 설치**합니다. 플랫폼에 따라 다음 명령 중 하나를 사용 합니다. 이 예제에서 패키지 파일 이름은 다운로드 한 정확한 이름으로를 바꿉니다.

   | 플랫폼 | 패키지 설치 명령 |
   |-----|-----|
   | RHEL | `sudo yum localinstall mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `sudo zypper install mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `sudo dpkg -i mssql-server_versionnumber_amd64.deb` |

    > [!NOTE]
    > (RHEL 및 SLES) RPM 패키지를 사용 하 여 설치할 수도 있습니다는 `rpm -ivh` 명령 앞의 표에서 명령을 자동으로 설치 종속성에서 사용할 수 있는 리포지토리를 승인 하는 경우.

1. **누락 된 종속성 해결**: 이 시점에서 종속성 누락 있을 수 있습니다. 그렇지 않은 경우이 단계를 건너뛸 수 있습니다. Ubuntu에서 해당 종속성을 포함 하는 승인 된 저장소에 액세스할 수 있는 경우 가장 쉬운 해결 방법은 사용 하는 것은 `apt-get -f install` 명령입니다. 또한이 명령은 SQL Server 설치를 완료합니다. 수동으로 종속성을 검사 하려면 다음 명령을 사용 합니다.

   | 플랫폼 | 종속성 목록 표시 명령 |
   |-----|-----|
   | RHEL | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `dpkg -I mssql-server_versionnumber_amd64.deb` |

   누락 된 종속성을 해결 한 후 mssql server 패키지를 다시 설치 하려고 합니다.

1. **SQL Server 설치를 완료**합니다. 사용 하 여 **mssql conf** SQL Server 설치를 완료 하려면:

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

## <a name="licensing-and-pricing"></a>라이선스 및 가격

SQL Server 라이선스는 Linux 및 Windows에 대해 동일 합니다. SQL Server에 대 한 자세한 정보에 대 한 라이선스 및 가격 정보 참조 [SQL Server 라이선스 방법](https://www.microsoft.com/sql-server/sql-server-2017-pricing)합니다.

## <a name="optional-sql-server-features"></a>선택적 SQL Server 기능

설치가 끝나면 설치 하거나 수도 선택적 SQL Server 기능을 사용 하도록 설정 합니다.

- [SQL Server 명령줄 도구](sql-server-linux-setup-tools.md)
- [SQL Server 에이전트](sql-server-linux-setup-sql-agent.md)
- [SQL Server 전체 텍스트 검색](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services](sql-server-linux-setup-ssis.md)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

> [!TIP]
> 자주 묻는 질문에 대한 답변은, [SQL Server on Linux FAQ](sql-server-linux-faq.md)를 참조하세요.
