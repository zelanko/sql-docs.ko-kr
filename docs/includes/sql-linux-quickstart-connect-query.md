## <a name="connect-locally"></a>로컬로 연결

다음 단계에서는 **sqlcmd**를 사용하여 새 SQL Server 인스턴스에 로컬로 연결합니다.

1. **sqlcmd**를 SQL Server 이름(-S), 사용자 이름(-U) 및 암호(-P)의 매개 변수를 사용하여 실행합니다. 이 자습서에서는 로컬로 연결하므로 서버 이름은 `localhost`입니다. 사용자 이름은 `SA`이고 암호는 설치할 때 SA 계정에 지정한 암호입니다.

   ```bash
   sqlcmd -S localhost -U SA -P '<YourPassword>'
   ```

   > [!TIP]
   > 명령줄에서 암호를 생략하여 입력하라는 메시지가 표시되도록 할 수 있습니다.

   > [!TIP]
   > 나중에 원격으로 연결하려는 경우 **-S** 매개 변수에 컴퓨터 이름 또는 IP 주소를 지정하고 방화벽에서 포트 1433이 열려 있는지 확인합니다.

1. 성공하면 **sqlcmd** 명령 프롬프트 `1>`이 표시됩니다.

1. 연결 오류가 발생하는 경우 먼저 오류 메시지에서 문제를 진단합니다. 그런 다음 [connection troubleshooting recommendations](../linux/sql-server-linux-troubleshooting-guide.md#connection)(연결 문제 해결 권장 사항)를 검토합니다.

## <a name="create-and-query-data"></a>데이터 만들기 및 쿼리
다음 섹션에서는 **sqlcmd**를 사용하여 새 데이터베이스를 만들고, 데이터를 추가하고, 간단한 쿼리를 실행하는 단계를 안내합니다.

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

**sqlcmd** 세션을 종료하려면 `QUIT`를 입력합니다.

```sql
QUIT
```

## <a name="connect-from-windows"></a>Windows에서 연결

Windows의 SQL Server 도구는 원격 SQL Server 인스턴스에 연결할 때와 동일하게 Linux의 SQL Server 인스턴스에 연결합니다.

Linux 컴퓨터에 연결할 수 있는 Windows 컴퓨터가 있는 경우 이 항목의 단계와 동일하게 Windows 명령 프롬프트에서 **sqlcmd**를 실행해 보세요. localhost 대신 대상 Linux 컴퓨터 이름이나 IP 주소를 사용하고 TCP 포트 1433이 열려 있는지 확인하기만 하면 됩니다. Windows에서 연결하는 데 문제가 있는 경우 [connection troubleshooting recommendations](../linux/sql-server-linux-troubleshooting-guide.md#connection)(연결 문제 해결 권장 사항)를 참조하세요.

Windows에서 실행하지만 Linux의 SQL Server에 연결하는 다른 도구는 다음을 참조하세요.

- [SSMS(SQL Server Management Studio)](../linux/sql-server-linux-develop-use-ssms.md)
- [Windows PowerShell](../linux/sql-server-linux-manage-powershell.md)
- [SSDT(SQL Server Data Tools)](../linux/sql-server-linux-develop-use-ssdt.md)

## <a name="next-steps"></a>다음 단계

다른 설치 시나리오의 경우 다음 리소스를 참조하세요.

|||
|---|---|
| [업그레이드](../linux/sql-server-linux-setup.md#upgrade) | Linux에서 SQL Server의 기존 설치를 업그레이드하는 방법 알아보기 |
| [제거](../linux/sql-server-linux-setup.md#uninstall) | Linux에서 SQL Server 제거 |
| [무인 설치](../linux/sql-server-linux-setup.md#unattended) | 확인 메시지를 표시하지 않고 설치를 스크립팅하는 방법을 알아봅니다. |
| [오프라인 설치](../linux/sql-server-linux-setup.md#offline) | 오프라인 설치에 대한 패키지를 수동으로 다운로드하는 방법을 알아봅니다. |

SQL Server를 연결하고 관리하는 다른 방법을 살펴보려면 [Visual Studio Code](../linux/sql-server-linux-develop-use-vscode.md) 및 [SQL Server Management Studio](../linux/sql-server-linux-develop-use-ssms.md)를 참조하세요.

Transact-SQL 문 및 쿼리를 작성하는 방법에 대한 자세한 내용은 [자습서: TRANSACT-SQL 문 작성](../t-sql/tutorial-writing-transact-sql-statements.md)을 참조하세요.
