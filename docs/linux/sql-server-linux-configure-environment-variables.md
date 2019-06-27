---
title: 환경 변수를 사용 하 여 SQL Server 설정 구성 | Microsoft Docs
description: 이 문서에서는 Linux에서 특정 SQL Server 2017 설정을 구성 하려면 환경 변수를 사용 하는 방법을 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 2b32c965dfed3647484a1de54539c79af3777ce4
ms.sourcegitcommit: 65ceea905030582f8d89e75e97758abf3b1f0bd6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67400075"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Linux의 환경 변수를 사용 하 여 SQL Server 설정 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Linux에서 SQL Server 2017을 구성 하려면 몇 가지 다른 환경 변수를 사용할 수 있습니다. 이러한 변수는 두 가지 시나리오에서 사용 됩니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Linux에서 SQL Server 2019 미리 보기를 구성 하려면 몇 가지 다른 환경 변수를 사용할 수 있습니다. 이러한 변수는 두 가지 시나리오에서 사용 됩니다.

::: moniker-end

- 사용 하 여 초기 설치를 구성 하는 `mssql-conf setup` 명령입니다.
- 새 구성 하려면 [Docker에서 SQL Server 컨테이너](quickstart-install-connect-docker.md)합니다.

> [!TIP]
> 이러한 설치 시나리오 후 SQL Server를 구성 하는 경우 참조 [mssql-conf 도구를 사용 하 여 Linux에서 SQL Server 구성](sql-server-linux-configure-mssql-conf.md)합니다.

## <a name="environment-variables"></a>환경 변수

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| 환경 변수 | Description |
|-----|-----|
| **ACCEPT_EULA** | 모든 값 (예: ' Y')로 설정 하면 SQL Server 사용권 계약에 동의 합니다. |
| **MSSQL_SA_PASSWORD** | SA 사용자 암호를 구성 합니다. |
| **MSSQL_PID** | SQL Server 버전 또는 제품 키를 설정 합니다. 가능한 값은 다음과 같습니다. </br></br>**Evaluation**</br>**개발자**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**제품 키**</br></br>제품 키를 지정 하는 경우 # # #-# # #-# # #-# # #-# # #, '#'은 숫자 이거나 문자 형식에서 이어야 합니다.|
| **MSSQL_LCID** | SQL Server에 사용할 언어 ID를 설정 합니다. 예를 들어 1036 프랑스어가 있습니다. |
| **MSSQL_COLLATION** | SQL Server에 대 한 기본 데이터 정렬을 설정합니다. 이 언어 id (LCID) 데이터 정렬의 기본 매핑을 재정의합니다. |
| **MSSQL_MEMORY_LIMIT_MB** | 최대 메모리 (MB) SQL Server에서 사용할 수 있는 설정입니다. 기본적으로 총 실제 메모리의 80%는 것입니다. |
| **MSSQL_TCP_PORT** | SQL Server (기본값 1433)를 수신 하는 TCP 포트를 구성 합니다. |
| **MSSQL_IP_ADDRESS** | IP 주소를 설정 합니다. 현재 IP 주소는 IPv4 스타일 (0.0.0.0) 이어야 합니다. |
| **MSSQL_BACKUP_DIR** | 기본 백업 디렉터리 위치를 설정 합니다. |
| **MSSQL_DATA_DIR** | 새 SQL Server 데이터베이스 데이터 파일 (.mdf) 만들어지는 디렉터리를 변경 합니다. |
| **MSSQL_LOG_DIR** | 새 SQL Server 데이터베이스 로그 (.ldf) 파일이 만들어지는 디렉터리를 변경 합니다. |
| **MSSQL_DUMP_DIR** | 여기서 SQL Server를 맡 메모리 덤프 및 기타 문제 해결 파일 기본적으로 디렉터리를 변경 합니다. |
| **MSSQL_ENABLE_HADR** | 가용성 그룹을 사용 하도록 설정 합니다. 예를 들어, '1'을 사용 하 고 '0'은 사용할 수 없습니다. |
| **MSSQL_AGENT_ENABLED** | SQL Server 에이전트를 사용 하도록 설정 합니다. 예를 들어, 'true' 켜져 있고 'f a l'은 사용 하지 않도록 설정 합니다. 기본적으로 에이전트를 비활성화 합니다.  |
| **MSSQL_MASTER_DATA_FILE** | Master 데이터베이스 데이터 파일의 위치를 설정합니다. 이름을 지정 해야 합니다 **master.mdf** SQL Server를 처음 실행 될 때까지 합니다. |
| **MSSQL_MASTER_LOG_FILE** | Master 데이터베이스 로그 파일의 위치를 설정합니다. 이름을 지정 해야 합니다 **mastlog.ldf** SQL Server를 처음 실행 될 때까지 합니다. |
| **MSSQL_ERROR_LOG_FILE** | 오류 로그 파일의 위치를 설정합니다. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| 환경 변수 | Description |
|-----|-----|
| **ACCEPT_EULA** | 모든 값 (예: ' Y')로 설정 하면 SQL Server 사용권 계약에 동의 합니다. |
| **MSSQL_SA_PASSWORD** | SA 사용자 암호를 구성 합니다. |
| **MSSQL_PID** | SQL Server 버전 또는 제품 키를 설정 합니다. 가능한 값은 다음과 같습니다. </br></br>**Evaluation**</br>**개발자**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**제품 키**</br></br>제품 키를 지정 하는 경우 # # #-# # #-# # #-# # #-# # #, '#'은 숫자 이거나 문자 형식에서 이어야 합니다.|
| **MSSQL_LCID** | SQL Server에 사용할 언어 ID를 설정 합니다. 예를 들어 1036 프랑스어가 있습니다. |
| **MSSQL_COLLATION** | SQL Server에 대 한 기본 데이터 정렬을 설정합니다. 이 언어 id (LCID) 데이터 정렬의 기본 매핑을 재정의합니다. |
| **MSSQL_MEMORY_LIMIT_MB** | 최대 메모리 (MB) SQL Server에서 사용할 수 있는 설정입니다. 기본적으로 총 실제 메모리의 80%는 것입니다. |
| **MSSQL_TCP_PORT** | SQL Server (기본값 1433)를 수신 하는 TCP 포트를 구성 합니다. |
| **MSSQL_IP_ADDRESS** | IP 주소를 설정 합니다. 현재 IP 주소는 IPv4 스타일 (0.0.0.0) 이어야 합니다. |
| **MSSQL_BACKUP_DIR** | 기본 백업 디렉터리 위치를 설정 합니다. |
| **MSSQL_DATA_DIR** | 새 SQL Server 데이터베이스 데이터 파일 (.mdf) 만들어지는 디렉터리를 변경 합니다. |
| **MSSQL_LOG_DIR** | 새 SQL Server 데이터베이스 로그 (.ldf) 파일이 만들어지는 디렉터리를 변경 합니다. |
| **MSSQL_DUMP_DIR** | 여기서 SQL Server를 맡 메모리 덤프 및 기타 문제 해결 파일 기본적으로 디렉터리를 변경 합니다. |
| **MSSQL_ENABLE_HADR** | 가용성 그룹을 사용 하도록 설정 합니다. 예를 들어, '1'을 사용 하 고 '0'은 사용할 수 없습니다. |
| **MSSQL_AGENT_ENABLED** | SQL Server 에이전트를 사용 하도록 설정 합니다. 예를 들어, 'true' 켜져 있고 'f a l'은 사용 하지 않도록 설정 합니다. 기본적으로 에이전트를 비활성화 합니다.  |
| **MSSQL_MASTER_DATA_FILE** | Master 데이터베이스 데이터 파일의 위치를 설정합니다. 이름을 지정 해야 합니다 **master.mdf** SQL Server를 처음 실행 될 때까지 합니다. |
| **MSSQL_MASTER_LOG_FILE** | Master 데이터베이스 로그 파일의 위치를 설정합니다. 이름을 지정 해야 합니다 **mastlog.ldf** SQL Server를 처음 실행 될 때까지 합니다. |
| **MSSQL_ERROR_LOG_FILE** | 오류 로그 파일의 위치를 설정합니다. |

