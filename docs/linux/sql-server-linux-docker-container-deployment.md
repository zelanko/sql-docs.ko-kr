---
title: SQL Server Docker 컨테이너 배포 및 연결
description: Docker 컨테이너에 SQL Server를 배포하는 방법과 컨테이너 내외에서 SQL Server와 연결하는 다양한 도구 설명
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.custom: contperfq1
ms.date: 09/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
zone_pivot_groups: cs1-command-shell
ms.openlocfilehash: 228c5a9f468ad7f82f6ca9c291a532466a5441df
ms.sourcegitcommit: 678f513b0c4846797ba82a3f921ac95f7a5ac863
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2020
ms.locfileid: "89511592"
---
# <a name="deploy-and-connect-to-sql-server-docker-containers"></a>SQL Server Docker 컨테이너 배포 및 연결

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 SQL Server Docker 컨테이너 배포 및 연결 방법을 설명합니다.

기타 배포 시나리오는 다음을 참조하세요.

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Kubernetes - 빅 데이터 클러스터](../big-data-cluster/deploy-get-started.md)

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

## <a name="connect-and-query"></a>연결 및 쿼리

컨테이너 외부나 컨테이너 내에서 컨테이너의 SQL Server를 연결하고 쿼리할 수 있습니다. 다음 섹션에서는 두 시나리오를 모두 설명합니다.

### <a name="tools-outside-the-container"></a>컨테이너 외부 도구

SQL 연결을 지원하는 모든 외부 Linux, Windows 또는 macOS 도구에서 Docker 머신의 SQL Server 인스턴스에 연결할 수 있습니다. 몇 가지 일반적인 도구는 다음과 같습니다.

- [Azure Data Studio](../azure-data-studio/quickstart-sql-server.md)
- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [Windows의 SSMS(SQL Server Management Studio)](sql-server-linux-manage-ssms.md)

다음 예제에서는 **sqlcmd**를 사용하여 Docker 컨테이너에서 실행되는 SQL Server에 연결합니다. 연결 문자열의 IP 주소는 컨테이너를 실행하는 호스트 머신의 IP 주소입니다.

::: zone pivot="cs1-bash"
```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```
::: zone-end

기본값 **1433**이 아닌 호스트 포트를 매핑한 경우 해당 포트를 연결 문자열에 추가합니다. 예를 들어 `docker run` 명령에 `-p 1400:1433`을 지정한 경우 포트 1400을 명시적으로 지정하여 연결합니다.

::: zone pivot="cs1-bash"
```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```
::: zone-end

### <a name="tools-inside-the-container"></a>컨테이너 내부 도구

SQL Server 2017부터 [SQL Server 명령줄 도구](sql-server-linux-setup-tools.md)가 컨테이너 이미지에 포함되었습니다. 대화형 명령 프롬프트를 사용하여 이미지에 연결하는 경우 로컬에서 도구를 실행할 수 있습니다.

1. `docker exec -it` 명령을 사용하여 실행 중인 컨테이너 내에서 대화형 bash 셸을 시작합니다. 다음 예제에서 `e69e056c702d`는 컨테이너 ID입니다.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 항상 전체 컨테이너 ID를 지정할 필요는 없습니다. 고유하게 식별하는 데 충분한 문자만 지정하면 됩니다. 따라서 이 예제에서는 전체 ID가 아닌 `e6` 또는 `e69`만 사용해도 충분할 수 있습니다. 컨테이너 ID를 확인하려면 `docker ps -a` 명령을 실행합니다.

2. 컨테이너 내부로 들어가면 sqlcmd를 사용하여 로컬로 연결합니다. Sqlcmd는 기본적으로 경로에 있지 않으므로 전체 경로를 지정해야 합니다.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. sqlcmd를 마쳤으면 `exit`를 입력합니다.

4. 대화형 명령 프롬프트를 마쳤으면 `exit`를 입력합니다. 컨테이너는 대화형 bash 셸을 종료한 후에도 계속 실행됩니다.

## <a name="check-the-container-version"></a><a id="version"></a> 컨테이너 버전 확인

