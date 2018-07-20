---
title: Docker에서 SQL Server 2017에 대 한 구성 옵션 | Microsoft Docs
description: 사용 하 여 SQL Server 2017 컨테이너 이미지 Docker에서 상호 작용 하는 여러 가지를 살펴봅니다. 이 파일을 복사 하 고 문제 해결을 유지 데이터가 포함 됩니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/02/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.custom: sql-linux
ms.openlocfilehash: 420a7577a526ed07f564b762c48e6528db323f08
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085875"
---
# <a name="configure-sql-server-container-images-on-docker"></a>Docker에서 SQL Server 컨테이너 이미지를 구성 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 구성 및 사용 하는 방법을 설명 합니다 [mssql server linux 컨테이너 이미지](https://hub.docker.com/r/microsoft/mssql-server-linux/) Docker를 사용 하 여 합니다. 이 이미지는 Ubuntu 16.04 기반 Linux에서 실행 중인 SQL Server로 구성됩니다. Linux 또는 Mac/Windows용 Docker에서 Docker Engine 1.8+와 함께 사용할 수 있습니다.

> [!NOTE]
> 이 문서에서는 mssql server linux 이미지를 사용 하 여 특별히 중점을 둡니다. Windows 이미지는 다루지 않지만에서 자세히 알아보십시오 합니다 [mssql server windows Docker 허브 페이지](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)합니다.

## <a name="pull-and-run-the-container-image"></a>컨테이너 이미지를 끌어와 실행하기

끌어오고 SQL Server 2017 Docker 컨테이너 이미지를 실행 하려면 필수 구성 요소 및 다음 빠른 시작의 단계를 수행 합니다.

- [Docker를 사용 하 여 SQL Server 2017 컨테이너 이미지 실행](quickstart-install-connect-docker.md)

이 구성 문서의 다음 섹션에 대 한 추가 시나리오를 제공합니다.

## <a id="production"></a> 프로덕션 컨테이너 이미지 실행

Docker 허브에서 무료 개발자 버전의 SQL Server를 실행 하는 이전 섹션에서 빠른 시작 합니다. 대부분의 정보에는 프로덕션 Enterprise, Standard 또는 Web 버전 같은 컨테이너 이미지를 실행 하려는 경우 여전히 적용 됩니다. 그러나 여기서 설명 하는 몇 가지 차이점이 있습니다.

