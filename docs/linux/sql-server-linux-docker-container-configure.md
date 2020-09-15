---
title: SQL Server Docker 컨테이너 구성 및 사용자 지정
description: SQL Server Docker 컨테이너를 사용자 지정하는 다양한 방법과 요구 사항에 따라 이를 구성하는 방법 이해
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
ms.openlocfilehash: 53bfe3652df7136b0358590f6d9be51f36907b2d
ms.sourcegitcommit: 678f513b0c4846797ba82a3f921ac95f7a5ac863
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2020
ms.locfileid: "89511583"
---
# <a name="configure-and-customize-sql-server-docker-containers"></a>SQL Server Docker 컨테이너 구성 및 사용자 지정

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 데이터 유지, 컨테이너 간 파일 이동, 기본 설정 변경과 같이 SQL Server Docker 컨테이너의 구성 및 사용자 지정 방식을 설명합니다.

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

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

이 방법을 사용하여 Docker 외부에서 호스트의 파일을 공유하고 볼 수도 있습니다.

> [!IMPORTANT]
> **Docker on Windows**의 호스트 볼륨 매핑은 현재 전체 `/var/opt/mssql` 디렉터리 매핑을 지원하지 않습니다. 그러나 `/var/opt/mssql/data` 등의 하위 디렉터리를 호스트 머신에 매핑할 수 있습니다.
>
> SQL Server on Linux 이미지와 **Docker on Mac** 간의 호스트 볼륨 매핑은 현재 지원되지 않습니다. 대신, 데이터 볼륨 컨테이너를 사용합니다. 이 제한 사항은 `/var/opt/mssql` 디렉터리에만 적용됩니다. 탑재된 디렉터리에서 읽을 수는 있습니다. 예를 들어 Mac에서-v를 사용하여 호스트 디렉터리를 탑재하고 호스트에 있는 .bak 파일에서 백업을 복원할 수 있습니다.

### <a name="use-data-volume-containers"></a>데이터 볼륨 컨테이너 사용

두 번째 옵션은 데이터 볼륨 컨테이너를 사용하는 것입니다. `-v` 매개 변수를 사용하여 호스트 디렉터리 대신 볼륨 이름을 지정하면 데이터 볼륨 컨테이너를 만들 수 있습니다. 다음 예제에서는 **sqlvolume**이라는 공유 데이터 볼륨을 만듭니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

> [!NOTE]
> run 명령에서 암시적으로 데이터 볼륨을 만드는 이 방법은 이전 버전의 Docker에서 작동하지 않습니다. 이 경우에는 Docker 설명서인 [데이터 볼륨 컨테이너 만들기 및 탑재](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container)에 간략하게 설명된 명시적 단계를 사용합니다.

이 컨테이너를 중지하고 제거해도 데이터 볼륨이 계속 유지됩니다. `docker volume ls` 명령을 사용하여 데이터 볼륨을 볼 수 있습니다.

```command
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

## <a name="copy-files-from-a-container"></a>컨테이너에서 파일 복사

컨테이너에서 파일을 복사하려면 다음 명령을 사용합니다.

```command
docker cp <Container ID>:<Container path> <host path>
```

`docker ps -a` 명령을 실행하여 컨테이너 ID를 가져올 수 있습니다.

**예:**

::: zone pivot="cs1-bash"
```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```
::: zone-end

## <a name="copy-files-into-a-container"></a>컨테이너에 파일 복사

컨테이너에 파일을 복사하려면 다음 명령을 사용합니다.

```command
docker cp <Host path> <Container ID>:<Container path>
```

**예:**

::: zone pivot="cs1-bash"
```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
::: zone-end

## <a name="configure-the-timezone"></a><a id="tz"></a> 표준 시간대 구성

특정 표준 시간대의 Linux 컨테이너에서 SQL Server를 실행하려면 `TZ` 환경 변수를 구성합니다. 올바른 표준 시간대 값을 찾으려면 Linux bash 프롬프트에서 `tzselect` 명령을 실행합니다.

```command
tzselect
```

표준 시간대를 선택하면 `tzselect`에서 다음과 비슷한 출력이 표시됩니다.

```output
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

이 정보를 사용하여 Linux 컨테이너에서 동일한 환경 변수를 설정할 수 있습니다. 다음 예제에서는 `Americas/Los_Angeles` 표준 시간대의 컨테이너에서 SQL Server를 실행하는 방법을 보여 줍니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

::: zone pivot="cs1-bash"
```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'A_PASSWORD=<YourStrong!Passw0rd>' \
-p 1433:1433 --name sql1 \
-e 'TZ=America/Los_Angeles'\
-d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
-p 1433:1433 --name sql1 `
-e "TZ=America/Los_Angeles" `
-d mcr.microsoft.com/mssql/server:2017-latest 
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
sudo docker run -e 'ACCEPT_EULA=Y' -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
-p 1433:1433 --name sql1 ^
-e "TZ=America/Los_Angeles" ^
-d mcr.microsoft.com/mssql/server:2017-latest 
```
::: zone-end

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

::: zone pivot="cs1-bash"
```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

## <a name="change-the-default-file-location"></a><a id="changefilelocation"></a> 기본 파일 위치 변경

`MSSQL_DATA_DIR` 변수를 추가하여 `docker run` 명령에서 데이터 디렉터리를 변경한 다음, 컨테이너의 사용자가 액세스할 수 있는 위치에 볼륨을 탑재합니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=MyStrongPassword' -e 'MSSQL_DATA_DIR=/my/file/path' -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e 'ACCEPT_EULA=Y' -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=MyStrongPassword' -e 'MSSQL_DATA_DIR=/my/file/path' -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e 'ACCEPT_EULA=Y' -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

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

- [SQL Server Docker 컨테이너 문제 해결](sql-server-linux-docker-container-troubleshooting.md)

- [SQL Server Docker 컨테이너 보안 유지](sql-server-linux-docker-container-security.md)