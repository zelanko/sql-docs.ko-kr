---
title: 'Docker: SQL Server on Linux의 컨테이너 설치'
description: 이 빠른 시작에서는 Docker를 사용하여 SQL Server 2017 및 2019 컨테이너 이미지를 실행하는 방법을 보여 줍니다. 그런 다음, sqlcmd 사용하여 데이터베이스를 만들고 쿼리합니다.
ms.custom: seo-lt-2019
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 03/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.prod_service: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
zone_pivot_groups: cs1-command-shell
ms.openlocfilehash: afc420ffe62f31c5793f00f3acea12dedac7f509
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79198400"
---
# <a name="quickstart-run-sql-server-container-images-with-docker"></a>빠른 시작: Docker에서 SQL Server 컨테이너 이미지 실행

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

이 빠른 시작에서 Docker를 사용하여 SQL Server 2017 컨테이너 이미지인 [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server)를 끌어와 실행합니다. 그런 다음, **sqlcmd**로 연결하여 첫 번째 데이터베이스를 만들고 쿼리를 실행합니다.

> [!TIP]
> SQL Server 2019 컨테이너를 실행하려면 [이 문서의 SQL Server 2019 버전](quickstart-install-connect-docker.md?view=sql-server-linux-ver15)을 참조하세요.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

> [!NOTE]
> SQL Server 2019 CU3부터 Ubuntu 18.04가 지원됩니다.