- 유효한 라이선스가 있는 경우 SQL Server 프로덕션 환경에서 사용할 수 있습니다. 무료 SQL Server Express 프로덕션 라이선스를 가져올 수 있습니다 [여기](https://go.microsoft.com/fwlink/?linkid=857693)합니다. 통해 사용할 수 있는 SQL Server Standard 및 Enterprise Edition 라이선스 [Microsoft Volume Licensing](https://www.microsoft.com/en-us/licensing/default.aspx)합니다.

- 프로덕션 SQL Server 컨테이너 이미지를 끌어와야 [Docker 저장소](https://store.docker.com)합니다. 이미 없는, 하는 경우 Docker 저장소 계정을 만듭니다.

- 도 프로덕션 버전을 실행 하려면 Docker 스토어에서 개발자 컨테이너 이미지를 구성할 수 있습니다. 프로덕션 버전을 실행 하려면 다음 단계를 사용 합니다.

   1. 먼저 로그인 docker id 명령줄에서.

      ```bash
      docker login
      ```

   1. 다음으로, 컨테이너 이미지 Docker 스토어에서 무료 개발자를 가져올 해야 합니다. 로 이동 [ https://store.docker.com/images/mssql-server-linux ](https://store.docker.com/images/mssql-server-linux), 클릭 **결제로 진행 한**, 지침을 따릅니다.

   1. 프로시저를 실행 하 고 요구 사항을 검토 합니다 [퀵 스타트](quickstart-install-connect-docker.md)합니다. 하지만 두 가지 차이점이 있습니다. 이미지를 가져와야 **저장소/microsoft/mssql-서버-linux:\<태그 이름\>**  Docker 저장소에서. 사용 하 여 프로덕션 버전을 지정 해야 합니다 **MSSQL_PID** 환경 변수입니다. 다음 예제에서는 Enterprise Edition에 대 한 최신 SQL Server 2017 컨테이너 이미지를 실행 하는 방법을 보여 줍니다.

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
      > 값을 전달 하 여 **Y** 환경 변수에 **ACCEPT_EULA** 과 버전 값을 **MSSQL_PID**를 유효 하 고 기존 라이선스를 있다고 표현 됩니다 버전 및 사용 하려는 SQL Server의 버전입니다. 또한는 Docker 컨테이너 이미지가 실행 되는 SQL Server 소프트웨어의 사용 받습니다 SQL Server 라이선스 조건에 동의 합니다.

      > [!NOTE]
      > 에 대 한 가능한 값의 전체 목록은 **MSSQL_PID**를 참조 하세요 [Linux의 환경 변수를 사용 하 여 SQL Server 구성 설정](sql-server-linux-configure-environment-variables.md)합니다.

## <a name="connect-and-query"></a>연결 및 쿼리

컨테이너 내에서 또는 컨테이너 외부에서에서 SQL Server 쿼리를 연결할 수는 컨테이너입니다. 다음 섹션에서는 두 시나리오 모두에 대해 설명 합니다. 

### <a name="tools-outside-the-container"></a>컨테이너 외부 도구

SQL 연결을 지 원하는 모든 외부 Linux, Windows, 또는 macOS 도구에서 Docker 컴퓨터에 SQL Server 인스턴스에 연결할 수 있습니다. 일부 일반 도구는 다음과 같습니다.

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [Windows의 SSMS(SQL Server Management Studio)](sql-server-linux-manage-ssms.md)

다음 예제에서는 **sqlcmd** Docker 컨테이너에서 실행 중인 SQL Server에 연결 합니다. 연결 문자열에서 IP 주소는 컨테이너를 실행 하는 호스트 컴퓨터의 IP 주소가입니다.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

기본 되지 않은 호스트 포트를 매핑한 **1433**, 연결 문자열에 해당 포트를 추가 합니다. 예를 들어 지정한 `-p 1400:1433` 에서 프로그램 `docker run` 명령을 사용한 다음, 명시적으로 연결 하 여 1400 포트를 지정 합니다.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>컨테이너 내에서 도구

SQL Server 2017 CTP 2.0을 사용 하 여 시작 합니다 [SQL Server 명령줄 도구](sql-server-linux-setup-tools.md) 컨테이너 이미지에 포함 됩니다. 대화형 명령 프롬프트를 사용 하 여 이미지를 연결 하는 경우 도구를 로컬로 실행할 수 있습니다.

1. `docker exec -it` 명령을 사용하여 실행 중인 컨테이너 내에서 대화형 bash 셸을 시작합니다. 다음 예에서 `e69e056c702d` 컨테이너 ID입니다.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 항상 전체 컨테이너 id를 지정할 필요가 없습니다. 고유 하 게 식별에 필요한 만큼의 문자를 지정 해야 합니다. 이 예제에서는 수 있으므로 사용 하기에 충분 `e6` 또는 `e69` 전체 id 대신 합니다.

2. 컨테이너 내부로 들어가면 sqlcmd를 사용하여 로컬로 연결합니다. Note는 sqlcmd 아니므로 기본적으로 경로에 전체 경로 지정 해야 합니다.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Sqlcmd를 사용 하 여 완료 되 면 입력 `exit`합니다.

4. 대화형 명령 프롬프트를 사용 하 여 완료 되 면 입력 `exit`합니다. 컨테이너는 대화형 bash 셸을 종료한 후에도 계속 실행됩니다.

## <a name="run-multiple-sql-server-containers"></a>여러 SQL Server 컨테이너를 실행 합니다.

Docker는 동일한 호스트 컴퓨터에서 여러 SQL Server 컨테이너를 실행 하는 방법을 제공 합니다. 이 동일한 호스트에서 SQL Server의 여러 인스턴스를 필요로 하는 시나리오에 대 한 방법입니다. 각 컨테이너는 다른 포트에서 자체를 노출 해야 합니다.

다음 예제에서는 두 개의 SQL Server 컨테이너를 만들어 포트로 매핑합니다 **1401** 하 고 **1402** 호스트 컴퓨터에서.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:2017-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d microsoft/mssql-server-linux:2017-latest
```

이제 별도 컨테이너에서 실행 중인 SQL Server의 두 인스턴스가 있습니다. 클라이언트는 컨테이너용 Docker 호스트 및 포트 번호의 IP 주소를 사용 하 여 각 SQL Server 인스턴스에 연결할 수 있습니다.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```
## <a id="customcontainer"></a> 사용자 지정된 컨테이너 만들기

사용자가 직접 만들 수 있기 [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) 사용자 지정 된 SQL Server 컨테이너를 만들려고 합니다. 자세한 내용은 [SQL Server 및 Node 응용 프로그램을 결합 하는 데모](https://github.com/twright-msft/mssql-node-docker-demo-app)합니다. 이 프로세스는 컨테이너의 수명 제어 하기 때문에 사용자 고유의 Dockerfile을 만든 경우 포그라운드 프로세스가 고려해 야 합니다. 종료 될 경우 컨테이너를 종료 합니다. 예를 들어 스크립트를 실행 하 고 SQL Server를 시작 하려는 경우 SQL Server 프로세스의 가장 오른쪽 명령 인지 확인 합니다. 다른 모든 명령은 백그라운드에서 실행 됩니다. 이 Dockerfile 내에서 다음 명령을 보여 줍니다.

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

이전 예의 명령은 반대로 수행-내-sql-commands.sh 스크립트가 완료 되 컨테이너 종료를 것입니다.

## <a id="persist"></a> 데이터를 유지 합니다.

SQL Server 구성 변경과 데이터베이스 파일에에서 유지 되는 컨테이너와 컨테이너를 다시 시작 하는 경우에 `docker stop` 고 `docker start`입니다. 그러나 사용 하 여 컨테이너를 제거 하면 `docker rm`, 컨테이너의 모든 삭제 된 SQL Server 데이터베이스를 포함 합니다. 다음 섹션을 사용 하는 방법에 설명 **데이터 볼륨** 관련된 컨테이너 삭제 되는 경우에 데이터베이스 파일을 유지 합니다.

> [!IMPORTANT]
> 이 SQL Server 용 Docker에서 데이터 지 속성을 이해 하는 중요 합니다. 이 단원의 내용은 외에도 Docker의 설명서를 참조 [Docker 컨테이너에서 데이터를 관리 하는 방법](https://docs.docker.com/engine/tutorials/dockervolumes/)합니다.

### <a name="mount-a-host-directory-as-data-volume"></a>데이터 볼륨으로 호스트 디렉터리 탑재

첫 번째 방법은 호스트에서 컨테이너의 데이터 볼륨으로 디렉터리를 탑재 하는 것입니다. 이 작업을 수행 하려면 사용 합니다 `docker run` 명령과 `-v <host directory>:/var/opt/mssql` 플래그. 따라서 데이터를 컨테이너 실행 간에 복원할 수 있습니다.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
```

또한이 기술을 공유 하 고 외부 Docker 호스트의 파일을 볼 수 있습니다.

> [!IMPORTANT]
> 이 이번에는 Linux 이미지에서 SQL Server를 사용 하 여 Mac에서 docker 호스트 볼륨 매핑이 지원 되지 않습니다. 데이터 볼륨 컨테이너를 대신 사용 합니다. 이 제한은 관련 된 `/var/opt/mssql` 디렉터리입니다. 탑재 디렉터리 작동을 읽기만 합니다. 예를 들어, – v를 사용 하 여 Mac의 호스트 디렉터리 탑재 하 고 호스트에 상주 하는.bak 파일에서 백업 복원 수 있습니다.

### <a name="use-data-volume-containers"></a>데이터 볼륨 컨테이너를 사용 합니다.

두 번째 옵션은 데이터 볼륨 컨테이너를 사용 하는 것입니다. 사용 하 여 호스트 디렉터리 대신 볼륨 이름을 지정 하 여 데이터 볼륨 컨테이너를 만들 수 있습니다는 `-v` 매개 변수입니다. 다음 예제에서는 명명 된 공유 데이터 볼륨을 만듭니다 **sqlvolume**합니다.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
```

> [!NOTE]
> 이전 버전의 Docker 사용 하 여 암시적으로 실행된 명령에서 데이터 볼륨을 만들기 위한이 기술 작동 하지 않습니다. 이런 경우 Docker 설명서에 설명 된 단계를 사용 하 여 [만들기 및 데이터 볼륨 컨테이너를 탑재](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container)합니다.

중지 하 고이 컨테이너를 제거 하는 경우에 데이터 볼륨을 유지 합니다. 사용 하 여 볼 수 있습니다는 `docker volume ls` 명령입니다.

```bash
docker volume ls
```

볼륨 이름이 같은 다른 컨테이너를 만든 경우 새 컨테이너는 동일한 SQL Server에에서 포함 된 데이터 볼륨을 사용 합니다.

데이터 볼륨 컨테이너를 제거 하려면 사용 된 `docker volume rm` 명령입니다.

> [!WARNING]
> 데이터 볼륨 컨테이너를 삭제 하면 모든 SQL Server 컨테이너의 데이터가 *영구적으로* 삭제 합니다.

### <a name="backup-and-restore"></a>Backup 및 Restore 메서드

이러한 컨테이너 기술 외에도 표준 SQL Server backup을 사용 하 고 복원 기술도 수 있습니다. 데이터를 보호 하기 위해 또는 다른 SQL Server 인스턴스로 데이터를 이동 하려면 백업 파일을 사용할 수 있습니다. 자세한 내용은 [Linux에서 SQL Server 데이터베이스 백업 및 복원](sql-server-linux-backup-and-restore-database.md)합니다.

> [!WARNING]
> 백업을 만든 경우에를 만들거나 컨테이너의 외부 백업 파일을 복사 해야 합니다. 이 고, 그렇지 컨테이너 제거 되 면 백업 파일이 삭제 됩니다.

## <a name="execute-commands-in-a-container"></a>컨테이너에서 명령 실행

실행 중인 컨테이너에 있는 경우 터미널 호스트에서 컨테이너 내에서 명령을 실행할 수 있습니다.

실행 컨테이너 ID를 가져오려면:

```bash
docker ps
```

Bash 터미널을 실행 하는 컨테이너에 시작 합니다.

```bash
docker exec -ti <Container ID> /bin/bash
```

이제 컨테이너 내에서 터미널에서 실행 중인 것 처럼 명령을 실행할 수 있습니다. 완료되면 `exit`을 입력합니다. 대화형 명령 세션에서이 종료 하지만 컨테이너가 계속 실행 됩니다.

## <a name="copy-files-from-a-container"></a>컨테이너에서 파일을 복사 합니다.

컨테이너에서 파일을 복사 하려면 다음 명령을 사용 합니다.

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

## <a name="copy-files-into-a-container"></a>컨테이너에 파일을 복사 합니다.

컨테이너에 파일을 복사, 다음 명령을 사용 합니다.

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

## <a name="run-a-specific-sql-server-container-image"></a>특정 SQL Server 컨테이너 이미지 실행

여기서 최신 SQL Server 컨테이너 이미지를 사용 하려는 하지 시나리오가 있습니다. 특정 SQL Server 컨테이너 이미지를 실행 하려면 다음 단계를 사용 합니다.

1. Docker를 식별 **태그** 사용 하려는 릴리스에 대 한 합니다. 사용 가능한 태그를 보려면 [mssql server linux Docker 허브 페이지](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/)합니다.

1. 태그를 사용 하 여 SQL Server 컨테이너 이미지를 끌어옵니다. 예를 들어 이미지를 가져와 RC1을 대체할 `<image_tag>` 사용 하 여 다음 명령에서 `rc1`합니다.

   ```bash
   docker pull microsoft/mssql-server-linux:<image_tag>
   ```

1. 새 컨테이너 이미지를 사용 하 여를 실행 하려면에 태그 이름을 지정 합니다 `docker run` 명령입니다. 다음 명령에서 `<image_tag>` 실행 하려는 버전을 사용 하 여 합니다.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
   ```

이러한 단계는 기존 컨테이너를 다운 그레이드 하려면 데도 사용할 수 있습니다. 예를 들어 롤백하려면 하거나 문제 해결 또는 테스트에 대 한 실행 중인 컨테이너를 다운 그레이드할 수 있습니다. 실행 중인 컨테이너를 다운 그레이드 하려면 사용 해야 하는 지 속성 기술 데이터 폴더에 대 한 합니다. 에 설명 된 동일한 단계를 수행 합니다 [업그레이드 섹션](#upgrade), 새 컨테이너를 실행 하면 이전 버전의 태그 이름을 지정 합니다.

> [!IMPORTANT]
> 업그레이드 및 다운 그레이드 지금은 RC1 및 RC2 간의 지원만 됩니다.

## <a id="version"></a> 컨테이너 버전 확인

실행 중인 docker 컨테이너에서 SQL Server의 버전을 알면 하려는 경우에 표시 하려면 다음 명령을 실행 합니다. 대체 `<Container ID or name>` 대상 컨테이너 ID 또는 이름입니다. 대체 `<YourStrong!Passw0rd>` SA 로그인에 대 한 SQL Server 암호를 사용 합니다.

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

SQL Server 버전을 식별 하 고 빌드 대상 docker 컨테이너 이미지에 대 한 번호 수도 있습니다. 다음 명령은 표시에 대 한 SQL Server 버전 및 빌드 정보를 **microsoft/mssql-서버-linux: 2017-최신** 이미지입니다. 환경 변수를 사용 하 여 새 컨테이너를 실행 하 여 이렇게 **PAL_PROGRAM_INFO = 1**합니다. 결과 컨테이너 즉시 종료 하며 `docker rm` 명령을 제거 합니다.

```bash
sudo docker run -e PAL_PROGRAM_INFO=1 --name sqlver \
   -ti microsoft/mssql-server-linux:2017-latest && \
   sudo docker rm sqlver
```

```PowerShell
docker run -e PAL_PROGRAM_INFO=1 --name sqlver `
   -ti microsoft/mssql-server-linux:2017-latest; `
   docker rm sqlver
```

다음 출력과 유사한 버전 정보를 표시 하는 이전 명령:

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

## <a id="upgrade"></a> 컨테이너에서 SQL Server 업그레이드

Docker 사용 하 여 컨테이너 이미지를 업그레이드 하려면 먼저 업그레이드에 대 한 릴리스에 대 한 태그를 식별 합니다. 이 버전을 사용 하 여 레지스트리에서 끌어오기는 `docker pull` 명령:

```bash
docker pull microsoft/mssql-server-linux:<image_tag>
```

SQL Server 이미지를 만든 모든 새 컨테이너를 업데이트 하지만 실행 중인 모든 컨테이너에서 SQL Server를 업데이트 하지 않습니다. 이렇게 하려면 최신 SQL Server 컨테이너 이미지를 사용 하 여 새 컨테이너를 만듭니다를 해당 새 컨테이너에 데이터를 마이그레이션.

1. 하나를 사용 하 고 있는지 확인 합니다 [데이터 지 속성 기술을](#persist) 기존 SQL Server 컨테이너에 대 한 합니다. 이 옵션을 사용 하면 동일한 데이터를 사용 하 여 새 컨테이너를 시작할 수 있습니다.

1. SQL Server 컨테이너를 중지 합니다 `docker stop` 명령입니다.

1. 사용 하 여 새 SQL Server 컨테이너를 만들고 `docker run` 매핑된 호스트 디렉터리 또는 데이터 볼륨 컨테이너를 지정 합니다. SQL Server 업그레이드에 대 한 특정 태그를 사용 해야 합니다. 이제 새 컨테이너는 기존 SQL Server 데이터를 사용 하 여 새 버전의 SQL Server를 사용합니다.

   > [!IMPORTANT]
   > 업그레이드는 지금 GA, RC1 및 RC2 사이 지원 됩니다.

1. 데이터베이스 및 새 컨테이너에 데이터를 확인 합니다.

1. 필요에 따라 사용 하 여 기존 컨테이너를 제거 `docker rm`합니다.

## <a id="troubleshooting"></a> 문제 해결

다음 섹션에서는 컨테이너에서 SQL Server를 실행 하기 위한 문제 해결 제안 사항을 제공 합니다.

### <a name="docker-command-errors"></a>Docker 명령 오류

에 대 한 오류가 발생할 경우 `docker` 명령을 docker 서비스가 실행 중인지 확인 하 고 관리자 권한으로 실행 하려고 합니다.

예를 들어 linux에서 오류가 발생할 수 있습니다는 다음 실행 하는 경우 `docker` 명령:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Linux에서이 오류를 받게 되 면 앞과 동일한 명령을 실행 하십시오 `sudo`합니다. 실패할 경우 docker 서비스가 실행 되 고 필요한 경우 시작을 확인 합니다.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

Windows에는 시작 하는 PowerShell 또는 관리자 권한으로 명령 프롬프트를 확인 합니다.

### <a name="sql-server-container-startup-errors"></a>SQL Server 컨테이너 시작 오류

SQL Server 컨테이너를 실행 하지 못하는 경우에 다음 테스트를 시도해 보세요.

- 와 같은 오류가 발생할 경우 **' 네트워크 브리지에서 CONTAINER_NAME 끝점을 만들지 못했습니다. 프록시 시작 오류: 수신 tcp 0.0.0.0:1433 바인딩: 이미 사용 중인 주소입니다.'** , 컨테이너 포트 1433을 이미 사용 중인 포트를 매핑할 하려고 합니다. 이 호스트 컴퓨터에서 로컬로 SQL Server를 실행 하는 경우 발생할 수 있습니다. 두 SQL Server 컨테이너를 시작 하 고 둘 다 동일한 호스트 포트 매핑을 시도 하는 경우에 발생할 수 있습니다. 사용 하 여 이런 경우는 `-p` 매개 변수를 다른 호스트 포트에 컨테이너 포트 1433을 매핑합니다. 예를 들어: 

    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d microsoft/mssql-server-linux:2017-latest`.
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d microsoft/mssql-server-linux:2017-latest`.
    ```

- 컨테이너에서 모든 오류 메시지가 있는지 확인 합니다.

    ```bash
    docker logs e69e056c702d
    ```

- 에 지정 된 최소 메모리 및 디스크 요구 사항을 충족 해야 합니다 [요구 사항](#requirements) 이 문서의 섹션입니다.

- 컨테이너 관리 소프트웨어를 사용 하는 경우 루트로 실행 중인 컨테이너 프로세스를 지원 해야 합니다. Sqlservr 프로세스 컨테이너의 루트로 실행합니다.

- 검토 합니다 [SQL Server 설치 및 오류 로그](#errorlogs)합니다.

### <a name="enable-dump-captures"></a>덤프 캡처를 사용 하도록 설정

SQL Server 프로세스를 컨테이너 내에서 실패 하는 경우 사용 하 여 새 컨테이너를 만들어야 **SYS_PTRACE** 사용 하도록 설정 합니다. 이 예외는 덤프 파일을 만드는 데 필요 하는 프로세스를 추적 하는 Linux 기능을 추가 합니다. 덤프 파일 문제를 해결 하려면 기술 지원 서비스에서 사용할 수 있습니다. 이 기능을 사용 하는 다음 docker 명령을 실행 합니다.

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux:2017-latest
```

### <a name="sql-server-connection-failures"></a>SQL Server 연결 실패

컨테이너에서 실행 중인 SQL Server 인스턴스에 연결할 수 없으면, 다음 테스트를 시도해 보세요.

- 확인 하 여 SQL Server 컨테이너가 실행 되 고 있는지 확인 합니다 **상태** 열의 `docker ps -a` 출력 합니다. 그렇지 않으면 `docker start <Container ID>` 시작 합니다.

- 기본이 아닌 호스트 포트 (1433)에 매핑된 경우 연결 문자열에 포트를 지정 하는 있는지 확인 합니다. 에 포트 매핑을 볼 수 있습니다 합니다 **포트** 열을 `docker ps -a` 출력 합니다. 예를 들어 다음 명령은 포트 1401에서 수신 대기 하는 컨테이너에 sqlcmd를 연결 합니다.

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- 사용 하는 경우 `docker run` 기존 매핑된 데이터 볼륨 또는 데이터 볼륨 컨테이너를 사용 하 여 SQL Server의 값을 무시 `MSSQL_SA_PASSWORD`합니다. 대신, 데이터 볼륨 또는 데이터 볼륨 컨테이너에서 SQL Server 데이터에서 미리 구성 된 SA 사용자 암호가 사용 됩니다. 에 연결 하는 데이터와 관련 된 SA 암호를 사용 하 고 있는지 확인 합니다.

- 검토 합니다 [SQL Server 설치 및 오류 로그](#errorlogs)합니다.

### <a name="sql-server-availability-groups"></a>SQL Server 가용성 그룹

SQL Server 가용성 그룹을 사용 하 여 Docker를 사용 중인 경우 두 가지 추가 요구 사항이 있습니다.

- (기본값 5022) 복제본 통신에 사용 되는 포트를 매핑하십시오. 예를 들어 지정할 `-p 5022:5022` 의 일부로 프로그램 `docker run` 명령입니다.

- 명시적으로 사용 하 여 컨테이너 호스트 이름을 설정 합니다 `-h YOURHOSTNAME` 의 매개 변수는 `docker run` 명령입니다. 가용성 그룹을 구성할 때이 호스트 이름이 사용 됩니다. 사용 하 여 지정 하지 않으면 `-h`, 컨테이너 id입니다. 기본값은

### <a id="errorlogs"></a> SQL Server 설치 및 오류 로그

SQL Server 설치 프로그램을 살펴볼 수 있습니다 하 고 오류 로그인 **/var/opt/mssql/log**합니다. 컨테이너를 실행 하지 않는 경우 먼저 컨테이너를 시작 합니다. 다음 로그를 검사 하는 대화형 명령 프롬프트를 사용 합니다.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

컨테이너 내에서 bash 세션에서 다음 명령을 실행 합니다.

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> 호스트 디렉터리를 탑재 하는 경우 **/var/opt/mssql** 컨테이너를 만들 때을 대신 참조를 **로그** 호스트에서 매핑된 경로에 하위 디렉터리입니다.

## <a name="next-steps"></a>다음 단계

통해 이동 하 여 Docker에서 SQL Server 2017 컨테이너 이미지를 사용 하 여 시작 합니다 [퀵 스타트](quickstart-install-connect-docker.md)합니다.

참고: 합니다 [mssql docker GitHub 리포지토리](https://github.com/Microsoft/mssql-docker) 리소스, 피드백 및 알려진된 문제에 대 한 합니다.
