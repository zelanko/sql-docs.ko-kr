---
title: Docker의 SQL Server에 대 한 구성 옵션
description: Docker에서 SQL Server 2017 및 2019 미리 보기 컨테이너 이미지를 사용 하 고 상호 작용 하는 다양 한 방법을 알아봅니다. 여기에는 데이터 유지, 파일 복사 및 문제 해결이 포함 됩니다.
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: d24bb3566195c71a3b62d16fab867ab5085404b7
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388384"
---
# <a name="configure-sql-server-container-images-on-docker"></a>Docker에서 SQL Server 컨테이너 이미지 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Docker를 사용 하 여 [mssql-server-linux 컨테이너 이미지](https://hub.docker.com/_/microsoft-mssql-server) 를 구성 하 고 사용 하는 방법을 설명 합니다. 이 이미지는 Ubuntu 16.04 기반 Linux에서 실행 중인 SQL Server로 구성됩니다. Linux 또는 Mac/Windows용 Docker에서 Docker Engine 1.8+와 함께 사용할 수 있습니다.

> [!NOTE]
> 이 문서에서는 특히 mssql-server linux 이미지를 사용 하는 방법을 집중적으로 설명 합니다. Windows 이미지는 다루지 않지만 [mssql-server-Windows Docker Hub 페이지](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)에서 자세히 알아볼 수 있습니다.

## <a name="pull-and-run-the-container-image"></a>컨테이너 이미지를 끌어와 실행하기

SQL Server 2017 및 SQL Server 2019 preview에 대 한 Docker 컨테이너 이미지를 끌어오거나 실행 하려면 다음 빠른 시작의 전제 조건 및 단계를 따르세요.

- [Docker를 사용 하 여 SQL Server 2017 컨테이너 이미지 실행](quickstart-install-connect-docker.md?view=sql-server-2017)
- [Docker를 사용 하 여 SQL Server 2019 미리 보기 컨테이너 이미지 실행](quickstart-install-connect-docker.md?view=sql-server-ver15)

이 구성 문서는 다음 섹션의 추가 사용 시나리오를 제공 합니다.

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a>RHEL 기반 컨테이너 이미지 실행

SQL Server Linux 컨테이너 이미지에 대 한 모든 설명서는 Ubuntu 기반 컨테이너를 가리킵니다. SQL Server 2019 preview부터 Red Hat Enterprise Linux (RHEL)를 기반으로 하는 컨테이너를 사용할 수 있습니다. 모든 docker 명령에서 컨테이너 리포지토리를 **mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu** 에서 **mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1** 로 변경 합니다.

예를 들어 다음 명령은 RHEL를 사용 하는 최신 SQL Server 2019 미리 보기 컨테이너를 가져옵니다.

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a>프로덕션 컨테이너 이미지 실행

이전 섹션의 빠른 시작에서는 Docker 허브에서 SQL Server의 무료 Developer edition을 실행 합니다. Enterprise, Standard 또는 Web edition과 같은 프로덕션 컨테이너 이미지를 실행 하려면 대부분의 정보가 여전히 적용 됩니다. 그러나 여기서 설명 하는 몇 가지 차이점이 있습니다.

