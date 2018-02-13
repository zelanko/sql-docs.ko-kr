---
title: "Ubuntu에서 SQL Server에 대 한 자동된 설치 | Microsoft Docs"
description: "SQL Server 스크립트 샘플 ubuntu 무인된 설치"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: f6df20d942331b6361651ade82b6158b2c6798de
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/13/2018
---
# <a name="sample-unattended-sql-server-installation-script-for-ubuntu"></a>Ubuntu 용 SQL Server 무인된 설치 스크립트 샘플:

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 샘플 Bash 스크립트 대화형 입력이 없는 Ubuntu 16.04에 SQL Server 2017를 설치합니다. 데이터베이스 엔진, SQL Server Agent, SQL Server 명령줄 도구를 설치 하는 방식의 예제를 제공 하 고 설치 후 단계를 수행 합니다. 필요에 따라 전체 텍스트 검색을 설치 하 고 관리 사용자를 만들 수 있습니다.

> [!TIP]
> SQL Server를 설치 하는 가장 빠른 방법은 따라야 하는 무인된 설치 스크립트를 필요 하지 않은 경우는 [Ubuntu 용 퀵 스타트](quickstart-install-connect-ubuntu.md)합니다. 다른 설정 정보를 참조 하십시오. [Linux에서 SQL Server에 대 한 설치 지침](sql-server-linux-setup.md)합니다.

## <a name="prerequisites"></a>필수 구성 요소