실행 중인 docker 컨테이너의 SQL Server 버전을 확인하려면 다음 명령을 실행하여 버전을 표시합니다. `<Container ID or name>`을 대상 컨테이너 ID 또는 이름으로 바꿉니다. `<YourStrong!Passw0rd>`를 SA 로그인의 SQL Server 암호로 바꿉니다.

::: zone pivot="cs1-bash"
```bash
sudo docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd \
-S localhost -U SA -P '<YourStrong!Passw0rd>' \
-Q 'SELECT @@VERSION'
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd `
-S localhost -U SA -P "<YourStrong!Passw0rd>" `
-Q "SELECT @@VERSION"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd ^
-S localhost -U SA -P "<YourStrong!Passw0rd>" ^
-Q "SELECT @@VERSION"
```
::: zone-end

대상 docker 컨테이너 이미지의 SQL Server 버전 및 빌드 번호를 확인할 수도 있습니다. 다음 명령은 **mcr.microsoft.com/mssql/server:2017-latest** 이미지의 SQL Server 버전 및 빌드 정보를 표시합니다. 이 작업을 위해 **PAL_PROGRAM_INFO=1** 환경 변수를 사용하여 새 컨테이너를 실행합니다. 생성된 컨테이너는 즉시 종료되고 `docker rm` 명령이 컨테이너를 제거합니다.

::: zone pivot="cs1-bash"
```bash
sudo docker run -e PAL_PROGRAM_INFO=1 --name sqlver \
-ti mcr.microsoft.com/mssql/server:2019-latest && \
sudo docker rm sqlver
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e PAL_PROGRAM_INFO=1 --name sqlver `
-ti mcr.microsoft.com/mssql/server:2019-latest; `
docker rm sqlver
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e PAL_PROGRAM_INFO=1 --name sqlver ^
-ti mcr.microsoft.com/mssql/server:2019-latest && ^
docker rm sqlver
```
::: zone-end

위 명령은 다음 출력과 비슷한 버전 정보를 표시합니다.

```output
sqlservr
  Version 15.0.4063.15
  Build ID 8a3bb4cca325e1d0b3071b3a193f6a1d74b440fbd95d2fb18881651a5b9ec8e8
  Build Type release
  Git Version 0335c462
  Built at Fri Aug 28 04:50:27 GMT 2020

PAL
  Build ID cc5ceea1b3d294f7d0166f99932f98c7eacfaaa81bcd7cf23c6a89f785829b63
  Build Type release
  Git Version ae9d66dff
  Built at Fri Aug 28 04:46:48 GMT 2020

Packages
  system.security                         6.2.9200.10,unset,
  system.certificates                     6.2.9200.10,unset,
  secforwarderxplat                       15.0.4063.15
  sqlservr                                15.0.4063.15
  system.common                           10.0.17134.1246.202005133
  system.netfx                            4.7.2.461814
  system                                  6.2.9200.10,unset,
  sqlagent                                15.0.4063.15
```

## <a name="run-a-specific-sql-server-container-image"></a><a id="tags"></a> 특정 SQL Server 컨테이너 이미지 실행

> [!NOTE]
> SQL Server 2019 CU3부터 Ubuntu 18.04가 지원됩니다. <https://mcr.microsoft.com/v2/mssql/server/tags/list>에서 mssql/server에 사용 가능한 모든 태그 목록을 검색할 수 있습니다.

최신 SQL Server 컨테이너 이미지를 사용하지 않으려는 시나리오도 있습니다. 특정 SQL Server 컨테이너 이미지를 실행하려면 다음 단계를 사용합니다.

