---
title: Docker에서 SQL Server 데이터베이스 복원
description: 이 자습서에서는 새 Linux Docker 컨테이너에서 SQL Server 데이터베이스 백업을 복원하는 방법을 보여 줍니다.
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 28c2bbd60b5a1565e2920968e40bb1dc4e75db22
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531194"
---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>Linux Docker 컨테이너에서 SQL Server 데이터베이스 복원

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

이 자습서에서는 SQL Server 백업 파일을 Docker에서 실행되는 SQL Server 2017 Linux 컨테이너 이미지로 이동하고 복원하는 방법을 보여 줍니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

이 자습서에서는 SQL Server 백업 파일을 Docker에서 실행되는 SQL Server 2019 Linux 컨테이너 이미지로 이동하고 복원하는 방법을 보여 줍니다.

::: moniker-end

> [!div class="checklist"]
> * 최신 SQL Server Linux 컨테이너 이미지를 가져오고 실행합니다.
> * Wide World Importers 데이터베이스 파일을 컨테이너로 복사합니다.
> * 컨테이너에서 데이터베이스를 복원합니다.
> * Transact-SQL 문을 실행하여 데이터베이스를 보고 수정합니다.
> * 수정된 데이터베이스를 백업합니다.

## <a name="prerequisites"></a>사전 요구 사항

