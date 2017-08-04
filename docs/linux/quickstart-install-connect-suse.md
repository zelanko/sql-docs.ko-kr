---
title: "SUSE Linux Enterprise Server에서 SQL Server 2017 시작 | Microsoft Docs"
description: "이 빠른 시작 자습서에는 SQL Server 2017 SUSE Linux Enterprise Server에 설치할 로컬 폴더를 만들고 sqlcmd 사용 하 여 데이터베이스를 쿼리 하는 방법을 보여 줍니다."
author: sabotta
ms.author: carlasab
manager: craigg
ms.date: 07/24/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 21a482de29640b217f1cf6afe1e7b0eeff0ccf85
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server에서 데이터베이스를 만들고 SQL Server 설치

이 빠른 시작 자습서에서는 먼저 SUSE Linux Enterprise Server (SLES) v12 s p 2에서 SQL Server 2017 r c 2를 설치합니다. 다음으로 연결 **sqlcmd** 첫 번째 데이터베이스를 만들고 쿼리를 실행 합니다.

> [!TIP]
> 이 자습서에는 사용자 입력 및 인터넷 연결이 필요합니다. 에 관심이 있는 경우는 [무인](sql-server-linux-setup.md#unattended) 또는 [오프 라인](sql-server-linux-setup.md#offline) 설치 절차 참조 [Linux에서 SQL Server에 대 한 설치 지침](sql-server-linux-setup.md)합니다.

## <a name="prerequisites"></a>필수 구성 요소

와 SLES v12 SP2 시스템이 있어야 **3.25 GB 이상** 메모리입니다. 파일 시스템을 해야 **XFS** 또는 **EXT4**합니다. 와 같은 다른 파일 시스템, **BTRFS**, 지원 되지 않습니다.

SUSE Linux Enterprise Server를 사용자의 컴퓨터에 설치 하려면로 이동 [https://www.suse.com/products/server](https://www.suse.com/products/server)합니다. 또한 Azure에서 SLES 가상 컴퓨터를 만들 수 있습니다. 참조 [만들기 및 Azure CLI Linux Vm 관리](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)를 사용 하 여 `--image SLES` 에 대 한 호출에서 `az vm create`합니다.

다른 시스템 요구 사항에 대 한 참조 [Linux에서 SQL Server에 대 한 시스템 요구 사항](sql-server-linux-setup.md#system)합니다.

## <a id="install"></a>SQL Server 설치

SLES에 SQL Server를 구성 하려면 종료를 설치 하려면 다음 명령을 실행는 **mssql 서버** 패키지:

1. Microsoft SQL Server SLES 저장소 구성 파일을 다운로드 합니다.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server.repo
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. SQL Server를 설치 하려면 다음 명령을 실행 합니다.

   ```bash
   sudo zypper install -y mssql-server
   ```

1. 실행 패키지 설치 완료 후 **mssql conf 설치** 따르다 SA 암호를 설정 하 고 버전을 선택 합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > (최소 길이가 8 자, 대문자를 포함 하 고 소문자, 10 진수 및/또는 영숫자가 아닌 기호가) SA 계정에 대 한 강력한 암호를 지정 해야 합니다.

   > [!TIP]
   > R c 2를 설치할 때 구매한 라이선스가 없습니다.는 버전 중 하나를 수행 해야 합니다. 출시 후보 이기 때문에 선택한 버전에 관계 없이 다음과 같은 메시지가 나타납니다.
   >
   > `This is an evaluation version.  There are [175] days left in the evaluation period.`
   >
   > 이 메시지는 선택한 버전을 반영 하지 않습니다. R c 2에 대 한 미리 보기 기간을 연결합니다.

1. 구성 작업이 완료 되 면 서비스가 실행 되 고 있는지 확인 합니다.

   ```bash
   systemctl status mssql-server
   ```

1. 원격으로 연결 하려면 방화벽에서 SQL Server TCP 포트 (기본값 1433)를 열려고 할 수도 있습니다.

이 시점에서 SQL Server SLES 컴퓨터에서 실행 되 고 사용할 준비가 되었습니다!

## <a id="tools"></a>SQL Server 명령줄 도구를 설치 합니다.

데이터베이스를 만들려면 SQL Server에서 TRANSACT-SQL 문을 실행할 수 있는 도구와 연결 해야 합니다. SQL Server 명령줄 도구를 설치 하는 다음 단계를 수행: [sqlcmd](../tools/sqlcmd-utility.md) 및 [bcp](../tools/bcp-utility.md)합니다.

1. Zypper에 Microsoft SQL Server 저장소를 추가 합니다.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. 설치 **mssql 도구** unixODBC 개발자 패키지와 함께 합니다.

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
   ```

1. 편의 위해 추가 `/opt/mssql-tools/bin/` 하 여 **경로** 환경 변수입니다. 따라서 전체 경로 지정 하지 않고 도구를 실행할 수 있습니다. 수정 하려면 다음 명령을 실행 하는 **경로** 로그인 세션 및 대화형/비-로그인 세션 모두에 대해:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd** 쿼리를 실행 하 고 관리 및 개발 작업을 수행 하도록 SQL Server에 연결 하기 위한 하나의 도구입니다. 다른 도구로 [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md) 및 [Visual Studio Code](sql-server-linux-develop-use-vscode.md)합니다.

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
