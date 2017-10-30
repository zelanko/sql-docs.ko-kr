---
title: "SQL Server에 대 한 Visual Studio Code mssql 확장을 사용 하 여 | Microsoft Docs"
description: "이 자습서에서는 VS Code에 mssql 확장명을 사용 하는 방법을 보여 줍니다. 이 확장을 사용 하면 편집 하 고 VS Code에서 Transact SQL 스크립트를 실행할 수 있습니다."
author: erickangMSFT
ms.author: erickang
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.custom: H1Hack27Feb2017
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 2d8ba0dcd52de143cd935eab6e8bba95e924409d
ms.contentlocale: ko-kr
ms.lasthandoff: 10/10/2017

---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts-for-sql-server"></a>Visual Studio 코드를 사용 하 여 만들고 SQL Server에 대 한 TRANSACT-SQL 스크립트를 실행 합니다.

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 항목에서는 사용 하는 **mssql** Visual Studio 코드 (VS) SQL Server 데이터베이스를 개발 하기에 대 한 확장입니다.

Visual Studio 코드는 Linux, macOS 등 및 확장을 지 원하는 Windows 그래픽 코드 편집기입니다. [ **mssql** VS Code에 대 한 확장] TRANSACT-SQL (T-SQL) 사용 하 여 쿼리를 SQL Server에 연결 하 고 결과 볼 수 있습니다.

## <a name="install-vs-code"></a>VS Code 설치
1. VS Code를 아직 설치 하지 않은 경우 [다운로드 하 고 VS Code 설치] 컴퓨터에 있습니다.

2. VS Code를 시작 합니다.

## <a name="install-the-mssql-extension"></a>Mssql 확장 설치
다음 단계에는 mssql 확장을 설치 하는 방법을 설명 합니다. 

1. 키를 눌러 **CTRL + SHIFT + P** (또는 **F1**)를 VS Code에 명령 팔레트를 엽니다. 

2. 선택 **설치 확장** 유형과 **mssql**합니다.
   > [!TIP] 
   > MacOS 등에 대 한는 **CMD** 키가 같음 **CTRL** Linux와 Windows에서 키입니다.

2. 설치 클릭 **mssql**합니다. 
   
   <img src="./media/sql-server-linux-develop-use-vscode/vscode-extension.png" alt="Install the extension" style="width: 600px;"/>

3. **mssql** 확장을 설치 하는 최대 1 분이 걸립니다. 성공적으로 설치 알려주는 메시지가 표시 될 때까지 기다립니다.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-install-success-notification.png" alt="Installation success notification" style="width: 600px;"/>

   > [!NOTE]
   > MacOS 등 OpenSSL을 설치 해야 합니다. 이.Net에 대 한 필수 코어 mssql 확장 프로그램에서 사용 합니다. 에 따라는 **필수 소프트웨어를 설치** 의 단계는 [.NET 지침 핵심]합니다. 또는 터미널 프로그램 macOS에서 다음 명령을 실행할 수 있습니다.
   >
   >   ```bash
   >   brew update
   >   brew install openssl
   >   ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
   >   ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
   >   ```
   
   > [!NOTE]
   > Windows 8.1, Windows Server 2012 또는 더 낮은 버전을 다운로드 하 고 설치 해야는 [Windows 10 유니버설 C 런타임]합니다. 다운로드 하 여 zip 파일을 엽니다. 그런 다음 현재 운영 체제 구성의 대상으로 설치 관리자 (.msu 파일)를 실행 합니다.

## <a name="create-or-open-a-sql-file"></a>SQL 파일 만들기 또는 열기

**mssql** 확장을 사용 하면 mssql 명령 및 IntelliSense T-SQL 편집기에서 언어 모드로 설정 된 경우 **SQL**합니다.

1. 키를 눌러 **CTRL + N**합니다. Visual Studio Code 기본적으로 새 ' 일반 텍스트 ' 파일을 엽니다. 

2. 키를 눌러 **CTRL + K, M** 언어 모드를 변경 하 고 **SQL**합니다. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png" alt="SQL language mode" style="width: 500px;" />

3. 또는.sql 파일 확장명을 가진 기존 파일을 엽니다. 언어 모드는 자동으로 **SQL** 확장명이.sql 인 파일에 대 한 합니다.  

## <a name="connect-to-sql-server"></a>SQL Server에 연결

다음 단계에는 SQL server VS Code로 연결 하는 방법을 보여 줍니다.

1. VS Code에서 눌러 **CTRL + SHIFT + P** (또는 **F1**) 명령 팔레트를 엽니다.

2. 형식 **sql** mssql 명령이 표시 됩니다.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-commands.png" alt="mssql commands" style="width: 500px;" />
   

3. 선택 된 **MS SQL: 연결** 명령입니다. 입력 하면 **sqlcon** 누릅니다 **ENTER**합니다.

