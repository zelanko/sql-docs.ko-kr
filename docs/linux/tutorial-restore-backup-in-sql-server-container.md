---
title: "Docker에서 SQL Server 데이터베이스를 복원 | Microsoft Docs"
description: "이 자습서에서는 어떻게 새 Linux Docker 컨테이너에 SQL Server 데이터베이스 백업을 복원 합니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.translationtype: MT
ms.sourcegitcommit: 51f60c4fecb56aca3f4fb007f8e6a68601a47d11
ms.openlocfilehash: 1f3cc214be4eaac2199c17c3bea1da7fd02956f1
ms.contentlocale: ko-kr
ms.lasthandoff: 10/14/2017

---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>Linux Docker 컨테이너에서 SQL Server 데이터베이스 복원

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 자습서에서는 이동 하 고 Docker에서 실행 중인 SQL Server 2017 Linux 컨테이너 이미지에 SQL Server 백업 파일을 복원 하는 방법을 설명 합니다.

> [!div class="checklist"]
> * 끌어오기 및 최신 SQL Server 2017 Linux 컨테이너 이미지를 실행 합니다.
> * 컨테이너에 Wide World Importers 데이터베이스 파일을 복사 합니다.
> * 컨테이너에서 데이터베이스를 복원 합니다.
> * 보고 데이터베이스를 수정 하는 TRANSACT-SQL 문을 실행 합니다.
> * 수정 된 데이터베이스를 백업 합니다.

## <a name="prerequisites"></a>필수 구성 요소

