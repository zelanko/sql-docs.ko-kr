---
title: Ubuntu의 SQL Server 시작
titleSuffix: SQL Server
description: 이 빠른 시작에는 SQL Server 2017 또는 SQL Server 2019 Ubuntu에 설치 로컬 폴더를 만들고 sqlcmd 사용 하 여 데이터베이스를 쿼리 하는 방법을 보여 줍니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/28/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 93b02908a1341af18044c1c8a86dfd2e6024f8f3
ms.sourcegitcommit: 02df4e7965b2a858030bb508eaf8daa9bc10b00b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66265359"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>빠른 시작: SQL Server를 설치 하 고 Ubuntu에서 데이터베이스 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]


<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

이 빠른 시작에서는 SQL Server 2017 또는 SQL Server 2019 preview에 설치한 Ubuntu 16.04 합니다. 다음 사용 하 여 연결한 **sqlcmd** 첫 번째 데이터베이스를 만들고 쿼리를 실행 합니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

이 빠른 시작에서는 Ubuntu 16.04에 SQL Server 2019 preview를 설치 합니다. 다음 사용 하 여 연결한 **sqlcmd** 첫 번째 데이터베이스를 만들고 쿼리를 실행 합니다.

::: moniker-end

> [!TIP]
> 이 자습서에는 사용자 입력 및 인터넷 연결이 필요합니다. 참조 무인 또는 오프 라인 설치 절차에 관심이 [Linux의 SQL Server에 대 한 설치 지침은](sql-server-linux-setup.md)합니다.

## <a name="prerequisites"></a>사전 요구 사항

사용 하 여 Ubuntu 16.04 컴퓨터가 있어야 **2GB 이상의** 메모리입니다.

Ubuntu 16.04를 자신의 컴퓨터에 설치 하려면로 이동 [ http://releases.ubuntu.com/xenial/ ](http://releases.ubuntu.com/xenial/)합니다. 또한 Azure에서 Ubuntu 가상 머신을 만들 수도 있습니다. [Azure CLI로 Linux VM을 만들고 관리하기](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)를 참조하십시오.

> [!NOTE]
> 현재 Windows 10의 [Linux용 Windows 하위 시스템](https://msdn.microsoft.com/commandline/wsl/about) 은 지원되지 않는 설치 대상입니다. 

다른 시스템 요구 사항에 대해서는 [SQL Server on Linux에 대한 시스템 요구 사항](sql-server-linux-setup.md#system)을 참조하십시오.

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>SQL Server 설치

Ubuntu에 SQL Server를 구성하려면, **mssql 서버** 패키지를 설치하는 다음 명령을 터미널에서 실행합니다.

1. 공용 리포지토리 GPG 키를 가져옵니다.

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Microsoft SQL Server Ubuntu 리포지토리를 등록합니다.

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!TIP]
   > SQL Server 2019 시도 하려는 경우 대신를 등록 해야 합니다 **미리 보기 (2019)** 리포지토리. SQL Server 2019 설치의 경우 다음 명령을 사용 합니다.
   >
   > ```bash
   > sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
   > ```

3. SQL Server를 설치하려면 다음 명령을 실행합니다.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
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
   systemctl status mssql-server --no-pager
   ```

6. 원격으로 연결하려면 방화벽에서 SQL Server TCP 포트(기본값 1433)를 열어야 할 수도 있습니다.

이제 SQL Server가 Ubuntu 컴퓨터에서 실행되고 있으며 사용할 준비가 되었습니다!

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>SQL Server 설치

Ubuntu에 SQL Server를 구성하려면, **mssql 서버** 패키지를 설치하는 다음 명령을 터미널에서 실행합니다.

1. 공용 리포지토리 GPG 키를 가져옵니다.

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. SQL Server 2019 preview 용 Microsoft SQL Server Ubuntu 리포지토리를 등록 합니다.

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
   ```

3. SQL Server를 설치하려면 다음 명령을 실행합니다.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. 패키지 설치가 완료된 후, **mssql-conf setup**을 실행하고 지시에 따라 SA 암호를 설정하고 해당 버전을 선택합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > SA 계정에 대한 강력한 암호를 지정해야 합니다(최소 길이가 8자, 대문자와 소문자를 포함, 10 진수 및/또는 영숫자가 아닌 기호).

5. 구성 작업이 완료되면 서비스가 실행되고 있는지 확인합니다.

   ```bash
   systemctl status mssql-server --no-pager
   ```

6. 원격으로 연결하려면 방화벽에서 SQL Server TCP 포트(기본값 1433)를 열어야 할 수도 있습니다.

이 시점에서 SQL Server 2019 미리 보기 Ubuntu 컴퓨터에서 실행 되 고 사용할 준비가 되었습니다!

::: moniker-end

## <a id="tools"></a>SQL Server 명령줄 도구 설치

데이터베이스를 만들려면 Transact-SQL 문을 실행할 수 있는 도구로 SQL Server에 연결해야 합니다. 다음 단계를 수행하여 SQL Server 명령줄 도구([sqlcmd](../tools/sqlcmd-utility.md) 및 [bcp](../tools/bcp-utility.md)) 를 설치합니다.

다음 단계를 사용 하 여 설치 합니다 **mssql 도구** ubuntu 합니다. 

1. 공용 리포지토리 GPG 키를 가져옵니다.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Microsoft Ubuntu 리포지토리를 등록 합니다.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. 원본 목록을 업데이트 하 고 unixODBC 개발자 패키지를 사용 하 여 설치 명령을 실행 합니다.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > 최신 버전으로 업데이트 **mssql 도구** 다음 명령을 실행 합니다.
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **선택적**: 추가 `/opt/mssql-tools/bin/` 에 사용자 **경로** 는 bash 셸에서 환경 변수입니다.

   되도록 **sqlcmd/bcp** 로그인 세션에 대 한 bash 셸에서 액세스할 수 있는 수정 프로그램 **경로** 에 **~/.bash_profile** 다음 명령 사용 하 여 파일:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   되도록 **sqlcmd/bcp** 대화형/비-로그인 세션에 대 한 bash 셸에서 액세스할 수 있는 수정 합니다 **경로** 에 **~/.bashrc** 다음 명령 사용 하 여 파일:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
