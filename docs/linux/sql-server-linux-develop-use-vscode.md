---
title: SQL Server에 대해 Visual Studio Code mssql 확장 사용
titleSuffix: SQL Server
description: Visual Studio Code mssql 확장을 사용하여 SQL Server on Linux용 Transact-SQL 스크립트를 편집하고 실행합니다.
author: VanMSFT
ms.author: vanto
ms.date: 12/18/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.openlocfilehash: 207a542e07f271607e5d2266b8c32e313b1dff13
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077316"
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts"></a>Visual Studio Code를 사용하여 Transact-SQL 스크립트 만들기 및 실행

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Visual Studio Code **mssql** 확장을 사용하여 SQL Server 데이터베이스를 개발하는 방법을 보여 줍니다. Visual Studio Code는 플랫폼 간에 지원되므로 Linux, macOS 및 Windows에서 **mssql** 확장을 사용할 수 있습니다.

## <a name="install-and-start-visual-studio-code"></a>Visual Studio Code 설치 및 시작

Visual Studio Code는 확장을 지원하는 플랫폼 간 그래픽 코드 편집기입니다.

1. 머신에서 [Visual Studio Code를 다운로드하여 설치](https://code.visualstudio.com/)합니다.

1. Visual Studio Code를 시작합니다.

   >[!NOTE]
   >xrdp 원격 데스크톱 세션을 통해 연결된 경우 Visual Studio Code가 시작되지 않으면 [XRDP를 사용하여 연결된 경우 Ubuntu에서 VS Code가 작동하지 않음](https://github.com/Microsoft/vscode/issues/3451)을 참조하세요.

## <a name="install-the-mssql-extension"></a>mssql 확장 설치

[Visual Studio Code mssql 확장](https://aka.ms/mssql-marketplace)을 사용하면 SQL Server에 연결하고 T-SQL(Transact-SQL)을 사용하여 쿼리한 다음, 결과를 볼 수 있습니다.

1. Visual Studio Code에서 **보기** > **명령 팔레트**를 선택하거나, **Ctrl**+**Shift**+**P** 또는 **F1** 키를 눌러 **명령 팔레트**를 엽니다.

1. **명령 팔레트**의 드롭다운에서 **확장: 확장 설치**를 선택합니다. 

1. **확장** 창에서 *mssql*을 입력합니다.

1. **SQL Server(mssql)** 확장을 선택한 다음, **설치**를 선택합니다.

   ![mssql 확장 설치](./media/sql-server-linux-develop-use-vscode/vscode-extension.png)

1. 설치가 완료되면 **다시 로드**를 선택하여 확장을 사용하도록 설정합니다.

## <a name="create-or-open-a-sql-file"></a>SQL 파일 만들기 또는 열기

mssql 확장은 언어 모드가 **SQL**로 설정된 경우 코드 편집기에서 mssql 명령과 T-SQL IntelliSense를 사용하도록 설정합니다.

1. **파일** > **새 파일**을 선택하거나 **Ctrl**+**N**을 누릅니다. Visual Studio Code는 기본적으로 새 일반 텍스트 파일을 엽니다. 

1. 아래쪽 상태 표시줄에서 **일반 텍스트**를 선택하거나, **Ctrl**+**K** > **M**을 누르고 언어 드롭다운에서 **SQL**을 선택합니다. 

   ![SQL 언어 모드](./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png)

   > [!NOTE]
   > 확장을 처음 사용하는 경우 확장에서 지원하는 SQL Server 도구를 설치합니다.

*.sql* 파일 확장명을 가진 기존 파일을 열면 언어 모드가 자동으로 SQL로 설정됩니다.  

## <a name="connect-to-sql-server"></a>SQL Server에 연결

연결 프로필을 만들고 SQL Server에 연결하려면 다음 단계를 수행합니다.

1. **Ctrl**+**Shift**+**P** 또는 **F1** 키를 눌러 **명령 팔레트**를 엽니다. 

1. *sql*을 입력하여 mssql 명령을 표시하거나, *sqlcon*을 입력하고 드롭다운에서 **MS SQL: 연결**을 선택합니다.

   ![mssql 명령](./media/sql-server-linux-develop-use-vscode/vscode-commands.png)

   >[!NOTE]
   >사용자가 만든 빈 SQL 파일 등의 SQL 파일은 코드 편집기에서 포커스가 있어야 mssql 명령을 실행할 수 있습니다.

1. **MS SQL: 연결 프로필 관리** 명령을 선택합니다.

1. **만들기**를 선택하여 SQL Server의 새 연결 프로필을 만듭니다.

1. 프롬프트에 따라 새 연결 프로필의 속성을 지정합니다. 각 값을 지정한 후 **Enter** 키를 눌러 계속합니다.

   | 연결 속성 | 설명 |
   |---|---|
   | **서버 이름 또는 ADO 연결 문자열** | SQL Server 인스턴스 이름을 지정합니다. *localhost*를 사용하여 로컬 머신의 SQL Server 인스턴스에 연결합니다. 원격 SQL Server에 연결하려면 대상 SQL Server의 이름 또는 해당 IP 주소를 입력합니다. SQL Server 컨테이너에 연결하려면 컨테이너 호스트 머신의 IP 주소를 지정합니다. 포트를 지정해야 하는 경우 쉼표를 사용하여 이름과 구분합니다. 예를 들어 포트 1401에서 수신 대기하는 서버의 경우 `<servername or IP>,1401`을 입력합니다.<br/><br/>또는 여기서 데이터베이스의 ADO 연결 문자열을 입력할 수 있습니다. |
   | **데이터베이스 이름**(선택 사항) | 사용하려는 데이터베이스입니다. 기본 데이터베이스에 연결하려면 여기서 데이터베이스 이름을 지정하지 않습니다. |
   | **인증 유형** | **통합** 또는 **SQL 로그인**을 선택합니다. |
   | **User name** | **SQL 로그인**을 선택한 경우 서버의 데이터베이스에 대한 액세스 권한이 있는 사용자의 이름을 입력합니다. |
   | **암호** | 지정된 사용자의 암호를 입력합니다. |
   | **암호 저장** | **Enter** 키를 눌러 **예**를 선택하고 암호를 저장합니다. 연결 프로필을 사용할 때마다 암호 확인 메시지를 표시하려면 **아니요**를 선택합니다. |
   | **프로필 이름**(선택 사항) | 연결 프로필의 이름(예: *localhost profile*)을 입력합니다. |

   모든 값을 입력하고 **Enter** 키를 선택하면 Visual Studio Code에서 연결 프로필을 만들고 SQL Server에 연결합니다.

   > [!TIP]
   > 연결에 실패하면 Visual Studio Code **출력** 패널의 오류 메시지를 통해 문제를 진단해 봅니다. **출력** 패널을 열려면 **보기** > **출력**을 선택합니다. 또한 [연결 문제 해결 권장 사항](./sql-server-linux-troubleshooting-guide.md#connection)을 검토합니다.

1. 아래쪽 상태 표시줄에서 연결을 확인합니다.

   ![연결 상태](./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png)

이전 단계 대신 사용자 설정 파일(*settings.json*)에서 연결 프로필을 만들고 편집할 수도 있습니다. 설정 파일을 열려면 **파일** > **기본 설정** > **설정**을 선택합니다. 자세한 내용은 [연결 프로필 관리](https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles)를 참조하세요.

## <a name="create-a-sql-database"></a>SQL 데이터베이스 만들기

1. 앞에서 시작한 새 SQL 파일에서 *sql*을 입력하여 편집 가능한 코드 조각 목록을 표시합니다. 

   ![SQL 코드 조각](./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png)

1. **sqlCreateDatabase**

1. 코드 조각에서 `TutorialDB`를 입력하여 ‘DatabaseName’을 바꿉니다.

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

1. **Ctrl**+**Shift**+**E**를 눌러 Transact-SQL 명령을 실행합니다. 쿼리 창에서 결과를 확인합니다.

   ![데이터베이스 메시지 만들기](./media/sql-server-linux-develop-use-vscode/vscode-create-database-messages.png)

   > [!TIP]
   > mssql 명령의 바로 가기 키를 사용자 지정할 수 있습니다. [바로 가기 사용자 지정](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts)을 참조하세요.

## <a name="create-a-table"></a>테이블 만들기

1. 코드 편집기 창의 내용을 삭제합니다.

1. **Ctrl**+**Shift**+**P** 또는 **F1** 키를 눌러 **명령 팔레트**를 엽니다. 

1. *sql*을 입력하여 mssql 명령을 표시하거나, *sqluse*를 입력하고 **MS SQL: 데이터베이스 사용** 명령을 선택합니다.

1. 새 **TutorialDB** 데이터베이스를 선택합니다. 

   ![데이터베이스 사용](./media/sql-server-linux-develop-use-vscode/vscode-use-database.png)

1. 코드 편집기에서 *sql*을 입력하여 코드 조각을 표시하고 **sqlCreateTable**을 선택한 다음, **Enter** 키를 누릅니다.

1. 코드 조각에서 테이블 이름으로 `Employees`를 입력합니다.

1. **Tab** 키를 눌러 다음 필드로 이동한 다음, 스키마 이름으로 `dbo`를 입력합니다.

1. 열 정의를 다음 열로 바꿉니다.

   ```sql
   EmployeesId INT NOT NULL PRIMARY KEY,
   Name [NVARCHAR](50)  NOT NULL,
   Location [NVARCHAR](50)  NOT NULL
   ```

1. **Ctrl**+**Shift**+**E**를 눌러 테이블을 만듭니다.

## <a name="insert-and-query"></a>삽입 및 쿼리

1. 다음 문을 추가하여 **Employees** 테이블에 행 4개를 삽입합니다.

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

   입력하는 동안 T-SQL IntelliSense에서 문을 완성할 수 있도록 지원합니다.

   ![T-SQL IntelliSense](./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png)

   > [!TIP]
   > mssql 확장에는 INSERT 및 SELECT 문을 만드는 데 도움이 되는 명령도 있습니다. 이 명령은 앞의 예제에서 사용되지 않았습니다.

1. **Ctrl**+**Shift**+**E**를 눌러 명령을 실행합니다. **결과** 창에 두 개의 결과 집합이 표시됩니다. 

   ![결과](./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png)

## <a name="view-and-save-the-result"></a>결과 보기 및 저장

1. **보기** > **편집기 레이아웃** > **레이아웃 대칭 이동**을 선택하여 세로 또는 가로 분할 레이아웃으로 전환합니다.

1. **결과** 및 **메시지** 패널 헤더를 선택하여 패널을 축소하거나 확장합니다.

   ![헤더 설정/해제](./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png)

   > [!TIP]
   > mssql 확장의 기본 동작을 사용자 지정할 수 있습니다. [확장 옵션 사용자 지정](https://github.com/Microsoft/vscode-mssql/wiki/customize-options)을 참조하세요.

1. 두 번째 결과 그리드에서 그리드 최대화 아이콘을 선택하여 해당 결과를 확대합니다.

   ![그리드 최대화](./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png)

   > [!NOTE]
   > T-SQL 스크립트에서 두 개 이상의 결과 그리드를 생성하면 최대화 아이콘이 표시됩니다.

1. 그리드를 마우스 오른쪽 단추로 클릭하여 그리드 상황에 맞는 메뉴를 엽니다. 

   ![상황에 맞는 메뉴](./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png)

1. **모두 선택**을 선택합니다.

1. 그리드 상황에 맞는 메뉴를 다시 열고 **JSON으로 저장**을 선택하여 결과를 *.json* 파일에 저장합니다.

1. JSON 파일의 파일 이름을 지정합니다. 

1. JSON 파일이 저장되고 Visual Studio Code에서 열리는지 확인합니다.

   ![JSON으로 저장](./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png)

나중에 관리 또는 대규모 개발 프로젝트를 위해 SQL 스크립트를 저장하고 실행해야 하는 경우 스크립트를 *.sql* 확장명으로 저장합니다.

## <a name="next-steps"></a>다음 단계

T-SQL을 처음 사용하는 경우 [자습서: Transact-SQL 문 작성](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements) 및 [Transact-SQL 참조(데이터베이스 엔진)](https://docs.microsoft.com/sql/t-sql/language-reference)를 참조하세요.

mssql 확장을 사용하거나 참여하는 방법에 대한 자세한 내용은 [mssql 확장 프로젝트 wiki](https://github.com/Microsoft/vscode-mssql/wiki)를 참조하세요.

Visual Studio Code 사용 방법에 대한 자세한 내용은 [Visual Studio Code 설명서](https://code.visualstudio.com/docs)를 참조하세요.