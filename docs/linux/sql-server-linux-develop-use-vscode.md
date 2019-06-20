---
title: SQL Server 용 Visual Studio Code mssql 확장 사용
titleSuffix: SQL Server
description: Visual Studio Code 용 mssql 확장을 사용 하 여 편집 하 여 Linux에서 SQL Server에 대 한 TRANSACT-SQL 스크립트를 실행 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/18/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.openlocfilehash: b4d29739748b477adbef79bd1d6cf266aa16d2c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705541"
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts"></a>Visual Studio 코드를 사용 하 여 TRANSACT-SQL 스크립트 만들기 및 실행

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 사용 하는 **mssql** SQL Server 데이터베이스를 개발 하려면 Visual Studio Code 용 확장 합니다. Visual Studio Code는 플랫폼 간, 이므로 사용할 수 있습니다 **mssql** Linux, macOS 및 Windows에서 확장 합니다.

## <a name="install-and-start-visual-studio-code"></a>설치 하 고 Visual Studio Code 시작

Visual Studio Code는 확장을 지 원하는 플랫폼 간, 그래픽 코드 편집기입니다.

1. [다운로드 하 여 Visual Studio Code 설치](https://code.visualstudio.com/) 컴퓨터에 있습니다.

1. Visual Studio Code를 시작 합니다.

   >[!NOTE]
   >Xrdp 원격 데스크톱 세션을 통해 연결 되어 있는 경우에 Visual Studio Code 시작 되지 않으면, 참조 [XRDP를 사용 하 여 연결 하는 경우 Ubuntu에서 작동 하지 않는 VS Code](https://github.com/Microsoft/vscode/issues/3451)합니다.

## <a name="install-the-mssql-extension"></a>Mssql 확장 설치

합니다 [Visual Studio Code 용 mssql 확장](https://aka.ms/mssql-marketplace) SQL Server에 연결할 수 있도록 TRANSACT-SQL (T-SQL)를 사용 하 여 쿼리 및 결과 확인 합니다.

1. Visual Studio Code에서 선택 **뷰** > **명령 팔레트**를 누르거나 **Ctrl**+**Shift** + **P**를 누르거나 **F1** 열려는 합니다 **명령 팔레트**합니다.

1. 에 **명령 팔레트**, 선택 **확장: 확장 설치** 드롭다운 목록에서. 

1. 에 **Extensions** 창, 형식 *mssql*합니다.

1. 선택 된 **SQL Server (mssql)** 확장을 선택한 후 **설치**합니다.

   ![Mssql 확장 설치](./media/sql-server-linux-develop-use-vscode/vscode-extension.png)

1. 설치가 완료 되 면 선택 **다시 로드** 확장을 사용 하도록 합니다.

## <a name="create-or-open-a-sql-file"></a>SQL 파일 만들기 또는 열기

Mssql 확장을 설정 하면 mssql 명령 및 T-SQL IntelliSense 코드 편집기에서 언어 모드 설정 된 경우 **SQL**합니다.

1. 선택 **파일** > **새 파일** 누르거나 **Ctrl**+**N**합니다. Visual Studio Code는 기본적으로 새 일반 텍스트 파일을 엽니다. 

1. 선택 **일반 텍스트** 아래쪽 상태 표시줄에 키를 눌러 **Ctrl**+**K** > **M**, 선택한 **SQL** 언어 드롭다운 목록에서. 

   ![SQL 언어 모드](./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png)

   > [!NOTE]
   > 처음 확장을 사용 하는 경우 확장을 지 원하는 SQL Server 도구를 설치 합니다.

에 기존 파일을 열면를 *.sql* 파일 확장명을 언어 모드를 SQL로 자동 설정 됩니다.  

## <a name="connect-to-sql-server"></a>SQL Server에 연결

연결 프로필을 만들고 SQL Server에 연결 하려면 다음이 단계를 따릅니다.

1. 키를 눌러 **Ctrl**+**Shift**+**P** 나 **F1** 열려는 **명령 팔레트**. 

1. 형식 *sql* mssql 표시할 명령 또는 형식 *sqlcon*를 선택한 후 **MS SQL: 연결** 드롭다운 목록에서.

   ![mssql 명령](./media/sql-server-linux-develop-use-vscode/vscode-commands.png)

   >[!NOTE]
   >SQL 파일을 만든 빈 SQL 파일 같은 있어야 코드 편집기에서 포커스 mssql 명령을 실행할 수 있습니다.

1. 선택 된 **MS SQL: 연결 프로필을 관리** 명령입니다.

1. 선택한 **만들기** SQL Server에 대 한 새 연결 프로필을 만들려고 합니다.

1. 지시에 따라 새 연결 프로필에 대 한 속성을 지정 합니다. 키를 눌러 각 값을 지정한 후 **Enter** 를 계속 합니다.

   | 연결 속성 | Description |
   |---|---|
   | **서버 이름 또는 ADO 연결 문자열** | SQL Server 인스턴스 이름을 지정 합니다. 사용 하 여 *localhost* 로컬 컴퓨터에 SQL Server 인스턴스에 연결 합니다. 원격 SQL Server에 연결 하려면 SQL Server 대상의 이름 또는 IP 주소를 입력 합니다. SQL Server 컨테이너에 연결 하려면 컨테이너의 호스트 컴퓨터의 IP 주소를 지정 합니다. 포트를 지정 하는 경우 이름에서 분리 하려면 쉼표를 사용 합니다. 예를 들어 포트 1401에서 수신 대기 하는 서버에 대 한 입력 `<servername or IP>,1401`합니다.<br/><br/>대신 여기에서 데이터베이스에 대 한 ADO 연결 문자열을 입력할 수 있습니다. |
   | **데이터베이스 이름** (선택 사항) | 사용 하려는 데이터베이스입니다. 기본 데이터베이스에 연결 하려면 여기에 데이터베이스 이름을 지정 하지 마십시오. |
   | **인증 유형** | 선택할 **통합** 하거나 **SQL 로그인**합니다. |
   | **사용자 이름** | 선택한 경우 **SQL 로그인**, 서버에서 데이터베이스에 액세스할 수 있는 사용자의 이름을 입력 합니다. |
   | **암호** | 지정된 사용자의 암호를 입력합니다. |
   | **암호 저장** | 키를 눌러 **Enter** 선택할 **예** 암호를 저장 합니다. 선택 **No** 연결 프로필 사용 될 때마다 암호를 입력 해야 하는 합니다. |
   | **프로필 이름** (선택 사항) | 같은 연결 프로필에 대 한 이름을 입력 *localhost 프로필*합니다. |

   모든 값을 입력 하 고 선택 후 **Enter**, Visual Studio Code 연결 프로필을 만들고 SQL Server에 연결 합니다.

   > [!TIP]
   > 연결이 실패 하는 경우의 오류 메시지에서 문제를 진단 하려고 합니다 **출력** Visual Studio Code에서 패널입니다. 열려는 합니다 **출력** 패널에서 **뷰** > **출력**합니다. 또한 검토 해야 합니다 [연결 문제 해결 권장 사항이](./sql-server-linux-troubleshooting-guide.md#connection)합니다.

1. 아래쪽 상태 표시줄에 대 한 연결을 확인 합니다.

   ![연결 상태](./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png)

이전 단계를 대신 하도 만들고 편집할 수 있습니다 사용자 설정 파일에서 연결 프로필 (*settings.json*). 설정 파일을 열려면 **파일** > **기본 설정** > **설정**합니다. 자세한 내용은 [연결 프로필을 관리](https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles)합니다.

## <a name="create-a-sql-database"></a>SQL database 만들기

1. 이전에 시작 하는 새 SQL 파일에서 입력 *sql* 편집할 수 있는 코드 조각의 목록을 표시 합니다. 

   ![SQL 코드 조각](./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png)

1. 선택 **sqlCreateDatabase**합니다.

1. 코드 조각에서 입력 `TutorialDB` 'DatabaseName'의 이름을 바꾸려면:

   ```sql
   -- Create a new database called 'TutorialDB'
   -- Connect to the 'master' database to run this snippet
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO
   ```

1. 키를 눌러 **Ctrl**+**Shift**+**E** TRANSACT-SQL 명령을 실행 합니다. 쿼리 창에서 결과 봅니다.

   ![데이터베이스 메시지 만들기](./media/sql-server-linux-develop-use-vscode/vscode-create-database-messages.png)

   > [!TIP]
   > Mssql 명령에 대 한 바로 가기 키를 사용자 지정할 수 있습니다. 참조 [바로 가기를 사용자 지정](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts)합니다.

## <a name="create-a-table"></a>테이블 생성하기

1. 코드 편집기 창의 내용을 삭제 합니다.

1. 키를 눌러 **Ctrl**+**Shift**+**P** 나 **F1** 열려는 **명령 팔레트**. 

1. 형식 *sql* mssql 표시할 명령 또는 형식 *sqluse*를 선택한 후는 **MS SQL: 데이터베이스를 사용 하 여** 명령입니다.

1. 새 선택 **TutorialDB** 데이터베이스입니다. 

   ![데이터베이스 사용](./media/sql-server-linux-develop-use-vscode/vscode-use-database.png)

1. 코드 편집기에서 입력 *sql* 코드를 표시 하려면 선택 **sqlCreateTable**을 누릅니다 **Enter**합니다.

1. 코드 조각에서 입력 `Employees` 테이블 이름에 대 한 합니다.

1. 키를 눌러 **탭** 다음 필드를 가져오고 입력 `dbo` 스키마 이름에 대 한 합니다.

1. 다음 열이 있는 열 정의 바꿉니다.

   ```sql
   EmployeesId INT NOT NULL PRIMARY KEY,
   Name [NVARCHAR](50)  NOT NULL,
   Location [NVARCHAR](50)  NOT NULL
   ```

1. 키를 눌러 **Ctrl**+**Shift**+**E** 테이블을 만듭니다.

## <a name="insert-and-query"></a>삽입 및 쿼리

1. 4 개의 행을 삽입 하려면 다음 문을 추가 합니다 **직원** 테이블입니다.

   ```sql
   -- Insert rows into table 'Employees'
   INSERT INTO Employees
      ([EmployeesId],[Name],[Location])
   VALUES
      ( 1, N'Jared', N'Australia'),
      ( 2, N'Nikita', N'India'),
      ( 3, N'Tom', N'Germany'),
      ( 4, N'Jake', N'United States')
   GO
   -- Query the total count of employees
   SELECT COUNT(*) as EmployeeCount FROM dbo.Employees;
   -- Query all employee information
   SELECT e.EmployeesId, e.Name, e.Location 
   FROM dbo.Employees as e
   GO
   ```

   입력 하는 동안 T-SQL IntelliSense를 사용 하면 문을 완료할 수 있습니다.

   ![T-SQL IntelliSense](./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png)

   > [!TIP]
   > Mssql 확장 명령을 INSERT 및 SELECT 문을 만드는 데 있습니다. 이러한 값은 이전 예제에서 사용 되지 않았습니다.

1. 키를 눌러 **Ctrl**+**Shift**+**E** 명령을 실행 합니다. 두 결과 집합 표시에는 **결과** 창입니다. 

   ![결과](./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png)

## <a name="view-and-save-the-result"></a>보기 및 결과 저장 합니다.

1. 선택 **뷰** > **편집기 레이아웃** > **대칭 이동 레이아웃** 수직 또는 수평 분할 레이아웃으로 전환 합니다.

1. 선택 합니다 **결과** 하 고 **메시지** 헤더 패널을 확장 및 축소를 패널입니다.

   ![설정/해제 헤더](./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png)

   > [!TIP]
   > Mssql 확장의 기본 동작을 사용자 지정할 수 있습니다. 참조 [확장 옵션을 사용자 지정](https://github.com/Microsoft/vscode-mssql/wiki/customize-options)합니다.

1. 이러한 결과를 확대 하려면 두 번째 결과 그리드에서 최대화 표 아이콘을 선택 합니다.

   ![표를 최대화 합니다.](./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png)

   > [!NOTE]
   > 최대화 아이콘을 두 개 이상의 결과 표를 생성 하는 T-SQL 스크립트를 표시 합니다.

1. 눈금을 마우스 오른쪽 단추로 클릭 하 여 그리드 상황에 맞는 메뉴를 엽니다. 

   ![상황에 맞는 메뉴](./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png)

1. 선택 **모두 선택**합니다.

1. 그리드 상황에 맞는 메뉴를 다시 열고 선택 **JSON으로 저장** 결과를 저장 하는 *.json* 파일입니다.

1. JSON 파일의 파일 이름을 지정 합니다. 

1. JSON 파일을 저장 하 고 Visual Studio Code에서 열립니다를 확인 합니다.

   ![JSON으로 저장](./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png)

저장 하 고 나중에 관리 하거나 대규모 개발 프로젝트에 대 한 SQL 스크립트를 실행 하는 경우에 스크립트를 사용 하 여 저장 된 *.sql* 확장 합니다.

## <a name="next-steps"></a>다음 단계

T-SQL을 처음 접하는 경우 [자습서: TRANSACT-SQL 문 작성](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements) 하며 [TRANSACT-SQL 참조 (데이터베이스 엔진)](https://docs.microsoft.com/sql/t-sql/language-reference)합니다.

사용 하 여 mssql 확장에 영향을 주는에 대 한 자세한 내용은 참조는 [mssql 확장 프로젝트 wiki](https://github.com/Microsoft/vscode-mssql/wiki)합니다.

Visual Studio Code 사용에 대 한 자세한 내용은 참조는 [Visual Studio Code 설명서](https://code.visualstudio.com/docs)합니다.