1. 사용하려는 릴리스의 Docker **태그**를 확인합니다. 사용 가능한 태그를 보려면 [mssql-server-linux Docker Hub 페이지](https://hub.docker.com/_/microsoft-mssql-server)를 참조하세요.

2. 태그를 사용하여 SQL Server 컨테이너 이미지를 끌어옵니다. 예를 들어 2019-CU7-ubuntu-18.04 이미지를 끌어오려면 다음 명령에서 `<image_tag>`를 `2019-CU7-ubuntu-18.04`로 바꿉니다.

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. 해당 이미지를 사용하여 새 컨테이너를 실행하려면 `docker run` 명령에 태그 이름을 지정합니다. 다음 명령에서 `<image_tag>`를 실행하려는 버전으로 바꿉니다.

   ::: zone pivot="cs1-bash"
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```
   ::: zone-end

이러한 단계를 사용하여 기존 컨테이너를 다운그레이드할 수도 있습니다. 예를 들어 문제 해결이나 테스트를 위해 실행 중인 컨테이너를 롤백 또는 다운그레이드할 수 있습니다. 실행 중인 컨테이너를 다운그레이드하려면 데이터 폴더에 대해 지속성 방법을 사용해야 합니다. [업그레이드 섹션](#upgrade)에 간략하게 설명된 것과 동일한 단계를 수행하지만, 새 컨테이너를 실행할 때 이전 버전의 태그 이름을 지정합니다.

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="run-rhel-based-container-images"></a><a id="rhel"></a> RHEL 기반 컨테이너 이미지 실행

SQL Server Linux 컨테이너 이미지에 대한 문서는 Ubuntu 기반 컨테이너를 가리킵니다. SQL Server 2019부터 RHEL(Red Hat Enterprise Linux)를 기반으로 하는 컨테이너를 사용할 수 있습니다. RHEL에 대한 이미지 예제는 **mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8**과 같을 것입니다.

예를 들어 다음 명령은 RHEL을 사용하는 SQL Server 2019 컨테이너의 누적 업데이트 1을 끌어옵니다.

::: zone pivot="cs1-bash"
```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```
::: zone-end

::: moniker-end

## <a name="run-production-container-images"></a><a id="production"></a> 프로덕션 컨테이너 이미지 실행

이전 섹션의 [빠른 시작](quickstart-install-connect-docker.md)에서는 Docker Hub에서 무료 SQL Server Developer 버전을 실행합니다. 하지만 대부분의 정보는 Enterprise, Standard 또는 Web Edition과 같은 프로덕션 컨테이너 이미지를 실행하려는 경우에도 적용됩니다. 그러나 여기서 설명하는 몇 가지 차이점이 있습니다.

- 유효한 라이선스가 있는 경우에만 프로덕션 환경에서 SQL Server를 사용할 수 있습니다. [여기](https://go.microsoft.com/fwlink/?linkid=857693)서 체험용 SQL Server Express 프로덕션 라이선스를 받을 수 있습니다. SQL Server Standard 및 Enterprise Edition 라이선스는 [Microsoft 볼륨 라이선싱](https://www.microsoft.com/licensing/default.aspx)을 통해 사용할 수 있습니다.

- 프로덕션 버전도 실행하도록 개발자 컨테이너 이미지를 구성할 수 있습니다. 프로덕션 버전을 실행하려면 다음 단계를 사용합니다.

[빠른 시작](quickstart-install-connect-docker.md)에서 요구 사항을 검토하고 절차를 실행합니다. **MSSQL_PID** 환경 변수를 사용하여 프로덕션 버전을 지정해야 합니다. 다음 예제에서는 Enterprise Edition용 최신 SQL Server 2017 컨테이너 이미지를 실행하는 방법을 보여 줍니다.

::: zone pivot="cs1-bash"
```bash
docker run --name sqlenterprise \
-e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
-e 'MSSQL_PID=Enterprise' -p 1433:1433 \
-d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run --name sqlenterprise `
-e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
-e "MSSQL_PID=Enterprise" -p 1433:1433 `
-d "mcr.microsoft.com/mssql/server:2019-latest"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run --name sqlenterprise `
-e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" ^
-e "MSSQL_PID=Enterprise" -p 1433:1433 ^
-d "mcr.microsoft.com/mssql/server:2019-latest"
```
::: zone-end

> [!IMPORTANT]
> **ACCEPT_EULA** 환경 변수에 **Y** 값을 전달하고 **MSSQL_PID**에 버전 값을 전달하면 사용하려는 SQL Server 에디션 및 버전에 유효한 기존 라이선스가 있음을 나타냅니다. 또한 Docker 컨테이너 이미지에서 실행되는 SQL Server 소프트웨어 사용에 SQL Server 사용 조건이 적용되는 것에 동의하게 됩니다.

> [!NOTE]
> **MSSQL_PID**에 사용 가능한 값의 전체 목록은 [Linux에서 환경 변수를 사용하여 SQL Server 설정 구성](sql-server-linux-configure-environment-variables.md)을 참조하세요.

## <a name="run-multiple-sql-server-containers"></a><a id="multiple"></a>여러 SQL Server 컨테이너 실행

Docker는 동일한 호스트 머신에서 여러 SQL Server 컨테이너를 실행하는 방법을 제공합니다. 동일한 호스트에 여러 개의 SQL Server 인스턴스가 필요한 시나리오에서 이 방법을 사용합니다. 각 컨테이너가 다른 포트에 공개되어야 합니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

다음 예제에서는 SQL Server 2017 컨테이너 2개를 만들고 호스트 머신의 **1401** 및 **1402** 포트에 매핑합니다.

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

다음 예제에서는 SQL Server 2019 컨테이너 2개를 만들고 호스트 머신의 **1401** 및 **1402** 포트에 매핑합니다.

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

이제 개별 컨테이너에서 실행되는 SQL Server 인스턴스 2개가 있습니다. 클라이언트는 Docker 호스트의 IP 주소와 컨테이너의 포트 번호를 사용하여 각 SQL Server 인스턴스에 연결할 수 있습니다.

::: zone pivot="cs1-bash"
```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```
::: zone-end

## <a name="upgrade-sql-server-in-containers"></a><a id="upgrade"></a> 컨테이너의 SQL Server 업그레이드

Docker에서 컨테이너 이미지를 업그레이드하려면 먼저 업그레이드 릴리스의 태그를 확인합니다. `docker pull` 명령을 사용하여 레지스트리에서 이 버전을 끌어옵니다.

```command
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

그러면 새로 만든 컨테이너의 SQL Server 이미지가 업데이트되지만 실행 중인 컨테이너의 SQL Server는 업데이트되지 않습니다. 이렇게 하려면 최신 SQL Server 컨테이너 이미지를 사용하여 새 컨테이너를 만들고 데이터를 새 컨테이너로 마이그레이션해야 합니다.

1. 기존 SQL Server 컨테이너에 대해 [데이터 지속성 방법](sql-server-linux-docker-container-configure.md#persist) 중 하나를 사용해야 합니다. 그러면 동일한 데이터를 사용하여 새 컨테이너를 시작할 수 있습니다.

1. `docker stop` 명령을 사용하여 SQL Server 컨테이너를 중지합니다.

1. `docker run`을 사용하여 새 SQL Server 컨테이너를 만들고 매핑된 호스트 디렉터리 또는 데이터 볼륨 컨테이너를 지정합니다. SQL Server 업그레이드의 특정 태그를 사용해야 합니다. 이제 새 컨테이너에서 기존 SQL Server 데이터와 함께 새 SQL Server 버전을 사용합니다.

   > [!IMPORTANT]
   > 업그레이드는 현재 RC1, RC2 및 GA 간에만 지원됩니다.

1. 새 컨테이너의 데이터베이스와 데이터를 확인합니다.

1. 필요에 따라 `docker rm`을 사용하여 이전 컨테이너를 제거합니다.

## <a name="next-steps"></a>다음 단계

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

- [빠른 시작](quickstart-install-connect-docker.md?view=sql-server-2017)을 진행하여 Docker에서 SQL Server 2017 컨테이너 이미지로 시작합니다.

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

- [빠른 시작](quickstart-install-connect-docker.md?view=sql-server-ver15)을 진행하여 Docker에서 SQL Server 2019 컨테이너 이미지로 시작합니다.

::: moniker-end

- [Docker 컨테이너에 대한 추가 구성 및 사용자 지정 참조](sql-server-linux-docker-container-configure.md)

- 리소스, 피드백 및 알려진 문제는 [mssql-docker GitHub 리포지토리](https://github.com/Microsoft/mssql-docker)를 참조하세요.

- [SQL Server Docker 컨테이너 문제 해결](sql-server-linux-docker-container-troubleshooting.md)

- [SQL Server 컨테이너의 고가용성을 살펴봅니다](sql-server-linux-container-ha-overview.md).

- [SQL Server Docker 컨테이너 보안 유지](sql-server-linux-docker-container-security.md)
