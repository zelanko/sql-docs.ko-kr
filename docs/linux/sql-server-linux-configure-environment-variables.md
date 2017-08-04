---
title: "환경 변수를 SQL Server 설정 구성 | Microsoft Docs"
description: "이 항목에서는 환경 변수를 사용 하 여 Linux에서 특정 SQL Server 2017 설정을 구성 하는 방법에 설명 합니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/21/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 4951f503a7b5c395f86cb6daf2ba705ca69fbd83
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Linux에서 환경 변수를 SQL Server 설정 구성

Linux에서 SQL Server 2017 RC2를 구성 하려면 몇 가지 서로 다른 환경 변수를 사용할 수 있습니다. 이러한 변수는 두 가지 시나리오에서 사용 됩니다.

- 초기 설치 프로그램을 구성 하는 `mssql-conf setup` 명령입니다.
- 새 구성 하려면 [Docker에서 SQL Server 컨테이너](quickstart-install-connect-docker.md)합니다.

> [!TIP]
> 이러한 설치 시나리오 후 SQL Server를 구성 해야 할 경우 참조 [mssql conf 도구와 함께 Linux에서 SQL Server 구성](sql-server-linux-configure-mssql-conf.md)합니다.

## <a name="environment-variables"></a>환경 변수

| 환경 변수 | Description |
|-----|-----|
| **ACCEPT_EULA** | 모든 값 (예를 들어, ' Y')로 설정 된 경우 SQL Server 사용권 계약에 동의 합니다. |
| **MSSQL_SA_PASSWORD** | SA 암호를 구성 합니다. |
| **MSSQL_PID** | SQL Server 버전 또는 제품 키를 설정 합니다. 가능한 값: Evaluation, Developer, Express, 웹, Standard, Enterprise, 또는 # # #-# # #-# # #-# # #-# # #, '#'은 숫자 이거나 문자의 형태로 제품 키를 합니다. |
| **MSSQL_LCID** | SQL Server에 사용할 언어 ID를 설정 합니다. 예를 들어 1036 프랑스어입니다. |
| **MSSQL_COLLATION** | SQL Server에 대 한 기본 데이터 정렬을 설정합니다. 이 언어 id (LCID) 데이터 정렬의 기본 매핑을 재정의합니다. |
| **MSSQL_MEMORY_LIMIT_MB** | 메모리 (MB) SQL Server에서 사용할 수 있는 최대 크기를 설정 합니다. 기본적으로 것은 총 실제 메모리의 80%입니다. |
| **MSSQL_TCP_PORT** | SQL Server (기본값 1433)에서 수신 대기 하는 TCP 포트를 구성 합니다. |
| **MSSQL_IP_ADDRESS** | IP 주소를 설정 합니다. 현재 IP 주소는 IPv4 스타일 (0.0.0.0) 이어야 합니다. |
| **MSSQL_BACKUP_DIR** | 기본 백업 디렉터리 위치를 설정 합니다. |
| **MSSQL_DATA_DIR** | 새 SQL Server 데이터베이스 데이터 파일 (.mdf)이 생성 되는 위치는 디렉터리를 변경 합니다. |
| **MSSQL_LOG_DIR** | 새 SQL Server 데이터베이스 로그 (.ldf) 파일을 만드는 하는 디렉터리를 변경 합니다. |
| **MSSQL_DUMP_DIR** | 여기서 SQL Server는 보관할 메모리 덤프 및 기타 문제 해결 파일 기본적으로 디렉터리를 변경 합니다. |
| **MSSQL_ENABLE_HADR** | 가용성 그룹을 사용 하도록 설정 합니다. |

## <a name="example-initial-setup"></a>예: 초기 설치

이 예제에서는 실행 `mssql-conf setup` 으로 환경 변수를 구성 합니다. 다음과 같은 환경 변수는 지정 됩니다.

- **ACCEPT_EULA** 최종 사용자 사용권 계약에 동의 합니다.
- **MSSSQL_PID** 자유롭게 사용이 허가 된 개발자의 SQL Server 버전 비-프로덕션 용도로 지정 합니다.
- **MSSQL_SA_PASSWORD** 강력한 암호를 설정 합니다.
- **MSSQL_TCP_PORT** 1234에 SQL Server는 수신 하는 TCP 포트를 설정 합니다.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="example-docker"></a>예: Docker

이 예제에서는 docker 명령은 다음과 같은 환경 변수를 사용 하 여 새 SQL Server 2017 컨테이너를 만들려면:

- **ACCEPT_EULA** 최종 사용자 사용권 계약에 동의 합니다.
- **MSSSQL_PID** 자유롭게 사용이 허가 된 개발자의 SQL Server 버전 비-프로덕션 용도로 지정 합니다.
- **MSSQL_SA_PASSWORD** 강력한 암호를 설정 합니다.
- **MSSQL_TCP_PORT** 1234에 SQL Server는 수신 하는 TCP 포트를 설정 합니다. 즉, 호스트 포트 매핑 포트 1433 (기본값) 대신 사용자 지정 TCP 포트 해야 매핑되도록와 `-p 1234:1234` 이 예제의 명령입니다.

Linux/macOS에서 Docker를 실행 하는 경우에 작은따옴표로 다음 구문을 사용 합니다.

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 --cap-add SYS_PTRACE -p 1234:1234 -d microsoft/mssql-server-linux
```

Windows에서 Docker를 실행 하는 경우에 큰따옴표로 다음 구문을 사용 합니다.

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 --cap-add SYS_PTRACE -p 1234:1234 -d microsoft/mssql-server-linux
```

## <a name="next-steps"></a>다음 단계

여기에 나열 되지 다른 SQL Server 설정은 참조 [mssql conf 도구와 함께 Linux에서 SQL Server 구성](sql-server-linux-configure-mssql-conf.md)합니다.

설치 하 고 Linux에서 SQL Server를 실행 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Linux에서 SQL Server 설치](sql-server-linux-setup.md)합니다.

