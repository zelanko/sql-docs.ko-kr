---
title: Ubuntu Server 2017 SQL 시작 | Microsoft Docs
description: 이 퀵 스타트의 Ubuntu에 SQL Server 2017을 설치할 로컬 폴더를 만들고 sqlcmd 사용 하 여 데이터베이스를 쿼리 하는 방법을 보여 줍니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/22/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 140aa9d888eb2e58963dda50e3ff7a6fb68d37fe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>SQL Server를 설치 하는 빠른 시작: ubuntu 데이터베이스를 만듭니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 빠른 시작에서 먼저 Ubuntu 16.04에 SQL Server 2017를 설치 합니다. 다음으로 첫 번째 데이터베이스를 만들고 쿼리를 실행하기 위해서 **sqlcmd** 를 사용해서 연결합니다.

> [!TIP]
> 이 자습서에는 사용자 입력 및 인터넷 연결이 필요합니다. 만약 [무인](sql-server-linux-setup.md#unattended) 또는 [오프라인](sql-server-linux-setup.md#offline) 설치 절차에 관심이 있는 경우는, [SQL Server on Linux 설치 지침](sql-server-linux-setup.md)을 참조합니다.

## <a name="prerequisites"></a>필수 구성 요소

사용 하는 Ubuntu 16.04 컴퓨터가 있어야 **최소 2GB** 메모리입니다.

Ubuntu을 사용자의 컴퓨터에 설치 하려면로 이동 [ http://www.ubuntu.com/download/server ](http://www.ubuntu.com/download/server)합니다. 또한 Azure에서 Ubuntu 가상 머신을 만들 수도 있습니다. [Azure CLI로 Linux VM을 만들고 관리하기](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)를 참조하십시오.

> [!NOTE]
> 현재 Windows 10의 [Linux용 Windows 하위 시스템](https://msdn.microsoft.com/commandline/wsl/about) 은 지원되지 않는 설치 대상입니다. 

다른 시스템 요구 사항에 대해서는 [SQL Server on Linux에 대한 시스템 요구 사항](sql-server-linux-setup.md#system)을 참조하십시오.

## <a id="install"></a>SQL Server 설치

Ubuntu에 SQL Server를 구성하려면, **mssql 서버** 패키지를 설치하는 다음 명령을 터미널에서 실행합니다.

> [!IMPORTANT]
> SQL Server 2017의 CTP나 RC 릴리스를 미리 설치한 경우, GA 리포지토리 중 하나를 등록하기 전에 이전 리포지토리를 먼저 제거해야 합니다. 자세한 내용은 [Preview 리포지토리에서 GA 리포지토리로 변경](sql-server-linux-change-repo.md)을 참고하십시오.

1. 공용 리포지토리 GPG 키를 가져옵니다.

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Microsoft SQL Server Ubuntu 리포지토리를 등록합니다.

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!NOTE]
   > CU(누적 업데이트) 리포지토리입니다. 리포지토리 옵션 및 그 차이점에 대한 자세한 내용은 [Linux에서 SQL Server 용 리포지토리 구성](sql-server-linux-change-repo.md)을 참조하십시오.

1. SQL Server를 설치하려면 다음 명령을 실행합니다.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

1. 패키지 설치가 완료된 후, **mssql-conf setup**을 실행하고 지시에 따라 SA 암호를 설정하고 해당 버전을 선택합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 이 자습서에서는 SQL Server 2017을 사용하는 경우, Evaluation, Developer 및 Express 버전은 자유롭게 사용이 가능합니다.

   > [!NOTE]
   > SA 계정에 대한 강력한 암호를 지정해야 합니다(최소 길이가 8자, 대문자와 소문자를 포함, 10 진수 및/또는 영숫자가 아닌 기호).

1. 구성 작업이 완료되면 서비스가 실행되고 있는지 확인합니다.

   ```bash
   systemctl status mssql-server
   ```

1. 원격으로 연결하려면 방화벽에서 SQL Server TCP 포트(기본값 1433)를 열어야 할 수도 있습니다.

이제 SQL Server가 Ubuntu 컴퓨터에서 실행되고 있으며 사용할 준비가 되었습니다!

## <a id="tools"></a>SQL Server 명령줄 도구 설치

데이터베이스를 만들려면 Transact-SQL 문을 실행할 수 있는 도구로 SQL Server에 연결해야 합니다. 다음 단계를 수행하여 SQL Server 명령줄 도구([sqlcmd](../tools/sqlcmd-utility.md) 및 [bcp](../tools/bcp-utility.md)) 를 설치합니다.

다음 단계를 사용 하 여 설치 하는 **mssql 도구** ubuntu 합니다. 

1. 공용 저장소 GPG 키를 가져옵니다.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Microsoft Ubuntu 리포지토리를 등록 합니다.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. 원본 목록 업데이트 하 고 설치 명령을 unixODBC 개발자 패키지가 함께 실행 합니다.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > 최신 버전으로 업데이트 하려면 **mssql 도구** 다음 명령을 실행 합니다.
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **선택적**: 추가 `/opt/mssql-tools/bin/` 하 여 **경로** bash 셸의 환경 변수입니다.

   있도록 **sqlcmd/bcp** 로그인 세션에 대 한 bash 셸의에서 액세스할 수 있는 수정 프로그램 **경로** 에 **~/.bash_profile** 다음 명령 사용 하 여 파일:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   있도록 **sqlcmd/bcp** 대화형/비-로그인 세션에 대 한 bash 셸의에서 액세스할 수 있는 수정 된 **경로** 에 **~/.bashrc** 다음 명령 사용 하 여 파일:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd** 는 SQL Server에 연결해서 쿼리를 실행하고 관리 및 개발 작업을 수행하는 하나의 도구입니다. 다른 도구는 다음과 같습니다.
>
> * [SQL Server Operations Studio(미리 보기)](../sql-operations-studio/what-is.md)
> * 다른 도구는 [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md)
> * 및[Visual Studio Code](sql-server-linux-develop-use-vscode.md)가 있습니다.
> * [mssql-cli(미리 보기)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
