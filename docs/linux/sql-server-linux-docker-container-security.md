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
ms.openlocfilehash: 60ee13c6715362ba821575a3f8b9f9d5bc3e2bfa
ms.sourcegitcommit: 764f90cf2eeca8451afdea2753691ae4cf032bea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91589332"
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
## <a name="encrypting-connections-to-sql-server-linux-containers"></a>SQL Server Linux 컨테이너에 대한 연결 암호화

SQL Server Linux 컨테이너에 대한 연결을 암호화하려면 요구 사항이 [여기]에 문서화되어 있는 인증서가 필요합니다.

다음은 SQL Server Linux 컨테이너에 대한 연결을 암호화하는 방법의 예입니다. 여기서는 자체 서명된 인증서를 사용합니다. 이러한 환경의 프로덕션 시나리오에는 사용해서는 안되며, CA 인증서를 사용해야 합니다.

1. 테스트 및 비 프로덕션 환경에만 적합한 자체 서명된 인증서를 만듭니다.
  
      ```bash
      openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=sql1.contoso.com' -keyout /container/sql1/mssql.key -out /container/sql1/mssql.pem -days 365
      ```
     여기서 sql1은 SQL 컨테이너의 호스트 이름이므로 이 컨테이너에 연결할 때 연결 문자열에 사용되는 이름은 \'sql1.contoso.com,port\'가 됩니다.

    > [!NOTE]
    > 위의 명령을 실행하기 전에 /container/sql1/ 폴더 경로가 이미 있는지 확인합니다.

2. mssql.key 및 mssql.pem 파일에 올바른 사용 권한을 설정했는지 확인하여 SQL 컨테이너에 파일을 탑재할 때 오류가 발생하지 않도록 합니다.

    ```bash
    chmod 440 /container/sql1/mssql.pem
    chmod 440 /container/sql1/mssql.key
    ```

3. 이제 아래 내용이 포함된 mssql.conf 파일을 생성하여 서버 시작 암호화를 사용하도록 설정합니다. 클라이언트 시작 암호화의 경우 마지막 줄을 'forceencryption = 0\'으로 변경합니다.

    ```bash
    [network]
    tlscert = /etc/ssl/certs/mssql.pem
    tlskey = /etc/ssl/private/mssql.key
    tlsprotocols = 1.2
    forceencryption = 1
    ```

    > [!NOTE]
    > 일부 Linux 배포판의 경우 인증서 및 키를 저장하는 경로는 각각 /etc/pki/tls/certs/ 및 /etc/pki/tls/private/이 될 수도 있습니다. SQL 컨테이너에 대한 mssql.conf를 업데이트하기 전에 경로를 확인하세요. mssql.conf에서 설정한 위치는 컨테이너의 SQL Server가 인증서와 해당 키를 검색할 위치가 됩니다. 이 경우 해당 위치는 /etc/ssl/certs/ 및 /etc/ssl/private/입니다.

    mssql.conf 파일도 동일한 폴더 위치인 /container/sql1/ 아래에 생성됩니다. 위의 단계를 실행한 후에는 sql1 폴더에 mssql.conf, mssql.key 및 mssql.pem의 세 파일이 있어야 합니다.

4. 아래에 표시된 명령을 사용하여 SQL 컨테이너를 배포합니다.

    ```bash
    docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=P@ssw0rd" -p 5434:1433 --name sql1 -h sql1 -v /container/sql1/mssql.conf:/var/opt/mssql/mssql.conf -v   /container/sql1/mssql.pem:/etc/ssl/certs/mssql.pem -v /container/sql1/mssql.key:/etc/ssl/private/mssql.key -d mcr.microsoft.com/mssql/server:2019-latest
    ```

    위의 명령에서 mssql.conf, mssql.pem 및 mssql.key 파일을 컨테이너에 탑재하고 컨테이너의 1433(SQL Server 기본 포트) 포트를 호스트의 5434 포트에 매핑했습니다. 

    > [!NOTE]
    > RHEL 8 이상을 사용하는 경우 \'docker run\' 대신 \'podman run\' 명령을 사용할 수도 있습니다. 

\"클라이언트 컴퓨터에 인증서 등록\" 및 [여기][1]에 설명된 \"연결 문자열 예제\" 섹션에 따라 Linux 컨테이너에서 SQL Server에 대한 연결 암호화를 시작합니다.

  [Encrypting connection to SQL Server Linux]: https://docs.microsoft.com/sql/linux/sql-server-linux-encrypted-connections?view=sql-server-ver15&preserve-view=true
  [여기]: https://docs.microsoft.com/sql/linux/sql-server-linux-encrypted-connections?view=sql-server-ver15&preserve-view=true#requirements-for-certificates
  [1]: https://docs.microsoft.com/sql/linux/sql-server-linux-encrypted-connections?view=sql-server-ver15&preserve-view=true#client-initiated-encryption

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