이 빠른 시작에서 Docker를 사용하여 SQL Server 2019 컨테이너 이미지인 [mssql-server](https://hub.docker.com/r/microsoft/mssql-server)를 끌어와 실행합니다. 그런 다음, **sqlcmd**로 연결하여 첫 번째 데이터베이스를 만들고 쿼리를 실행합니다.

> [!TIP]
> 이 빠른 시작에서는 SQL Server 2019 컨테이너를 만듭니다. SQL Server 2017 컨테이너를 만들려는 경우 [이 문서의 SQL Server 2017 버전](quickstart-install-connect-docker.md?view=sql-server-linux-2017)을 참조하세요.

::: moniker-end

이 이미지는 Ubuntu 18.04 기반 Linux에서 실행되는 SQL Server로 구성되어 있습니다. Linux 또는 Mac/Windows용 Docker에서 Docker Engine 1.8+와 함께 사용할 수 있습니다. 이 빠른 시작에서는 특히 SQL Server on **Linux** 이미지 사용에 중점을 둡니다. Windows 이미지는 다루지 않지만, [mssql-server-windows-developer Docker 허브 페이지](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)에서 자세히 알아볼 수 있습니다.

## <a name="prerequisites"></a><a id="requirements"></a> 필수 조건

- 지원되는 모든 Linux 배포판 또는 Mac/Windows용 Docker에서 Docker Engine 1.8+. 자세한 내용은 [사용자 Docker 설치](https://docs.docker.com/engine/installation/)를 참조하세요.
- Docker **overlay2** 스토리지 드라이버. 대부분의 사용자에게 적용되는 기본값입니다. 이 스토리지 공급자를 사용하지 않고 변경해야 하는 경우 [overlay2 구성에 대한 docker 설명서](https://docs.docker.com/storage/storagedriver/overlayfs-driver/#configure-docker-with-the-overlay-or-overlay2-storage-driver)의 지침 및 경고를 참조하세요.
- 최소 2GB의 디스크 공간.
- 최소 2GB의 RAM.
- [Linux에서 SQL Server에 대한 시스템 요구 사항](sql-server-linux-setup.md#system)

<!--The following H2 is versioned for 2017 and 2019. Much of the content is duplicated, so
any changes to one section should be duplicated in the other-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a name="pull-and-run-the-container-image"></a><a id="pullandrun2017"></a> 컨테이너 이미지를 끌어와 실행

다음 단계를 시작하기 전에 이 문서의 맨 위에서 기본 셸(bash, PowerShell 또는 cmd)을 선택했는지 확인합니다.

1. Microsoft Container Registry에서 SQL Server 2017 Linux 컨테이너 이미지를 끌어옵니다.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   > [!TIP]
   > SQL Server 2019 컨테이너를 실행하려면 [이 문서의 SQL Server 2019 버전](quickstart-install-connect-docker.md?view=sql-server-linux-ver15#pullandrun2019)을 참조하세요.

   이전 명령은 최신 SQL Server 2017 컨테이너 이미지를 끌어옵니다. 특정 이미지를 끌어오려면 콜론 및 태그 이름(예를 들어 `mcr.microsoft.com/mssql/server:2017-GA-ubuntu`)을 추가합니다. 사용 가능한 모든 이미지를 보려면 [mssql-server Docker 허브 페이지](https://hub.docker.com/r/microsoft/mssql-server)를 참조하세요.

   ::: zone pivot="cs1-bash"
   이 문서의 bash 명령에는 `sudo`를 사용합니다. macOS에서는 `sudo`가 필요하지 않을 수도 있습니다. Linux에서 `sudo`로 Docker를 실행하지 않으려는 경우 **docker** 그룹을 구성하고 해당 그룹에 사용자를 추가할 수 있습니다. 자세한 내용은 [Linux용 설치 후 단계](https://docs.docker.com/install/linux/linux-postinstall/)를 참조하세요.
   ::: zone-end

2. Docker를 사용하여 컨테이너 이미지를 실행하려면 bash 셸(Linux/macOS) 또는 상승된 권한 PowerShell 명령 프롬프트에서 다음 명령을 사용할 수 있습니다.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" \
      -p 1433:1433 --name sql1 \
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   > [!NOTE]
   > 암호는 SQL Server 기본 암호 정책이 따라야 합니다. 그렇지 않으면 컨테이너는 SQL 서버를 설정할 수 없어 작동이 중지됩니다. 기본적으로 암호는 8자 이상이어야 하며 대문자, 소문자, 십진수 숫자 및 기호의 네 가지 집합 중 세 집합의 문자를 포함해야 합니다. [docker 로그](https://docs.docker.com/engine/reference/commandline/logs/) 명령을 실행하여 오류 로그를 검사할 수 있습니다.

   > [!NOTE]
   > 기본적으로 이렇게 하면 개발자 버전의 SQL Server 2017를 사용하여 컨테이너를 만듭니다. 컨테이너에서 프로덕션 버전을 실행하는 프로세스는 약간 다릅니다. 자세한 내용은 [프로덕션 컨테이너 이미지 실행](sql-server-linux-configure-docker.md#production)을 참조하세요.

   다음 표에서는 이전 `docker run` 보기의 매개 변수에 대해 설명합니다.

   | 매개 변수 | Description |
   |-----|-----|
   | **-e "ACCEPT_EULA=Y"** |  [최종 사용자 사용권 계약](https://go.microsoft.com/fwlink/?LinkId=746388) 수락을 확인하기 위해 **ACCEPT_EULA** 변수를 어떤 값에 설정합니다. SQL Server 이미지에 대한 설정을 해야 합니다. |
   | **-e "SA_PASSWORD=\<YourStrong@Passw0rd\>"** | 8자 이상이고 [SQL Server 암호 요구 사항](../relational-databases/security/password-policy.md)을 충족하는 자신만의 강력한 암호를 지정합니다. SQL Server 이미지에 대한 설정을 해야 합니다. |
   | **-p 1433:1433** | 호스트 환경의 TCP 포트(첫 번째 값)를 컨테이너의 TCP 포트(두 번째 값)로 매핑합니다. 이 예제에서 SQL Server는 컨테이너의 TCP 1433에서 수신 대기하고 호스트의 포트 1433에 공개됩니다. |
   | **--name sql1** | 컨테이너에 대해 임의로 생성된 이름보다는 사용자 지정 이름을 지정합니다. 둘 이상의 컨테이너를 실행하는 경우 이 동일한 이름을 다시 사용할 수 없습니다. |
   | **-d mcr.microsoft.com/mssql/server:2017-latest** | SQL Server 2017 Linux 컨테이너 이미지입니다. |

3. Docker 컨테이너를 보려면 `docker ps` 명령을 사용합니다.


   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker ps -a
   ```
   ::: zone-end

   다음 스크린샷과 비슷한 내용이 출력됩니다.

   ![Docker ps 명령 출력](./media/sql-server-linux-setup-docker/docker-ps-command.png)

4. **상태** 열이 **Up**의 상태를 표시하는 경우, SQL Server는 컨테이너에서 실행되며 **포트** 열의 지정된 포트에서 수신 대기합니다. SQL Server 컨테이너의 **상태** 열이 **Exited**를 표시하는 경우, [구성 가이드의 문제 해결 섹션](sql-server-linux-configure-docker.md#troubleshooting)을 참조하세요.

`-h`(호스트 이름) 매개 변수도 유용하지만 간단한 설명을 위해 이 자습서에서 사용되지 않습니다. 이렇게 하면 컨테이너의 내부 이름이 사용자 지정 값으로 변경됩니다. 이 값은 다음 Transact SQL 쿼리에서 반환되는 이름입니다.

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

`-h` 및 `--name`을 같은 값에 설정하는 것은 대상 컨테이너를 쉽게 식별하는 데 유용한 좋은 방법입니다.

::: moniker-end
<!--End of 2017 "Pull and run" section-->

<!--This is the 2019 version of the "Pull and run" section-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="pull-and-run-the-container-image"></a><a id="pullandrun2019"></a> 컨테이너 이미지를 끌어와 실행

다음 단계를 시작하기 전에 이 문서의 맨 위에서 기본 셸(bash, PowerShell 또는 cmd)을 선택했는지 확인합니다.

1. Docker Hub에서 SQL Server 2019 Linux 컨테이너 이미지를 끌어옵니다.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker pull mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04
   ```
   ::: zone-end

   > [!TIP]
   > 이 빠른 시작에서는 SQL Server 2019 Docker 이미지를 사용합니다. SQL Server 2017 이미지를 실행하려면 [이 문서의 SQL Server 2017 버전](quickstart-install-connect-docker.md?view=sql-server-linux-2017#pullandrun2017)을 참조하세요.

   이전 명령은 Ubuntu를 기반으로 하는 SQL Server 2019 컨테이너 이미지를 끌어옵니다. RedHat을 기반으로 하는 컨테이너 이미지를 대신 사용하려면 [RHEL 기반 컨테이너 이미지 실행](sql-server-linux-configure-docker.md#rhel)을 참조하세요. 사용 가능한 모든 이미지를 보려면 [mssql-server-linux Docker 허브 페이지](https://hub.docker.com/_/microsoft-mssql-server)를 참조하세요.

   ::: zone pivot="cs1-bash"
   이 문서의 bash 명령에는 `sudo`를 사용합니다. macOS에서는 `sudo`가 필요하지 않을 수도 있습니다. Linux에서 `sudo`로 Docker를 실행하지 않으려는 경우 **docker** 그룹을 구성하고 해당 그룹에 사용자를 추가할 수 있습니다. 자세한 내용은 [Linux용 설치 후 단계](https://docs.docker.com/install/linux/linux-postinstall/)를 참조하세요.
   ::: zone-end

2. Docker를 사용하여 컨테이너 이미지를 실행하려면 bash 셸(Linux/macOS) 또는 상승된 권한 PowerShell 명령 프롬프트에서 다음 명령을 사용할 수 있습니다.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" \
      -p 1433:1433 --name sql1 \
      -d mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04
   ```
   ::: zone-end

   > [!NOTE]
   > 암호는 SQL Server 기본 암호 정책이 따라야 합니다. 그렇지 않으면 컨테이너는 SQL 서버를 설정할 수 없어 작동이 중지됩니다. 기본적으로 암호는 8자 이상이어야 하며 대문자, 소문자, 십진수 숫자 및 기호의 네 가지 집합 중 세 집합의 문자를 포함해야 합니다. [docker 로그](https://docs.docker.com/engine/reference/commandline/logs/) 명령을 실행하여 오류 로그를 검사할 수 있습니다.

   > [!NOTE]
   > 기본적으로 이렇게 하면 개발자 버전의 SQL Server 2019를 사용하여 컨테이너를 만듭니다.

   다음 표에서는 이전 `docker run` 보기의 매개 변수에 대해 설명합니다.

   | 매개 변수 | Description |
   |-----|-----|
   | **-e "ACCEPT_EULA=Y"** |  [최종 사용자 사용권 계약](https://go.microsoft.com/fwlink/?LinkId=746388) 수락을 확인하기 위해 **ACCEPT_EULA** 변수를 어떤 값에 설정합니다. SQL Server 이미지에 대한 설정을 해야 합니다. |
   | **-e "SA_PASSWORD=\<YourStrong@Passw0rd\>"** | 8자 이상이고 [SQL Server 암호 요구 사항](../relational-databases/security/password-policy.md)을 충족하는 자신만의 강력한 암호를 지정합니다. SQL Server 이미지에 대한 설정을 해야 합니다. |
   | **-p 1433:1433** | 호스트 환경의 TCP 포트(첫 번째 값)를 컨테이너의 TCP 포트(두 번째 값)로 매핑합니다. 이 예제에서 SQL Server는 컨테이너의 TCP 1433에서 수신 대기하고 호스트의 포트 1433에 공개됩니다. |
   | **--name sql1** | 컨테이너에 대해 임의로 생성된 이름보다는 사용자 지정 이름을 지정합니다. 둘 이상의 컨테이너를 실행하는 경우 이 동일한 이름을 다시 사용할 수 없습니다. |
   | **mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04** | SQL Server 2019 Ubuntu Linux 컨테이너 이미지입니다. |

3. Docker 컨테이너를 보려면 `docker ps` 명령을 사용합니다.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker ps -a
   ```
   ::: zone-end

   다음 스크린샷과 비슷한 내용이 출력됩니다.

   ![Docker ps 명령 출력](./media/sql-server-linux-setup-docker/docker-ps-command.png)

4. **상태** 열이 **Up**의 상태를 표시하는 경우, SQL Server는 컨테이너에서 실행되며 **포트** 열의 지정된 포트에서 수신 대기합니다. SQL Server 컨테이너의 **상태** 열이 **Exited**를 표시하는 경우, [구성 가이드의 문제 해결 섹션](sql-server-linux-configure-docker.md#troubleshooting)을 참조하세요.

`-h`(호스트 이름) 매개 변수도 유용하지만 간단한 설명을 위해 이 자습서에서 사용되지 않습니다. 이렇게 하면 컨테이너의 내부 이름이 사용자 지정 값으로 변경됩니다. 이 값은 다음 Transact SQL 쿼리에서 반환되는 이름입니다.

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

`-h` 및 `--name`을 같은 값에 설정하는 것은 대상 컨테이너를 쉽게 식별하는 데 유용한 좋은 방법입니다.

::: moniker-end
<!--End of 2019 "Pull and run" section-->

## <a name="change-the-sa-password"></a><a id="sapassword"></a> SA 암호 변경

<!-- This section was pasted in from includes/sql-server-linux-change-docker-password.md, to better support zone pivots. 2019/02/11 -->

**SA** 계정은 설치 중에 생성되는 SQL Server 인스턴스의 시스템 관리자입니다. SQL Server 컨테이너를 만든 후 컨테이너에서 `echo $SA_PASSWORD`를 실행하여 지정한 `SA_PASSWORD` 환경 변수를 검색할 수 있습니다. 보안을 위해 SA 암호를 변경합니다.

1. SA 사용자에게 사용할 강력한 암호를 선택합니다.

1. `docker exec`를 사용하여 **sqlcmd**를 실행하고 Transact-SQL을 사용하여 암호를 변경합니다. 다음 예제에서는 이전 암호 `<YourStrong!Passw0rd>`와 새 암호 `<YourNewStrong!Passw0rd>`를 사용자 고유의 암호 값으로 바꿉니다.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P "<YourStrong@Passw0rd>" \
      -Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong@Passw0rd>"'
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong@Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong@Passw0rd>'"
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong!Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong@Passw0rd>'"
   ```
   ::: zone-end

## <a name="connect-to-sql-server"></a>SQL Server에 연결

다음 단계에서는 SQL Server에 연결하기 위해 컨테이너 내에서 SQL Server 명령줄 도구 **sqlcmd**를 사용합니다.

1. `docker exec -it` 명령을 사용하여 실행 중인 컨테이너 내에서 대화형 bash 셸을 시작합니다. 다음 예에서 `sql1`은 컨테이너를 만들 때 `--name` 매개 변수가 지정한 이름입니다.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker exec -it sql1 "bash"
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker exec -it sql1 "bash"
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker exec -it sql1 "bash"
   ```
   ::: zone-end

2. 컨테이너 내부로 들어가면 sqlcmd를 사용하여 로컬로 연결합니다. Sqlcmd는 기본적으로 경로에 있지 않으므로 전체 경로를 지정해야 합니다.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P "<YourNewStrong@Passw0rd>"
   ```

   > [!TIP]
   > 명령줄에서 암호를 생략하여 입력하라는 메시지가 표시되도록 할 수 있습니다.

3. 성공하면 **sqlcmd** 명령 프롬프트 `1>`이 표시됩니다.

## <a name="create-and-query-data"></a>데이터 만들기 및 쿼리

다음 섹션에서는 **sqlcmd** 및 Transact-SQL을 사용하여 새 데이터베이스를 만들고, 데이터를 추가하고, 간단한 쿼리를 실행하는 단계를 안내합니다.

### <a name="create-a-new-database"></a>새 데이터베이스 만들기

다음 단계에서는 `TestDB`라는 새 데이터베이스를 만듭니다.

1. **sqlcmd** 명령 프롬프트에서 다음 Transact-SQL 명령을 붙여넣어 테스트 데이터베이스를 만듭니다.

   ```sql
   CREATE DATABASE TestDB
   ```

2. 다음 줄에 서버에 있는 모든 데이터베이스의 이름을 반환하는 쿼리를 작성합니다.

   ```sql
   SELECT Name from sys.Databases
   ```

3. 앞의 두 명령은 즉시 실행되지 않았습니다. 앞의 명령을 실행하려면 새 줄에 `GO`를 입력해야 합니다.

   ```sql
   GO
   ```

### <a name="insert-data"></a>데이터 삽입

다음으로 새 테이블 `Inventory`를 만들고 두 개의 새 행을 삽입합니다.

1. **sqlcmd** 명령 프롬프트에서 컨텍스트를 새 `TestDB` 데이터베이스로 전환합니다.

   ```sql
   USE TestDB
   ```

2. `Inventory`라는 새 테이블을 만듭니다.

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

3. 새 테이블에 데이터를 삽입합니다.

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

4. `GO`를 입력하여 앞의 명령을 실행합니다.

   ```sql
   GO
   ```

### <a name="select-data"></a>데이터 선택

이제 쿼리를 실행하여 `Inventory` 테이블에서 데이터를 반환합니다.

1. **sqlcmd** 명령 프롬프트에서 `Inventory` 테이블에서 수량이 152보다 큰 행을 반환하는 쿼리를 입력합니다.

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

2. 다음 명령을 실행합니다.

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>sqlcmd 명령 프롬프트 종료

1. **sqlcmd** 세션을 종료하려면 `QUIT`를 입력합니다.

   ```sql
   QUIT
   ```

2. 컨테이너에서 대화형 명령 프롬프트를 종료하려면 `exit`을 입력합니다. 컨테이너는 대화형 bash 셸을 종료한 후에도 계속 실행됩니다.

## <a name="connect-from-outside-the-container"></a><a id="connectexternal"></a> 컨테이너 외부에서 연결

SQL 연결을 지원하는 모든 외부 Linux, Windows 또는 macOS 도구에서 Docker 컴퓨터에 있는 SQL Server 인스턴스에 연결할 수 있습니다.

다음 단계는 컨테이너에서 실행 중인 SQL Server에 연결하기 위해 컨테이너 외부에서 **sqlcmd**를 사용합니다. 이러한 단계는 컨테이너의 외부에 설치된 SQL Server 명령줄 도구가 이미 있다고 가정합니다. 다른 도구를 사용하는 경우에도 동일한 보안 주체가 적용되지만 연결 프로세스는 도구마다 고유합니다.

1. 컨테이너를 호스팅하는 컴퓨터에 대한 IP 주소를 찾습니다. Linux에서 **ifconfig** 또는 **ip 주소**를 사용합니다. Windows에서 **ipconfig**를 사용합니다.

1. 이 예제에서는 클라이언트 머신에 **sqlcmd** 도구를 설치합니다. 자세한 내용은 [Windows에서 sqlcmd 설치](../tools/sqlcmd-utility.md) 또는 [Linux에서 sqlcmd 설치](sql-server-linux-setup-tools.md)를 참조하세요.

1. 컨테이너의 포트 1433에 매핑된 IP 주소와 포트를 지정하는 sqlcmd를 실행합니다. 이 예제에서는 호스트 머신의 동일한 포트 1433을 사용합니다. 호스트 머신의 다른 매핑된 포트를 지정한 경우 해당 포트를 여기서 사용합니다.

   ::: zone pivot="cs1-bash"
   ```bash
   sqlcmd -S <ip_address>,1433 -U SA -P "<YourNewStrong@Passw0rd>"
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   sqlcmd -S <ip_address>,1433 -U SA -P "<YourNewStrong@Passw0rd>"
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   sqlcmd -S <ip_address>,1433 -U SA -P "<YourNewStrong@Passw0rd>"
   ```
   ::: zone-end

1. Transact-SQL 명령을 실행합니다. 완료되면 `QUIT`을 입력합니다.

SQL Server에 연결할 다른 일반적인 도구는 다음과 같습니다.

- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [Windows의 SSMS(SQL Server Management Studio)](sql-server-linux-manage-ssms.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)
- [mssql-cli(미리 보기)](https://github.com/dbcli/mssql-cli/blob/master/doc/usage_guide.md)
- [PowerShell Core](sql-server-linux-manage-powershell-core.md)

## <a name="remove-your-container"></a>컨테이너 제거

이 자습서에 사용되는 SQL Server 컨테이너를 제거하려면 다음 명령을 실행합니다.

::: zone pivot="cs1-bash"
```bash
sudo docker stop sql1
sudo docker rm sql1
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker stop sql1
docker rm sql1
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker stop sql1
docker rm sql1
```
::: zone-end

> [!WARNING]
> 컨테이너를 영구적으로 중지하고 제거하면 컨테이너의 모든 SQL Server 데이터가 삭제됩니다. 데이터를 보존해야 하는 경우 [컨테이너에서 백업 파일을 만들고 복사](tutorial-restore-backup-in-sql-server-container.md)하거나 [컨테이너 데이터 지속성 기술](sql-server-linux-configure-docker.md#persist)을 사용합니다.

## <a name="docker-demo"></a>Docker 데모

Docker에 대한 SQL Server 컨테이너 이미지를 사용하여 시도한 후에 Docker를 사용하여 개발 및 테스트를 개선하는 방법을 알아 보고자 할 수도 있습니다. 다음 비디오는 Docker를 연속 통합 및 배포 시나리오에서 사용할 수 있는 방법을 보여줍니다.

> [!VIDEO https://channel9.msdn.com/Events/Connect/2017/T152/player]

## <a name="next-steps"></a>다음 단계

데이터베이스 백업 파일을 컨테이너로 복원하는 방법에 대한 자습서는 [SQL Server 데이터베이스를 Linux Docker 컨테이너에 복원](tutorial-restore-backup-in-sql-server-container.md)을 참조하세요. 여러 컨테이너 실행, 데이터 지속성, 문제 해결 등의 다른 시나리오를 살펴보려면 [Docker에서 SQL Server 컨테이너 이미지 구성](sql-server-linux-configure-docker.md)을 참조하세요.

또한, 리소스, 피드백 및 알려진 문제에 대한 [mssql docker GitHub 리포지토리](https://github.com/Microsoft/mssql-docker)를 확인합니다.
