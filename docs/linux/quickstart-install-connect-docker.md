---
title: "Docker에서 SQL Server 2017 시작 | Microsoft Docs"
description: "이 빠른 시작 자습서에는 SQL Server 2017 컨테이너 이미지를 실행 하려면 Docker를 사용 하는 방법을 보여 줍니다. 그런 다음 만들고 sqlcmd 사용 하 여 데이터베이스를 쿼리 합니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/31/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.workload: Active
ms.openlocfilehash: 80d3d05fcd693f6290649c2c63446c400c9ad3b2
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2017
---
# <a name="run-the-sql-server-2017-container-image-with-docker"></a>Docker가 있는 SQL Server 2017 컨테이너 이미지를 실행 합니다.

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 빠른 시작 자습서를 사용 하 여 Docker pull 및 SQL Server 2017 컨테이너 이미지를 실행 [mssql-서버-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/)합니다. 다음으로 연결 **sqlcmd** 첫 번째 데이터베이스를 만들고 쿼리를 실행 합니다.

이 이미지는 Ubuntu 16.04에 따라 Linux에서 실행 중인 SQL Server 구성 됩니다. Mac/Windows 용 Docker 엔진 1.8 + linux 또는 Docker에서 사용할 수 있습니다.

> [!NOTE]
> 이 빠른 시작에 중점을 mssql를 사용 하 여-서버-**linux** 이미지입니다. Windows 이미지 적용 되지 않는 있지만에서 항목에 대 한 자세히 알아볼 수 있습니다는 [mssql 서버-windows 개발자 Docker 허브 페이지](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)합니다.

## <a id="requirements"></a> 필수 구성 요소

