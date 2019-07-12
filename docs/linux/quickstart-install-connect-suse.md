---
title: SUSE Linux Enterprise Server의 SQL Server 시작
titleSuffix: SQL Server
description: 이 빠른 시작에는 SUSE Linux Enterprise Server에서 SQL Server 2017 또는 SQL Server 2019 설치 로컬 폴더를 만들고 sqlcmd 사용 하 여 데이터베이스를 쿼리 하는 방법을 보여 줍니다.
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.openlocfilehash: 19f74067db365fd9bdc867b97cef6ee5aa5162d8
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833255"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>빠른 시작: SUSE Linux Enterprise Server에서 데이터베이스를 만들고 SQL Server 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

이 빠른 시작에서는 SQL Server 2017 또는 SQL Server 2019 preview에 설치한 SUSE Linux Enterprise Server (SLES) v12 SP2. 다음 사용 하 여 연결한 **sqlcmd** 첫 번째 데이터베이스를 만들고 쿼리를 실행 합니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

이 빠른 시작에서는 SUSE Linux Enterprise Server (SLES) v12 SP2에서 SQL Server 2019 preview를 설치 합니다. 다음 사용 하 여 연결한 **sqlcmd** 첫 번째 데이터베이스를 만들고 쿼리를 실행 합니다.

::: moniker-end

> [!TIP]
> 이 자습서에는 사용자 입력 및 인터넷 연결이 필요합니다. 만약 [무인](sql-server-linux-setup.md#unattended) 또는 [오프라인](sql-server-linux-setup.md#offline) 설치 절차에 관심이 있는 경우는, [SQL Server on Linux 설치 지침](sql-server-linux-setup.md)을 참조합니다.

## <a name="prerequisites"></a>사전 요구 사항

SLES v12 SP2 컴퓨터 있어야 **2GB 이상의** 메모리입니다. 파일 시스템에 있어야 **XFS** 하거나 **EXT4**합니다. 와 같은 다른 파일 시스템 **BTRFS**, 지원 되지 않습니다.

SUSE Linux Enterprise Server 자신의 컴퓨터에 설치 하려면로 이동 [ https://www.suse.com/products/server ](https://www.suse.com/products/server)합니다. 또한 Azure에서 SLES 가상 머신을 만들 수 있습니다. [Azure CLI로 Linux VM을 만들고 관리하기](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm) 를 참조하여, `az vm create` 를 호출 시 `--image SLES` 를 사용합니다.

CTP 또는 SQL Server 2017 RC 릴리스 이전에 설치한 경우 다음 단계를 수행 하기 전에 이전 리포지토리를 먼저 제거 해야 합니다. 자세한 내용은 [SQL Server 2017 및 2019에 대해 Linux 구성 리포지토리](sql-server-linux-change-repo.md)합니다.

> [!NOTE]
> 현재 Windows 10의 [Linux용 Windows 하위 시스템](https://msdn.microsoft.com/commandline/wsl/about) 은 지원되지 않는 설치 대상입니다.

다른 시스템 요구 사항에 대해서는 [SQL Server on Linux에 대한 시스템 요구 사항](sql-server-linux-setup.md#system)을 참조하십시오.

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>SQL Server 설치

SLES의 SQL Server를 구성 하려면 설치 하려면 터미널에서 다음 명령을 실행 합니다 **mssql server** 패키지:

1. Microsoft SQL Server 2017 SLES 리포지토리 구성 파일을 다운로드 합니다.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   ```

   > [!TIP]
   > SQL Server 2019 시도 하려는 경우 대신를 등록 해야 합니다 **미리 보기 (2019)** 리포지토리. SQL Server 2019 설치의 경우 다음 명령을 사용 합니다.
   >
   > ```bash
   > sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo
   > ```

2. 리포지토리를 새로 고칩니다.

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. SQL Server를 설치하려면 다음 명령을 실행합니다.

   ```bash
   sudo zypper install -y mssql-server
   ```

4. 패키지 설치가 완료된 후, **mssql-conf setup**을 실행하고 지시에 따라 SA 암호를 설정하고 해당 버전을 선택합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 다음 SQL Server 2017 버전 자유롭게 사용이 허가 됩니다. Evaluation, Developer 및 Express입니다.

   > [!NOTE]
   > SA 계정에 대한 강력한 암호를 지정해야 합니다(최소 길이가 8자, 대문자와 소문자를 포함, 10 진수 및/또는 영숫자가 아닌 기호).

5. 구성 작업이 완료되면 서비스가 실행되고 있는지 확인합니다.

   ```bash
   systemctl status mssql-server
   ```

6. 원격으로 연결하려면 방화벽에서 SQL Server TCP 포트(기본값 1433)를 열어야 할 수도 있습니다. SuSE 방화벽을 사용 하는 경우 편집 해야 합니다 **/etc/sysconfig/SuSEfirewall2** 구성 파일입니다. 수정 된 **FW_SERVICES_EXT_TCP** SQL Server 포트 번호를 포함 하는 항목입니다.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

이 시점에서 SQL Server SLES 컴퓨터에서 실행 되 고 사용할 준비가 되었습니다!

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>SQL Server 설치

SLES의 SQL Server를 구성 하려면 설치 하려면 터미널에서 다음 명령을 실행 합니다 **mssql server** 패키지:

1. Microsoft SQL Server 2019 미리 보기 SLES 리포지토리 구성 파일을 다운로드 합니다.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo
   ```

2. 리포지토리를 새로 고칩니다.

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. SQL Server를 설치하려면 다음 명령을 실행합니다.

   ```bash
   sudo zypper install -y mssql-server
   ```

4. 패키지 설치가 완료된 후, **mssql-conf setup**을 실행하고 지시에 따라 SA 암호를 설정하고 해당 버전을 선택합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > SA 계정에 대한 강력한 암호를 지정해야 합니다(최소 길이가 8자, 대문자와 소문자를 포함, 10 진수 및/또는 영숫자가 아닌 기호).

5. 구성 작업이 완료되면 서비스가 실행되고 있는지 확인합니다.

   ```bash
   systemctl status mssql-server
   ```

6. 원격으로 연결하려면 방화벽에서 SQL Server TCP 포트(기본값 1433)를 열어야 할 수도 있습니다. SuSE 방화벽을 사용 하는 경우 편집 해야 합니다 **/etc/sysconfig/SuSEfirewall2** 구성 파일입니다. 수정 된 **FW_SERVICES_EXT_TCP** SQL Server 포트 번호를 포함 하는 항목입니다.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

이 시점에서 SQL Server 2019 미리 보기 SLES 컴퓨터에서 실행 되 고 사용할 준비가 되었습니다!

::: moniker-end


## <a id="tools"></a>SQL Server 명령줄 도구 설치

데이터베이스를 만들려면 Transact-SQL 문을 실행할 수 있는 도구로 SQL Server에 연결해야 합니다. 다음 단계를 수행하여 SQL Server 명령줄 도구([sqlcmd](../tools/sqlcmd-utility.md) 및 [bcp](../tools/bcp-utility.md)) 를 설치합니다.

1. Zypper를 사용 하려면 Microsoft SQL Server 리포지토리를 추가 합니다.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. 설치할 **mssql 도구** unixODBC 개발자 패키지를 사용 하 여 합니다.

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
   ```

1. 편의를 위해, `/opt/mssql-tools/bin/` 을 **PATH** 환경 변수에 추가합니다. 이는 전체 경로를 지정하지 않고 도구를 실행할 수 있게 해줍니다. 로그인 세션 및 대화형/비-로그인 세션 모두에 대해 **PATH** 를 수정하려면 다음 명령을 실행합니다.

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
