---
title: SQL Server on Linux의 환경 변수 구성
description: 이 문서에서는 환경 변수를 사용하여 Linux에서 특정 SQL Server 2017 설정을 구성하는 방법을 설명합니다.
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: f768a79512059025ebd6dfe6a6f339175b6149f3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75558376"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Linux에서 환경 변수를 사용하여 SQL Server 설정 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

여러 다른 환경 변수를 사용하여 Linux에서 SQL Server 2017을 구성할 수 있습니다. 이 변수는 다음과 같은 두 가지 시나리오에서 사용됩니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

여러 다른 환경 변수를 사용하여 Linux에서 SQL Server 2019를 구성할 수 있습니다. 이 변수는 다음과 같은 두 가지 시나리오에서 사용됩니다.

::: moniker-end

- `mssql-conf setup` 명령을 사용하여 초기 설치를 구성합니다.
- [Docker에서 새 SQL Server 컨테이너](quickstart-install-connect-docker.md)를 구성합니다.

> [!TIP]
> 이 설정 시나리오 후에 SQL Server를 구성해야 하는 경우 [mssql-conf tool을 사용하여 SQL Server on Linux 구성](sql-server-linux-configure-mssql-conf.md)을 참조하세요.

## <a name="environment-variables"></a>환경 변수

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| 환경 변수 | Description |
|-----|-----|
| **ACCEPT_EULA** | [최종 사용자 사용권 계약](https://go.microsoft.com/fwlink/?LinkId=746388) 수락을 확인하기 위해 **ACCEPT_EULA** 변수를 어떤 값에 설정합니다. SQL Server 이미지에 대한 설정을 해야 합니다. |
| **MSSQL_SA_PASSWORD** | SA 사용자 암호를 구성합니다. |
| **MSSQL_PID** | SQL Server 버전 또는 제품 키를 설정합니다. 가능한 값은 다음과 같습니다. </br></br>**Evaluation**</br>**개발자**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**제품 키**</br></br>제품 키를 지정하는 경우 #####-#####-#####-#####-##### 형식이어야 합니다. 여기서 '#'은 숫자 또는 문자입니다.|
| **MSSQL_LCID** | SQL Server에 사용할 언어 ID를 설정합니다. 예를 들어 1036은 프랑스어입니다. |
| **MSSQL_COLLATION** | SQL Server에 대한 기본 데이터 정렬을 설정합니다. 이렇게 하면 데이터 정렬에 대한 언어 ID(LCID)의 기본 매핑이 재정의됩니다. |
| **MSSQL_MEMORY_LIMIT_MB** | SQL Server에서 사용할 수 있는 최대 메모리 크기(MB)를 설정합니다. 기본적으로 총 실제 메모리의 80%입니다. |
| **MSSQL_TCP_PORT** | SQL Server가 수신 대기하는 TCP 포트(기본값 1433)를 구성합니다. |
| **MSSQL_IP_ADDRESS** | IP 주소를 설정합니다. 현재 IP 주소는 IPv4 스타일(0.0.0.0)이어야 합니다. |
| **MSSQL_BACKUP_DIR** | 기본 백업 디렉터리 위치를 설정합니다. |
| **MSSQL_DATA_DIR** | 새 SQL Server 데이터베이스 데이터 파일(.mdf)이 생성되는 디렉터리를 변경합니다. |
| **MSSQL_LOG_DIR** | 새 SQL Server 데이터베이스 로그(.ldf) 파일이 생성되는 디렉터리를 변경합니다. |
| **MSSQL_DUMP_DIR** | 기본적으로 SQL Server가 메모리 덤프 및 기타 문제 해결 파일을 보관할 디렉터리를 변경합니다. |
| **MSSQL_ENABLE_HADR** | 가용성 그룹을 사용하도록 설정합니다. 예를 들어 '1'은 사용이고 '0'은 사용 안 함입니다. |
| **MSSQL_AGENT_ENABLED** | SQL Server 에이전트를 사용하도록 설정합니다. 예를 들어 'true'는 사용이고 'false'는 사용 안 함입니다. 기본적으로 에이전트는 사용하지 않도록 설정됩니다.  |
| **MSSQL_MASTER_DATA_FILE** | master 데이터베이스 데이터 파일의 위치를 설정합니다. SQL Server를 처음 실행할 때까지 이름은 **master.mdf**여야 합니다. |
| **MSSQL_MASTER_LOG_FILE** | master 데이터베이스 로그 파일의 위치를 설정합니다. SQL Server를 처음 실행할 때까지 이름은 **master.ldf**여야 합니다. |
| **MSSQL_ERROR_LOG_FILE** | 오류 로그 파일의 위치를 설정합니다. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| 환경 변수 | Description |
|-----|-----|
| **ACCEPT_EULA** | [최종 사용자 사용권 계약](https://go.microsoft.com/fwlink/?LinkId=746388) 수락을 확인하기 위해 **ACCEPT_EULA** 변수를 어떤 값에 설정합니다. SQL Server 이미지에 대한 설정을 해야 합니다. |
| **MSSQL_SA_PASSWORD** | SA 사용자 암호를 구성합니다. |
| **MSSQL_PID** | SQL Server 버전 또는 제품 키를 설정합니다. 가능한 값은 다음과 같습니다. </br></br>**Evaluation**</br>**개발자**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**제품 키**</br></br>제품 키를 지정하는 경우 #####-#####-#####-#####-##### 형식이어야 합니다. 여기서 '#'은 숫자 또는 문자입니다.|
| **MSSQL_LCID** | SQL Server에 사용할 언어 ID를 설정합니다. 예를 들어 1036은 프랑스어입니다. |
| **MSSQL_COLLATION** | SQL Server에 대한 기본 데이터 정렬을 설정합니다. 이렇게 하면 데이터 정렬에 대한 언어 ID(LCID)의 기본 매핑이 재정의됩니다. |
| **MSSQL_MEMORY_LIMIT_MB** | SQL Server에서 사용할 수 있는 최대 메모리 크기(MB)를 설정합니다. 기본적으로 총 실제 메모리의 80%입니다. |
| **MSSQL_TCP_PORT** | SQL Server가 수신 대기하는 TCP 포트(기본값 1433)를 구성합니다. |
| **MSSQL_IP_ADDRESS** | IP 주소를 설정합니다. 현재 IP 주소는 IPv4 스타일(0.0.0.0)이어야 합니다. |
| **MSSQL_BACKUP_DIR** | 기본 백업 디렉터리 위치를 설정합니다. |
| **MSSQL_DATA_DIR** | 새 SQL Server 데이터베이스 데이터 파일(.mdf)이 생성되는 디렉터리를 변경합니다. |
| **MSSQL_LOG_DIR** | 새 SQL Server 데이터베이스 로그(.ldf) 파일이 생성되는 디렉터리를 변경합니다. |
| **MSSQL_DUMP_DIR** | 기본적으로 SQL Server가 메모리 덤프 및 기타 문제 해결 파일을 보관할 디렉터리를 변경합니다. |
| **MSSQL_ENABLE_HADR** | 가용성 그룹을 사용하도록 설정합니다. 예를 들어 '1'은 사용이고 '0'은 사용 안 함입니다. |
| **MSSQL_AGENT_ENABLED** | SQL Server 에이전트를 사용하도록 설정합니다. 예를 들어 'true'는 사용이고 'false'는 사용 안 함입니다. 기본적으로 에이전트는 사용하지 않도록 설정됩니다.  |
| **MSSQL_MASTER_DATA_FILE** | master 데이터베이스 데이터 파일의 위치를 설정합니다. SQL Server를 처음 실행할 때까지 이름은 **master.mdf**여야 합니다. |
| **MSSQL_MASTER_LOG_FILE** | master 데이터베이스 로그 파일의 위치를 설정합니다. SQL Server를 처음 실행할 때까지 이름은 **master.ldf**여야 합니다. |
| **MSSQL_ERROR_LOG_FILE** | 오류 로그 파일의 위치를 설정합니다. |

::: moniker-end

## <a name="use-with-initial-setup"></a>초기 설치와 함께 사용

이 예제에서는 구성된 환경 변수를 사용하여 `mssql-conf setup`을 실행합니다. 다음 환경 변수를 지정합니다.

- **ACCEPT_EULA**는 최종 사용자 사용권 계약에 동의합니다.
- **MSSQL_PID**는 비프로덕션 사용을 위해 SQL Server의 체험용 라이선스 디벨로퍼 버전을 지정합니다.
- **MSSQL_SA_PASSWORD**는 강력한 암호를 설정합니다.
- **MSSQL_TCP_PORT**는 SQL Server가 수신 대기하는 TCP 포트를 1234로 설정합니다.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>Docker와 함께 사용

이 예제 docker 명령은 다음 환경 변수를 사용하여 새 SQL Server 컨테이너를 만듭니다.

- **ACCEPT_EULA**는 최종 사용자 사용권 계약에 동의합니다.
- **MSSQL_PID**는 비프로덕션 사용을 위해 SQL Server의 체험용 라이선스 디벨로퍼 버전을 지정합니다.
- **MSSQL_SA_PASSWORD**는 강력한 암호를 설정합니다.
- **MSSQL_TCP_PORT**는 SQL Server가 수신 대기하는 TCP 포트를 1234로 설정합니다. 즉, 포트 1433(기본값)을 호스트 포트에 매핑하는 대신 이 예제에서는 `-p 1234:1234` 명령을 사용하여 사용자 지정 TCP 포트를 매핑해야 합니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Linux/macOS에서 Docker를 실행하는 경우 작은따옴표와 함께 다음 구문을 사용합니다.

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

Windows에서 Docker를 실행하는 경우 큰따옴표와 함께 다음 구문을 사용합니다.

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

> [!NOTE]
> 컨테이너에서 프로덕션 버전을 실행하는 프로세스는 약간 다릅니다. 자세한 내용은 [프로덕션 컨테이너 이미지 실행](sql-server-linux-configure-docker.md#production)을 참조하세요.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Linux/macOS에서 Docker를 실행하는 경우 작은따옴표와 함께 다음 구문을 사용합니다.

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

Windows에서 Docker를 실행하는 경우 큰따옴표와 함께 다음 구문을 사용합니다.

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

## <a name="next-steps"></a>다음 단계

여기에 나열되지 않은 다른 SQL Server 설정은 [mssql-conf tool을 사용하여 SQL Server on Linux 구성](sql-server-linux-configure-mssql-conf.md)을 참조하세요.

SQL Server on Linux를 설치하고 실행하는 방법에 대한 자세한 내용은 [SQL Server on Linux 설치](sql-server-linux-setup.md)를 참조하세요.
