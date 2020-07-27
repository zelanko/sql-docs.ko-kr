---
title: 'Ubuntu: SQL Server on Linux 설치'
description: 이 빠른 시작에서는 Ubuntu에 SQL Server 2017 또는 SQL Server 2019를 설치한 다음, sqlcmd를 사용하여 데이터베이스를 만들고 쿼리하는 방법을 보여 줍니다.
author: VanMSFT
ms.author: vanto
ms.date: 07/15/2020
ms.topic: conceptual
ms.prod: sql
ms.custom: seo-lt-2019
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: cce5af380f3706ef6fd6f22578c2b693aff1ad7c
ms.sourcegitcommit: 56f6892b3795da308d226d4b3c5c859ead2e830a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86438115"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>빠른 시작: Ubuntu에 SQL Server 설치 및 데이터베이스 만들기
[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]


<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

이 빠른 시작에서는 Ubuntu 18.04에 SQL Server 2017을 설치합니다. 그런 다음, **sqlcmd**를 통해 연결하여 첫 번째 데이터베이스를 만들고 쿼리를 실행합니다.

> [!TIP]
> 이 자습서를 사용하려면 사용자 입력과 인터넷 연결이 필요합니다. 무인 또는 오프라인 설치 절차에 관심이 있는 경우 [SQL Server on Linux 설치 지침](sql-server-linux-setup.md)을 참조하세요. 지원되는 플랫폼 목록은 [릴리스 정보](sql-server-linux-release-notes.md)를 참조하세요.

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

이 빠른 시작에서는 Ubuntu 18.04에 SQL Server 2019를 설치합니다. 그런 다음, **sqlcmd**를 통해 연결하여 첫 번째 데이터베이스를 만들고 쿼리를 실행합니다.

> [!TIP]
> 이 자습서를 사용하려면 사용자 입력과 인터넷 연결이 필요합니다. 무인 또는 오프라인 설치 절차에 관심이 있는 경우 [SQL Server on Linux 설치 지침](sql-server-linux-setup.md)을 참조하세요. 지원되는 플랫폼 목록은 [릴리스 정보](sql-server-linux-release-notes-2019.md)를 참조하세요.

::: moniker-end

## <a name="prerequisites"></a>사전 요구 사항

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

**최소 2GB**의 메모리를 포함하는 Ubuntu 16.04 또는 18.04 머신이 있어야 합니다.

고유한 머신에 Ubuntu 18.04를 설치하려면 <http://releases.ubuntu.com/bionic/>으로 이동합니다. Azure에서 Ubuntu 가상 머신을 만들 수도 있습니다. [Azure CLI를 사용하여 Linux VM 만들기 및 관리](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)를 참조하세요.

