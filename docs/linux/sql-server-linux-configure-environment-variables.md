---
title: 환경 변수를 사용 하 여 SQL Server 설정 구성
description: 이 문서에서는 환경 변수를 사용 하 여 Linux에서 특정 SQL Server 2017 설정을 구성 하는 방법을 설명 합니다.
author: VanMSFT
ms.author: vanto
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 51589a2183043c5c8ea8d1f9bf5d4af6fcc1eea3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419252"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Linux에서 환경 변수를 사용 하 여 SQL Server 설정 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

여러 다른 환경 변수를 사용 하 여 Linux에서 SQL Server 2017을 구성할 수 있습니다. 이러한 변수는 다음과 같은 두 가지 시나리오에서 사용 됩니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

여러 다른 환경 변수를 사용 하 여 Linux에서 SQL Server 2019 미리 보기를 구성할 수 있습니다. 이러한 변수는 다음과 같은 두 가지 시나리오에서 사용 됩니다.

::: moniker-end

- `mssql-conf setup` 명령을 사용 하 여 초기 설치를 구성 합니다.
- [Docker에서 새 SQL Server 컨테이너](quickstart-install-connect-docker.md)를 구성 하려면

> [!TIP]
> 이러한 설치 시나리오 후 SQL Server 구성 해야 하 [는 경우 mssql-회의 도구를 사용 하 여 SQL Server on Linux 구성](sql-server-linux-configure-mssql-conf.md)을 참조 하세요.