* 지원되는 모든 Linux 배포판 또는 Mac/Windows용 Docker에서 Docker Engine 1.8+. 자세한 내용은 [사용자 Docker 설치](https://docs.docker.com/engine/installation/)를 참조하세요.
* 최소 2GB의 디스크 공간
* 최소 2GB의 RAM
* [Linux에서 SQL Server에 대한 시스템 요구 사항](sql-server-linux-setup.md#system)

## <a name="pull-and-run-the-container-image"></a>컨테이너 이미지를 끌어와 실행하기

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Linux/Mac에서 Bash 터미널을 열거나 Windows에서 관리자 권한 PowerShell 세션을 엽니다.

1. Docker Hub를 사용하여 SQL Server 2017 Linux 컨테이너 이미지를 끌어오기.

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   > [!TIP]
   > 이 자습서 전체에서 Bash 셸(Linux/Mac) 및 PowerShell(Windows)에 대한 docker 명령 예제가 제공됩니다.

1. Docker를 사용하여 컨테이너 이미지를 실행하려면 다음 명령을 사용하면 됩니다.

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

   이 명령은 Developer Edition(기본값)을 사용하여 SQL Server 2017 컨테이너를 만듭니다. SQL Server 포트 **1433**은 호스트에서 포트 **1401**로 공개됩니다. 선택적 `-v sql1data:/var/opt/mssql` 매개 변수는 **sql1ddata**라는 데이터 볼륨 컨테이너를 만듭니다. 이 컨테이너는 SQL Server에서 생성된 데이터를 유지하는 데 사용됩니다.

   > [!NOTE]
   > 컨테이너에서 프로덕션 SQL Server 버전을 실행하는 프로세스는 약간 다릅니다. 자세한 내용은 [프로덕션 컨테이너 이미지 실행](sql-server-linux-configure-docker.md#production)을 참조하세요. 동일한 컨테이너 이름 및 포트를 사용하는 경우 이 연습의 나머지 부분은 프로덕션 컨테이너에서도 계속 작동합니다.

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

1. Linux/Mac에서 Bash 터미널을 열거나 Windows에서 관리자 권한 PowerShell 세션을 엽니다.

1. Docker Hub에서 SQL Server 2019 Linux 컨테이너 이미지를 끌어옵니다.

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   > [!TIP]
   > 이 자습서 전체에서 Bash 셸(Linux/Mac) 및 PowerShell(Windows)에 대한 docker 명령 예제가 제공됩니다.

1. Docker를 사용하여 컨테이너 이미지를 실행하려면 다음 명령을 사용하면 됩니다.

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   이 명령은 Developer Edition(기본값)을 사용하여 SQL Server 2019 컨테이너를 만듭니다. SQL Server 포트 **1433**은 호스트에서 포트 **1401**로 공개됩니다. 선택적 `-v sql1data:/var/opt/mssql` 매개 변수는 **sql1ddata**라는 데이터 볼륨 컨테이너를 만듭니다. 이 컨테이너는 SQL Server에서 생성된 데이터를 유지하는 데 사용됩니다.

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

## <a name="copy-a-backup-file-into-the-container"></a>컨테이너에 백업 파일 복사

이 자습서에서는 [Wide World Importers 샘플 데이터베이스](../sample/world-wide-importers/wide-world-importers-documentation.md)를 사용합니다. 다음 단계를 사용하여 Wide World Importers 데이터베이스 백업 파일을 다운로드하고 SQL Server 컨테이너에 복사합니다.

1. 먼저 **docker exec**를 사용하여 백업 폴더를 만듭니다. 다음 명령은 SQL Server 컨테이너 내부에 **/var/opt/mssql/backup** 디렉터리를 만듭니다.

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. 그런 다음, 호스트 컴퓨터에 [WideWorldImporters-Full.bak](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) 파일을 다운로드합니다. 다음 명령을 사용하여 home/user 디렉터리로 이동하고 백업 파일을 **wwi.bak**로 다운로드합니다.

   ```bash
   cd ~
   curl -L -o wwi.bak 'https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak'
   ```

   ```PowerShell
   curl -OutFile "wwi.bak" "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak"
   ```

1. **docker cp**를 사용하여 백업 파일을 **/var/opt/mssql/backup** 디렉터리의 컨테이너로 복사합니다.

   ```bash
   sudo docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

   ```PowerShell
   docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

## <a name="restore-the-database"></a>데이터베이스 복원

이제 백업 파일이 컨테이너 내부에 있습니다. 백업을 복원하기 전에 백업 내의 논리적 파일 이름 및 파일 형식을 알고 있어야 합니다. 다음 Transact-SQL 명령은 백업을 검사하고 컨테이너에서 **sqlcmd**를 사용하여 복원을 수행합니다.

> [!TIP]
> 컨테이너에 이 도구가 미리 설치되어 제공되므로 이 자습서에서는 컨테이너 내부에서 **sqlcmd**를 사용합니다. 그러나 컨테이너 외부에서 [Visual Studio Code](sql-server-linux-develop-use-vscode.md) 또는 [SQL Server Management Studio](sql-server-linux-manage-ssms.md)와 같은 다른 클라이언트 도구를 사용하여 Transact-SQL 문을 실행할 수도 있습니다. 연결하려면 컨테이너에서 포트 1433에 매핑된 호스트 포트를 사용합니다. 이 예제에서 해당 호스트 포트는 호스트 머신의 **localhost,1401** 및 원격으로 **Host_IP_Address,1401**입니다.

1. 컨테이너 내에서 **sqlcmd**를 실행하여 백업 내부 논리적 파일 이름 및 경로를 나열합니다. 이 작업에는 **RESTORE FILELISTONLY** Transact-SQL 문을 사용합니다.

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

   다음과 비슷한 내용이 출력됩니다.

   ```
   LogicalName   PhysicalName
   ------------------------------------------
   WWI_Primary   D:\Data\WideWorldImporters.mdf
   WWI_UserData   D:\Data\WideWorldImporters_UserData.ndf
   WWI_Log   E:\Log\WideWorldImporters.ldf
   WWI_InMemory_Data_1   D:\Data\WideWorldImporters_InMemory_Data_1
   ```

1. **RESTORE DATABASE** 명령을 호출하여 컨테이너 내부에서 데이터베이스를 복원합니다. 이전 단계에서 각 파일의 새 경로를 지정합니다.

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

   다음과 비슷한 내용이 출력됩니다.

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

## <a name="verify-the-restored-database"></a>복원된 데이터베이스 확인

다음 쿼리를 실행하여 컨테이너의 데이터베이스 이름 목록을 표시합니다.

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

데이터베이스 목록에 **WideWorldImporters**가 표시됩니다.

## <a name="make-a-change"></a>변경

다음 단계를 통해 데이터베이스를 변경합니다.

1. 쿼리를 실행하여 **Warehouse.StockItems** 테이블의 상위 10개 항목을 확인합니다.

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

   항목 식별자 및 이름 목록이 표시됩니다.

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

1. 다음 **UPDATE** 문을 사용하여 첫 번째 항목의 설명을 업데이트합니다.

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

   다음 텍스트와 비슷한 내용이 출력됩니다.

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>새 백업 만들기

데이터베이스를 컨테이너로 복원한 후 실행 중인 컨테이너 내에서 정기적으로 데이터베이스 백업을 만들 수도 있습니다. 해당 단계는 이전 단계와 비슷한 패턴을 따르지만 방향은 반대입니다.

1. **BACKUP DATABASE** Transact-SQL 명령을 사용하여 컨테이너에서 데이터베이스 백업을 만듭니다. 이 자습서에서는 이전에 만든 **/var/opt/mssql/backup** 디렉터리에 새 백업 파일인 **wwi_2.bak**를 만듭니다.

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

   다음과 비슷한 내용이 출력됩니다.

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

1. 그런 다음, 컨테이너에서 백업 파일을 복사하여 호스트 머신에 붙여넣습니다.

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

## <a name="use-the-persisted-data"></a>지속형 데이터 사용

데이터를 보호하기 위해 데이터베이스 백업을 수행할 뿐 아니라 데이터 볼륨 컨테이너를 사용할 수도 있습니다. 이 자습서의 시작 부분에서는 `-v sql1data:/var/opt/mssql` 매개 변수를 사용하여 **sql1** 컨테이너를 만들었습니다. **sql1data** 데이터 볼륨 컨테이너는 컨테이너가 제거된 후에도 **/var/opt/mssql** 데이터를 유지합니다. 다음 단계에서는 **sql1** 컨테이너를 완전히 제거한 후 지속형 데이터를 사용하여 새 컨테이너인 **sql2**를 만듭니다.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. **sql1** 컨테이너를 중지합니다.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. 컨테이너를 제거합니다. 이렇게 해도 이전에 만든 **sql1data** 데이터 볼륨 컨테이너와 해당 컨테이너의 지속형 데이터는 삭제되지 않습니다.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 새 컨테이너인 **sql2**를 만들고 **sql1data** 데이터 볼륨 컨테이너를 다시 사용합니다.

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

1. Wide World Importers 데이터베이스는 이제 새 컨테이너에 있습니다. 쿼리를 실행하여 이전에 변경한 내용을 확인합니다.

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
   > SA 암호는 **sql2** 컨테이너인 `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`에 대해 지정한 암호가 아닙니다. 자습서의 앞부분에서 변경된 암호를 포함하여 모든 SQL Server 데이터가 **sql1**에서 복원되었습니다. 실제로 /var/opt/mssql의 데이터를 복원하기 때문에 이와 같은 일부 옵션은 무시됩니다. 이런 이유로 암호는 여기 표시된 대로 `<YourNewStrong!Passw0rd>`입니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. **sql1** 컨테이너를 중지합니다.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. 컨테이너를 제거합니다. 이렇게 해도 이전에 만든 **sql1data** 데이터 볼륨 컨테이너와 해당 컨테이너의 지속형 데이터는 삭제되지 않습니다.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 새 컨테이너인 **sql2**를 만들고 **sql1data** 데이터 볼륨 컨테이너를 다시 사용합니다.

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
    ```

1. Wide World Importers 데이터베이스는 이제 새 컨테이너에 있습니다. 쿼리를 실행하여 이전에 변경한 내용을 확인합니다.

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
   > SA 암호는 **sql2** 컨테이너인 `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`에 대해 지정한 암호가 아닙니다. 자습서의 앞부분에서 변경된 암호를 포함하여 모든 SQL Server 데이터가 **sql1**에서 복원되었습니다. 실제로 /var/opt/mssql의 데이터를 복원하기 때문에 이와 같은 일부 옵션은 무시됩니다. 이런 이유로 암호는 여기 표시된 대로 `<YourNewStrong!Passw0rd>`입니다.

::: moniker-end

## <a name="next-steps"></a>다음 단계

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

이 자습서에서는 Windows에서 데이터베이스를 백업하고 SQL Server 2017을 실행하는 Linux 서버로 이동하는 방법을 알아보았습니다. 구체적으로 다음 작업 방법을 알아보았습니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

이 자습서에서는 Windows에서 데이터베이스를 백업하고 SQL Server 2019를 실행하는 Linux 서버로 이동하는 방법을 알아보았습니다. 구체적으로 다음 작업 방법을 알아보았습니다.

::: moniker-end

> [!div class="checklist"]
> * SQL Server Linux 컨테이너 이미지를 만듭니다.
> * SQL Server 데이터베이스 백업을 컨테이너에 복사합니다.
> * **sqlcmd**를 사용하여 컨테이너 내에서 Transact-SQL 문을 실행합니다.
> * 컨테이너에서 백업 파일을 만들고 추출합니다.
> * Docker의 데이터 볼륨 컨테이너를 사용하여 SQL Server 데이터를 유지합니다.

다음으로, 다른 Docker 구성 및 문제 해결 시나리오를 검토합니다.

> [!div class="nextstepaction"]
>[Docker의 SQL Server 2017에 대한 구성 가이드](sql-server-linux-configure-docker.md)