> [!NOTE]
> 현재 Windows 10의 [Linux용 Windows 하위 시스템](https://msdn.microsoft.com/commandline/wsl/about)은 설치 대상으로 지원되지 않습니다.

기타 시스템 요구 사항은 [SQL Server on Linux에 대한 시스템 요구 사항](sql-server-linux-setup.md#system)을 참조하세요.

> [!NOTE]
> SQL Server 2017 CU20부터 Ubuntu 18.04가 지원됩니다. Ubuntu 18.04에서 이 문서의 지침을 사용하려면 `16.04`대신 올바른 [리포지토리 경로](sql-server-linux-change-repo.md)인 `18.04`를 사용해야 합니다.
>
> 더 낮은 버전에서 SQL Server를 실행하는 경우 [수정](https://blogs.msdn.microsoft.com/sql_server_team/installing-sql-server-2017-for-linux-on-ubuntu-18-04-lts/)하여 구성할 수 있습니다.

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

**최소 2GB**의 메모리를 포함하는 Ubuntu 16.04 또는 18.04 머신이 있어야 합니다.

고유한 머신에 Ubuntu 18.04를 설치하려면 <http://releases.ubuntu.com/bionic/>으로 이동합니다. Azure에서 Ubuntu 가상 머신을 만들 수도 있습니다. [Azure CLI를 사용하여 Linux VM 만들기 및 관리](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)를 참조하세요.

> [!NOTE]
> 현재 Windows 10의 [Linux용 Windows 하위 시스템](https://msdn.microsoft.com/commandline/wsl/about)은 설치 대상으로 지원되지 않습니다.

기타 시스템 요구 사항은 [SQL Server on Linux에 대한 시스템 요구 사항](sql-server-linux-setup.md#system)을 참조하세요.

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a name="install-sql-server"></a><a id="install"></a>SQL Server 설치

> [!NOTE]
> SQL Server 2017에서 다음 명령은 Ubuntu 18.04 리포지토리를 가리킵니다. Ubuntu 16.04를 사용하는 경우 아래 경로를 `/ubuntu/18.04/` 대신 `/ubuntu/16.04/`로 변경합니다.

Ubuntu에서 SQL Server을 구성하려면 터미널에서 다음 명령을 실행하여 **mssql-server** 패키지를 설치합니다.

1. 공용 리포지토리 GPG 키를 가져옵니다.

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Microsoft SQL Server Ubuntu 리포지토리를 등록합니다.

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2017.list)"
   ```

   > [!TIP]
   > SQL Server 2019를 설치하려면 대신 SQL Server 2019 리포지토리를 등록해야 합니다. SQL Server 2019 설치에는 다음 명령을 사용합니다.
   >
   > ```bash
   > sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"
   > ```

3. 다음 명령을 실행하여 SQL Server를 설치합니다.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. 패키지 설치가 완료되면 **mssql-conf setup**을 실행하고, 프롬프트에 따라 SA 암호를 설정하고, 버전을 선택합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 다음 SQL Server 2017 버전은 체험용 라이선스인 Evaluation, Developer 및 Express로 제공됩니다.

   > [!NOTE]
   > SA 계정의 강력한 암호를 지정해야 합니다(대문자 및 소문자, 기본 10자리 숫자 및/또는 영숫자가 아닌 기호를 포함 하여 최소 길이 8자).

5. 구성이 완료되면 서비스가 실행 중인지 확인합니다.

   ```bash
   systemctl status mssql-server --no-pager
   ```

6. 원격으로 연결하려면 방화벽에서 SQL Server TCP 포트(기본값 1433)를 열어야 할 수도 있습니다.

이제 SQL Server는 Ubuntu 머신에서 실행 중이며 사용할 준비가 되었습니다.

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="install-sql-server"></a><a id="install"></a>SQL Server 설치

> [!NOTE]
> SQL Server 2019에서 다음 명령은 Ubuntu 18.04 리포지토리를 가리킵니다. Ubuntu 16.04를 사용하는 경우 아래 경로를 `/ubuntu/18.04/` 대신 `/ubuntu/16.04/`로 변경합니다.

Ubuntu에서 SQL Server을 구성하려면 터미널에서 다음 명령을 실행하여 **mssql-server** 패키지를 설치합니다.

1. 공용 리포지토리 GPG 키를 가져옵니다.

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. SQL Server 2019에 대한 Microsoft SQL Server Ubuntu 리포지토리를 등록합니다.

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"
   ```

3. 다음 명령을 실행하여 SQL Server를 설치합니다.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. 패키지 설치가 완료되면 **mssql-conf setup**을 실행하고, 프롬프트에 따라 SA 암호를 설정하고, 버전을 선택합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > SA 계정의 강력한 암호를 지정해야 합니다(대문자 및 소문자, 기본 10자리 숫자 및/또는 영숫자가 아닌 기호를 포함 하여 최소 길이 8자).

5. 구성이 완료되면 서비스가 실행 중인지 확인합니다.

   ```bash
   systemctl status mssql-server --no-pager
   ```

6. 원격으로 연결하려면 방화벽에서 SQL Server TCP 포트(기본값 1433)를 열어야 할 수도 있습니다.

이제 SQL Server 2019는 Ubuntu 머신에서 실행 중이며 사용할 준비가 되었습니다!

::: moniker-end

## <a name="install-the-sql-server-command-line-tools"></a><a id="tools"></a>SQL Server 명령줄 도구 설치

데이터베이스를 만들려면 SQL Server에서 Transact-SQL 문을 실행할 수 있는 도구와 연결해야 합니다. 다음 단계에서는 SQL Server 명령줄 도구인 [sqlcmd](../tools/sqlcmd-utility.md) 및 [bcp](../tools/bcp-utility.md)를 설치합니다.

다음 단계에 따라 Ubuntu에 **mssql-tools**를 설치합니다. 

1. 공용 리포지토리 GPG 키를 가져옵니다.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Microsoft Ubuntu 리포지토리를 등록합니다.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. 원본 목록을 업데이트하고 unixODBC 개발자 패키지를 사용하여 설치 명령을 실행합니다. 자세한 내용은 [Microsoft ODBC Driver for SQL Server(Linux) 설치](../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)를 참조하세요.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > 최신 버전의 **mssql-tools**로 업데이트하려면 다음 명령을 실행합니다.
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **선택 사항**: Bash 셸에서 **PATH** 환경 변수에 `/opt/mssql-tools/bin/`를 추가합니다.

   로그인 세션을 위해 bash 셸에서 **sqlcmd/bcp**에 액세스할 수 있도록 설정하려면 다음 명령을 사용하여 **~/.bash_profile** 파일에서 **PATH**를 수정합니다.

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   대화형/비로그인 세션을 위해 bash 셸에서 **sqlcmd/bcp**에 액세스할 수 있도록 설정하려면 다음 명령을 사용하여 **~/.bashrc** 파일에서 **PATH**를 수정합니다.

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