* docker 엔진 1.8 + Mac/창에 Linux 배포 또는 Docker를 지원 합니다. 자세한 내용은 참조 [설치 Docker](https://docs.docker.com/engine/installation/)합니다.
* 최소 4GB의 디스크 공간
* 최소 4GB의 RAM
* [Linux에서 SQL Server에 대 한 시스템 요구 사항](sql-server-linux-setup.md#system)합니다.

> [!IMPORTANT]
> Mac 용 Docker 및 Windows 용 Docker에 대 한 기본값 Moby VM에 대 한 2GB 이므로 4GB로 변경 해야 합니다. Mac 또는 Windows에서 실행 하는 경우 메모리 설정을 사용 하 여 증가 된 [Docker 빠른 시작의 지침에](quickstart-install-connect-docker.md)합니다.

## <a name="pull-and-run-the-container-image"></a>컨테이너 이미지를 실행 하 고 끌어오기

1. Linux/Mac에서 bash 터미널 또는 Windows에서 관리자 권한 PowerShell 세션을 엽니다.

1. Docker 허브에서 SQL Server 2017 Linux 컨테이너 이미지를 끌어옵니다.

    ```bash
    sudo docker pull microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker pull microsoft/mssql-server-linux:2017-latest
    ```

    > [!TIP]
    > 이 자습서에서는 전체 docker 명령 예제는 bash 셸의 (Linux/Mac) 및 PowerShell (Windows)에 대해 제공 됩니다.

1. Docker가 있는 컨테이너 이미지를 실행 하려면 다음 명령을 사용할 수 있습니다.

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql1' -p 1401:1433 \
       -v sql1data:/var/opt/mssql \
       -d microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql1" -p 1401:1433 `
       -v sql1data:/var/opt/mssql `
       -d microsoft/mssql-server-linux:2017-latest
    ```

    이 명령은 Developer edition (기본값)을 SQL Server 2017 컨테이너를 만듭니다. SQL Server 포트 **1433** 포트로 호스트에 노출 **1401**합니다. 선택적 `-v sql1data:/var/opt/mssql` 매개 변수 명명 된 데이터 볼륨 컨테이너를 만듦 **sql1ddata**합니다. SQL Server에서 만든 데이터를 유지 하는이 사용 됩니다.

   > [!NOTE]
   > 컨테이너에서 프로덕션 SQL Server 버전을 실행 하기 위한 프로세스는 약간 다릅니다. 자세한 내용은 참조 [프로덕션 컨테이너 이미지를 실행](sql-server-linux-configure-docker.md#production)합니다. 동일한 컨테이너 이름 및 포트를 사용 하는 경우이 연습의 나머지 부분 프로덕션 컨테이너와 계속 작동 합니다.

1. Docker 컨테이너를 보려면 사용 하 여는 `docker ps` 명령입니다.

    ```bash
    sudo docker ps -a
    ```

    ```PowerShell
    docker ps -a
    ```
 
1. 경우는 **상태** 열 표시의 상태 **를**컨테이너에서 SQL Server가 실행 한 다음, 및에 지정 된 포트에서 수신 하는 **포트** 열입니다. 경우는 **상태** SQL Server 컨테이너 표시에 대 한 열 **Exited**, 참조는 [구성 가이드의 섹션 문제 해결](sql-server-linux-configure-docker.md#troubleshooting)합니다.

   ```
   $ sudo docker ps -a

   CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
   941e1bdf8e1d        microsoft/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
   ```

## <a name="change-the-sa-password"></a>SA 암호를 변경 합니다.

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="copy-a-backup-file-into-the-container"></a>컨테이너에 백업 파일을 복사 합니다.

이 자습서에서는 [Wide World Importers 샘플 데이터베이스](../sample/world-wide-importers/wide-world-importers-documentation.md)합니다. 다음 단계를 사용 하 여를 다운로드 하 여 SQL Server 컨테이너로 Wide World Importers 데이터베이스 백업 파일을 복사 합니다.

1. 먼저, 사용 하 여 **docker exec** 백업 폴더를 만들 수 있습니다. 다음 명령은 만듭니다는 **/var/옵트인/mssql/** 컨테이너 내에서 SQL Server 디렉터리입니다.

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. 다음으로, 다운로드는 [WideWorldImporters Full.bak](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) 호스트 컴퓨터에는 파일입니다. 다음 명령을 홈/사용자 디렉터리로 이동 하 한으로 백업 파일을 다운로드 **wwi.bak**합니다.

   ```bash
   cd ~
   curl -L -o wwi.bak 'https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak'
   ```

   ```PowerShell
   curl -OutFile "wwi.bak" "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak"
   ```

1. 사용 하 여 **docker cp** 에서 컨테이너에 백업 파일을 복사 하는 **/var/opt/mssql/backup** 디렉터리입니다.

   ```bash
   sudo docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

   ```PowerShell
   docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

## <a name="restore-the-database"></a>데이터베이스 복원

백업 파일은 이제 컨테이너 내 위치입니다. 백업, 복원 하기 전에 논리적 파일 이름 및 백업 내의 파일 형식을 확인 해야 합니다. 다음 TRANSACT-SQL 명령을 백업을 검사 하 고 사용 하 여 복원을 수행할 **sqlcmd** 컨테이너에 있습니다.

> [!TIP]
> 이 자습서에서는 **sqlcmd** 컨테이너 안에 컨테이너 미리 설치 된이 도구를 제공 하므로 합니다. 그러나 실행할 수도 있습니다 TRANSACT-SQL 문을 다른 클라이언트와 컨테이너의 외부 도구와 같은 [Visual Studio Code](sql-server-linux-develop-use-vscode.md) 또는 [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md)합니다. 에 연결 하려면 컨테이너의 포트 1433에 매핑된 호스트 포트를 사용 합니다. 이 예제에서 **localhost, 1401** 호스트 컴퓨터에서 및 **Host_IP_Address, 1401** 원격으로 합니다.

1. 실행 **sqlcmd** 컨테이너 내에서 논리적 파일 이름 및 백업 내 경로 목록에 있습니다. 이러한 용도로 **RESTORE FILELISTONLY** Transact SQL 문입니다.

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

   다음과 비슷한 출력이 표시 되어야 합니다.

   ```
   LogicalName   PhysicalName
   ------------------------------------------
   WWI_Primary   D:\Data\WideWorldImporters.mdf
   WWI_UserData   D:\Data\WideWorldImporters_UserData.ndf
   WWI_Log   E:\Log\WideWorldImporters.ldf
   WWI_InMemory_Data_1   D:\Data\WideWorldImporters_InMemory_Data_1
   ```

1. 호출 된 **데이터베이스 복원** 컨테이너 내에서 데이터베이스를 복원 하는 명령입니다. 이전 단계에서 파일을 각각에 대 한 새 경로 지정 합니다.

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

   다음과 비슷한 출력이 표시 되어야 합니다.

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

표시 되어야 **WideWorldImporters** 데이터베이스 목록에 있습니다.

## <a name="make-a-change"></a>변경

다음 단계는 데이터베이스에 변경을 합니다.

1. 상위 10 개의 항목을 보려면 쿼리를 실행 하는 **Warehouse.StockItems** 테이블입니다.

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

   항목 식별자, 이름 목록이 표시 되어야 합니다.

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

1. 다음으로 첫 번째 항목의 설명을 업데이트 **업데이트** 문:

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

   다음 텍스트와 유사한 출력이 표시 되어야 합니다.

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>새 백업 만들기

복원한 후 데이터베이스 컨테이너에, 정기적으로 실행 중인 컨테이너 내 데이터베이스 백업을 만들 수도 있습니다. 단계는 이전 단계에 있지만 반대 방향으로 유사한 패턴을 따릅니다.

1. 사용 하 여는 **백업 데이터베이스** 컨테이너에 데이터베이스 백업을 만드는 TRANSACT-SQL 명령입니다. 이 자습서에서는 새 백업 파일을 만듭니다. **wwi_2.bak**, 이전에 만든에서 **/var/opt/mssql/backup** 디렉터리입니다.

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

   다음과 비슷한 출력이 표시 되어야 합니다.

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

1. 다음으로, 컨테이너 및 호스트 컴퓨터에 백업 파일을 복사 합니다.

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

## <a name="use-the-persisted-data"></a>지속된 된 데이터를 사용 하 여

데이터베이스 백업 데이터를 보호 하는 것을 외에도 데이터 볼륨 컨테이너를 사용할 수 있습니다. 만든이 자습서의 시작 부분에서 **sql1** 가 있는 컨테이너는 `-v sql1data:/var/opt/mssql` 매개 변수입니다. **sql1data** 계속 되 면 데이터 볼륨 컨테이너는 **/var/opt/mssql** 데이터 컨테이너를 제거한 후에 합니다. 다음 단계를 완전히 제거는 **sql1** 컨테이너 한 다음 새 컨테이너를 만듭니다 **sql2**, 지속형된 데이터를 사용 합니다.

1. 중지 된 **sql1** 컨테이너입니다.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. 컨테이너를 제거 합니다. 이전에 만든 삭제 되지 않습니다 **sql1data** 데이터 볼륨 컨테이너와 그 안에 있는 지속형된 데이터입니다.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 새 컨테이너 만들기 **sql2**, 다른 사람이 다시는 **sql1data** 데이터 볼륨 컨테이너입니다.

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
    ```

1. 이제 Wide World Importers 데이터베이스가 새 컨테이너에 표시 됩니다. 이전 변경 내용이 확인 하는 쿼리를 실행 합니다.

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
   > SA 암호가 대 한 지정한 암호는 **sql2** 컨테이너 `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`합니다. 모든 SQL Server 데이터 복원 **sql1**에서 변경된 된 암호를 포함 하 여이 자습서의 앞부분에 나오는 합니다. 실제로 다음과 같이 몇 가지 옵션은 /var/opt/mssql에 데이터를 복원으로 인해 무시 됩니다. 이러한 이유로 암호는 `<YourNewStrong!Passw0rd>` 다음과 같이 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Windows에서 데이터베이스를 백업 하 고 SQL Server 2017 r c 2를 실행 하는 Linux 서버를 이동 하는 방법을 배웠습니다. 방법에 대해 배웠습니다에:
> [!div class="checklist"]
> * SQL Server 2017 Linux 컨테이너 이미지를 만듭니다.
> * SQL Server 데이터베이스 백업 컨테이너에 복사 합니다.
> * 과 함께 컨테이너 안에 있는 Transact SQL 문 실행 **sqlcmd**합니다.
> * 페이지를 만들고 컨테이너에서 백업 파일을 추출 합니다.
> * Docker에서 데이터 볼륨 컨테이너를 사용 하 여 SQL Server 데이터를 유지 합니다.

다음으로, 다른 Docker 구성 및 문제 해결 시나리오를 검토 합니다.

> [!div class="nextstepaction"]
>[SQL Server 2017 Docker에 대 한 구성 가이드](sql-server-linux-configure-docker.md)