- 최소 2GB의 메모리 Linux에서 SQL Server를 실행 해야 합니다.
- 파일 시스템을 해야 **XFS** 또는 **EXT4**합니다. 와 같은 다른 파일 시스템, **BTRFS**, 지원 되지 않습니다.
- 다른 시스템 요구 사항에 대 한 참조 [Linux에서 SQL Server에 대 한 시스템 요구 사항](sql-server-linux-setup.md#system)합니다.

## <a name="sample-script"></a>샘플 스크립트

```bash
#!/bin/bash -e

# Use the following variables to control your install:

# Password for the SA user (required)
MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'

# Product ID of the version of SQL server you're installing
# Must be evaluation, developer, express, web, standard, enterprise, or your 25 digit product key
# Defaults to developer
MSSQL_PID='evaluation'

# Install SQL Server Agent (recommended)
SQL_INSTALL_AGENT='y'

# Install SQL Server Full Text Search (optional)
# SQL_INSTALL_FULLTEXT='y'

# Create an additional user with sysadmin privileges (optional)
# SQL_INSTALL_USER='<Username>'
# SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'

if [ -z $MSSQL_SA_PASSWORD ]
then
  echo Environment variable MSSQL_SA_PASSWORD must be set for unattended install
  exit 1
fi

echo Adding Microsoft repositories...
sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
repoargs="$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
sudo add-apt-repository "${repoargs}"
repoargs="$(curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
sudo add-apt-repository "${repoargs}"

echo Running apt-get update -y...
sudo apt-get update -y

echo Installing SQL Server...
sudo apt-get install -y mssql-server

echo Running mssql-conf setup...
sudo MSSQL_SA_PASSWORD=$MSSQL_SA_PASSWORD \
     MSSQL_PID=$MSSQL_PID \
     /opt/mssql/bin/mssql-conf -n setup accept-eula

echo Installing mssql-tools and unixODBC developer...
sudo ACCEPT_EULA=Y apt-get install -y mssql-tools unixodbc-dev

# Add SQL Server tools to the path by default:
echo Adding SQL Server tools to your path...
echo PATH="$PATH:/opt/mssql-tools/bin" >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc

# Optional SQL Server Agent installation:
if [ ! -z $SQL_INSTALL_AGENT ]
then
  echo Installing SQL Server Agent...
  sudo apt-get install -y mssql-server-agent
fi

# Optional SQL Server Full Text Search installation:
if [ ! -z $SQL_INSTALL_FULLTEXT ]
then
    echo Installing SQL Server Full-Text Search...
    sudo apt-get install -y mssql-server-fts
fi

# Configure firewall to allow TCP port 1433:
echo Configuring UFW to allow traffic on port 1433...
sudo ufw allow 1433/tcp
sudo ufw reload

# Optional example of post-installation configuration.
# Trace flags 1204 and 1222 are for deadlock tracing.
# echo Setting trace flags...
# sudo /opt/mssql/bin/mssql-conf traceflag 1204 1222 on

# Restart SQL Server after installing:
echo Restarting SQL Server...
sudo systemctl restart mssql-server

# Connect to server and get the version:
counter=1
errstatus=1
while [ $counter -le 5 ] && [ $errstatus = 1 ]
do
  echo Waiting for SQL Server to start...
  sleep 3s
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "SELECT @@VERSION" 2>/dev/null
  errstatus=$?
  ((counter++))
done

# Display error if connection failed:
if [ $errstatus = 1 ]
then
  echo Cannot connect to SQL Server, installation aborted
  exit $errstatus
fi

# Optional new user creation:
if [ ! -z $SQL_INSTALL_USER ] && [ ! -z $SQL_INSTALL_USER_PASSWORD ]
then
  echo Creating user $SQL_INSTALL_USER
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "CREATE LOGIN [$SQL_INSTALL_USER] WITH PASSWORD=N'$SQL_INSTALL_USER_PASSWORD', DEFAULT_DATABASE=[master], CHECK_EXPIRATION=ON, CHECK_POLICY=ON; ALTER SERVER ROLE [sysadmin] ADD MEMBER [$SQL_INSTALL_USER]"
fi

echo Done!
```

### <a name="running-the-script"></a>스크립트 실행

스크립트를 실행하려면

1. 샘플 원하는 텍스트 편집기에 붙여넣고 같은 기억 하기 쉬운 이름으로 저장 `install_sql.sh`합니다.

1. 사용자 지정 `MSSQL_SA_PASSWORD`, `MSSQL_PID`, 및의 변경 하려는 다른 변수 중 하나입니다.

1. 스크립트 실행 가능으로 표시 합니다.

   ```bash
   chmod +x install_sql.sh
   ```

1. 스크립트 실행

   ```bash
   ./install_sql.sh
   ```

### <a name="understanding-the-script"></a>스크립트 이해
가장 먼저 Bash 스크립트는 몇 가지 변수를 설정 됩니다. 이러한 샘플에서와 같은 스크립팅 변수 또는 환경 변수 가능 합니다. 변수 ``` MSSQL_SA_PASSWORD ``` 은 **필요한** SQL Server를 설치 하는 사용자 들이 스크립트에 대해 만든 사용자 지정 변수입니다. 샘플 스크립트는 다음 단계를 수행합니다.

1. Microsoft GPG 공개 키를 가져옵니다.

1. SQL Server 및 명령줄 도구에 대 한 Microsoft 리포지토리를 등록 합니다.

1. 로컬 리포지토리를 업데이트 합니다.

1. SQL Server 설치

1. SQL Server와 구성는 ```MSSQL_SA_PASSWORD``` 자동으로 최종 사용자 사용권 계약에 동의 합니다.

1. 자동으로 SQL Server 명령줄 도구에 대 한 최종 사용자 사용권 계약에 동의 하 고, 설치 unixodbc dev 패키지를 설치 합니다.

1. SQL Server 명령줄 도구 사용 편의성에 대 한 경로를 추가 합니다.

1. 경우에 SQL Server 에이전트를 설치 스크립팅 변수 ```SQL_INSTALL_AGENT``` 에 기본적으로 설정 됩니다.

1. 경우에 필요에 따라 SQL Server 전체 텍스트 검색을 설치 변수 ```SQL_INSTALL_FULLTEXT``` 설정 됩니다.

1. 다른 시스템에서 SQL Server에 연결 하는 데 필요한 시스템 방화벽에서 포트 1433 TCP에 대 한 차단을 해제 합니다.

1. 필요에 따라 교착 상태 추적에 대 한 추적 플래그를 설정 합니다. (줄의 주석 처리 해야 함)

1. SQL Server가 설치 되어 이제, 작동 하도록 하려면 프로세스를 다시 시작 합니다.

1. SQL Server 오류 메시지는 숨기 려 제대로 설치 되어 있는지 확인 합니다.

1. 경우 서버 관리자가 새 사용자를 만들 ```SQL_INSTALL_USER``` 및 ```SQL_INSTALL_USER_PASSWORD``` 모두 설정 합니다.

## <a name="next-steps"></a>다음 단계

여러 무인된 설치를 단순화 하 고 적절 한 환경 변수를 설정 하는 독립 실행형 Bash 스크립트를 만듭니다. 샘플 스크립트를 사용 하 고, 자신의 Bash 스크립트 변수를 제거할 수 있습니다.

```bash
#!/bin/bash
export MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'
export MSSQL_PID='evaluation'
export SQL_INSTALL_AGENT='y'
export SQL_INSTALL_USER='<Username>'
export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'
export SQL_INSTALL_AGENT='y'
```

그런 다음 Bash 스크립트를 다음과 같이 실행 합니다.
```bash
. ./my_script_name.sh
```

Linux에서 SQL Server에 대 한 자세한 내용은 참조 [Linux 개요에서 SQL Server](sql-server-linux-overview.md)합니다.