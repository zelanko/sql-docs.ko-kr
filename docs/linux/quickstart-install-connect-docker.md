---
title: "Docker에서 SQL Server 2017 시작 | Microsoft Docs"
description: "이 빠른 시작 자습서에는 SQL Server 2017 컨테이너 이미지를 실행 하려면 Docker를 사용 하는 방법을 보여 줍니다. 그런 다음 만들고 sqlcmd 사용 하 여 데이터베이스를 쿼리 합니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 77d8c7d01cd5d7a1787b9deddbe7003e09e32e6f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="run-the-sql-server-2017-container-image-with-docker"></a>Docker가 있는 SQL Server 2017 컨테이너 이미지를 실행 합니다.

이 빠른 시작 자습서를 사용 하 여 Docker pull 및 SQL Server 2017 RC2 컨테이너 이미지를 실행 [mssql-서버-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/)합니다. 다음으로 연결 **sqlcmd** 첫 번째 데이터베이스를 만들고 쿼리를 실행 합니다.

이 이미지는 Ubuntu 16.04에 따라 Linux에서 실행 중인 SQL Server 구성 됩니다. Mac/Windows 용 Docker 엔진 1.8 + linux 또는 Docker에서 사용할 수 있습니다.

> [!NOTE]
> 이 빠른 시작 mssql-서버-linux 이미지를 사용 하 여에 특별히 중점을 둡니다. Windows 이미지 적용 되지 않는 있지만에서 항목에 대 한 자세히 알아볼 수 있습니다는 [mssql-서버-windows Docker 허브 페이지](https://hub.docker.com/r/microsoft/mssql-server-windows/)합니다.

## <a id="requirements"></a> 필수 구성 요소

- docker 엔진 1.8 + Mac/창에 Linux 배포 또는 Docker를 지원 합니다.
- 최소 4GB의 디스크 공간
- 최소 4GB의 RAM
- [Linux에서 SQL Server에 대 한 시스템 요구 사항](sql-server-linux-setup.md#system)합니다.

> [!IMPORTANT]
> Mac 용 Docker 및 Windows 용 Docker에 대 한 기본값 Moby VM에 대 한 2GB 이므로 4GB로 변경 해야 합니다. Mac 또는 Windows에서 실행 하는 경우에 메모리를 늘리기 위해 다음 절차를 따르세요.

### <a name="increase-docker-memory-to-4-gb-mac"></a>4GB (Mac) Docker 메모리 증가

다음 단계는 4GB로 Mac 용 Docker에 대 한 메모리를 늘리십시오.

1. 상위 상태 표시줄에 Docker 로고를 클릭 합니다.
1. 선택 **기본 설정**합니다.
1. 4GB 이상의 메모리 표시기를 이동 합니다.
1. 클릭는 **다시 시작** 화면 단추에 있는 단추입니다.

### <a name="increase-docker-memory-to-4-gb-windows"></a>4GB (Windows) Docker 메모리 증가

다음 단계는 4GB로 Windows 용 Docker에 대 한 메모리를 늘리십시오.

1. 작업 표시줄에서 Docker 아이콘을 마우스 오른쪽 단추로 클릭 합니다.
1. 클릭 **설정을** 해당 메뉴.
1. 클릭는 **고급** 탭 합니다.
1. 4GB 이상의 메모리 표시기를 이동 합니다.
1. 클릭는 **적용** 단추입니다.

## <a name="pull-and-run-the-container-image"></a>컨테이너 이미지를 실행 하 고 끌어오기

1. Docker 허브에서 컨테이너 이미지를 끌어옵니다.

    ```bash
    docker pull microsoft/mssql-server-linux
    ```

    > [!TIP]
    > Linux 시스템 및 사용자 구성에 따라 해야 할 수 있습니다 각 앞 `docker` 명령을 `sudo`합니다.

1. Docker가 있는 컨테이너 이미지를 실행 하려면 bash 셸의 (Linux/macOS)에서 다음 명령을 사용할 수 있습니다.

    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -e 'MSSQL_PID=Developer' --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
    ```

    Windows 용 Docker를 사용 하는 경우에 관리자 권한 PowerShell 명령 프롬프트에서 다음 명령을 사용 합니다.

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
    ```

    > [!NOTE]
    > Bash (Linux/macOS) 예제와 PowerShell (Windows) 예제 간의 유일한 차이점은 환경 변수 주위 큰따옴표와 작은따옴표 합니다. Docker run 명령에 잘못 된을 사용 하는 경우 실패 합니다. 이 항목의 나머지 bash 및 PowerShell 코드 블록 편의 위해 제공 됩니다. 예제로 이면 Windows를 비롯 한 모든 플랫폼에서 작동 합니다.

    다음 표에서 이전에 매개 변수 설명을 `docker run` 예제:

    | 매개 변수 | Description |
    |-----|-----|
    | **-e ' ACCEPT_EULA = Y'** |  설정의 **ACCEPT_EULA** 동의한 것에 어떤 값이 변수는 [최종 사용자 사용권 계약](http://go.microsoft.com/fwlink/?LinkId=746388)합니다. SQL Server 이미지에 대 한 설정 해야 합니다. |
    | **-e ' MSSQL_SA_PASSWORD =\<YourStrong! Passw0rd\>'** | 사용자 고유의 강력한 암호를 8 자 이상 있고에 맞는 지정 [SQL Server 암호 요구 사항을](../relational-databases/security/password-policy.md)합니다. SQL Server 이미지에 대 한 설정 해야 합니다. |
    | **-e ' MSSQL_PID 개발자 ='** | 버전 또는 제품 키를 지정합니다. 이 예제에서는 자유롭게 사용이 허가 된 Developer Edition은 비-프로덕션 테스트에 사용 됩니다. 다른 값을 참조 하십시오. [Linux에서 환경 변수를 사용 하 여 SQL Server 구성 설정](sql-server-linux-configure-environment-variables.md)합니다. |
    | **-cap 추가 SYS_PTRACE** | 프로세스를 추적 하는 Linux 기능을 추가 합니다. 이 통해 예외에서 덤프를 생성 합니다. |
    | **-p 1401:1433** | 호스트 환경에서 TCP 포트 매핑 (첫째 값) 컨테이너의 TCP 포트 (두 번째 값). 이 예제에서는 SQL Server가 컨테이너의 TCP 1433에서 수신 하 고 호스트에서 1401 포트에 노출 됩니다. |
    | **microsoft/mssql-서버-linux** | SQL Server Linux 컨테이너 이미지입니다. 기본값은 별도로 지정 하지 않으면는 **최신** 이미지입니다. |

1. Docker 컨테이너를 보려면 사용 하 여는 `docker ps` 명령입니다.

    ```bash
    docker ps -a
    ```

    다음 스크린샷과 유사한 출력이 표시 되어야 합니다.

    ![Docker ps 명령 출력](./media/sql-server-linux-setup-docker/docker-ps-command.png)

1. 경우는 **상태** 열 표시의 상태 **를**컨테이너에서 SQL Server가 실행 한 다음, 및에 지정 된 포트에서 수신 하는 **포트** 열입니다. 경우는 **상태** SQL Server 컨테이너 표시에 대 한 열 **Exited**, 참조는 [구성 가이드의 섹션 문제 해결](sql-server-linux-configure-docker.md#troubleshooting)합니다.

두 개의 유용한 `docker run` 편의상 이전 예제에서 사용 되지 옵션입니다. `-h` (호스트 이름) 매개 변수는 컨테이너의 내부 이름을 사용자 지정 값으로 변경 합니다. 이 다음 Transact SQL 쿼리에서 반환 된 이름이 표시 됩니다.

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

또한 확인할 수도 `--name` 매개 변수 생성된 컨테이너 이름을 보다는 컨테이너 이름을 지정 하는 데 유용 합니다. 설정 `-h` 및 `--name` 과 같은 값은 쉽게 대상 컨테이너를 식별 하는 데 유용 합니다.

## <a name="change-the-sa-password"></a>SA 암호를 변경 합니다.

SA 계정이 설치 중 생성 되는 SQL Server 인스턴스에서 시스템 관리자입니다. SQL Server 컨테이너를 만든 후의 `MSSQL_SA_PASSWORD` 지정한 환경 변수를 실행 하 여 검색할 수 `echo $MSSQL_SA_PASSWORD` 컨테이너에 있습니다. 보안을 위해 SA 암호를 변경 합니다.

1. SA 사용자에 사용할 수 있는 강력한 암호를 선택 합니다.

1. 사용 하 여 `docker exec` 실행 **sqlcmd** TRANSACT-SQL을 사용 하 여 암호를 변경 합니다. 대체 `<Old Password>` 및 `<New Password>` 암호 값입니다.

> ```bash
> docker exec -it <Container ID> /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<Old Password>' -Q 'ALTER LOGIN SA WITH PASSWORD="<New Password>";'
> ```

## <a name="connect-to-sql-server"></a>SQL Server에 연결

다음 단계에 SQL Server 명령줄 도구를 사용 하 여 **sqlcmd**, 컨테이너 내에서 SQL Server에 연결 합니다.

1. 사용 하 여는 `docker exec -it` 는 대화형 bash 셸의 실행 중인 컨테이너 내 시작 명령입니다. 다음 예에서 `e69e056c702d` 컨테이너 ID입니다.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 항상 전체 컨테이너 id를 지정할 필요가 없습니다. 고유 하 게 식별 필요한 만큼의 문자를 지정 해야 합니다. 이 예제에서 사용 하기에 충분 한 않을 수도 것 `e6` 또는 `e69` 전체 id 대신 합니다.

1. 한 번, 컨테이너 내부 연결 로컬로 sqlcmd 합니다. Sqlcmd 아니므로 기본적으로 경로에 전체 경로 지정 해야 합니다.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
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

## <a name="connect-from-outside-the-container"></a>컨테이너 외부에서 연결

연결할 수 있습니다도 SQL Server 인스턴스에 Docker 컴퓨터에 SQL 연결을 지 원하는 Linux, Windows 또는 macOS 도구 외부에서.

다음 단계를 사용 하 여 **sqlcmd** 컨테이너에서 실행 중인 SQL Server에 연결 하 여 컨테이너의 외부입니다. 다음이 단계에 컨테이너의 외부에 설치 된 SQL Server 명령줄 도구 이미 있다고 가정 합니다. 다른 도구를 사용 하는 경우 동일한 주체 적용 하지만 연결 하는 프로세스는 각 도구에 고유 합니다.

1. 컨테이너를 호스팅하는 컴퓨터에 대 한 IP 주소를 찾습니다. Linux에서 사용 하 여 **ifconfig** 또는 **ip 주소**합니다. Windows에서 사용 하 여 **ipconfig**합니다.

1. IP 주소와 컨테이너의 포트 1433에 매핑된 포트를 지정 하는 sqlcmd를 실행 합니다. 이 예제에서는 호스트 컴퓨터에 1401 포트입니다.

   ```bash
   sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
   ```

1. TRANSACT-SQL 명령이 실행된 합니다. 완료 되 면 입력 `QUIT`합니다.

다른 일반적인 도구는 SQL Server에 연결 하는 다음과 같습니다.

- [Visual Studio 코드](sql-server-linux-develop-use-vscode.md)
- [Windows에서 SQL Server Management Studio (SSMS)](sql-server-linux-develop-use-ssms.md)

## <a name="next-steps"></a>다음 단계

여러 컨테이너, 데이터 지 속성 및 troublehshooting를 실행 하는 등의 다른 시나리오 참조 [Docker에 SQL Server 2017 구성 컨테이너 이미지](sql-server-linux-configure-docker.md)합니다.

또한, 체크 아웃 된 [mssql docker GitHub 리포지토리](https://github.com/Microsoft/mssql-docker) 리소스, 피드백 및 알려진된 문제에 대 한 합니다.