- docker 엔진 1.8 + Mac/창에 Linux 배포 또는 Docker를 지원 합니다. 자세한 내용은 참조 [설치 Docker](https://docs.docker.com/engine/installation/)합니다.
- 최소 2GB의 디스크 공간
- 2GB ram 이상
- [Linux에서 SQL Server에 대 한 시스템 요구 사항](sql-server-linux-setup.md#system)합니다.

## <a name="pull-and-run-the-container-image"></a>컨테이너 이미지를 실행 하 고 끌어오기

1. Docker 허브에서 SQL Server 2017 Linux 컨테이너 이미지를 끌어옵니다.

   ```bash
   sudo docker pull microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker pull microsoft/mssql-server-linux:2017-latest
   ```

   이 명령은 최신 SQL Server 2017 컨테이너 이미지를 끌어옵니다. 태그 이름과 콜론을 추가할 특정 이미지를 끌어오려면 하려는 경우 (예를 들어 `microsoft/mssql-server-linux:2017-GA`). 사용 가능한 모든 이미지를 보려면 [mssql-서버-linux Docker 허브 페이지](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/)합니다.

1. Docker가 있는 컨테이너 이미지를 실행 하려면 bash 셸의 (Linux/macOS) 또는 관리자 권한 PowerShell 명령 프롬프트에서 다음 명령을 사용할 수 있습니다.

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1401:1433 --name sql1 \
      -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1401:1433 --name sql1 `
      -d microsoft/mssql-server-linux:2017-latest
   ```

   > [!NOTE]
   > 기본적으로 개발자 버전의 SQL Server 2017와 컨테이너를 만듭니다이 있습니다. 컨테이너의 프로덕션 버전을 실행 하기 위한 프로세스는 약간 다릅니다. 자세한 내용은 참조 [프로덕션 컨테이너 이미지를 실행](sql-server-linux-configure-docker.md#production)합니다.

   다음 표에서 이전에 매개 변수 설명을 `docker run` 예제:

   | 매개 변수 | Description |
   |-----|-----|
   | **-e ' ACCEPT_EULA = Y'** |  설정의 **ACCEPT_EULA** 동의한 것에 어떤 값이 변수는 [최종 사용자 사용권 계약](http://go.microsoft.com/fwlink/?LinkId=746388)합니다. SQL Server 이미지에 대 한 설정 해야 합니다. |
   | **-e ' MSSQL_SA_PASSWORD =\<YourStrong! Passw0rd\>'** | 8 자 이상 되며 충족 된 강력한 암호를 지정 된 [SQL Server 암호 요구 사항을](../relational-databases/security/password-policy.md)합니다. SQL Server 이미지에 대 한 설정 해야 합니다. |
   | **-p 1401:1433** | 호스트 환경에서 TCP 포트 매핑 (첫째 값) 컨테이너의 TCP 포트 (두 번째 값). 이 예제에서는 SQL Server가 컨테이너의 TCP 1433에서 수신 하 고 호스트에서 1401 포트에 노출 됩니다. |
   | **-이름 s q l 1** | 임의로 생성 된 것 보다는 컨테이너에 대 한 사용자 지정 이름을 지정 합니다. 둘 이상의 컨테이너를 실행 하는 경우에이 이름을 다시 사용할 수 없습니다. |
   | **microsoft/mssql-서버-linux:2017-최신** | SQL Server 2017 Linux 컨테이너 이미지입니다. |

1. Docker 컨테이너를 보려면 사용 하 여는 `docker ps` 명령입니다.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

   다음 스크린샷과 유사한 출력이 표시 되어야 합니다.

   ![Docker ps 명령 출력](./media/sql-server-linux-setup-docker/docker-ps-command.png)

1. 경우는 **상태** 열 표시의 상태 **를**컨테이너에서 SQL Server가 실행 한 다음, 및에 지정 된 포트에서 수신 하는 **포트** 열입니다. 경우는 **상태** SQL Server 컨테이너 표시에 대 한 열 **Exited**, 참조는 [구성 가이드의 섹션 문제 해결](sql-server-linux-configure-docker.md#troubleshooting)합니다.

`-h` 도 유용 합니다 (호스트 이름) 매개 변수 이지만 간단한 설명을 위해이 자습서에서 사용 되지 않습니다. 이 컨테이너의 내부 이름을 사용자 지정 값으로 변경 합니다. 이 다음 Transact SQL 쿼리에서 반환 된 이름이 표시 됩니다.

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

설정 `-h` 및 `--name` 과 같은 값은 쉽게 대상 컨테이너를 식별 하는 데 유용 합니다.

## <a name="change-the-sa-password"></a>SA 암호를 변경 합니다.

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="connect-to-sql-server"></a>SQL Server에 연결

다음 단계에 SQL Server 명령줄 도구를 사용 하 여 **sqlcmd**, 컨테이너 내에서 SQL Server에 연결 합니다.

1. 사용 하 여는 `docker exec -it` 는 대화형 bash 셸의 실행 중인 컨테이너 내 시작 명령입니다. 다음 예에서 `sql1` 으로 이름이 지정 되는 `--name` 컨테이너를 만들 때 매개 변수입니다.

   ```bash
   sudo docker exec -it sql1 "bash"
   ```

   ```PowerShell
   docker exec -it sql1 "bash"
   ```

1. 한 번, 컨테이너 내부 연결 로컬로 sqlcmd 합니다. Sqlcmd 아니므로 기본적으로 경로에 전체 경로 지정 해야 합니다.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   > [!TIP]
   > 명령줄에서 암호를 생략하여 입력하라는 메시지가 표시되도록 할 수 있습니다.

1. 성공하면 **sqlcmd** 명령 프롬프트 `1>`이 표시됩니다.

## <a name="create-and-query-data"></a>데이터 만들기 및 쿼리

다음 섹션에서는 **sqlcmd** 및 Transact-SQL을 사용하여 새 데이터베이스를 만들고, 데이터를 추가하고, 간단한 쿼리를 실행하는 단계를 안내합니다.

### <a name="create-a-new-database"></a>새 데이터베이스 만들기

다음 단계에서는 `TestDB`라는 새 데이터베이스를 만듭니다.

1. **sqlcmd** 명령 프롬프트에서 다음 Transact-SQL 명령을 붙여넣어 테스트 데이터베이스를 만듭니다.

   ```sql
   CREATE DATABASE TestDB
   ```

1. 다음 줄에 서버에 있는 모든 데이터베이스의 이름을 반환하는 쿼리를 작성합니다.

   ```sql
   SELECT Name from sys.Databases
   ```

1. 앞의 두 명령은 즉시 실행되지 않았습니다. 앞의 명령을 실행하려면 새 줄에 `GO`를 입력해야 합니다.

   ```sql
   GO
   ```

### <a name="insert-data"></a>데이터 삽입

다음으로 새 테이블 `Inventory`를 만들고 두 개의 새 행을 삽입합니다.

1. **sqlcmd** 명령 프롬프트에서 컨텍스트를 새 `TestDB` 데이터베이스로 전환합니다.

   ```sql
   USE TestDB
   ```

1. `Inventory`라는 새 테이블을 만듭니다.

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

1. 새 테이블에 데이터를 삽입합니다.

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

1. `GO`를 입력하여 앞의 명령을 실행합니다.

   ```sql
   GO
   ```

### <a name="select-data"></a>데이터 선택

이제 쿼리를 실행하여 `Inventory` 테이블에서 데이터를 반환합니다.

1. **sqlcmd** 명령 프롬프트에서 `Inventory` 테이블에서 수량이 152보다 큰 행을 반환하는 쿼리를 입력합니다.

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

1. 명령을 실행합니다.

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>sqlcmd 명령 프롬프트 종료

1. **sqlcmd** 세션을 종료하려면 `QUIT`를 입력합니다.

   ```sql
   QUIT
   ```

1. 컨테이너의 대화형 명령 프롬프트를 종료 하려면 입력 `exit`합니다. 컨테이너에서 대화형 bash 셸의 종료 한 후 실행 계속 합니다.

## <a id="connectexternal"></a>컨테이너 외부에서 연결

연결할 수 있습니다도 SQL Server 인스턴스에 Docker 컴퓨터에 SQL 연결을 지 원하는 Linux, Windows 또는 macOS 도구 외부에서.

다음 단계를 사용 하 여 **sqlcmd** 컨테이너에서 실행 중인 SQL Server에 연결 하 여 컨테이너의 외부입니다. 다음이 단계에 컨테이너의 외부에 설치 된 SQL Server 명령줄 도구 이미 있다고 가정 합니다. 다른 도구를 사용 하는 경우 동일한 주체 적용 하지만 연결 하는 프로세스는 각 도구에 고유 합니다.

1. 컨테이너를 호스팅하는 컴퓨터에 대 한 IP 주소를 찾습니다. Linux에서 사용 하 여 **ifconfig** 또는 **ip 주소**합니다. Windows에서 사용 하 여 **ipconfig**합니다.

1. IP 주소와 컨테이너의 포트 1433에 매핑된 포트를 지정 하는 sqlcmd를 실행 합니다. 이 예제에서는 호스트 컴퓨터에 1401 포트입니다.

   ```bash
   sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourNewStrong!Passw0rd>"
   ```

1. TRANSACT-SQL 명령이 실행된 합니다. 완료 되 면 입력 `QUIT`합니다.

다른 일반적인 도구는 SQL Server에 연결 하는 다음과 같습니다.

- [Visual Studio 코드](sql-server-linux-develop-use-vscode.md)
- [Windows에서 SQL Server Management Studio (SSMS)](sql-server-linux-develop-use-ssms.md)

## <a name="remove-your-container"></a>컨테이너 제거

이 자습서에 사용 되는 SQL Server 컨테이너를 제거 하려는 경우에 다음 명령을 실행 합니다.

```bash
sudo docker stop sql1
sudo docker rm sql1
```

```PowerShell
docker stop sql1
docker rm sql1
```

> [!WARNING]
> 중지 하 고 컨테이너를 영구적으로 제거에 컨테이너의 모든 SQL Server 데이터를 삭제 합니다. 데이터를 보존 하는 경우 [만들고 컨테이너에서 백업 파일을 복사](tutorial-restore-backup-in-sql-server-container.md) 하거나 사용 하 여 한 [컨테이너 데이터 지 속성 기술](sql-server-linux-configure-docker.md#persist)합니다.

## <a name="next-steps"></a>다음 단계

컨테이너에 데이터베이스 백업 파일을 복원 하는 방법에 대 한 자습서를 참조 하십시오. [Linux Docker 컨테이너에서 SQL Server 데이터베이스를 복원](tutorial-restore-backup-in-sql-server-container.md)합니다. 여러 컨테이너를 실행 하는 등의 다른 시나리오 데이터 지 속성 및 문제 해결, 참조 [Docker에 SQL Server 2017 구성 컨테이너 이미지](sql-server-linux-configure-docker.md)합니다.

또한, 체크 아웃 된 [mssql docker GitHub 리포지토리](https://github.com/Microsoft/mssql-docker) 리소스, 피드백 및 알려진된 문제에 대 한 합니다.
