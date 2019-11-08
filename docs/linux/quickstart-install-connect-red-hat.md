---
title: Red Hat Enterprise Linux에서 SQL Server 시작
titleSuffix: SQL Server
description: 이 빠른 시작에서는 Red Hat Enterprise Linux에 SQL Server 2017 또는 SQL Server 2019를 설치한 다음, sqlcmd를 사용하여 데이터베이스를 만들고 쿼리하는 방법을 보여 줍니다.
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: b94ea0ef8956e7807f075da548ae817dc6a205df
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531370"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>빠른 시작: Red Hat에 SQL Server 설치 및 데이터베이스 만들기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

이 빠른 시작에서는 RHEL(Red Hat Enterprise Linux)에 SQL Server 2017 또는 SQL Server 2019를 설치합니다. 그런 다음, **sqlcmd**를 통해 연결하여 첫 번째 데이터베이스를 만들고 쿼리를 실행합니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

이 빠른 시작에서는 RHEL(Red Hat Enterprise Linux) 7.3 이상에 SQL Server 2019를 설치합니다. 그런 다음, **sqlcmd**를 통해 연결하여 첫 번째 데이터베이스를 만들고 쿼리를 실행합니다.

::: moniker-end

> [!TIP]
> 이 자습서를 사용하려면 사용자 입력과 인터넷 연결이 필요합니다. [무인](sql-server-linux-setup.md#unattended) 또는 [오프라인](sql-server-linux-setup.md#offline) 설치 절차에 관심이 있는 경우 [SQL Server on Linux 설치 지침](sql-server-linux-setup.md)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

**최소 2GB**의 메모리를 포함하는 RHEL 7.3, 7.4, 7.5 또는 7.6 머신이 있어야 합니다.

사용자의 머신에 Red Hat Enterprise Linux를 설치하려면 [https://access.redhat.com/products/red-hat-enterprise-linux/evaluation](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation)으로 이동합니다. Azure에서 RHEL 가상 머신을 만들 수도 있습니다. [Azure CLI를 사용하여 Linux VM 만들기 및 관리](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)를 참조하고 `az vm create`에 대한 호출에 `--image RHEL`을 사용하세요.

이전에 SQL Server의 CTP 또는 RC 릴리스를 설치한 경우 다음 단계를 수행하기 전에 이전 리포지토리를 제거해야 합니다. 자세한 내용은 [SQL Server 2017 및 2019에 대한 Linux 리포지토리 구성](sql-server-linux-change-repo.md)을 참조하세요.

기타 시스템 요구 사항은 [SQL Server on Linux에 대한 시스템 요구 사항](sql-server-linux-setup.md#system)을 참조하세요.

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>SQL Server 설치

RHEL에서 SQL Server을 구성하려면 터미널에서 다음 명령을 실행하여 **mssql-server** 패키지를 설치합니다.

1. Microsoft SQL Server 2017 Red Hat 리포지토리 구성 파일을 다운로드합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!TIP]
   > SQL Server 2019를 설치하려면 대신 SQL Server 2019 리포지토리를 등록해야 합니다. SQL Server 2019 설치에는 다음 명령을 사용합니다.
   >
   > ```bash
   > sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   > ```

2. 다음 명령을 실행하여 SQL Server를 설치합니다.

   ```bash
   sudo yum install -y mssql-server
   ```

3. 패키지 설치가 완료되면 **mssql-conf setup**을 실행하고, 프롬프트에 따라 SA 암호를 설정하고, 버전을 선택합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 다음 SQL Server 2017 버전은 체험용 라이선스인 Evaluation, Developer 및 Express로 제공됩니다.

   > [!NOTE]
   > SA 계정의 강력한 암호를 지정해야 합니다(대문자 및 소문자, 기본 10자리 숫자 및/또는 영숫자가 아닌 기호를 포함 하여 최소 길이 8자).

4. 구성이 완료되면 서비스가 실행 중인지 확인합니다.

   ```bash
   systemctl status mssql-server
   ```

5. 원격 연결을 허용하려면 RHEL의 방화벽에서 SQL Server 포트를 엽니다. 기본 SQL Server 포트는 TCP 1433입니다. 방화벽에 **FirewallD**를 사용하는 경우 다음 명령을 사용할 수 있습니다.

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

이제 SQL Server는 RHEL 머신에서 실행 중이며 사용할 준비가 되었습니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>SQL Server 설치

RHEL에서 SQL Server을 구성하려면 터미널에서 다음 명령을 실행하여 **mssql-server** 패키지를 설치합니다.

1. Microsoft SQL Server 2019 Red Hat 리포지토리 구성 파일을 다운로드합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   ```

2. 다음 명령을 실행하여 SQL Server를 설치합니다.

   ```bash
   sudo yum install -y mssql-server
   ```

3. 패키지 설치가 완료되면 **mssql-conf setup**을 실행하고, 프롬프트에 따라 SA 암호를 설정하고, 버전을 선택합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > SA 계정의 강력한 암호를 지정해야 합니다(대문자 및 소문자, 기본 10자리 숫자 및/또는 영숫자가 아닌 기호를 포함 하여 최소 길이 8자).

4. 구성이 완료되면 서비스가 실행 중인지 확인합니다.

   ```bash
   systemctl status mssql-server
   ```

5. 원격 연결을 허용하려면 RHEL의 방화벽에서 SQL Server 포트를 엽니다. 기본 SQL Server 포트는 TCP 1433입니다. 방화벽에 **FirewallD**를 사용하는 경우 다음 명령을 사용할 수 있습니다.

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

이제 SQL Server 2019는 RHEL 머신에서 실행 중이며 사용할 준비가 되었습니다.

::: moniker-end

## <a id="tools"></a>SQL Server 명령줄 도구 설치

데이터베이스를 만들려면 SQL Server에서 Transact-SQL 문을 실행할 수 있는 도구와 연결해야 합니다. 다음 단계에서는 SQL Server 명령줄 도구인 [sqlcmd](../tools/sqlcmd-utility.md) 및 [bcp](../tools/bcp-utility.md)를 설치합니다.

1. Microsoft Red Hat 리포지토리 구성 파일을 다운로드합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. 이전 버전의 **mssql-tools**가 설치되어 있는 경우 이전 unixODBC 패키지를 제거합니다.

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. 다음 명령을 실행하여 unixODBC 개발자 패키지와 함께 **mssql-tools**를 설치합니다.

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. 편의를 위해 **PATH** 환경 변수에 `/opt/mssql-tools/bin/`를 추가합니다. 이렇게 하면 전체 경로를 지정하지 않고 도구를 실행할 수 있습니다. 다음 명령을 실행하여 로그인 세션과 대화형/비로그인 세션에 대한 **PATH**를 수정합니다.

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
