---
title: SQL Server Docker 컨테이너 보안 유지
description: SQL Server Docker 컨테이너 보안을 유지하는 다양한 방법 및 컨테이너를 호스트의 다른 루트가 아닌 사용자로 실행하는 방법 이해
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.custom: contperfq1
ms.date: 09/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 10d2eb061a4ee6d9ff9c8d0594561667dd882dc9
ms.sourcegitcommit: 678f513b0c4846797ba82a3f921ac95f7a5ac863
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2020
ms.locfileid: "89511591"
---
# <a name="secure-sql-server-docker-containers"></a>SQL Server Docker 컨테이너 보안 유지

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

SQL Server 2017 컨테이너는 기본적으로 루트 사용자로 시작합니다. 이로 인해 보안 문제가 발생할 수 있습니다. 이 문서에서는 SQL Server Docker 컨테이너를 실행할 때의 보안 옵션 및 SQL Server 컨테이너를 루트가 아닌 사용자로 빌드하는 방법을 설명합니다.

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

    ```bash
    docker exec -it sql1 bash
    ```

    컨테이너 내에서 실행 중인 사용자를 반환하는 `whoami`를 실행합니다.
    
    ```bash
    whoami
    ```

## <a name="run-container-as-a-different-non-root-user-on-the-host"></a><a id="nonrootuser"></a> 컨테이너를 호스트의 루트가 아닌 다른 사용자로 실행

SQL Server 컨테이너를 루트가 아닌 다른 사용자로 실행하려면 docker run 명령에 -u 플래그를 추가합니다. 루트가 아닌 사용자가 액세스할 수 있는 `/var/opt/mssql`에 볼륨이 탑재되지 않은 경우 루트가 아닌 컨테이너를 루트 그룹의 일부로 실행해야 한다는 제한 사항이 있습니다. 루트 그룹은 루트가 아닌 사용자에게 추가 루트 사용 권한을 부여하지 않습니다.

#### <a name="run-as-a-user-with-a-uid-4000"></a>UID 4000을 갖는 사용자로 실행

사용자 지정 UID를 사용하여 SQL Server를 시작할 수 있습니다. 예를 들어, 다음 명령은 UID 4000을 사용하여 SQL Server를 시작합니다.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u 4000:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

> [!Warning]
> SQL Server 컨테이너에 'mssql' 또는 'root'와 같은 명명된 사용자가 있는지 확인합니다. 그렇지 않으면 SQLCMD를 컨테이너 내에서 실행할 수 없습니다. 컨테이너 내에서 `whoami`를 실행하여 SQL Server 컨테이너가 명명된 사용자로 실행되고 있는지 확인할 수 있습니다.

#### <a name="run-the-non-root-container-as-the-root-user"></a>루트가 아닌 컨테이너를 루트 사용자 권한으로 실행

필요한 경우 루트가 아닌 컨테이너를 루트 사용자 권한으로 실행할 수 있습니다. 이 권한이 더 높으므로 컨테이너에 모든 파일 사용 권한이 자동으로 부여됩니다.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -u 0:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

#### <a name="run-as-a-user-on-your-host-machine"></a>호스트 머신에서 사용자로 실행

다음 명령을 사용하여 호스트 머신에서 기존 사용자를 사용하여 SQL Server를 시작할 수 있습니다.
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u $(id -u myusername):0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

#### <a name="run-as-a-different-user-and-group"></a>다른 사용자 및 그룹으로 실행

사용자 지정 사용자 및 그룹을 사용하여 SQL Server를 시작할 수 있습니다. 이 예제에서 탑재된 볼륨에는 호스트 머신의 사용자 또는 그룹에 대해 구성된 사용 권한이 있습니다.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u (id -u myusername):(id -g myusername) -v /path/to/mssql:/var/opt/mssql -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a name="configure-persistent-storage-permissions-for-non-root-containers"></a><a id="storagepermissions"></a> 루트가 아닌 컨테이너에 대한 영구 스토리지 권한 구성

루트가 아닌 사용자가 탑재된 볼륨에 있는 데이터베이스 파일에 액세스할 수 있도록 하려면 컨테이너를 실행하는 사용자 또는 그룹이 영구 파일 스토리지를 읽고 쓸 수 있는지 확인합니다.  

이 명령을 사용하여 데이터베이스 파일의 현재 소유권을 확인할 수 있습니다.

```bash
ls -ll <database file dir>
```

SQL Server에 지속형 데이터베이스 파일에 대한 액세스 권한이 없는 경우 다음 명령 중 하나를 실행합니다.

#### <a name="grant-the-root-group-rw-access-to-the-db-files"></a>루트 그룹에 DB 파일에 대한 r/w 액세스 권한 부여

루트가 아닌 SQL Server 컨테이너가 데이터베이스 파일에 액세스할 수 있도록 루트 그룹에 다음 디렉터리에 대한 권한을 부여합니다.

```bash
chgrp -R 0 <database file dir>
chmod -R g=u <database file dir>
```

#### <a name="set-the-non-root-user-as-the-owner-of-the-files"></a>루트가 아닌 사용자를 파일의 소유자로 설정

이것은 루트가 아닌 기본 사용자이거나 지정하려는 다른 루트가 아닌 사용자일 수 있습니다. 이 예제에서는 UID 10001을 루트가 아닌 사용자로 설정합니다.

```bash
chown -R 10001:0 <database file dir>
```

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

- [SQL Server Docker 컨테이너 문제 해결](sql-server-linux-docker-container-troubleshooting.md)