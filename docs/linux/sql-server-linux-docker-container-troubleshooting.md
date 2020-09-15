---
title: SQL Server Docker 컨테이너 문제 해결
description: SQL Server 이미지에서 Linux Docker 컨테이너를 사용할 때 표시되는 일반적인 오류를 해결하는 데 사용할 수 있는 다양한 문제 해결 기술을 알아봅니다.
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.custom: contperfq1
ms.date: 09/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
zone_pivot_groups: cs1-command-shell
ms.openlocfilehash: 0a58ad0e4271833c7aef24333b14a61ef80a16c9
ms.sourcegitcommit: 678f513b0c4846797ba82a3f921ac95f7a5ac863
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2020
ms.locfileid: "89511584"
---
# <a name="troubleshooting-sql-server-docker-containers"></a>SQL Server Docker 컨테이너 문제 해결

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 SQL Server Docker 컨테이너 배포 및 사용 시 발생하는 일반적인 오류를 설명하고, 문제 해결에 도움이 되는 문제 해결 기술을 제공합니다.

## <a name="docker-command-errors"></a>Docker 명령 오류

`docker` 명령과 관련된 오류가 발생할 경우 docker 서비스가 실행되고 있는지 확인하고 관리자 권한으로 실행해 봅니다.

예를 들어 Linux에서 `docker` 명령을 실행할 때 다음과 같은 오류가 발생할 수 있습니다.

```output
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Linux에서 이 오류가 발생할 경우 앞에 `sudo`를 추가하여 동일한 명령을 실행해 봅니다. 이 명령이 실패하면 docker 서비스가 실행되고 있는지 확인하고, 필요한 경우 서비스를 시작합니다.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

Windows에서 PowerShell 또는 명령 프롬프트를 관리자 권한으로 시작했는지 확인합니다.

## <a name="sql-server-container-startup-errors"></a>SQL Server 컨테이너 시작 오류

SQL Server 컨테이너가 실행되지 않으면 다음 테스트를 시도합니다.

- `failed to create endpoint CONTAINER_NAME on network bridge. Error starting proxy: listen tcp 0.0.0.0:1433 bind: address already in use.` 등과 같은 오류가 발생하면 컨테이너 포트 1433을 이미 사용 중인 포트에 매핑하려고 시도하는 것입니다. 이 문제는 호스트 머신에서 SQL Server를 로컬로 실행하는 경우에 발생할 수 있습니다. 두 개의 SQL Server 컨테이너를 시작하고 둘 다 동일한 호스트 포트에 매핑하려고 하는 경우에도 발생할 수 있습니다. 이 문제가 발생할 경우 `-p` 매개 변수를 사용하여 컨테이너 포트 1433을 다른 호스트 포트에 매핑합니다. 예를 들면 다음과 같습니다. 

    <!--SQL Server 2017 on Linux -->
    ::: moniker range="= sql-server-linux-2017 || = sql-server-2017"
    
    ::: zone pivot="cs1-bash"
    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
    ```
    ::: zone-end
    
    ::: zone pivot="cs1-powershell"
    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
    ```
    ::: zone-end
    
    ::: zone pivot="cs1-cmd"
    ```cmd
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
    ```
    ::: zone-end
    
    ::: moniker-end
    
    <!--SQL Server 2019 on Linux-->
    ::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"
    
    ::: zone pivot="cs1-bash"
    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-latest`.
    ```
    ::: zone-end
    
    ::: zone pivot="cs1-powershell"
    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-latest`.
    ```
    ::: zone-end
    
    ::: zone pivot="cs1-cmd"
    ```cmd
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-latest`.
    ```
    ::: zone-end
    
    ::: moniker-end

- 컨테이너를 시작하려고 할 때 `Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: dial unix /var/run/docker.sock: connect: permission denied` 등과 같은 오류가 발생하는 경우 Ubuntu의 Docker 그룹에 사용자를 추가합니다. 이 변경 내용은 새 세션에 영향을 주기 때문에 로그아웃한 후 다시 로그인합니다. 

   ```bash
    usermod -aG docker $USER
   ```

- 컨테이너의 오류 메시지가 있는지 확인합니다.

   ```bash
   docker logs e69e056c702d
   ```

