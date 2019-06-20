---
title: Docker에서 SQL Server 데이터베이스를 복원 합니다. | Microsoft Docs
description: 이 자습서에서는 새 Linux Docker 컨테이너에서 SQL Server 데이터베이스 백업을 복원 하는 어떻게 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: f688a95135716a41ae37cb86b50bcb90fc6cce5e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712821"
---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>Linux Docker 컨테이너에서 SQL Server 데이터베이스를 복원 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

이 자습서에는 이동 하 고 Docker에서 실행 하는 SQL Server 2017 Linux 컨테이너 이미지를 SQL Server 백업 파일을 복원 하는 방법을 보여 줍니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

이 자습서에는 이동 하 고 Docker에서 실행 되는 SQL Server 2019 미리 보기 Linux 컨테이너 이미지를 SQL Server 백업 파일을 복원 하는 방법을 보여 줍니다.

::: moniker-end

> [!div class="checklist"]
> * 끌어오기 및 최신 SQL Server Linux 컨테이너 이미지를 실행 합니다.
> * Wide World Importers 데이터베이스 파일을 컨테이너에 복사 합니다.
> * 컨테이너에서 데이터베이스를 복원 합니다.
> * 보고 데이터베이스를 수정 하려면 TRANSACT-SQL 문을 실행 합니다.
> * 수정 된 데이터베이스를 백업 합니다.

## <a name="prerequisites"></a>사전 요구 사항