- 유효한 라이선스가 있는 경우 프로덕션 환경 에서만 SQL Server를 사용할 수 있습니다. [여기](https://go.microsoft.com/fwlink/?linkid=857693)에서 무료 SQL Server Express 프로덕션 라이선스를 받을 수 있습니다. SQL Server Standard 및 Enterprise Edition 라이선스는 [Microsoft 볼륨 라이선스](https://www.microsoft.com/licensing/default.aspx)를 통해 사용할 수 있습니다.


- 개발자 컨테이너 이미지는 프로덕션 버전도 실행 하도록 구성할 수 있습니다. 다음 단계를 사용 하 여 프로덕션 버전을 실행 합니다.

[빠른](quickstart-install-connect-docker.md)시작에서 요구 사항 및 실행 절차를 검토 합니다. **MSSQL_PID** 환경 변수를 사용 하 여 프로덕션 버전을 지정 해야 합니다. 다음 예제에서는 Enterprise Edition에 대 한 최신 SQL Server 2017 컨테이너 이미지를 실행 하는 방법을 보여 줍니다.

```bash
docker run --name sqlenterprise \
      -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
      -d store/microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run --name sqlenterprise `
      -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -e "MSSQL_PID=Enterprise" -p 1433:1433 `
      -d "store/microsoft/mssql-server-linux:2017-latest"
 ```

> [!IMPORTANT]
> **Y** 값을 환경 변수 **ACCEPT_EULA** 에 전달 하 고 edition 값을 **MSSQL_PID**에 전달 하 여 사용 하려는 버전 및 SQL Server 버전에 대 한 유효한 기존 라이선스가 있음을 표현 하는 것입니다. 또한 Docker 컨테이너 이미지에서 실행 되는 SQL Server 소프트웨어를 사용 하는 경우 SQL Server 라이선스의 적용을 받습니다.

> [!NOTE]
> **MSSQL_PID**의 가능한 값에 대 한 전체 목록은 [Linux에서 환경 변수를 사용 하 여 SQL Server 설정 구성](sql-server-linux-configure-environment-variables.md)을 참조 하세요.

::: moniker-end

## <a name="connect-and-query"></a>연결 및 쿼리

컨테이너 외부 또는 컨테이너 내에서 컨테이너의 SQL Server를 연결 하 고 쿼리할 수 있습니다. 다음 섹션에서는 두 시나리오에 대해 설명 합니다. 

### <a name="tools-outside-the-container"></a>컨테이너 외부 도구

SQL 연결을 지 원하는 모든 외부 Linux, Windows 또는 macOS 도구에서 Docker 컴퓨터의 SQL Server 인스턴스에 연결할 수 있습니다. 몇 가지 일반적인 도구는 다음과 같습니다.

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [Windows의 SSMS(SQL Server Management Studio)](sql-server-linux-manage-ssms.md)

다음 예에서는 **sqlcmd** 를 사용 하 여 Docker 컨테이너에서 실행 되는 SQL Server에 연결 합니다. 연결 문자열의 IP 주소는 컨테이너를 실행 하는 호스트 컴퓨터의 IP 주소입니다.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

기본 **1433**이 아닌 호스트 포트를 매핑한 경우 해당 포트를 연결 문자열에 추가 합니다. 예를 들어 `docker run` 명령에을 `-p 1400:1433` 지정한 경우 포트 1400을 명시적으로 지정 하 여 연결 합니다.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>컨테이너 내의 도구

SQL Server 2017 preview부터 [SQL Server 명령줄 도구가](sql-server-linux-setup-tools.md) 컨테이너 이미지에 포함 됩니다. 대화형 명령 프롬프트를 사용 하 여 이미지에 연결 하는 경우 도구를 로컬로 실행할 수 있습니다.

1. `docker exec -it` 명령을 사용하여 실행 중인 컨테이너 내에서 대화형 bash 셸을 시작합니다. 다음 예 `e69e056c702d` 에서는 컨테이너 ID입니다.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 항상 전체 컨테이너 id를 지정할 필요는 없습니다. 고유 하 게 식별할 수 있도록 충분 한 문자만 지정 하면 됩니다. 따라서이 예에서는 전체 id가 아닌 또는 `e6` `e69` 를 사용 하는 것이 충분 합니다.

2. 컨테이너 내부로 들어가면 sqlcmd를 사용하여 로컬로 연결합니다. Sqlcmd는 기본적으로 경로에 있지 않으므로 전체 경로를 지정 해야 합니다.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Sqlcmd를 사용 하 여 마치면 `exit`를 입력 합니다.

4. 대화형 명령 프롬프트를 마치면를 입력 `exit`합니다. 컨테이너는 대화형 bash 셸을 종료한 후에도 계속 실행됩니다.

## <a name="run-multiple-sql-server-containers"></a>여러 SQL Server 컨테이너 실행

Docker는 동일한 호스트 컴퓨터에서 여러 SQL Server 컨테이너를 실행 하는 방법을 제공 합니다. 동일한 호스트에서 SQL Server의 여러 인스턴스가 필요한 시나리오에 대 한 방법입니다. 각 컨테이너는 다른 포트에서 자신을 노출 해야 합니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

다음 예제에서는 두 개의 SQL Server 2017 컨테이너를 만들어 호스트 컴퓨터의 **1401** 및 **1402** 포트에 매핑합니다.

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

다음 예제에서는 두 개의 SQL Server 2019 미리 보기 컨테이너를 만들어 호스트 컴퓨터의 **1401** 및 **1402** 포트에 매핑합니다.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

이제 별도의 컨테이너에서 실행 되는 SQL Server 인스턴스가 두 개 있습니다. 클라이언트는 Docker 호스트의 IP 주소와 컨테이너의 포트 번호를 사용 하 여 각 SQL Server 인스턴스에 연결할 수 있습니다.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a>사용자 지정 컨테이너 만들기

사용자 고유의 [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) 을 만들어 사용자 지정 SQL Server 컨테이너를 만들 수 있습니다. 자세한 내용은 [SQL Server 및 노드 응용 프로그램을 결합 하는 데모](https://github.com/twright-msft/mssql-node-docker-demo-app)를 참조 하세요. 사용자 고유의 Dockerfile을 만드는 경우이 프로세스는 컨테이너의 수명을 제어 하므로 포그라운드 프로세스를 염두에 두어야 합니다. 종료 되 면 컨테이너가 종료 됩니다. 예를 들어 스크립트를 실행 하 고 SQL Server를 시작 하려면 SQL Server 프로세스가 맨 오른쪽 명령 인지 확인 합니다. 다른 모든 명령은 백그라운드에서 실행 됩니다. 이는 Dockerfile 내의 다음 명령에 설명 되어 있습니다.

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

이전 예제의 명령을 역순으로 하면 do-my-sql-commands.sh 스크립트가 완료 될 때 컨테이너가 종료 됩니다.

## <a id="persist"></a>데이터 유지

`docker stop` 및`docker start`를 사용 하 여 컨테이너를 다시 시작 하는 경우에도 SQL Server 구성 변경 내용과 데이터베이스 파일은 컨테이너에 유지 됩니다. 그러나를 사용 `docker rm`하 여 컨테이너를 제거 하면 SQL Server 및 데이터베이스를 포함 하 여 컨테이너의 모든 항목이 삭제 됩니다. 다음 섹션에서는 연결 된 컨테이너가 삭제 된 경우에도 **데이터 볼륨** 을 사용 하 여 데이터베이스 파일을 유지 하는 방법을 설명 합니다.

> [!IMPORTANT]
> SQL Server의 경우 Docker의 데이터 지 속성을 이해 하는 것이 중요 합니다. 이 섹션에서 설명 하는 것 외에도 docker [컨테이너의 데이터를 관리 하는 방법](https://docs.docker.com/engine/tutorials/dockervolumes/)에 대 한 docker 설명서를 참조 하세요.

### <a name="mount-a-host-directory-as-data-volume"></a>호스트 디렉터리를 데이터 볼륨으로 탑재

첫 번째 옵션은 호스트의 디렉터리를 컨테이너의 데이터 볼륨으로 탑재 하는 것입니다. 이렇게 하려면 `docker run` `-v <host directory>:/var/opt/mssql` 플래그와 함께 명령을 사용 합니다. 이렇게 하면 컨테이너 실행 간에 데이터를 복원할 수 있습니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

이 기술을 사용 하 여 Docker 외부에서 호스트의 파일을 공유 하 고 볼 수도 있습니다.

> [!IMPORTANT]
> SQL Server on Linux 이미지를 사용 하는 Mac의 Docker에 대 한 호스트 볼륨 매핑은 지금은 지원 되지 않습니다. 대신 데이터 볼륨 컨테이너를 사용 하십시오. 이 제한은 `/var/opt/mssql` 디렉터리에만 적용 됩니다. 탑재 된 디렉터리에서 읽기는 정상적으로 작동 합니다. 예를 들어, Mac에서-v를 사용 하 여 호스트 디렉터리를 탑재 하 고 호스트에 있는 .bak 파일에서 백업을 복원할 수 있습니다.

### <a name="use-data-volume-containers"></a>데이터 볼륨 컨테이너 사용

두 번째 옵션은 데이터 볼륨 컨테이너를 사용 하는 것입니다. `-v` 매개 변수를 사용 하 여 호스트 디렉터리 대신 볼륨 이름을 지정 하 여 데이터 볼륨 컨테이너를 만들 수 있습니다. 다음 예에서는 **sqlvolume**이라는 공유 데이터 볼륨을 만듭니다.

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```
::: moniker-end

> [!NOTE]
> 실행 명령에서 암시적으로 데이터 볼륨을 만들기 위한이 기술은 이전 버전의 Docker와는 작동 하지 않습니다. 이 경우 Docker 설명서에 설명 된 명시적 단계를 사용 하 여 [데이터 볼륨 컨테이너를 만들고 탑재](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container)합니다.

이 컨테이너를 중지 하 고 제거 해도 데이터 볼륨이 계속 유지 됩니다. `docker volume ls` 명령을 사용 하 여 볼 수 있습니다.

```bash
docker volume ls
```

그런 다음 동일한 볼륨 이름을 사용 하 여 다른 컨테이너를 만들면 새 컨테이너는 볼륨에 포함 된 것과 동일한 SQL Server 데이터를 사용 합니다.

데이터 볼륨 컨테이너를 제거 하려면 `docker volume rm` 명령을 사용 합니다.

> [!WARNING]
> 데이터 볼륨 컨테이너를 삭제 하면 컨테이너의 모든 SQL Server 데이터가 *영구적으로* 삭제 됩니다.

### <a name="backup-and-restore"></a>Backup 및 Restore 메서드

이러한 컨테이너 기술 외에도 표준 SQL Server 백업 및 복원 기술을 사용할 수 있습니다. 백업 파일을 사용 하 여 데이터를 보호 하거나 다른 SQL Server 인스턴스로 데이터를 이동할 수 있습니다. 자세한 내용은 [Linux에서 SQL Server 데이터베이스 백업 및 복원](sql-server-linux-backup-and-restore-database.md)을 참조 하세요.

> [!WARNING]
> 백업을 만들 경우 컨테이너 외부에서 백업 파일을 만들거나 복사 해야 합니다. 그렇지 않고 컨테이너가 제거 되 면 백업 파일도 삭제 됩니다.

## <a name="execute-commands-in-a-container"></a>컨테이너에서 명령 실행

컨테이너를 실행 하는 경우 호스트 터미널의 컨테이너 내에서 명령을 실행할 수 있습니다.

컨테이너 ID를 가져오려면 다음을 실행 합니다.

```bash
docker ps
```

컨테이너에서 bash 터미널을 시작 하려면 다음을 실행 합니다.

```bash
docker exec -it <Container ID> /bin/bash
```

이제 컨테이너 내부의 터미널에서 실행 하는 것 처럼 명령을 실행할 수 있습니다. 완료되면 `exit`을 입력합니다. 그러면 대화형 명령 세션이 종료 되지만 컨테이너는 계속 실행 됩니다.

## <a name="copy-files-from-a-container"></a>컨테이너에서 파일 복사

컨테이너에서 파일을 복사 하려면 다음 명령을 사용 합니다.

```bash
docker cp <Container ID>:<Container path> <host path>
```

**예제:**

```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```

```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```

## <a name="copy-files-into-a-container"></a>컨테이너에 파일 복사

컨테이너에 파일을 복사 하려면 다음 명령을 사용 합니다.

```bash
docker cp <Host path> <Container ID>:<Container path>
```

**예제:**

```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
## <a id="tz"></a>표준 시간대 구성

특정 표준 시간대를 사용 하 여 Linux 컨테이너에서 SQL Server를 실행 하려면 **TZ** 환경 변수를 구성 합니다. 올바른 표준 시간대 값을 찾으려면 Linux bash 프롬프트에서 **tzselect** 명령을 실행 합니다.

```bash
tzselect
```

표준 시간대를 선택한 후 **tzselect** 는 다음과 유사한 출력을 표시 합니다.

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

이 정보를 사용 하 여 Linux 컨테이너에서 동일한 환경 변수를 설정할 수 있습니다. 다음 예제에서는 `Americas/Los_Angeles` 표준 시간대의 컨테이너에서 SQL Server를 실행 하는 방법을 보여 줍니다.

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
   -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```
::: moniker-end

## <a id="tags"></a>특정 SQL Server 컨테이너 이미지 실행

최신 SQL Server 컨테이너 이미지를 사용 하지 않으려는 시나리오가 있습니다. 특정 SQL Server 컨테이너 이미지를 실행 하려면 다음 단계를 사용 합니다.

1. 사용 하려는 릴리스에 대 한 Docker **태그** 를 식별 합니다. 사용 가능한 태그를 보려면 [mssql-server-Linux Docker 허브 페이지](https://hub.docker.com/_/microsoft-mssql-server)를 참조 하세요.

2. 태그를 사용 하 여 SQL Server 컨테이너 이미지를 끌어옵니다. 예를 들어 RC1 이미지를 꺼내려면 다음 명령에서 `<image_tag>` 을로 `rc1`바꿉니다.

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. 해당 이미지를 사용 하 여 새 컨테이너를 실행 하려면 `docker run` 명령에서 태그 이름을 지정 합니다. 다음 명령에서를 실행 하려는 `<image_tag>` 버전으로 바꿉니다.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

이러한 단계를 사용 하 여 기존 컨테이너를 다운 그레이드할 수도 있습니다. 예를 들어 문제 해결 또는 테스트를 위해 실행 중인 컨테이너를 롤백 또는 다운 그레이드할 수 있습니다. 실행 중인 컨테이너를 다운 그레이드 하려면 데이터 폴더에 대 한 지 속성 기술을 사용 해야 합니다. [업그레이드 섹션](#upgrade)에 설명 된 동일한 단계를 따르고 새 컨테이너를 실행할 때 이전 버전의 태그 이름을 지정 합니다.

## <a id="version"></a>컨테이너 버전 확인

실행 중인 docker 컨테이너의 SQL Server 버전을 확인 하려면 다음 명령을 실행 하 여 표시 합니다. 대상 `<Container ID or name>` 컨테이너 ID 또는 이름으로 대체 합니다. 을 `<YourStrong!Passw0rd>` SA 로그인에 대 한 SQL Server 암호로 바꿉니다.

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

대상 docker 컨테이너 이미지에 대 한 SQL Server 버전 및 빌드 번호를 확인할 수도 있습니다. 다음 명령은 **microsoft/mssql-Server-linux: 2017-최신** 이미지에 대 한 SQL Server 버전 및 빌드 정보를 표시 합니다. **PAL_PROGRAM_INFO = 1**환경 변수를 사용 하 여 새 컨테이너를 실행 하 여이를 수행 합니다. 그러면 생성 된 컨테이너는 즉시 종료 되 `docker rm` 고 명령은 제거 합니다.

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

이전 명령은 다음 출력과 유사한 버전 정보를 표시 합니다.

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

## <a id="upgrade"></a>컨테이너의 업그레이드 SQL Server

Docker를 사용 하 여 컨테이너 이미지를 업그레이드 하려면 먼저 업그레이드할 릴리스 태그를 식별 합니다. 다음 `docker pull` 명령을 사용 하 여 레지스트리에서이 버전을 가져옵니다.

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

그러면 새로 만든 컨테이너의 SQL Server 이미지가 업데이트 되지만 실행 중인 컨테이너의 SQL Server 업데이트 되지는 않습니다. 이렇게 하려면 최신 SQL Server 컨테이너 이미지를 사용 하 여 새 컨테이너를 만들고 데이터를 새 컨테이너로 마이그레이션해야 합니다.

1. 기존 SQL Server 컨테이너에 대해 [데이터 지 속성 기술](#persist) 중 하나를 사용 하 고 있는지 확인 합니다. 이렇게 하면 동일한 데이터를 사용 하 여 새 컨테이너를 시작할 수 있습니다.

1. `docker stop` 명령을 사용 하 여 SQL Server 컨테이너를 중지 합니다.

1. 를 사용 하 여 `docker run` 새 SQL Server 컨테이너를 만들고 매핑된 호스트 디렉터리 또는 데이터 볼륨 컨테이너를 지정 합니다. SQL Server 업그레이드에 특정 태그를 사용 해야 합니다. 이제 새 컨테이너는 기존 SQL Server 데이터와 SQL Server 새 버전을 사용 합니다.

   > [!IMPORTANT]
   > 업그레이드는 현재 RC1, RC2 및 GA 간에만 지원 됩니다.

1. 새 컨테이너에서 데이터베이스 및 데이터를 확인 합니다.

1. 필요에 따라를 사용 하 여 `docker rm`이전 컨테이너를 제거 합니다.

## <a id="troubleshooting"></a> 문제 해결

다음 섹션에서는 컨테이너에서 SQL Server를 실행 하기 위한 문제 해결 제안 사항을 제공 합니다.

### <a name="docker-command-errors"></a>Docker 명령 오류

모든 `docker` 명령에 대 한 오류가 발생 하는 경우 docker 서비스가 실행 중인지 확인 하 고 승격 된 권한으로 실행을 시도 합니다.

예를 들어 Linux에서 명령을 실행할 `docker` 때 다음과 같은 오류가 발생할 수 있습니다.

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Linux에서이 오류가 발생 하는 경우로 `sudo`시작 하는 동일한 명령을 실행 해 봅니다. 실패 하면 docker 서비스가 실행 중인지 확인 하 고 필요한 경우 시작 합니다.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

Windows에서 PowerShell 또는 명령 프롬프트를 관리자 권한으로 시작 하 고 있는지 확인 합니다.

### <a name="sql-server-container-startup-errors"></a>SQL Server 컨테이너 시작 오류

SQL Server 컨테이너가 실행 되지 않으면 다음 테스트를 시도 합니다.

- **' 네트워크 브리지에서 끝점 CONTAINER_NAME를 만들지 못했습니다. 프록시를 시작 하는 동안 오류 발생: 수신 tcp 0.0.0.0:1433 바인딩: 주소가 이미 사용 중입니다. '** 컨테이너 포트 1433을 이미 사용 중인 포트에 매핑하려고 합니다. 이 문제는 호스트 컴퓨터에서 로컬로 SQL Server를 실행 하는 경우에 발생할 수 있습니다. 두 개의 SQL Server 컨테이너를 시작 하 고 둘 다 동일한 호스트 포트에 매핑하려고 시도 하는 경우에도 발생할 수 있습니다. 이 문제가 발생 하는 경우 `-p` 매개 변수를 사용 하 여 컨테이너 포트 1433을 다른 호스트 포트에 매핑합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다. 

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu`.
```

::: moniker-end

- Unix:///var/run/docker.sock에서 Docker 디먼 소켓에 연결 **하려고 시도 하는 동안 ' 사용 권한이 거부 되었습니다. '와 같은 오류가 발생 하는 경우: 컨테이너 http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: 를 시작 하려는 경우 전화 접속 unix/var/run/docker.sock:** 연결: 사용 권한 거부 '를 가져온 다음 사용자를 Ubuntu의 docker 그룹에 추가 합니다. 그런 다음이 변경 내용이 새 세션에 영향을 주기 때문에 로그 아웃 하 고 다시 로그인 합니다. 

   ```bash
    usermod -aG docker $USER
    ```
- 컨테이너의 오류 메시지가 있는지 확인 하십시오.

    ```bash
    docker logs e69e056c702d
    ```

- 빠른 시작 문서의 [필수 구성 요소](quickstart-install-connect-docker.md#requirements) 섹션에 지정 된 최소 메모리 및 디스크 요구 사항을 충족 하는지 확인 합니다.

- 컨테이너 관리 소프트웨어를 사용 하는 경우 루트로 실행 되는 컨테이너 프로세스를 지원 하는지 확인 합니다. 컨테이너의 sqlservr.exe 프로세스는 루트로 실행 됩니다.

- [SQL Server 설정 및 오류 로그](#errorlogs)를 검토 합니다.

### <a name="enable-dump-captures"></a>덤프 캡처 사용

SQL Server 프로세스가 컨테이너 내부에서 실패 하는 경우 **SYS_PTRACE** 를 사용 하도록 설정 된 새 컨테이너를 만들어야 합니다. 그러면 예외에 덤프 파일을 만드는 데 필요한 프로세스를 추적 하는 Linux 기능이 추가 됩니다. 덤프 파일은 지원 서비스에서 문제를 해결 하는 데 사용할 수 있습니다. 다음 docker run 명령을 사용 하면이 기능을 사용할 수 있습니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>SQL Server 연결 오류

컨테이너에서 실행 중인 SQL Server 인스턴스에 연결할 수 없는 경우 다음 테스트를 시도 합니다.

- `docker ps -a` 출력의 **상태** 열을 확인 하 여 SQL Server 컨테이너가 실행 되 고 있는지 확인 합니다. 그렇지 않으면를 사용 `docker start <Container ID>` 하 여 시작 합니다.

- 기본이 아닌 호스트 포트 (1433 아님)에 매핑한 경우 연결 문자열에 포트를 지정 해야 합니다. `docker ps -a` 출력의 **포트** 열에서 포트 매핑을 볼 수 있습니다. 예를 들어 다음 명령은 sqlcmd를 포트 1401에서 수신 대기 하는 컨테이너에 연결 합니다.

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- 기존 매핑된 데이터 `docker run` 볼륨 또는 데이터 볼륨 컨테이너와 함께를 사용 하는 경우 SQL Server의 `MSSQL_SA_PASSWORD`값을 무시 합니다. 대신, 데이터 볼륨 또는 데이터 볼륨 컨테이너의 SQL Server 데이터에서 미리 구성 된 SA 사용자 암호를 사용 합니다. 연결 중인 데이터와 연결 된 SA 암호를 사용 하 고 있는지 확인 합니다.

- [SQL Server 설정 및 오류 로그](#errorlogs)를 검토 합니다.

### <a name="sql-server-availability-groups"></a>가용성 그룹 SQL Server

SQL Server 가용성 그룹과 함께 Docker를 사용 하는 경우 두 가지 추가 요구 사항이 있습니다.

- 복제본 통신에 사용 되는 포트를 매핑합니다 (기본값 5022). 예를 들어 `docker run` 명령의 `-p 5022:5022` 일부로를 지정 합니다.

- `docker run` 명령의 `-h YOURHOSTNAME` 매개 변수를 사용 하 여 컨테이너 호스트 이름을 명시적으로 설정 합니다. 이 호스트 이름은 가용성 그룹을 구성할 때 사용 됩니다. 을 사용 하 여 지정 하지 `-h`않으면 기본적으로 컨테이너 ID가 사용 됩니다.

### <a id="errorlogs"></a>설정 및 오류 로그 SQL Server

**/Var/opt/mssql/log**에서 SQL Server 설정 및 오류 로그를 확인할 수 있습니다. 컨테이너가 실행 되 고 있지 않으면 먼저 컨테이너를 시작 합니다. 그런 다음 대화형 명령 프롬프트를 사용 하 여 로그를 검사 합니다.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

컨테이너 내부의 bash 세션에서 다음 명령을 실행 합니다.

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> 컨테이너를 만들 때 **/var/opt/mssql** 에 호스트 디렉터리를 탑재 한 경우 호스트에서 매핑된 경로에 대 한 **로그** 하위 디렉터리를 대신 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

[빠른](quickstart-install-connect-docker.md)시작을 진행 하 여 Docker에서 SQL Server 2017 컨테이너 이미지를 시작 합니다.

또한 리소스, 사용자 의견 및 알려진 문제에 대 한 [mssql Docker GitHub 리포지토리](https://github.com/Microsoft/mssql-docker) 를 참조 하세요.

[SQL Server 컨테이너의 고가용성 살펴보기](sql-server-linux-container-ha-overview.md)
