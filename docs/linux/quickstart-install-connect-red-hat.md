---
title: "Red Hat Enterprise Linux에서 SQL Server 2017 시작 | Microsoft Docs"
description: "이 빠른 시작에서는 Red Hat Enterprise Linux에 SQL Server 2017을 설치할 로컬 폴더를 만들고 sqlcmd 사용 하 여 데이터베이스를 쿼리 하는 방법을 보여 줍니다."
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.workload: Active
ms.openlocfilehash: cea19257746be6e16c835764605eb6005e565dab
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="install-sql-server-and-create-a-database-on-red-hat"></a>Red Hat에서 데이터베이스를 만들고 SQL Server 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 빠른 시작에서 처음 설치할 SQL Server 2017에 Red Hat Enterprise Linux (RHEL) 7.3 + 합니다. 다음으로 연결 **sqlcmd** 첫 번째 데이터베이스를 만들고 쿼리를 실행 합니다.

> [!TIP]
> 이 자습서에는 사용자 입력 및 인터넷 연결이 필요합니다. 에 관심이 있는 경우는 [무인](sql-server-linux-setup.md#unattended) 또는 [오프 라인](sql-server-linux-setup.md#offline) 설치 절차 참조 [Linux에서 SQL Server에 대 한 설치 지침](sql-server-linux-setup.md)합니다.

## <a name="prerequisites"></a>필수 구성 요소

RHEL 7.3 또는 7.4 컴퓨터 있어야 **최소 2GB** 메모리입니다.

Red Hat Enterprise Linux을 사용자의 컴퓨터에 설치 하려면로 이동 [http://access.redhat.com/products/red-hat-enterprise-linux/evaluation](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)합니다. 또한 Azure에서 RHEL 가상 컴퓨터를 만들 수 있습니다. 참조 [만들기 및 Azure CLI Linux Vm 관리](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)를 사용 하 여 `--image RHEL` 에 대 한 호출에서 `az vm create`합니다.

다른 시스템 요구 사항에 대 한 참조 [Linux에서 SQL Server에 대 한 시스템 요구 사항](sql-server-linux-setup.md#system)합니다.

## <a id="install"></a>SQL Server 설치

RHEL에 SQL Server를 구성 하려면 종료를 설치 하려면 다음 명령을 실행는 **mssql 서버** 패키지:

> [!IMPORTANT]
> CTP 또는 SQL Server 2017 RC 릴리스 이전에 설치한 경우 GA 저장소 중 하나를 등록 하기 전에 이전 저장소를 먼저 제거 해야 있습니다. 자세한 내용은 참조 [GA 저장소에 미리 보기 저장소에서 리포지토리 변경](sql-server-linux-change-repo.md)합니다.

1. Microsoft SQL Server Red Hat 저장소 구성 파일을 다운로드 합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!NOTE]
   > CU (누적 업데이트) 저장소입니다. 저장소 옵션 및 간 차이점에 대 한 자세한 내용은 참조 [소스 저장소 변경](sql-server-linux-setup.md#repositories)합니다.

1. SQL Server를 설치 하려면 다음 명령을 실행 합니다.

   ```bash
   sudo yum install -y mssql-server
   ```

1. 실행 패키지 설치 완료 후 **mssql conf 설치** 지시에 따라 SA 암호를 설정 하 고 해당 버전을 선택 하 고 있습니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```
   > [!TIP]
   > 이 자습서에서는 SQL Server 2017을 시도 하는 경우 다음과 같은 버전 자유롭게 사용이 허가 됩니다: Evaluation, Developer 및 Express입니다.

   > [!NOTE]
   > (최소 길이가 8 자, 대문자를 포함 하 고 소문자, 10 진수 및/또는 영숫자가 아닌 기호가) SA 계정에 대 한 강력한 암호를 지정 해야 합니다.

1. 구성 작업이 완료 되 면 서비스가 실행 되 고 있는지 확인 합니다.

   ```bash
   systemctl status mssql-server
   ```
   
1. 원격 연결을 허용 하려면 RHEL에 방화벽에서 SQL Server 포트를 엽니다. 기본 SQL Server 포트는 TCP 1433입니다. 사용 중인 경우 **FirewallD** 방화벽에 대 한 다음 명령을 사용할 수 있습니다.

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

이 시점에서 SQL Server RHEL 컴퓨터에서 실행 되 고 사용할 준비가 되었습니다!

## <a id="tools"></a>SQL Server 명령줄 도구를 설치 합니다.

데이터베이스를 만들려면 SQL Server에서 TRANSACT-SQL 문을 실행할 수 있는 도구와 연결 해야 합니다. SQL Server 명령줄 도구를 설치 하는 다음 단계를 수행: [sqlcmd](../tools/sqlcmd-utility.md) 및 [bcp](../tools/bcp-utility.md)합니다.

1. Red Hat Microsoft 저장소 구성 파일을 다운로드 합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. 이전 버전의 경우 **mssql 도구** 설치 이전 unixODBC 패키지를 제거 합니다.

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. 설치 하려면 다음 명령을 실행 **mssql 도구** unixODBC 개발자 패키지와 함께 합니다.

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. 편의 위해 추가 `/opt/mssql-tools/bin/` 하 여 **경로** 환경 변수입니다. 따라서 전체 경로 지정 하지 않고 도구를 실행할 수 있습니다. 수정 하려면 다음 명령을 실행 하는 **경로** 로그인 세션 및 대화형/비-로그인 세션 모두에 대해:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd** 쿼리를 실행 하 고 관리 및 개발 작업을 수행 하도록 SQL Server에 연결 하기 위한 하나의 도구입니다. 다른 도구는 다음과 같습니다.
>
> * [SQL Server 작업 Studio (미리 보기)](../sql-operations-studio/what-is.md)
> * [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md)
> * [Visual Studio Code](sql-server-linux-develop-use-vscode.md)합니다.
> * [mssql-cli (미리 보기)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
