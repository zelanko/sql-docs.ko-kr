---
title: 'SUSE: SQL Server on Linux 설치'
description: 이 빠른 시작에서는 SUSE Linux Enterprise Server에 SQL Server 2017 또는 SQL Server 2019를 설치한 다음, sqlcmd를 사용하여 데이터베이스를 만들고 쿼리하는 방법을 보여 줍니다.
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.openlocfilehash: 811438987106a5eb73a914e5d7bbceb139cd5c37
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558637"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>빠른 시작: SQL Server 설치 및 SUSE Linux Enterprise Server에 데이터베이스 만들기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

이 빠른 시작에서는 SLES(SUSE Linux Enterprise Server) v12 SP2에 SQL Server 2017 또는 SQL Server 2019를 설치합니다. 그런 다음, **sqlcmd**를 통해 연결하여 첫 번째 데이터베이스를 만들고 쿼리를 실행합니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

이 빠른 시작에서는 SLES(SUSE Linux Enterprise Server) v12에 SQL Server 2019를 설치합니다. 그런 다음, **sqlcmd**를 통해 연결하여 첫 번째 데이터베이스를 만들고 쿼리를 실행합니다.

> [!IMPORTANT]
> SQL Server 2019는 SUSE Enterprise Linux Server v12 SP2, SP3 또는 SP4에서 지원됩니다.

::: moniker-end

> [!TIP]
> 이 자습서를 사용하려면 사용자 입력과 인터넷 연결이 필요합니다. [무인](sql-server-linux-setup.md#unattended) 또는 [오프라인](sql-server-linux-setup.md#offline) 설치 절차에 관심이 있는 경우 [SQL Server on Linux 설치 지침](sql-server-linux-setup.md)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

**최소 2GB**의 메모리를 포함하는 SLES v12 SP2 머신이 있어야 합니다. 파일 시스템은 **XFS** 또는 **EXT4**여야 합니다. **BTRFS** 등의 다른 파일 시스템은 지원되지 않습니다.

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

**최소 2GB**의 메모리를 사용하는 SLES v12 SP2, SP3 또는 SP4 머신이 있어야 합니다. 파일 시스템은 **XFS** 또는 **EXT4**여야 합니다. **BTRFS** 등의 다른 파일 시스템은 지원되지 않습니다.

::: moniker-end

사용자의 머신에 SUSE Linux Enterprise Server를 설치하려면 [https://www.suse.com/products/server](https://www.suse.com/products/server)으로 이동합니다. Azure에서 SLES 가상 머신을 만들 수도 있습니다. [Azure CLI를 사용하여 Linux VM 만들기 및 관리](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)를 참조하고 `az vm create`에 대한 호출에 `--image SLES`을 사용하세요.

이전에 SQL Server의 CTP 또는 RC 릴리스를 설치한 경우 다음 단계를 수행하기 전에 이전 리포지토리를 제거해야 합니다. 자세한 내용은 [SQL Server 2017 및 2019에 대한 Linux 리포지토리 구성](sql-server-linux-change-repo.md)을 참조하세요.

> [!NOTE]
> 현재 Windows 10의 [Linux용 Windows 하위 시스템](https://msdn.microsoft.com/commandline/wsl/about)은 설치 대상으로 지원되지 않습니다.

기타 시스템 요구 사항은 [SQL Server on Linux에 대한 시스템 요구 사항](sql-server-linux-setup.md#system)을 참조하세요.

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>SQL Server 설치

SLES에서 SQL Server을 구성하려면 터미널에서 다음 명령을 실행하여 **mssql-server** 패키지를 설치합니다.

1. Microsoft SQL Server 2017 SLES 리포지토리 구성 파일을 다운로드합니다.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   ```

   > [!TIP]
   > SQL Server 2019를 설치하려면 대신 SQL Server 2019 리포지토리를 등록해야 합니다. SQL Server 2019 설치에는 다음 명령을 사용합니다.
   >
   > ```bash
   > sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo
   > ```

2. 리포지토리를 새로 고칩니다.

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. 다음 명령을 실행하여 SQL Server를 설치합니다.

   ```bash
   sudo zypper install -y mssql-server
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
   systemctl status mssql-server
   ```

6. 원격으로 연결하려면 방화벽에서 SQL Server TCP 포트(기본값 1433)를 열어야 할 수도 있습니다. SuSE 방화벽을 사용하는 경우 **/etc/sysconfig/SuSEfirewall2** 구성 파일을 편집해야 합니다. SQL Server 포트 번호를 포함하도록 **FW_SERVICES_EXT_TCP** 항목을 수정합니다.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

이제 SQL Server는 SLES 머신에서 실행 중이며 사용할 준비가 되었습니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>SQL Server 설치

SLES에서 SQL Server을 구성하려면 터미널에서 다음 명령을 실행하여 **mssql-server** 패키지를 설치합니다.

1. Microsoft SQL Server 2019 SLES 리포지토리 구성 파일을 다운로드합니다.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo
   ```

2. 리포지토리를 새로 고칩니다.

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. 다음 명령을 실행하여 SQL Server를 설치합니다.

   ```bash
   sudo zypper install -y mssql-server
   ```

4. 패키지 설치가 완료되면 **mssql-conf setup**을 실행하고, 프롬프트에 따라 SA 암호를 설정하고, 버전을 선택합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > SA 계정의 강력한 암호를 지정해야 합니다(대문자 및 소문자, 기본 10자리 숫자 및/또는 영숫자가 아닌 기호를 포함 하여 최소 길이 8자).

5. 구성이 완료되면 서비스가 실행 중인지 확인합니다.

   ```bash
   systemctl status mssql-server
   ```

6. 원격으로 연결하려면 방화벽에서 SQL Server TCP 포트(기본값 1433)를 열어야 할 수도 있습니다. SuSE 방화벽을 사용하는 경우 **/etc/sysconfig/SuSEfirewall2** 구성 파일을 편집해야 합니다. SQL Server 포트 번호를 포함하도록 **FW_SERVICES_EXT_TCP** 항목을 수정합니다.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

이제 SQL Server 2019는 SLES 머신에서 실행 중이며 사용할 준비가 되었습니다.

::: moniker-end


## <a id="tools"></a>SQL Server 명령줄 도구 설치

데이터베이스를 만들려면 SQL Server에서 Transact-SQL 문을 실행할 수 있는 도구와 연결해야 합니다. 다음 단계에서는 SQL Server 명령줄 도구인 [sqlcmd](../tools/sqlcmd-utility.md) 및 [bcp](../tools/bcp-utility.md)를 설치합니다.

1. Zypper에 Microsoft SQL Server 리포지토리를 추가합니다.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. unixODBC 개발자 패키지와 함께 **mssql-tools**를 설치합니다.

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
   ```

1. 편의를 위해 **PATH** 환경 변수에 `/opt/mssql-tools/bin/`를 추가합니다. 이렇게 하면 전체 경로를 지정하지 않고 도구를 실행할 수 있습니다. 다음 명령을 실행하여 로그인 세션과 대화형/비로그인 세션에 대한 **PATH**를 수정합니다.

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