- 빠른 시작 문서의 [필수 조건](quickstart-install-connect-docker.md#requirements) 섹션에 지정된 최소 메모리 및 디스크 요구 사항을 충족하는지 확인합니다.

- 컨테이너 관리 소프트웨어를 사용하는 경우 소프트웨어가 루트로 실행 중인 컨테이너 프로세스를 지원하는지 확인합니다. 컨테이너의 sqlservr.exe 프로세스가 루트로 실행됩니다.

- SQL Server Docker 컨테이너가 시작 후 즉시 종료되는 경우 Docker 로그를 확인합니다. `docker run` 명령을 사용하여 Windows에서 PowerShell을 사용하는 경우 작은따옴표 대신 큰따옴표를 사용합니다. PowerShell Core를 사용하는 경우 작은따옴표를 사용합니다.

- [SQL Server 설치 및 오류 로그](#errorlogs)를 검토합니다.

## <a name="enable-dump-captures"></a>덤프 캡처 사용

컨테이너 내부에서 SQL Server 프로세스가 실패하는 경우 **SYS_PTRACE**를 사용하도록 설정하여 새 컨테이너를 만들어야 합니다. 그러면 예외 발생 시 덤프 파일을 만드는 데 필요한 Linux 프로세스 추적 기능이 추가됩니다. 덤프 파일은 고객 지원팀이 문제를 해결하는 데 사용할 수 있습니다. 다음 docker run 명령은 이 기능을 사용하도록 설정합니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -e 'MSSQL_PID=Developer' --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -e 'MSSQL_PID=Developer' --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

## <a name="sql-server-connection-failures"></a>SQL Server 연결 실패

컨테이너에서 실행되는 SQL Server 인스턴스에 연결할 수 없는 경우 다음 테스트를 시도합니다.

- `docker ps -a` 출력의 **STATUS** 열을 확인하여 SQL Server 컨테이너가 실행되고 있는지 확인합니다. 컨테이너가 실행되고 있지 않으면 `docker start <Container ID>`를 사용하여 시작합니다.

- 기본값이 아닌 호스트 포트(1433이 아님)에 매핑한 경우 연결 문자열에 포트를 지정해야 합니다. `docker ps -a` 출력의 **PORTS** 열에서 포트 매핑을 확인할 수 있습니다. 예를 들어 다음 명령은 sqlcmd를 포트 1401에서 수신 대기 중인 컨테이너에 연결합니다.

    ::: zone pivot="cs1-bash"
    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```
    ::: zone-end

    ::: zone pivot="cs1-powershell"
    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```
    ::: zone-end

    ::: zone pivot="cs1-cmd"
    ```cmd
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```
    ::: zone-end

- 기존의 매핑된 데이터 볼륨 또는 데이터 볼륨 컨테이너와 함께 `docker run`을 사용한 경우 SQL Server는 `SA_PASSWORD` 값을 무시합니다. 대신, 데이터 볼륨 또는 데이터 볼륨 컨테이너의 SQL Server 데이터에서 미리 구성된 SA 사용자 암호를 사용합니다. 연결 중인 데이터와 연결된 SA 암호를 사용하고 있는지 확인합니다.

- [SQL Server 설치 및 오류 로그](#errorlogs)를 검토합니다.

## <a name="sql-server-availability-groups"></a>SQL Server 가용성 그룹

SQL Server 가용성 그룹과 함께 Docker를 사용하는 경우 두 가지 추가 요구 사항이 있습니다.

- 복제본 통신에 사용되는 포트를 매핑합니다(기본값 5022). 예를 들어 `docker run` 명령의 일부로 `-p 5022:5022`를 지정합니다.

- `docker run` 명령의 `-h YOURHOSTNAME` 매개 변수를 사용하여 컨테이너 호스트 이름을 명시적으로 설정합니다. 이 호스트 이름은 가용성 그룹을 구성할 때 사용됩니다. `-h`를 사용하여 지정하지 않으면 기본적으로 **컨테이너 ID**로 설정됩니다.

## <a name="sql-server-setup-and-error-logs"></a><a id="errorlogs"></a> SQL Server 설치 및 오류 로그

**/var/opt/mssql/log**에서 SQL Server 설치 및 오류 로그를 확인할 수 있습니다. 컨테이너가 실행되고 있지 않으면 먼저 컨테이너를 시작합니다. 그런 다음, 대화형 명령 프롬프트를 사용하여 로그를 검사합니다. `docker ps` 명령을 실행하여 컨테이너 ID를 가져올 수 있습니다.

```bash
docker start <ContainerID>
docker exec -it <ContainerID> "bash"
```

컨테이너 내부 bash 세션에서 다음 명령을 실행합니다.

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> 컨테이너를 만들 때 호스트 디렉터리를 **/var/opt/mssql**에 탑재한 경우, 대신 호스트의 매핑된 경로에 있는 **log** 하위 디렉터리에서 확인할 수 있습니다.

## <a name="execute-commands-in-a-container"></a>컨테이너에서 명령 실행

실행 중인 컨테이너가 있는 경우 호스트 터미널을 통해 컨테이너 내에서 명령을 실행할 수 있습니다.

컨테이너 ID를 가져오려면 다음 명령을 실행합니다.

```bash
docker ps -a
```

컨테이너에서 bash 터미널을 시작하려면 다음 명령을 실행합니다.

```bash
docker exec -it <Container ID> /bin/bash
```

이제 컨테이너 내부 터미널에서 실행하는 것처럼 명령을 실행할 수 있습니다. 완료되면 `exit`을 입력합니다. 대화형 명령 세션이 종료되지만 컨테이너는 계속 실행됩니다.

## <a name="next-steps"></a>다음 단계

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

- [빠른 시작](quickstart-install-connect-docker.md?view=sql-server-2017)을 진행하여 Docker에서 SQL Server 2017 컨테이너 이미지로 시작합니다.

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

- [빠른 시작](quickstart-install-connect-docker.md?view=sql-server-ver15)을 진행하여 Docker에서 SQL Server 2019 컨테이너 이미지로 시작합니다.

::: moniker-end

- [SQL Server Docker 컨테이너 배포 및 연결](sql-server-linux-docker-container-deployment.md)

- [Docker 컨테이너에 대한 추가 구성 및 사용자 지정 참조](sql-server-linux-docker-container-configure.md)

- [SQL Server Docker 컨테이너 보안 유지](sql-server-linux-docker-container-security.md)