::: moniker-end

## <a name="use-with-initial-setup"></a>초기 설치 사용

이 예제에서는 실행 `mssql-conf setup` 사용 하 여 환경 변수를 구성 합니다. 다음 환경 변수를 지정 합니다.

- **ACCEPT_EULA** 가 최종 사용자 사용권 계약에 동의 합니다.
- **MSSSQL_PID** 자유롭게 사용이 허가 된 개발자 버전의 SQL Server 비-프로덕션 사용을 지정 합니다.
- **MSSQL_SA_PASSWORD** 강력한 암호를 설정 합니다.
- **MSSQL_TCP_PORT** 1234에 수신 하는 SQL Server는 TCP 포트를 설정 합니다.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>Docker 사용

이 예제에서는 docker 명령은 새 SQL Server 컨테이너를 만들려면 다음 환경 변수를 사용 합니다.

- **ACCEPT_EULA** 가 최종 사용자 사용권 계약에 동의 합니다.
- **MSSSQL_PID** 자유롭게 사용이 허가 된 개발자 버전의 SQL Server 비-프로덕션 사용을 지정 합니다.
- **MSSQL_SA_PASSWORD** 강력한 암호를 설정 합니다.
- **MSSQL_TCP_PORT** 1234에 수신 하는 SQL Server는 TCP 포트를 설정 합니다. 즉,는 호스트 포트 매핑 포트 1433 (기본값) 대신 사용자 지정 TCP 포트를 함께 매핑되어야 합니다 `-p 1234:1234` 이 예제의 명령을 합니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Linux/macOS에서 Docker를 실행 하는 경우 작은따옴표를 사용 하 여 다음 구문을 사용 합니다.

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

Linux/macOS에서 Docker를 실행 하는 경우 작은따옴표를 사용 하 여 다음 구문을 사용 합니다.

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

Windows에서 Docker를 실행 하는 경우 큰따옴표를 사용 하 여 다음 구문을 사용 합니다.

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

## <a name="next-steps"></a>다음 단계

여기에 나열 되지 다른 SQL Server 설정에 대 한 참조 [mssql-conf 도구를 사용 하 여 Linux에서 SQL Server 구성](sql-server-linux-configure-mssql-conf.md)합니다.

설치 및 Linux에서 SQL Server를 실행 하는 방법에 대 한 자세한 내용은 참조 하세요. [Linux의 SQL Server 설치](sql-server-linux-setup.md)합니다.