* 지원되는 모든 Linux 배포판 또는 Mac/Windows용 Docker에서 Docker Engine 1.8+. 자세한 내용은 [사용자 Docker 설치](https://docs.docker.com/engine/installation/)를 참조하세요.
* 최소 2GB의 디스크 공간
* 최소 2GB의 RAM
* [Linux에서 SQL Server에 대한 시스템 요구 사항](sql-server-linux-setup.md#system)

## <a name="pull-and-run-the-container-image"></a>컨테이너 이미지를 끌어와 실행하기

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Linux/Mac에서 bash 터미널 또는 Windows에서 관리자 권한 PowerShell 세션을 엽니다.

1. Docker Hub를 사용하여 SQL Server 2017 Linux 컨테이너 이미지를 끌어오기.

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   > [!TIP]
   > 이 자습서에서는 docker 명령 예제는 bash 셸 (Linux/Mac) 및 PowerShell (Windows)에 대해 제공 됩니다.

1. Docker를 사용 하 여 컨테이너 이미지를 실행 하려면 다음 명령을 사용할 수 있습니다.

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   이 명령은 Developer edition (기본값)를 사용 하 여 SQL Server 2017 컨테이너를 만듭니다. SQL Server 포트 **1433** 포트와 호스트에 노출 됩니다 **1401**합니다. 선택적 `-v sql1data:/var/opt/mssql` 매개 변수 라는 데이터 볼륨 컨테이너를 만듭니다 **sql1ddata**합니다. SQL Server에서 만든 데이터를 유지 하기 위해 사용 됩니다.

   > [!NOTE]
   > 컨테이너에서 프로덕션 SQL Server 버전을 실행 하기 위한 프로세스는 약간 다릅니다. 자세한 내용은 [프로덕션 컨테이너 이미지 실행](sql-server-linux-configure-docker.md#production)을 참조하세요. 동일한 컨테이너 이름 및 포트를 사용 하는 경우이 연습의 나머지 부분 프로덕션 컨테이너를 사용 하 여 계속 작동 합니다.

1. Docker 컨테이너를 보려면 `docker ps` 명령을 사용합니다.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. **상태** 열이 **Up**의 상태를 표시하는 경우, SQL Server는 컨테이너에서 실행되며 **포트** 열의 지정된 포트에서 수신 대기합니다. SQL Server 컨테이너의 **상태** 열이 **Exited**를 표시하는 경우, [구성 가이드의 문제 해결 섹션](sql-server-linux-configure-docker.md#troubleshooting)을 참조하세요.

  ```bash
  $ sudo docker ps -a

  CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
  941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
  ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. Linux/Mac에서 bash 터미널 또는 Windows에서 관리자 권한 PowerShell 세션을 엽니다.

1. Docker 허브에서 SQL Server 2019 미리 보기 Linux 컨테이너 이미지를 끌어옵니다.

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   > [!TIP]
   > 이 자습서에서는 docker 명령 예제는 bash 셸 (Linux/Mac) 및 PowerShell (Windows)에 대해 제공 됩니다.

1. Docker를 사용 하 여 컨테이너 이미지를 실행 하려면 다음 명령을 사용할 수 있습니다.

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   이 명령은 Developer edition (기본값)를 사용 하 여 SQL Server 2019 미리 보기 컨테이너를 만듭니다. SQL Server 포트 **1433** 포트와 호스트에 노출 됩니다 **1401**합니다. 선택적 `-v sql1data:/var/opt/mssql` 매개 변수 라는 데이터 볼륨 컨테이너를 만듭니다 **sql1ddata**합니다. SQL Server에서 만든 데이터를 유지 하기 위해 사용 됩니다.

1. Docker 컨테이너를 보려면 `docker ps` 명령을 사용합니다.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. **상태** 열이 **Up**의 상태를 표시하는 경우, SQL Server는 컨테이너에서 실행되며 **포트** 열의 지정된 포트에서 수신 대기합니다. SQL Server 컨테이너의 **상태** 열이 **Exited**를 표시하는 경우, [구성 가이드의 문제 해결 섹션](sql-server-linux-configure-docker.md#troubleshooting)을 참조하세요.

   ```bash
   $ sudo docker ps -a

   CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
   941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
   ```

::: moniker-end

## <a name="change-the-sa-password"></a>SA 암호 변경

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="copy-a-backup-file-into-the-container"></a>컨테이너에 백업 파일을 복사 합니다.

이 자습서에서는 합니다 [Wide World Importers 샘플 데이터베이스](../sample/world-wide-importers/wide-world-importers-documentation.md)합니다. 다음 절차를 다운로드 하 여 SQL Server 컨테이너에 Wide World Importers 데이터베이스 백업 파일을 복사 합니다.

1. 먼저 사용 하 여 **docker exec** 백업 폴더를 만들어야 합니다. 다음 명령은 만듭니다는 **/var/opt/mssql/backup** SQL Server 컨테이너 내의 디렉터리입니다.

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. 다음으로 다운로드 합니다 [WideWorldImporters Full.bak](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) 호스트 컴퓨터에 파일입니다. 다음 명령을 홈/사용자 디렉터리로 이동 하 고 백업 파일로 다운로드 **wwi.bak**합니다.

   ```bash
   cd ~
   curl -L -o wwi.bak 'https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak'
   ```

   ```PowerShell
   curl -OutFile "wwi.bak" "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak"
   ```

1. 사용 하 여 **docker cp** 컨테이너에 백업 파일을 복사 하는 **/var/opt/mssql/backup** 디렉터리입니다.

   ```bash
   sudo docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

   ```PowerShell
   docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

## <a name="restore-the-database"></a>데이터베이스 복원

백업 파일은 이제 컨테이너 내에서 위치 합니다. 백업을 복원 하기 전에 것이 논리적 파일 이름 및 백업 내에서 파일 형식을 알고 있어야 합니다. 다음 TRANSACT-SQL 명령을 백업을 검사 하 고 사용 하 여 복원을 수행할 **sqlcmd** 컨테이너에 있습니다.

> [!TIP]
> 이 자습서에서는 **sqlcmd** 컨테이너 내 컨테이너는이 도구가 미리 설치 되어 제공 되기 때문입니다. 그러나 실행할 수도 있습니다 TRANSACT-SQL 문을 다른 클라이언트를 사용 하 여 컨테이너의 외부 도구와 같은 [Visual Studio Code](sql-server-linux-develop-use-vscode.md) 하거나 [SQL Server Management Studio](sql-server-linux-manage-ssms.md)합니다. 연결할 컨테이너의 포트 1433에 매핑된 호스트 포트를 사용 합니다. 이 예에서 **1401 localhost** 호스트 컴퓨터에서 및 **Host_IP_Address, 1401** 원격으로 합니다.

1. 실행할 **sqlcmd** 논리적 파일 이름 및 백업 내에서 경로 목록 컨테이너 내에서. 사용 하 여 이렇게 합니다 **RESTORE FILELISTONLY** Transact SQL 문입니다.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost \
      -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE FILELISTONLY FROM DISK = "/var/opt/mssql/backup/wwi.bak"' \
      | tr -s ' ' | cut -d ' ' -f 1-2
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost `
      -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/wwi.bak'"
   ```

   다음과 유사한 출력이 표시 됩니다.

   ```
   LogicalName   PhysicalName
   ------------------------------------------
   WWI_Primary   D:\Data\WideWorldImporters.mdf
   WWI_UserData   D:\Data\WideWorldImporters_UserData.ndf
   WWI_Log   E:\Log\WideWorldImporters.ldf
   WWI_InMemory_Data_1   D:\Data\WideWorldImporters_InMemory_Data_1
   ```

1. 호출을 **RESTORE DATABASE** 명령을 컨테이너 내에서 데이터베이스를 복원 합니다. 이전 단계에서 파일을 각각에 대 한 새 경로 지정 합니다.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE DATABASE WideWorldImporters FROM DISK = "/var/opt/mssql/backup/wwi.bak" WITH MOVE "WWI_Primary" TO "/var/opt/mssql/data/WideWorldImporters.mdf", MOVE "WWI_UserData" TO "/var/opt/mssql/data/WideWorldImporters_userdata.ndf", MOVE "WWI_Log" TO "/var/opt/mssql/data/WideWorldImporters.ldf", MOVE "WWI_InMemory_Data_1" TO "/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE DATABASE WideWorldImporters FROM DISK = '/var/opt/mssql/backup/wwi.bak' WITH MOVE 'WWI_Primary' TO '/var/opt/mssql/data/WideWorldImporters.mdf', MOVE 'WWI_UserData' TO '/var/opt/mssql/data/WideWorldImporters_userdata.ndf', MOVE 'WWI_Log' TO '/var/opt/mssql/data/WideWorldImporters.ldf', MOVE 'WWI_InMemory_Data_1' TO '/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1'"
   ```

   다음과 유사한 출력이 표시 됩니다.

   ```
   Processed 1464 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   Processed 33 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   Processed 3862 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Converting database 'WideWorldImporters' from version 852 to the current version 869.
   Database 'WideWorldImporters' running the upgrade step from version 852 to version 853.
   Database 'WideWorldImporters' running the upgrade step from version 853 to version 854.
   Database 'WideWorldImporters' running the upgrade step from version 854 to version 855.
   Database 'WideWorldImporters' running the upgrade step from version 855 to version 856.
   Database 'WideWorldImporters' running the upgrade step from version 856 to version 857.
   Database 'WideWorldImporters' running the upgrade step from version 857 to version 858.
   Database 'WideWorldImporters' running the upgrade step from version 858 to version 859.
   Database 'WideWorldImporters' running the upgrade step from version 859 to version 860.
   Database 'WideWorldImporters' running the upgrade step from version 860 to version 861.
   Database 'WideWorldImporters' running the upgrade step from version 861 to version 862.
   Database 'WideWorldImporters' running the upgrade step from version 862 to version 863.
   Database 'WideWorldImporters' running the upgrade step from version 863 to version 864.
   Database 'WideWorldImporters' running the upgrade step from version 864 to version 865.
   Database 'WideWorldImporters' running the upgrade step from version 865 to version 866.
   Database 'WideWorldImporters' running the upgrade step from version 866 to version 867.
   Database 'WideWorldImporters' running the upgrade step from version 867 to version 868.
   Database 'WideWorldImporters' running the upgrade step from version 868 to version 869.
   RESTORE DATABASE successfully processed 58455 pages in 18.069 seconds (25.273 MB/sec).
   ```

## <a name="verify-the-restored-database"></a>복원된 된 데이터베이스를 확인 합니다.

컨테이너의 데이터베이스 이름 목록을 표시 하려면 다음 쿼리를 실행 합니다.

```bash
sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
   -Q 'SELECT Name FROM sys.Databases'
```

```PowerShell
docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
   -Q "SELECT Name FROM sys.Databases"
```

나타납니다 **WideWorldImporters** 데이터베이스 목록에서.

## <a name="make-a-change"></a>변경

다음 단계를 데이터베이스에서 변경합니다.

1. 상위 10 개 항목을 보려면 쿼리를 실행 합니다 **Warehouse.StockItems** 테이블입니다.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID"
   ```

   항목 식별자와 이름 목록이 표시 됩니다.

   ```
   StockItemID StockItemName
   ----------- -----------------
             1 USB missile launcher (Green)
             2 USB rocket launcher (Gray)
             3 Office cube periscope (Black)
             4 USB food flash drive - sushi roll
             5 USB food flash drive - hamburger
             6 USB food flash drive - hot dog
             7 USB food flash drive - pizza slice
             8 USB food flash drive - dim sum 10 drive variety pack
             9 USB food flash drive - banana
            10 USB food flash drive - chocolate bar
   ```

1. 다음을 사용 하 여 첫 번째 항목의 설명을 업데이트 **업데이트** 문:

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName="USB missile launcher (Dark Green)" WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName='USB missile launcher (Dark Green)' WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   다음 텍스트와 유사한 출력이 표시 됩니다.

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>새 백업 만들기

복원한 후 데이터베이스 컨테이너에, 정기적으로 실행 중인 컨테이너 내에서 데이터베이스 백업을 만들 수도 있습니다. 단계 이전 단계에 있지만 역순에서 비슷한 패턴을 따릅니다.

1. 사용 하 여는 **BACKUP DATABASE** 컨테이너에 데이터베이스 백업을 만들려면 TRANSACT-SQL 명령입니다. 이 자습서에서는 새 백업 파일을 만듭니다 **wwi_2.bak**에서 이전에 만든 **/var/opt/mssql/backup** 디렉터리입니다.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   다음과 유사한 출력이 표시 됩니다.

   ```
   10 percent processed.
   20 percent processed.
   30 percent processed.
   40 percent processed.
   50 percent processed.
   60 percent processed.
   70 percent processed.
   Processed 1200 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   80 percent processed.
   Processed 3865 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Processed 938 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   100 percent processed.
   BACKUP DATABASE successfully processed 59099 pages in 25.056 seconds (18.427 MB/sec).
   ```

1. 그런 다음 호스트 컴퓨터에 컨테이너에서 백업 파일을 복사 합니다.

   ```bash
   cd ~
   sudo docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

   ```PowerShell
   cd ~
   docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

## <a name="use-the-persisted-data"></a>지속된 된 데이터를 사용 합니다.

데이터 보호를 위한 데이터베이스 백업 외에 데이터 볼륨 컨테이너를 사용할 수 있습니다. 이 자습서에서는 시작 부분을 **sql1** 사용 하 여 컨테이너를 `-v sql1data:/var/opt/mssql` 매개 변수입니다. 합니다 **sql1data** 지속 되 면 데이터 볼륨 컨테이너를 **/var/opt/mssql** 데이터 컨테이너를 제거한 후에 합니다. 다음 단계를 완전히 제거 합니다 **sql1** 컨테이너를 만든 다음 새 컨테이너를 **sql2**, 지속된 된 데이터를 사용 하 여 합니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 중지 된 **sql1** 컨테이너입니다.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. 컨테이너를 제거 합니다. 이전에 만든 삭제 되지는 않습니다 **sql1data** 데이터 볼륨 컨테이너와 지속형된 데이터입니다.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 새 컨테이너를 만듭니다 **sql2**, 및 다시 사용 합니다 **sql1data** 데이터 볼륨 컨테이너입니다.

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

1. Wide World Importers 데이터베이스를 새 컨테이너에 포함 되었습니다. 이전 변경 내용을 확인 하는 쿼리를 실행 합니다.

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > SA 암호에 대 한 지정 된 암호가 아닙니다 합니다 **sql2** 컨테이너 `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`합니다. 복원 된 모든 SQL Server 데이터 **sql1**, 자습서의 앞부분에서 변경된 된 암호를 포함 합니다. 실제로 다음과 같은 몇 가지 옵션은 /var/opt/mssql에서 데이터를 복원으로 인해 무시 됩니다. 이러한 이유로 암호는 `<YourNewStrong!Passw0rd>` 다음과 같이 합니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. 중지 된 **sql1** 컨테이너입니다.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. 컨테이너를 제거 합니다. 이전에 만든 삭제 되지는 않습니다 **sql1data** 데이터 볼륨 컨테이너와 지속형된 데이터입니다.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 새 컨테이너를 만듭니다 **sql2**, 및 다시 사용 합니다 **sql1data** 데이터 볼륨 컨테이너입니다.

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
    ```

1. Wide World Importers 데이터베이스를 새 컨테이너에 포함 되었습니다. 이전 변경 내용을 확인 하는 쿼리를 실행 합니다.

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > SA 암호에 대 한 지정 된 암호가 아닙니다 합니다 **sql2** 컨테이너 `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`합니다. 복원 된 모든 SQL Server 데이터 **sql1**, 자습서의 앞부분에서 변경된 된 암호를 포함 합니다. 실제로 다음과 같은 몇 가지 옵션은 /var/opt/mssql에서 데이터를 복원으로 인해 무시 됩니다. 이러한 이유로 암호는 `<YourNewStrong!Passw0rd>` 다음과 같이 합니다.

::: moniker-end

## <a name="next-steps"></a>다음 단계

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

이 자습서에서는 Windows에서 데이터베이스를 백업 하 고 SQL Server 2017을 실행 하는 Linux 서버로 이동 하는 방법을 알아보았습니다. 방법을 배웠습니다에:

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

이 자습서에서는 Windows에서 데이터베이스를 백업 하 고 SQL Server 2019 미리 보기를 실행 하는 Linux 서버로 이동 하는 방법을 알아보았습니다. 방법을 배웠습니다에:

::: moniker-end

> [!div class="checklist"]
> * SQL Server Linux 컨테이너 이미지를 만듭니다.
> * SQL Server 데이터베이스 백업 컨테이너에 복사 합니다.
> * TRANSACT-SQL 문을 사용 하 여 컨테이너 내에서 실행 **sqlcmd**합니다.
> * 페이지를 만들고 컨테이너에서 백업 파일을 추출 합니다.
> * Docker에서 데이터 볼륨 컨테이너를 사용 하 여 SQL Server 데이터를 유지 합니다.

다음으로, 다른 Docker 구성 및 문제 해결 시나리오를 검토 합니다.

> [!div class="nextstepaction"]
>[Docker에서 SQL Server 2017에 대 한 구성 가이드](sql-server-linux-configure-docker.md)