## <a name="environment-variables"></a>환경 변수

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| 환경 변수 | 설명 |
|-----|-----|
| **ACCEPT_EULA** | [최종 사용자 사용권 계약](https://go.microsoft.com/fwlink/?LinkId=746388) 수락을 확인하기 위해 **ACCEPT_EULA** 변수를 어떤 값에 설정합니다. SQL Server 이미지에 대한 설정을 해야 합니다. |
| **MSSQL_SA_PASSWORD** | SA 사용자 암호를 구성 합니다. |
| **MSSQL_PID** | SQL Server 버전 또는 제품 키를 설정 합니다. 가능한 값은 다음과 같습니다. </br></br>**Evaluation**</br>**개발자**</br>**Express**</br>**웹**</br>**Standard**</br>**Enterprise**</br>**제품 키**</br></br>제품 키를 지정 하는 경우 # # # # #-# # # # #-# # # # #-# # # # #-# # # # #-# # # # #-# # # # # 형식 이어야 합니다. 여기서 ' # '은 숫자 또는 문자입니다.|
| **MSSQL_LCID** | SQL Server에 사용할 언어 ID를 설정 합니다. 예를 들어 1036는 프랑스어입니다. |
| **MSSQL_COLLATION** | SQL Server에 대 한 기본 데이터 정렬을 설정 합니다. 이렇게 하면 언어 id (LCID)의 기본 매핑이 데이터 정렬로 재정의 됩니다. |
| **MSSQL_MEMORY_LIMIT_MB** | SQL Server에서 사용할 수 있는 최대 메모리 크기 (MB)를 설정 합니다. 기본적으로 총 실제 메모리의 80%입니다. |
| **MSSQL_TCP_PORT** | SQL Server 수신 대기 하는 TCP 포트 (기본값 1433)를 구성 합니다. |
| **MSSQL_IP_ADDRESS** | IP 주소를 설정 합니다. 현재 IP 주소는 IPv4 스타일 (0.0.0.0) 이어야 합니다. |
| **MSSQL_BACKUP_DIR** | 기본 백업 디렉터리 위치를 설정 합니다. |
| **MSSQL_DATA_DIR** | 새 SQL Server 데이터베이스 데이터 파일 (.mdf)이 생성 되는 디렉터리를 변경 합니다. |
| **MSSQL_LOG_DIR** | 새 SQL Server 데이터베이스 로그 (.ldf) 파일이 생성 되는 디렉터리를 변경 합니다. |
| **MSSQL_DUMP_DIR** | 기본적으로 SQL Server 메모리 덤프 및 기타 문제 해결 파일을 보관할 디렉터리를 변경 합니다. |
| **MSSQL_ENABLE_HADR** | 가용성 그룹을 사용 하도록 설정 합니다. 예를 들어 ' 1 '은 사용 하도록 설정 되 고 ' 0 '은 사용 하지 않도록 설정 됩니다. |
| **MSSQL_AGENT_ENABLED** | SQL Server 에이전트를 사용 하도록 설정 합니다. 예를 들어 ' t r u e '를 사용 하 고 ' f a l s e '를 사용할 수 없습니다 기본적으로 에이전트는 사용 하지 않도록 설정 되어 있습니다.  |
| **MSSQL_MASTER_DATA_FILE** | Master 데이터베이스 데이터 파일의 위치를 설정 합니다. SQL Server를 처음 실행할 때까지 **master.open** 이라는 이름을 지정 해야 합니다. |
| **MSSQL_MASTER_LOG_FILE** | Master 데이터베이스 로그 파일의 위치를 설정 합니다. SQL Server를 처음 실행할 때까지 이름을 **mastlog.ldf** 로 지정 해야 합니다. |
| **MSSQL_ERROR_LOG_FILE** | 오류 로그 파일의 위치를 설정 합니다. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| 환경 변수 | 설명 |
|-----|-----|
| **ACCEPT_EULA** | [최종 사용자 사용권 계약](https://go.microsoft.com/fwlink/?LinkId=746388) 수락을 확인하기 위해 **ACCEPT_EULA** 변수를 어떤 값에 설정합니다. SQL Server 이미지에 대한 설정을 해야 합니다. |
| **MSSQL_SA_PASSWORD** | SA 사용자 암호를 구성 합니다. |
| **MSSQL_PID** | SQL Server 버전 또는 제품 키를 설정 합니다. 가능한 값은 다음과 같습니다. </br></br>**Evaluation**</br>**개발자**</br>**Express**</br>**웹**</br>**Standard**</br>**Enterprise**</br>**제품 키**</br></br>제품 키를 지정 하는 경우 # # # # #-# # # # #-# # # # #-# # # # #-# # # # #-# # # # #-# # # # # 형식 이어야 합니다. 여기서 ' # '은 숫자 또는 문자입니다.|
| **MSSQL_LCID** | SQL Server에 사용할 언어 ID를 설정 합니다. 예를 들어 1036는 프랑스어입니다. |
| **MSSQL_COLLATION** | SQL Server에 대 한 기본 데이터 정렬을 설정 합니다. 이렇게 하면 언어 id (LCID)의 기본 매핑이 데이터 정렬로 재정의 됩니다. |
| **MSSQL_MEMORY_LIMIT_MB** | SQL Server에서 사용할 수 있는 최대 메모리 크기 (MB)를 설정 합니다. 기본적으로 총 실제 메모리의 80%입니다. |
| **MSSQL_TCP_PORT** | SQL Server 수신 대기 하는 TCP 포트 (기본값 1433)를 구성 합니다. |
| **MSSQL_IP_ADDRESS** | IP 주소를 설정 합니다. 현재 IP 주소는 IPv4 스타일 (0.0.0.0) 이어야 합니다. |
| **MSSQL_BACKUP_DIR** | 기본 백업 디렉터리 위치를 설정 합니다. |
| **MSSQL_DATA_DIR** | 새 SQL Server 데이터베이스 데이터 파일 (.mdf)이 생성 되는 디렉터리를 변경 합니다. |
| **MSSQL_LOG_DIR** | 새 SQL Server 데이터베이스 로그 (.ldf) 파일이 생성 되는 디렉터리를 변경 합니다. |
| **MSSQL_DUMP_DIR** | 기본적으로 SQL Server 메모리 덤프 및 기타 문제 해결 파일을 보관할 디렉터리를 변경 합니다. |
| **MSSQL_ENABLE_HADR** | 가용성 그룹을 사용 하도록 설정 합니다. 예를 들어 ' 1 '은 사용 하도록 설정 되 고 ' 0 '은 사용 하지 않도록 설정 됩니다. |
| **MSSQL_AGENT_ENABLED** | SQL Server 에이전트를 사용 하도록 설정 합니다. 예를 들어 ' t r u e '를 사용 하 고 ' f a l s e '를 사용할 수 없습니다 기본적으로 에이전트는 사용 하지 않도록 설정 되어 있습니다.  |
| **MSSQL_MASTER_DATA_FILE** | Master 데이터베이스 데이터 파일의 위치를 설정 합니다. SQL Server를 처음 실행할 때까지 **master.open** 이라는 이름을 지정 해야 합니다. |
| **MSSQL_MASTER_LOG_FILE** | Master 데이터베이스 로그 파일의 위치를 설정 합니다. SQL Server를 처음 실행할 때까지 이름을 **mastlog.ldf** 로 지정 해야 합니다. |
| **MSSQL_ERROR_LOG_FILE** | 오류 로그 파일의 위치를 설정 합니다. |

::: moniker-end

## <a name="use-with-initial-setup"></a>초기 설치와 함께 사용

이 예제는 `mssql-conf setup` 구성 된 환경 변수를 사용 하 여 실행 됩니다. 다음 환경 변수를 지정 합니다.

- **ACCEPT_EULA** 은 최종 사용자 사용권 계약을 수락 합니다.
- **MSSSQL_PID** 는 비프로덕션 사용을 위해 SQL Server의 무료로 사용이 허가 된 Developer 버전을 지정 합니다.
- **MSSQL_SA_PASSWORD** 는 강력한 암호를 설정 합니다.
- **MSSQL_TCP_PORT** 는 SQL Server 수신 대기 하는 TCP 포트를 1234로 설정 합니다.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>Docker와 함께 사용

이 예의 docker 명령은 다음 환경 변수를 사용 하 여 새 SQL Server 컨테이너를 만듭니다.

- **ACCEPT_EULA** 은 최종 사용자 사용권 계약을 수락 합니다.
- **MSSSQL_PID** 는 비프로덕션 사용을 위해 SQL Server의 무료로 사용이 허가 된 Developer 버전을 지정 합니다.
- **MSSQL_SA_PASSWORD** 는 강력한 암호를 설정 합니다.
- **MSSQL_TCP_PORT** 는 SQL Server 수신 대기 하는 TCP 포트를 1234로 설정 합니다. 즉, 포트 1433 (기본값)을 호스트 포트에 매핑하는 대신 사용자 지정 TCP 포트를이 예제에서 `-p 1234:1234` 명령을 사용 하 여 매핑해야 합니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Linux/macOS에서 Docker를 실행 하는 경우 작은따옴표로 다음 구문을 사용 합니다.

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

Windows에서 Docker를 실행 하는 경우 큰따옴표를 사용 하 여 다음 구문을 사용 합니다.

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

> [!NOTE]
> 컨테이너에서 프로덕션 버전을 실행하는 프로세스는 약간 다릅니다. 자세한 내용은 [프로덕션 컨테이너 이미지 실행](sql-server-linux-configure-docker.md#production)을 참조하세요.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Linux/macOS에서 Docker를 실행 하는 경우 작은따옴표로 다음 구문을 사용 합니다.

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

Windows에서 Docker를 실행 하는 경우 큰따옴표를 사용 하 여 다음 구문을 사용 합니다.

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

## <a name="next-steps"></a>다음 단계

여기에 나열 되지 않은 다른 SQL Server 설정은 [mssql-회의 도구를 사용 하 여 SQL Server on Linux 구성](sql-server-linux-configure-mssql-conf.md)을 참조 하세요.

SQL Server on Linux를 설치 하 고 실행 하는 방법에 대 한 자세한 내용은 [SQL Server on Linux 설치](sql-server-linux-setup.md)를 참조 하세요.
