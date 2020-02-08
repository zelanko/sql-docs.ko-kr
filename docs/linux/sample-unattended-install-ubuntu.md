---
title: Ubuntu에서 SQL Server에 대한 무인 설치
titleSuffix: SQL Server
description: SQL Server 스크립트 샘플 - Ubuntu에서 무인 설치
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: b71bad98aa6e9172b69efa67ce8708f1479fa691
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67910479"
---
# <a name="sample-unattended-sql-server-installation-script-for-ubuntu"></a>샘플: Ubuntu용 무인 SQL Server 설치 스크립트

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 샘플 Bash 스크립트는 대화형 입력 없이 Ubuntu 16.04에 SQL Server 2017을 설치합니다. 이 스크립트는 데이터베이스 엔진, SQL Server 명령줄 도구 및 SQL Server 에이전트를 설치하는 예를 제공하고, 설치 후 단계를 수행합니다. 필요에 따라 전체 텍스트 검색을 설치하고 관리자를 만들 수 있습니다.

> [!TIP]
> 무인 설치 스크립트가 필요하지 않은 경우 SQL Server를 설치하는 가장 빠른 방법은 [용 빠른 시작](quickstart-install-connect-ubuntu.md)을 따르는 것입니다. 다른 설치 정보는 [SQL Server on Linux 설치 지침](sql-server-linux-setup.md)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

- SQL Server on Linux를 실행하려면 2GB 이상의 메모리가 필요합니다.
- 파일 시스템은 **XFS** 또는 **EXT4**여야 합니다. **BTRFS** 등의 다른 파일 시스템은 지원되지 않습니다.
- 기타 시스템 요구 사항은 [SQL Server on Linux에 대한 시스템 요구 사항](sql-server-linux-setup.md#system)을 참조하세요.

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
source ~/.bashrc

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

1. 샘플을 즐겨 사용하는 텍스트 편집기에 붙여넣고 `install_sql.sh`와 같은 기억하기 쉬운 이름으로 저장합니다.

1. `MSSQL_SA_PASSWORD`, `MSSQL_PID` 및 변경하려는 다른 변수를 사용자 지정합니다.

1. 스크립트를 실행 파일로 표시

   ```bash
   chmod +x install_sql.sh
   ```

1. 스크립트 실행

   ```bash
   ./install_sql.sh
   ```

### <a name="understanding-the-script"></a>스크립트 이해
Bash 스크립트가 수행하는 첫 번째 작업은 몇 가지 변수를 설정하는 것입니다. 이 변수는 샘플과 같은 스크립팅 변수이거나 환경 변수일 수 있습니다. `MSSQL_SA_PASSWORD` 변수는 SQL Server 설치에 **필수**이며, 다른 변수는 스크립트용으로 생성된 사용자 지정 변수입니다. 샘플 스크립트는 다음 단계를 수행합니다.

1. 공용 Microsoft GPG 키를 가져옵니다.

1. SQL Server 및 명령줄 도구를 위한 Microsoft 리포지토리를 등록합니다.

1. 로컬 리포지토리 업데이트

1. SQL Server 설치

1. ```MSSQL_SA_PASSWORD```를 사용하여 SQL Server를 구성하고 최종 사용자 사용권 계약에 자동으로 동의합니다.

1. SQL Server 명령줄 도구에 대한 최종 사용자 사용권 계약에 자동으로 동의하고, 설치한 후 xodbc-dev 패키지를 설치합니다.

1. 간편하게 사용할 수 있도록 경로에 SQL Server 명령줄 도구를 추가합니다.

1. 스크립팅 변수 ```SQL_INSTALL_AGENT```가 기본값인 on으로 설정되면 SQL Server 에이전트를 설치합니다.

1. 변수 ```SQL_INSTALL_FULLTEXT```가 설정되면 필요에 따라 SQL Server 전체 텍스트 검색을 설치합니다.

1. 다른 시스템에서 SQL Server에 연결하는 데 필요한 TCP의 포트 1433을 시스템 방화벽에서 차단 해제합니다.

1. 필요에 따라 교착 상태 추적을 위한 추적 플래그를 설정합니다. (줄의 주석 처리를 제거해야 함)

1. SQL Server가 이제 설치되었습니다. 작동 가능하게 하려면 프로세스를 다시 시작합니다.

1. 오류 메시지는 숨겨지지만, SQL Server가 제대로 설치되었는지 확인합니다.

1. ```SQL_INSTALL_USER``` 및 ```SQL_INSTALL_USER_PASSWORD```가 둘 다 설정된 경우 새 서버 관리자 사용자를 만듭니다.

## <a name="next-steps"></a>다음 단계

여러 무인 설치를 간소화하고 적절한 환경 변수를 설정하는 독립 실행형 Bash 스크립트를 만듭니다. 예제 스크립트에서 사용하는 변수를 제거하고 해당 변수를 자체 Bash 스크립트에 넣을 수 있습니다.

```bash
#!/bin/bash
export MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'
export MSSQL_PID='evaluation'
export SQL_INSTALL_AGENT='y'
export SQL_INSTALL_USER='<Username>'
export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'
export SQL_INSTALL_AGENT='y'
```

그런 다음, Bash 스크립트를 다음과 같이 실행합니다.
```bash
. ./my_script_name.sh
```

SQL Server on Linux에 대한 자세한 내용은 [SQL Server on Linux 개요](sql-server-linux-overview.md)를 참조하세요.
