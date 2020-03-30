---
title: Docker의 SQL Server 구성 옵션
description: Docker에서 SQL Server 2017 및 2019 컨테이너 이미지를 사용하고 조작하는 다양한 방법을 살펴봅니다. 여기에는 데이터 유지, 파일 복사, 문제 해결 등이 포함됩니다.
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 01/08/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: e97f535dedd2b6ee25abfc886d1f08272697c549
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79287507"
---
# <a name="configure-sql-server-container-images-on-docker"></a>Docker에서 SQL Server 컨테이너 이미지 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Docker에서 [mssql-server-linux 컨테이너 이미지](https://hub.docker.com/_/microsoft-mssql-server)를 구성하고 사용하는 방법을 설명합니다. 

기타 배포 시나리오는 다음을 참조하세요.

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Kubernetes - 빅 데이터 클러스터](../big-data-cluster/deploy-get-started.md)

이 이미지는 Ubuntu 16.04 기반 Linux에서 실행 중인 SQL Server로 구성됩니다. Linux 또는 Mac/Windows용 Docker에서 Docker Engine 1.8+와 함께 사용할 수 있습니다.

> [!NOTE]
> 이 문서에서는 특히 mssql-server-linux 이미지 사용에 중점을 둡니다. Windows 이미지는 다루지 않지만, [mssql-server-windows Docker Hub 페이지](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)에서 자세히 알아볼 수 있습니다.

> [!IMPORTANT]
> 프로덕션 사용 사례를 위해 SQL Server 컨테이너를 실행하기로 선택하기 전에 [SQL Server 컨테이너에 대한 지원 정책](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)을 검토하여 지원되는 구성에서 실행 중인지 확인하세요.

6분 분량의 다음 동영상은 컨테이너에서 SQL Server를 실행하는 방법을 소개합니다.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2019-in-Containers/player?WT.mc_id=dataexposed-c9-niner]


## <a name="pull-and-run-the-container-image"></a>컨테이너 이미지를 끌어와 실행하기

SQL Server 2017 및 SQL Server 2019용 Docker 컨테이너 이미지를 끌어오고 실행하려면 다음 빠른 시작의 필수 조건 및 단계를 따르세요.

- [Docker에서 SQL Server 2017 컨테이너 이미지 실행](quickstart-install-connect-docker.md?view=sql-server-2017)
- [Docker에서 SQL Server 2019 컨테이너 이미지 실행](quickstart-install-connect-docker.md?view=sql-server-ver15)

이 구성 문서의 다음 섹션에서는 추가 사용 시나리오를 제공합니다.

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="run-rhel-based-container-images"></a><a id="rhel"></a> RHEL 기반 컨테이너 이미지 실행

SQL Server Linux 컨테이너 이미지에 대한 문서는 Ubuntu 기반 컨테이너를 가리킵니다. SQL Server 2019부터 RHEL(Red Hat Enterprise Linux)를 기반으로 하는 컨테이너를 사용할 수 있습니다. 모든 docker 명령에서 컨테이너 리포지토리를 **mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04**에서 **mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8**로 변경합니다.

예를 들어 다음 명령은 RHEL을 사용하는 SQL Server 2019 컨테이너의 누적 업데이트 1을 끌어옵니다.

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a name="run-production-container-images"></a><a id="production"></a> 프로덕션 컨테이너 이미지 실행

이전 섹션의 빠른 시작에서는 Docker Hub에서 체험용 SQL Server Developer Edition을 실행합니다. 하지만 대부분의 정보는 Enterprise, Standard 또는 Web Edition과 같은 프로덕션 컨테이너 이미지를 실행하려는 경우에도 적용됩니다. 그러나 여기서 설명하는 몇 가지 차이점이 있습니다.

