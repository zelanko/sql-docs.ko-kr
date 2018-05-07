---
title: Red Hat Enterprise Linux에서 SQL Server 2017 시작 | Microsoft Docs
description: 이 빠른 시작 자습서에서는 Red Hat Enterprise Linux에 SQL Server 2017을 설치할 로컬 폴더를 만들고 sqlcmd를 사용하여 데이터베이스를 쿼리하는 방법을 보여줍니다.
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
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: 9d23843466886a70d18038988d00c7152075ff07
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>SQL Server를 설치 하는 빠른 시작: Red Hat에 SQL Server를 설치하고 데이터베이스 만들기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 빠른 시작 자습서에서는 먼저 Red Hat Enterprise Linux (RHEL) 7.3 +에 SQL Server 2017를 설치합니다. 다음으로 첫 번째 데이터베이스를 만들고 쿼리를 실행하기 위해서 **sqlcmd** 를 사용해서 연결합니다.

> [!TIP]
> 이 자습서에는 사용자 입력 및 인터넷 연결이 필요합니다. 만약 [무인](sql-server-linux-setup.md#unattended) 또는 [오프라인](sql-server-linux-setup.md#offline) 설치 절차에 관심이 있는 경우는, [SQL Server on Linux 설치 지침](sql-server-linux-setup.md)을 참조합니다.

## <a name="prerequisites"></a>필수 구성 요소

**2GB 이상** 메모리를 가진 RHEL 7.3 또는 7.4 컴퓨터가 있어야 합니다.

Red Hat Enterprise Linux을 사용자의 컴퓨터에 설치 하려면로 이동 [ http://access.redhat.com/products/red-hat-enterprise-linux/evaluation ](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)합니다. 또한 Azure에서 RHEL 가상 머신을 만들 수도 있습니다. [Azure CLI로 Linux VM을 만들고 관리하기](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm) 를 참조하여, `az vm create` 를 호출 시 `--image RHEL` 를 사용합니다.

다른 시스템 요구 사항에 대해서는 [SQL Server on Linux에 대한 시스템 요구 사항](sql-server-linux-setup.md#system) 을 참조하십시오.

## <a id="install"></a>SQL Server 설치

RHEL에 SQL Server를 구성하려면, **mssql-server** 패키지를 설치하는 다음 명령을 터미널에서 실행합니다.

> [!IMPORTANT]
> SQL Server 2017의 CTP나 RC 릴리스를 미리 설치한 경우, GA 리포지토리 중 하나를 등록하기 전에 이전 리포지토리를 먼저 제거해야 합니다. 자세한 내용은 [Preview 리포지토리에서 GA 리포지토리로 변경](sql-server-linux-change-repo.md) 을 참고합니다.

1. Microsoft SQL Server Red Hat 리포지토리 구성 파일을 다운로드합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!NOTE]
   > CU(누적 업데이트) 리포지토리입니다. 리포지토리 옵션 및 그 차이점에 대한 자세한 내용은 [Linux에서 SQL Server 용 리포지토리 구성](sql-server-linux-change-repo.md)을 참조하십시오.

1. SQL Server를 설치하려면 다음 명령을 실행합니다.

   ```bash
   sudo yum install -y mssql-server
   ```

1. 패키지 설치가 완료된 후, **mssql-conf setup**을 실행하고 지시에 따라 SA 암호를 설정하고 해당 버전을 선택합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```
   > [!TIP]
   > 이 자습서에서는 SQL Server 2017을 사용하는 경우, Evaluation, Developer 및 Express 버전은 자유롭게 사용이 가능합니다.

   > [!NOTE]
   > SA 계정에 대한 강력한 암호를 지정해야 합니다(최소 길이가 8자, 대문자와 소문자를 포함, 10 진수 및/또는 영숫자가 아닌 기호).

1. 구성 작업이 완료되면, 서비스가 실행되고 있는지 확인합니다.

   ```bash
   systemctl status mssql-server
   ```
   
1. 원격 연결을 허용하려면 RHEL의 방화벽에서 SQL Server 포트를 엽니다. 기본 SQL Server 포트는 TCP 1433입니다. 방화벽으로 **FirewallD** 를 사용하는 경우, 다음 명령을 사용할 수 있습니다.

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

이제 SQL Server가 RHEL 컴퓨터에서 실행되고 있으며 사용할 준비가 되었습니다!

## <a id="tools"></a>SQL Server 명령줄 도구 설치

데이터베이스를 만들려면 Transact-SQL 문을 실행할 수 있는 도구로 SQL Server에 연결해야 합니다. 다음 단계를 수행하여 SQL Server 명령줄 도구([sqlcmd](../tools/sqlcmd-utility.md) 및 [bcp](../tools/bcp-utility.md)) 를 설치합니다.

1. Microsoft Red Hat 리포지토리 구성 파일을 다운로드합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. 이전 버전의 **mssql-tools** 가 설치된 경우, 기존 unixODBC 패키지를 제거합니다.

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. unixODBC 개발자 패키지와 함께 **mssql-tools** 를 설치하려면 다음 명령을 실행합니다.

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. 편의를 위해, `/opt/mssql-tools/bin/` 을 **PATH** 환경 변수에 추가합니다. 이는 전체 경로를 지정하지 않고 도구를 실행할 수 있게 해줍니다. 로그인 세션 및 대화형/비-로그인 세션 모두에 대해 **PATH** 를 수정하려면 다음 명령을 실행합니다.

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
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