4. 선택 **연결 프로필을 만들려면**합니다. SQL Server 인스턴스에 대 한 연결 프로필을 만듭니다.

5. 지시에 따라 새 연결 프로필에 대 한 연결 속성을 지정 합니다. 각 값을 지정한 후 눌러 **ENTER** 를 계속 합니다. 

   다음 표에서 연결 프로필 속성을 설명 합니다.

   | 설정 | Description |
   |-----|-----|
   | **서버 이름** | SQL Server 인스턴스 이름입니다. 이 자습서에서 사용 하 여 **localhost** 컴퓨터에 로컬 SQL Server 인스턴스에 연결할 수 있습니다. 원격 SQL Server에 연결 된 경우에 대상 SQL Server 컴퓨터 또는 IP 주소 이름을 입력 합니다. |
   | **[선택 사항] 데이터베이스 이름** | 이 데이터베이스에 사용 하려는입니다. 이 자습서에는 데이터베이스와 키를 눌러 지정 하지 않으면 **ENTER** 를 계속 합니다. |
   | **사용자 이름** | 서버에서 데이터베이스에 액세스할 수 있는 사용자의 이름을 입력 합니다. 이 자습서에서는 기본값을 사용 하 여 **SA** SQL Server 설치를 사용 하는 동안 만든 계정. |
   | **암호 (SQL 로그인)** | 지정된 사용자의 암호를 입력합니다. | 
   | **암호를 저장 하 시겠습니까?** | 형식 **예** 암호를 저장 합니다. 그렇지 않으면 입력 **아니요** 연결 프로필을 사용할 때마다 암호를 입력 합니다. |
   | **[선택 사항] 이 프로필의 이름을 입력 합니다.** | 연결 프로필 이름입니다. 예를 들어 프로필 이름이 있습니다 **localhost 프로필**합니다. 

   > [!Tip] 
   > 수 만들고 사용자 설정 파일 (settings.json)의 연결 프로필을 편집 합니다. 선택 하 여 설정 파일을 열고 **기본 설정** 차례로 **사용자 설정** VS Code 메뉴에서. 자세한 내용은 참조 하십시오. [연결 프로필을 관리]합니다.

6. 키를 눌러는 **ESC** 키 프로필 생성 되어 연결 된 사용자에 게 알려 주는 정보 메시지를 닫습니다.

   > [!TIP]
   > 연결 실패 시 발생 하는 경우에 오류 메시지에서 문제를 진단 하려면 먼저 시도 **출력** VS Code의 패널 (선택 **출력** 에 **보기** 메뉴). 그런 다음 [connection troubleshooting recommendations](연결 문제 해결 권장 사항)를 검토합니다.

7. 상태 표시줄에 대 한 연결을 확인 합니다.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png" alt="Connection status" style="width: 500px;" />

## <a name="create-a-database"></a>데이터베이스 만들기

1. 편집기에서 입력 **sql** 를 편집할 수 있는 코드 조각 목록을 표시 합니다. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png" alt="SQL snippets" style="width: 500px;" />

2. 선택 **sqlCreateDatabase**합니다.