- 유효한 라이선스가 있는 경우에만 프로덕션 환경에서 SQL Server를 사용할 수 있습니다. [여기](https://go.microsoft.com/fwlink/?linkid=857693)서 체험용 SQL Server Express 프로덕션 라이선스를 받을 수 있습니다. SQL Server Standard 및 Enterprise Edition 라이선스는 [Microsoft 볼륨 라이선싱](https://www.microsoft.com/licensing/default.aspx)을 통해 사용할 수 있습니다.


- 프로덕션 버전도 실행하도록 개발자 컨테이너 이미지를 구성할 수 있습니다. 프로덕션 버전을 실행하려면 다음 단계를 사용합니다.

[빠른 시작](quickstart-install-connect-docker.md)에서 요구 사항을 검토하고 절차를 실행합니다. **MSSQL_PID** 환경 변수를 사용하여 프로덕션 버전을 지정해야 합니다. 다음 예제에서는 Enterprise Edition용 최신 SQL Server 2017 컨테이너 이미지를 실행하는 방법을 보여 줍니다.

```bash
docker run --name sqlenterprise \
      -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
      -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run --name sqlenterprise `
      -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -e "MSSQL_PID=Enterprise" -p 1433:1433 `
      -d "mcr.microsoft.com/mssql/server:2017-latest"
```

> [!IMPORTANT]
> **ACCEPT_EULA** 환경 변수에 **Y** 값을 전달하고 **MSSQL_PID**에 버전 값을 전달하면 사용하려는 SQL Server 에디션 및 버전에 유효한 기존 라이선스가 있음을 나타냅니다. 또한 Docker 컨테이너 이미지에서 실행되는 SQL Server 소프트웨어 사용에 SQL Server 사용 조건이 적용되는 것에 동의하게 됩니다.

> [!NOTE]
> **MSSQL_PID**에 사용 가능한 값의 전체 목록은 [Linux에서 환경 변수를 사용하여 SQL Server 설정 구성](sql-server-linux-configure-environment-variables.md)을 참조하세요.

::: moniker-end

## <a name="connect-and-query"></a>연결 및 쿼리

컨테이너 외부나 컨테이너 내에서 컨테이너의 SQL Server를 연결하고 쿼리할 수 있습니다. 다음 섹션에서는 두 시나리오를 모두 설명합니다. 

### <a name="tools-outside-the-container"></a>컨테이너 외부 도구

SQL 연결을 지원하는 모든 외부 Linux, Windows 또는 macOS 도구에서 Docker 머신의 SQL Server 인스턴스에 연결할 수 있습니다. 몇 가지 일반적인 도구는 다음과 같습니다.

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [Windows의 SSMS(SQL Server Management Studio)](sql-server-linux-manage-ssms.md)

다음 예제에서는 **sqlcmd**를 사용하여 Docker 컨테이너에서 실행되는 SQL Server에 연결합니다. 연결 문자열의 IP 주소는 컨테이너를 실행하는 호스트 머신의 IP 주소입니다.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

기본값 **1433**이 아닌 호스트 포트를 매핑한 경우 해당 포트를 연결 문자열에 추가합니다. 예를 들어 `docker run` 명령에 `-p 1400:1433`을 지정한 경우 포트 1400을 명시적으로 지정하여 연결합니다.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>컨테이너 내부 도구

SQL Server 2017부터 [SQL Server 명령줄 도구](sql-server-linux-setup-tools.md)가 컨테이너 이미지에 포함되었습니다. 대화형 명령 프롬프트를 사용하여 이미지에 연결하는 경우 로컬에서 도구를 실행할 수 있습니다.

1. `docker exec -it` 명령을 사용하여 실행 중인 컨테이너 내에서 대화형 bash 셸을 시작합니다. 다음 예제에서 `e69e056c702d`는 컨테이너 ID입니다.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 항상 전체 컨테이너 ID를 지정할 필요는 없습니다. 고유하게 식별하는 데 충분한 문자만 지정하면 됩니다. 따라서 이 예제에서는 전체 ID가 아닌 `e6` 또는 `e69`만 사용해도 충분할 수 있습니다.

2. 컨테이너 내부로 들어가면 sqlcmd를 사용하여 로컬로 연결합니다. sqlcmd는 기본적으로 경로에 없으므로 전체 경로를 지정해야 합니다.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. sqlcmd를 마쳤으면 `exit`를 입력합니다.

4. 대화형 명령 프롬프트를 마쳤으면 `exit`를 입력합니다. 컨테이너는 대화형 bash 셸을 종료한 후에도 계속 실행됩니다.

## <a name="run-multiple-sql-server-containers"></a>여러 SQL Server 컨테이너 실행

Docker는 동일한 호스트 머신에서 여러 SQL Server 컨테이너를 실행하는 방법을 제공합니다. 동일한 호스트에 여러 개의 SQL Server 인스턴스가 필요한 시나리오에서 이 방법을 사용합니다. 각 컨테이너가 다른 포트에 공개되어야 합니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

다음 예제에서는 SQL Server 2017 컨테이너 2개를 만들고 호스트 머신의 **1401** 및 **1402** 포트에 매핑합니다.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

다음 예제에서는 SQL Server 2019 컨테이너 2개를 만들고 호스트 머신의 **1401** 및 **1402** 포트에 매핑합니다.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

이제 개별 컨테이너에서 실행되는 SQL Server 인스턴스 2개가 있습니다. 클라이언트는 Docker 호스트의 IP 주소와 컨테이너의 포트 번호를 사용하여 각 SQL Server 인스턴스에 연결할 수 있습니다.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a name="create-a-customized-container"></a><a id="customcontainer"></a> 사용자 지정 컨테이너 만들기

사용자 고유의 [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage)을 만들어 사용자 지정 SQL Server 컨테이너를 만들 수 있습니다. 자세한 내용은 [SQL Server와 노드 애플리케이션을 결합하는 데모](https://github.com/twright-msft/mssql-node-docker-demo-app)를 참조하세요. 사용자 고유의 Dockerfile을 만드는 경우 컨테이너의 수명을 제어하는 포그라운드 프로세스에 유의합니다. 프로세스가 종료되면 컨테이너도 종료됩니다. 예를 들어 스크립트를 실행하고 SQL Server를 시작하려면 SQL Server 프로세스가 맨 오른쪽 명령이어야 합니다. 다른 모든 명령은 백그라운드에서 실행됩니다. 다음 명령은 Dockerfile 내에서 이러한 동작을 보여 줍니다.

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

위 예제의 명령을 역순으로 실행하면 do-my-sql-commands.sh 스크립트가 완료될 때 컨테이너가 종료됩니다.

## <a name="persist-your-data"></a><a id="persist"></a> 데이터 유지

`docker stop` 및 `docker start`를 사용하여 컨테이너를 다시 시작하는 경우에도 SQL Server 구성 변경 내용과 데이터베이스 파일이 컨테이너에 유지됩니다. 그러나 `docker rm`을 사용하여 컨테이너를 제거하면 SQL Server 및 데이터베이스를 포함하여 컨테이너의 모든 항목이 삭제됩니다. 다음 섹션에서는 연결된 컨테이너가 삭제된 경우에도 **데이터 볼륨**을 사용하여 데이터베이스 파일을 유지하는 방법을 설명합니다.

> [!IMPORTANT]
> SQL Server와 관련해서 Docker의 데이터 지속성을 이해하는 것이 중요합니다. 이 섹션의 설명 외에도 [Docker 컨테이너의 데이터를 관리하는 방법](https://docs.docker.com/engine/tutorials/dockervolumes/)에 대한 Docker 설명서를 참조하세요.

### <a name="mount-a-host-directory-as-data-volume"></a>호스트 디렉터리를 데이터 볼륨으로 탑재

첫 번째 옵션은 호스트의 디렉터리를 컨테이너에 데이터 볼륨으로 탑재하는 것입니다. 이렇게 하려면 `docker run` 명령에 `-v <host directory>:/var/opt/mssql` 플래그를 사용합니다. 그러면 컨테이너 실행 간에 데이터를 복원할 수 있습니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

이 방법을 사용하여 Docker 외부에서 호스트의 파일을 공유하고 볼 수도 있습니다.

> [!IMPORTANT]
> **Docker on Windows**의 호스트 볼륨 매핑은 현재 전체 `/var/opt/mssql` 디렉터리 매핑을 지원하지 않습니다. 그러나 `/var/opt/mssql/data` 등의 하위 디렉터리를 호스트 머신에 매핑할 수 있습니다.

> [!IMPORTANT]
> SQL Server on Linux 이미지와 **Docker on Mac** 간의 호스트 볼륨 매핑은 현재 지원되지 않습니다. 대신, 데이터 볼륨 컨테이너를 사용합니다. 이 제한 사항은 `/var/opt/mssql` 디렉터리에만 적용됩니다. 탑재된 디렉터리에서 읽을 수는 있습니다. 예를 들어 Mac에서-v를 사용하여 호스트 디렉터리를 탑재하고 호스트에 있는 .bak 파일에서 백업을 복원할 수 있습니다.

### <a name="use-data-volume-containers"></a>데이터 볼륨 컨테이너 사용

두 번째 옵션은 데이터 볼륨 컨테이너를 사용하는 것입니다. `-v` 매개 변수를 사용하여 호스트 디렉터리 대신 볼륨 이름을 지정하면 데이터 볼륨 컨테이너를 만들 수 있습니다. 다음 예제에서는 **sqlvolume**이라는 공유 데이터 볼륨을 만듭니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

> [!NOTE]
> run 명령에서 암시적으로 데이터 볼륨을 만드는 이 방법은 이전 버전의 Docker에서 작동하지 않습니다. 이 경우에는 Docker 설명서인 [데이터 볼륨 컨테이너 만들기 및 탑재](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container)에 간략하게 설명된 명시적 단계를 사용합니다.

이 컨테이너를 중지하고 제거해도 데이터 볼륨이 계속 유지됩니다. `docker volume ls` 명령을 사용하여 데이터 볼륨을 볼 수 있습니다.

```bash
docker volume ls
```

그런 다음, 동일한 볼륨 이름을 사용하여 다른 컨테이너를 만들면 새 컨테이너는 볼륨에 포함된 것과 동일한 SQL Server 데이터를 사용합니다.

데이터 볼륨 컨테이너를 제거하려면 `docker volume rm` 명령을 사용합니다.

> [!WARNING]
> 데이터 볼륨 컨테이너를 삭제하면 컨테이너의 모든 SQL Server 데이터가 ‘영구적으로’ 삭제됩니다. 

### <a name="backup-and-restore"></a>백업 및 복원

이러한 컨테이너 방법 외에 표준 SQL Server 백업 및 복원 방법을 사용할 수도 있습니다. 백업 파일을 사용하여 데이터를 보호하거나 데이터를 다른 SQL Server 인스턴스로 이동할 수 있습니다. 자세한 내용은 [Linux에서 SQL Server 데이터베이스 백업 및 복원](sql-server-linux-backup-and-restore-database.md)을 참조하세요.

> [!WARNING]
> 백업을 만드는 경우 컨테이너 외부에 백업 파일을 만들거나 복사해야 합니다. 그러지 않고 컨테이너를 제거하면 백업 파일도 삭제됩니다.

## <a name="execute-commands-in-a-container"></a>컨테이너에서 명령 실행

실행 중인 컨테이너가 있는 경우 호스트 터미널을 통해 컨테이너 내에서 명령을 실행할 수 있습니다.

컨테이너 ID를 가져오려면 다음 명령을 실행합니다.

```bash
docker ps
```

컨테이너에서 bash 터미널을 시작하려면 다음 명령을 실행합니다.

```bash
docker exec -it <Container ID> /bin/bash
```

이제 컨테이너 내부 터미널에서 실행하는 것처럼 명령을 실행할 수 있습니다. 완료되면 `exit`을 입력합니다. 대화형 명령 세션이 종료되지만 컨테이너는 계속 실행됩니다.

## <a name="copy-files-from-a-container"></a>컨테이너에서 파일 복사

컨테이너에서 파일을 복사하려면 다음 명령을 사용합니다.

```bash
docker cp <Container ID>:<Container path> <host path>
```

**예:**

```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```

```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```

## <a name="copy-files-into-a-container"></a>컨테이너에 파일 복사

컨테이너에 파일을 복사하려면 다음 명령을 사용합니다.

```bash
docker cp <Host path> <Container ID>:<Container path>
```

**예:**

```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
## <a name="configure-the-timezone"></a><a id="tz"></a> 표준 시간대 구성

특정 표준 시간대의 Linux 컨테이너에서 SQL Server를 실행하려면 `TZ` 환경 변수를 구성합니다. 올바른 표준 시간대 값을 찾으려면 Linux bash 프롬프트에서 `tzselect` 명령을 실행합니다.

```bash
tzselect
```

표준 시간대를 선택하면 `tzselect`에서 다음과 비슷한 출력이 표시됩니다.

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

이 정보를 사용하여 Linux 컨테이너에서 동일한 환경 변수를 설정할 수 있습니다. 다음 예제에서는 `Americas/Los_Angeles` 표준 시간대의 컨테이너에서 SQL Server를 실행하는 방법을 보여 줍니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

## <a name="run-a-specific-sql-server-container-image"></a><a id="tags"></a> 특정 SQL Server 컨테이너 이미지 실행

최신 SQL Server 컨테이너 이미지를 사용하지 않으려는 시나리오도 있습니다. 특정 SQL Server 컨테이너 이미지를 실행하려면 다음 단계를 사용합니다.

1. 사용하려는 릴리스의 Docker **태그**를 확인합니다. 사용 가능한 태그를 보려면 [mssql-server-linux Docker Hub 페이지](https://hub.docker.com/_/microsoft-mssql-server)를 참조하세요.

2. 태그를 사용하여 SQL Server 컨테이너 이미지를 끌어옵니다. 예를 들어 RC1 이미지를 끌어오려면 다음 명령에서 `<image_tag>`를 `rc1`로 바꿉니다.

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. 해당 이미지를 사용하여 새 컨테이너를 실행하려면 `docker run` 명령에 태그 이름을 지정합니다. 다음 명령에서 `<image_tag>`를 실행하려는 버전으로 바꿉니다.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

이러한 단계를 사용하여 기존 컨테이너를 다운그레이드할 수도 있습니다. 예를 들어 문제 해결이나 테스트를 위해 실행 중인 컨테이너를 롤백 또는 다운그레이드할 수 있습니다. 실행 중인 컨테이너를 다운그레이드하려면 데이터 폴더에 대해 지속성 방법을 사용해야 합니다. [업그레이드 섹션](#upgrade)에 간략하게 설명된 것과 동일한 단계를 수행하지만, 새 컨테이너를 실행할 때 이전 버전의 태그 이름을 지정합니다.

## <a name="check-the-container-version"></a><a id="version"></a> 컨테이너 버전 확인

실행 중인 docker 컨테이너의 SQL Server 버전을 확인하려면 다음 명령을 실행하여 버전을 표시합니다. `<Container ID or name>`을 대상 컨테이너 ID 또는 이름으로 바꿉니다. `<YourStrong!Passw0rd>`를 SA 로그인의 SQL Server 암호로 바꿉니다.

```bash
sudo docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourStrong!Passw0rd>' \
   -Q 'SELECT @@VERSION'
```

```PowerShell
docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourStrong!Passw0rd>" `
   -Q 'SELECT @@VERSION'
```

대상 docker 컨테이너 이미지의 SQL Server 버전 및 빌드 번호를 확인할 수도 있습니다. 다음 명령은 **mcr.microsoft.com/mssql/server:2017-latest** 이미지의 SQL Server 버전 및 빌드 정보를 표시합니다. 이 작업을 위해 **PAL_PROGRAM_INFO=1** 환경 변수를 사용하여 새 컨테이너를 실행합니다. 생성된 컨테이너는 즉시 종료되고 `docker rm` 명령이 컨테이너를 제거합니다.

```bash
sudo docker run -e PAL_PROGRAM_INFO=1 --name sqlver \
   -ti mcr.microsoft.com/mssql/server:2017-latest && \
   sudo docker rm sqlver
```

```PowerShell
docker run -e PAL_PROGRAM_INFO=1 --name sqlver `
   -ti mcr.microsoft.com/mssql/server:2017-latest; `
   docker rm sqlver
```

위 명령은 다음 출력과 비슷한 버전 정보를 표시합니다.

```Text
sqlservr
  Version 14.0.3029.16
  Build ID ee3d3882f1c48a7a7e590a620153012eaedc2f37143d485df945a079b9d4eeea
  Build Type release
  Git Version 65d42c4
  Built at Sat Jun 16 01:20:11 GMT 2018

PAL
  Build ID 60cfcb134bbae96d311f6a4f56aeb5a685b3809de80bcb61ec587a8f58b555eb
  Build Type release
  Git Version 21a4c11
  Built at Sat Jun 16 01:18:53 GMT 2018

Packages
  system.sfp                    6.2.9200.1,21a4c1178,
  system.common.sfp             10.0.15063.540
  system.certificates.sfp       6.2.9200.1,21a4c1178,
  system.netfx.sfp              4.6.1590.0
  secforwarderxplat.sfp         14.0.3029.16
  sqlservr.sfp                  14.0.3029.16
  sqlagent.sfp                  14.0.3029.16
```

## <a name="upgrade-sql-server-in-containers"></a><a id="upgrade"></a> 컨테이너의 SQL Server 업그레이드

Docker에서 컨테이너 이미지를 업그레이드하려면 먼저 업그레이드 릴리스의 태그를 확인합니다. `docker pull` 명령을 사용하여 레지스트리에서 이 버전을 끌어옵니다.

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

그러면 새로 만든 컨테이너의 SQL Server 이미지가 업데이트되지만 실행 중인 컨테이너의 SQL Server는 업데이트되지 않습니다. 이렇게 하려면 최신 SQL Server 컨테이너 이미지를 사용하여 새 컨테이너를 만들고 데이터를 새 컨테이너로 마이그레이션해야 합니다.

1. 기존 SQL Server 컨테이너에 대해 [데이터 지속성 방법](#persist) 중 하나를 사용해야 합니다. 그러면 동일한 데이터를 사용하여 새 컨테이너를 시작할 수 있습니다.

1. `docker stop` 명령을 사용하여 SQL Server 컨테이너를 중지합니다.

1. `docker run`을 사용하여 새 SQL Server 컨테이너를 만들고 매핑된 호스트 디렉터리 또는 데이터 볼륨 컨테이너를 지정합니다. SQL Server 업그레이드의 특정 태그를 사용해야 합니다. 이제 새 컨테이너에서 기존 SQL Server 데이터와 함께 새 SQL Server 버전을 사용합니다.

   > [!IMPORTANT]
   > 업그레이드는 현재 RC1, RC2 및 GA 간에만 지원됩니다.

1. 새 컨테이너의 데이터베이스와 데이터를 확인합니다.

1. 필요에 따라 `docker rm`을 사용하여 이전 컨테이너를 제거합니다.

## <a name="build-and-run-non-root-sql-server-2017-containers"></a><a id="buildnonrootcontainer"></a> 루트가 아닌 SQL Server 2017 컨테이너를 빌드하여 실행

`mssql`(루트가 아닌) 사용자 권한으로 시작되는 SQL Server 2017 컨테이너를 빌드하려면 다음 단계를 수행합니다.

> [!NOTE]
> SQL Server 2019 컨테이너는 루트가 아닌 것으로 자동 시작되므로, 다음 단계는 기본적으로 루트로 시작되는 SQL Server 2017 컨테이너에만 적용됩니다.

1. [루트가 아닌 SQL Server 컨테이너에 대한 샘플 dockerfile](https://raw.githubusercontent.com/microsoft/mssql-docker/master/linux/preview/examples/mssql-server-linux-non-root/Dockerfile)을 다운로드한 후 `dockerfile`로 저장합니다.

2. dockerfile 디렉터리의 컨텍스트에서 다음 명령을 실행하여 루트가 아닌 SQL Server 컨테이너를 빌드합니다.

```bash
cd <path to dockerfile>
docker build -t 2017-latest-non-root .
```

3. 컨테이너를 시작합니다.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword@" --cap-add SYS_PTRACE --name sql1 -p 1433:1433 -d 2017-latest-non-root
```

> [!NOTE]
> `--cap-add SYS_PTRACE` 플래그는 루트가 아닌 SQL Server 컨테이너가 문제 해결을 위해 덤프를 생성하는 데 필요합니다.

4. 다음과 같이 컨테이너가 루트가 아닌 사용자로 실행 중인지 확인합니다.

컨테이너에 대해 docker exec를 실행합니다.
```bash
docker exec -it sql1 bash
```

컨테이너 내에서 실행 중인 사용자를 반환하는 `whoami`를 실행합니다.

```bash
whoami
```

## <a name="run-container-as-a-different-non-root-user-on-the-host"></a><a id="nonrootuser"></a> 컨테이너를 호스트의 루트가 아닌 다른 사용자로 실행

SQL Server 컨테이너를 루트가 아닌 다른 사용자로 실행하려면 docker run 명령에 -u 플래그를 추가합니다. 루트가 아닌 사용자가 액세스할 수 있는 '/var/opt/mssql'에 볼륨이 탑재되지 않은 경우 루트가 아닌 컨테이너를 루트 그룹의 일부로 실행해야 한다는 제한 사항이 있습니다. 루트 그룹은 루트가 아닌 사용자에게 추가 루트 사용 권한을 부여하지 않습니다.

**UID 4000을 갖는 사용자로 실행**

사용자 지정 UID를 사용하여 SQL Server를 시작할 수 있습니다. 예를 들어, 다음 명령은 UID 4000을 사용하여 SQL Server를 시작합니다.
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u 4000:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

> [!Warning]
> SQL Server 컨테이너에 'mssql' 또는 'root'와 같은 명명된 사용자가 있는지 확인합니다. 그렇지 않으면 SQLCMD를 컨테이너 내에서 실행할 수 없습니다. 컨테이너 내에서 `whoami`를 실행하여 SQL Server 컨테이너가 명명된 사용자로 실행되고 있는지 확인할 수 있습니다.

**루트가 아닌 컨테이너를 루트 사용자 권한으로 실행**

필요한 경우 루트가 아닌 컨테이너를 루트 사용자 권한으로 실행할 수 있습니다. 이 권한이 더 높으므로 컨테이너에 모든 파일 사용 권한이 자동으로 부여됩니다.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -u 0:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

**호스트 머신에서 사용자로 실행**

다음 명령을 사용하여 호스트 머신에서 기존 사용자를 사용하여 SQL Server를 시작할 수 있습니다.
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u $(id -u myusername):0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

**다른 사용자 및 그룹으로 실행**

사용자 지정 사용자 및 그룹을 사용하여 SQL Server를 시작할 수 있습니다. 이 예제에서 탑재된 볼륨에는 호스트 머신의 사용자 또는 그룹에 대해 구성된 사용 권한이 있습니다.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u (id -u myusername):(id -g myusername) -v /path/to/mssql:/var/opt/mssql -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a name="configure-persistent-storage-permissions-for-non-root-containers"></a><a id="storagepermissions"></a> 루트가 아닌 컨테이너에 대한 영구 스토리지 권한 구성

루트가 아닌 사용자가 탑재된 볼륨에 있는 DB 파일에 액세스할 수 있도록 하려면 컨테이너를 실행하는 사용자/그룹이 영구 파일 스토리지를 사용할 수 있는지 확인합니다.  

이 명령을 사용하여 데이터베이스 파일의 현재 소유권을 확인할 수 있습니다.

```bash
ls -ll <database file dir>
```

SQL Server에 지속형 데이터베이스 파일에 대한 액세스 권한이 없는 경우 다음 명령 중 하나를 실행합니다.

**루트 그룹에 DB 파일에 대한 r/w 액세스 권한 부여**

루트가 아닌 SQL Server 컨테이너가 데이터베이스 파일에 액세스할 수 있도록 루트 그룹에 다음 디렉터리에 대한 권한을 부여합니다.

```bash
chgrp -R 0 <database file dir>
chmod -R g=u <database file dir>
```

**루트가 아닌 사용자를 파일의 소유자로 설정**

이것은 루트가 아닌 기본 사용자이거나 지정하려는 다른 루트가 아닌 사용자일 수 있습니다. 이 예제에서는 UID 10001을 루트가 아닌 사용자로 설정합니다.

```bash
chown -R 10001:0 <database file dir>
```

## <a name="change-the-default-file-location"></a><a id="changefilelocation"></a> 기본 파일 위치 변경

`MSSQL_DATA_DIR` 변수를 추가하여 `docker run` 명령에서 데이터 디렉터리를 변경한 다음, 컨테이너의 사용자가 액세스할 수 있는 위치에 볼륨을 탑재합니다.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a name="troubleshooting"></a><a id="troubleshooting"></a> 문제 해결

다음 섹션에서는 컨테이너에서 SQL Server를 실행하기 위한 문제 해결 제안 사항을 제공합니다.

### <a name="docker-command-errors"></a>Docker 명령 오류

`docker` 명령과 관련된 오류가 발생할 경우 docker 서비스가 실행되고 있는지 확인하고 관리자 권한으로 실행해 봅니다.

예를 들어 Linux에서 `docker` 명령을 실행할 때 다음과 같은 오류가 발생할 수 있습니다.

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Linux에서 이 오류가 발생할 경우 앞에 `sudo`를 추가하여 동일한 명령을 실행해 봅니다. 이 명령이 실패하면 docker 서비스가 실행되고 있는지 확인하고, 필요한 경우 서비스를 시작합니다.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

Windows에서 PowerShell 또는 명령 프롬프트를 관리자 권한으로 시작했는지 확인합니다.

### <a name="sql-server-container-startup-errors"></a>SQL Server 컨테이너 시작 오류

SQL Server 컨테이너가 실행되지 않으면 다음 테스트를 시도합니다.

- **‘네트워크 브리지에서 CONTAINER_NAME 엔드포인트를 만들지 못했습니다. 프록시를 시작하는 중 오류 발생: listen tcp 0.0.0.0:1433 bind: 주소가 이미 사용 중입니다.’** 와 같은 오류가 발생할 경우 컨테이너 포트 1433을 이미 사용 중인 포트에 매핑하려고 한 것입니다. 이 문제는 호스트 머신에서 SQL Server를 로컬로 실행하는 경우에 발생할 수 있습니다. 두 개의 SQL Server 컨테이너를 시작하고 둘 다 동일한 호스트 포트에 매핑하려고 하는 경우에도 발생할 수 있습니다. 이 문제가 발생할 경우 `-p` 매개 변수를 사용하여 컨테이너 포트 1433을 다른 호스트 포트에 매핑합니다. 다음은 그 예입니다. 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

::: moniker-end

- 컨테이너를 시작할 때 **‘unix:///var/run/docker.sock에서 Docker 디먼 소켓에 연결하는 중 사용 권한이 거부되었습니다. http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: dial unix /var/run/docker.sock: connect: 사용 권한 거부됨이 표시됩니다.’** 와 같은 오류가 발생할 경우 Ubuntu의 docker 그룹에 사용자를 추가합니다. 이 변경 내용은 새 세션에 영향을 주기 때문에 로그아웃한 후 다시 로그인합니다. 

   ```bash
    usermod -aG docker $USER
   ```
- 컨테이너의 오류 메시지가 있는지 확인합니다.

    ```bash
    docker logs e69e056c702d
    ```

- 빠른 시작 문서의 [필수 조건](quickstart-install-connect-docker.md#requirements) 섹션에 지정된 최소 메모리 및 디스크 요구 사항을 충족하는지 확인합니다.

- 컨테이너 관리 소프트웨어를 사용하는 경우 소프트웨어가 루트로 실행 중인 컨테이너 프로세스를 지원하는지 확인합니다. 컨테이너의 sqlservr.exe 프로세스가 루트로 실행됩니다.

- [SQL Server 설치 및 오류 로그](#errorlogs)를 검토합니다.

### <a name="enable-dump-captures"></a>덤프 캡처 사용

컨테이너 내부에서 SQL Server 프로세스가 실패하는 경우 **SYS_PTRACE**를 사용하도록 설정하여 새 컨테이너를 만들어야 합니다. 그러면 예외 발생 시 덤프 파일을 만드는 데 필요한 Linux 프로세스 추적 기능이 추가됩니다. 덤프 파일은 고객 지원팀이 문제를 해결하는 데 사용할 수 있습니다. 다음 docker run 명령은 이 기능을 사용하도록 설정합니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>SQL Server 연결 실패

컨테이너에서 실행되는 SQL Server 인스턴스에 연결할 수 없는 경우 다음 테스트를 시도합니다.

- `docker ps -a` 출력의 **STATUS** 열을 확인하여 SQL Server 컨테이너가 실행되고 있는지 확인합니다. 컨테이너가 실행되고 있지 않으면 `docker start <Container ID>`를 사용하여 시작합니다.

- 기본값이 아닌 호스트 포트(1433이 아님)에 매핑한 경우 연결 문자열에 포트를 지정해야 합니다. `docker ps -a` 출력의 **PORTS** 열에서 포트 매핑을 확인할 수 있습니다. 예를 들어 다음 명령은 sqlcmd를 포트 1401에서 수신 대기 중인 컨테이너에 연결합니다.

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- 기존의 매핑된 데이터 볼륨 또는 데이터 볼륨 컨테이너와 함께 `docker run`을 사용한 경우 SQL Server는 `MSSQL_SA_PASSWORD` 값을 무시합니다. 대신, 데이터 볼륨 또는 데이터 볼륨 컨테이너의 SQL Server 데이터에서 미리 구성된 SA 사용자 암호를 사용합니다. 연결 중인 데이터와 연결된 SA 암호를 사용하고 있는지 확인합니다.

- [SQL Server 설치 및 오류 로그](#errorlogs)를 검토합니다.

### <a name="sql-server-availability-groups"></a>SQL Server 가용성 그룹

SQL Server 가용성 그룹과 함께 Docker를 사용하는 경우 두 가지 추가 요구 사항이 있습니다.

- 복제본 통신에 사용되는 포트를 매핑합니다(기본값 5022). 예를 들어 `docker run` 명령의 일부로 `-p 5022:5022`를 지정합니다.

- `docker run` 명령의 `-h YOURHOSTNAME` 매개 변수를 사용하여 컨테이너 호스트 이름을 명시적으로 설정합니다. 이 호스트 이름은 가용성 그룹을 구성할 때 사용됩니다. `-h`를 사용하여 지정하지 않으면 기본적으로 컨테이너 ID로 설정됩니다.

### <a name="sql-server-setup-and-error-logs"></a><a id="errorlogs"></a> SQL Server 설치 및 오류 로그

**/var/opt/mssql/log**에서 SQL Server 설치 및 오류 로그를 확인할 수 있습니다. 컨테이너가 실행되고 있지 않으면 먼저 컨테이너를 시작합니다. 그런 다음, 대화형 명령 프롬프트를 사용하여 로그를 검사합니다.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

컨테이너 내부 bash 세션에서 다음 명령을 실행합니다.

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> 컨테이너를 만들 때 호스트 디렉터리를 **/var/opt/mssql**에 탑재한 경우, 대신 호스트의 매핑된 경로에 있는 **log** 하위 디렉터리에서 확인할 수 있습니다.

## <a name="next-steps"></a>다음 단계

[빠른 시작](quickstart-install-connect-docker.md)을 진행하여 Docker에서 SQL Server 2017 컨테이너 이미지로 시작합니다.

또한 리소스, 피드백 및 알려진 문제는 [mssql-docker GitHub 리포지토리](https://github.com/Microsoft/mssql-docker)를 참조하세요.

[SQL Server 컨테이너의 고가용성을 살펴봅니다](sql-server-linux-container-ha-overview.md).