3. 코드 조각에서 입력 **TutorialDB** 데이터베이스 이름입니다.

   ```sql
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
   
4. 키를 눌러 **CTRL + SHIFT + E** TRANSACT-SQL 명령을 실행 합니다. 쿼리 창에서 결과 확인 합니다.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-create-database-messages.png" alt="create database messages" style="width: 500px;" />

   > [!TIP]
   > Mssql 확장 명령에 대 한 바로 가기 키 바인딩을 사용자 지정할 수 있습니다. 참조 [바로 가기를 사용자 지정]합니다.

## <a name="create-a-table"></a>테이블 만들기

1. 편집기 창의 내용을 제거 합니다.

2. 키를 눌러 **F1** 명령 팔레트를 표시 합니다.

3. 형식 **sql** SQL 명령 또는 형식을 표시 하려면 명령 팔레트에서 **sqluse** 에 대 한 **MS SQL:Use 데이터베이스** 명령입니다.

4. 클릭 **MS SQL:Use 데이터베이스**, 선택는 **TutorialDB** 데이터베이스입니다. 이 이전 섹션에서 만든 새 데이터베이스에는 컨텍스트를 변경 합니다.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-use-database.png" alt="use database" style="width: 500px;" />

3. 편집기에서 입력 **sql** 코드 조각, 표시 하 고 다음 선택 **sqlCreateTable** 누릅니다 **입력**합니다.

4. 코드 조각에서 입력 **직원** 테이블 이름에 대 한 합니다.

5. 키를 눌러 **탭**, 한 다음 입력 **dbo** 스키마 이름에 대 한 합니다.

   > [!NOTE]
   > 코드 조각을 추가한 후 VS Code 편집기에서 포커스를 변경 하지 않고 테이블 및 스키마 이름을 입력 해야 합니다.

6. 에 대 한 열 이름을 변경 **Column1** 를 **이름** 및 **Column2** 를 **위치**합니다.

   ```sql
   -- Create a new table called 'Employees' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Employees', 'U') IS NOT NULL
   DROP TABLE dbo.Employees
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Employees
   (
      EmployeesId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location   [NVARCHAR](50)  NOT NULL
   );
   GO
   ```

7. 키를 눌러 **CTRL + SHIFT + E** 는 테이블을 만듭니다.

## <a name="insert-and-query"></a>삽입 및 쿼리

1. 4 개의 행을 삽입 하려면 다음 문을 추가 하는 **직원** 테이블입니다. 그런 다음 모든 행을 선택 합니다.

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

   > [!TIP]
   > 입력 하는 동안 T-SQL IntelliSense 지원을 사용 합니다.
   >   <img src="./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png" alt="TSQL IntelliSense" style="width: 500px;" />

2. 키를 눌러 **CTRL + SHIFT + E** 는 명령을 실행 합니다. 두 개의 결과 집합에 표시 되는 **결과** 창. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png" alt="Results" style="width: 300px;" />

## <a name="view-and-save-the-result"></a>보기 및 결과 저장 합니다.

1. 에 **보기** 메뉴 선택 **편집기 전환 그룹 레이아웃** 수직 또는 수평 분할 레이아웃으로 전환 하려면.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-split.png" alt="Vertical split" style="width: 500px;" />

2. 클릭는 **결과** 및 **메시지** 패널 헤더를 축소 및 패널을 확장 합니다.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png" alt="Toggle Messages" style="width: 500px;" />

   > [!TIP]
   > Mssql 확장의 기본 동작을 사용자 지정할 수 있습니다. 참조 [확장 옵션을 사용자 지정]합니다.

2. 확대 하려면 두 번째 결과 표에서 최대화 표 아이콘을 클릭 합니다.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png" alt="Maximize grid" style="width: 500px;" />

   > [!NOTE]
   > 최대화 아이콘 T-SQL 스크립트에 두 개 이상의 결과 표를 표시 합니다.

3. 눈금에서 마우스 오른쪽 단추를 모눈 상황에 맞는 메뉴를 엽니다. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png" alt="Context menu" style="width: 500px;" />

4. 선택 **모두 선택**합니다.

5. 모눈 상황에 맞는 메뉴를 열고 선택 **JSON으로 저장** .json 파일에 결과 저장 하도록 합니다.

6. JSON 파일에 대 한 파일 이름을 지정 합니다. 이 자습서에 대 한 입력 **employees.json**합니다.

7. JSON 파일 저장 되 고 VS Code에서 열을 확인 합니다.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png" alt="Save as Json" style="width: 500px;" />

## <a name="next-steps"></a>다음 단계

실제 시나리오에서 저장 하 고 실행 해야 하는 스크립트를 만들 수 있습니다 (관리용 또는 더 큰 개발 프로젝트의 일부로) 이상. 이 예에서 사용 하 여 스크립트를 저장할 수 있습니다는 **.sql** 확장 합니다.

T-SQL을 처음 접하는 경우 참조 [자습서: TRANSACT-SQL 문 쓰기] 및 [TRANSACT-SQL 참조 (데이터베이스 엔진)]합니다.

사용 하 여 또는 mssql 확장에 기여에 대 한 자세한 내용은 참조 하십시오. [mssql 확장 프로젝트 wiki]합니다.

VS Code 사용에 대 한 자세한 내용은 참조는 [Visual Studio Code 설명서](https://code.visualstudio.com/docs)합니다.

[* * mssql * * VS Code에 대 한 확장 합니다.]:https://aka.ms/mssql-marketplace
[다운로드 하 고 VS Code 설치]:https://code.visualstudio.com/Download
[.NET 지침 핵심]:https://www.microsoft.com/net/core
[연결 프로필을 관리]:https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles
[connection troubleshooting recommendations]:./sql-server-linux-troubleshooting-guide.md#connection
[바로 가기를 사용자 지정]:https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts
[자습서: TRANSACT-SQL 문 쓰기]:https://msdn.microsoft.com/library/ms365303.aspx
[TRANSACT-SQL 참조 (데이터베이스 엔진)]:https://msdn.microsoft.com/library/bb510741.aspx
[Visual Studio Code documentation]:https://code.visualstudio.com/docs
[Windows 10 유니버설 C 런타임]:https://github.com/Microsoft/vscode-mssql/wiki/windows10-universal-c-runtime-requirement
[확장 옵션을 사용자 지정]: https://github.com/Microsoft/vscode-mssql/wiki/customize-options
[mssql 확장 프로젝트 wiki]: https://github.com/Microsoft/vscode-mssql/wiki

