---
title: "Transact-sql (VS Code)는 SSIS 패키지를 실행 합니다. | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: a912bf7f7944d4af3d41c5596e67aa77f3214112
ms.contentlocale: ko-kr
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-visual-studio-code-with-transact-sql"></a>Transact SQL을 사용한 Visual Studio Code에서 SSIS 패키지를 실행 합니다.
이 빠른 시작에는 Visual Studio 코드를 사용 하 여 SSIS 카탈로그 데이터베이스에 연결한 다음 TRANSACT-SQL 문을 사용 하 여 SSIS 카탈로그에 저장 하는 SSIS 패키지를 실행 하는 방법을 보여 줍니다.

Visual Studio 코드는 Windows, macOS 등을 지 원하는 확장을 포함 하 여 Linux 용 코드 편집기는 `mssql` 에 Microsoft SQL Server, Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스에 연결 하기 위한 확장 합니다. VS Code에 대 한 자세한 내용은 참조 하십시오. [Visual Studio Cod](https://code.visualstudio.com/)합니다.

## <a name="prerequisites"></a>필수 구성 요소

시작 하기 전에 최신 버전의 Visual Studio 코드를 설치 하 고 로드 했는지 확인는 `mssql` 확장 합니다. 이러한 도구를 다운로드 하려면 다음 페이지를 참조 합니다.
-   [Visual Studio 코드 다운로드](https://code.visualstudio.com/Download)
-   [mssql 확장](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="set-language-mode-to-sql-in-vs-code"></a>VS Code에는 SQL로 언어 모드 설정

사용할 수 있도록 `mssql` 집합이 언어 모드가 설정 된 명령 및 T-SQL IntelliSense **SQL** Visual Studio Code에서 합니다.

1. Visual Studio 코드를 열고 새 창을 엽니다. 

2. 클릭 **일반 텍스트** 상태 표시줄의 오른쪽 아래 모서리에 있습니다.

3. 에 **언어 선택 모드** 열리면 선택 또는 입력 된 드롭 다운 메뉴 **SQL**, 한 다음 키를 누릅니다 **ENTER** to SQL 언어 모드를 설정 하려면. 

## <a name="connect-to-the-ssis-catalog-database"></a>SSIS 카탈로그 데이터베이스에 연결

Visual Studio 코드를 사용 하 여 SSIS 카탈로그에 대 한 연결을 설정 합니다.

> [!IMPORTANT]
> 계속 하기 전에 서버, 데이터베이스 및 로그인 정보를 준비 있는지를 확인 합니다. 연결 프로필 정보를 입력 하기 시작 하면 후 Visual Studio Code에서 포커스 변경 하면 연결 프로필 만들기를 다시 시작 해야 합니다.

1. VS Code에서 눌러 **CTRL + SHIFT + P** (또는 **F1**) 명령 팔레트를 엽니다.

2. 형식 **sqlcon** 누릅니다 **ENTER**합니다.

3. 키를 눌러 **ENTER** 선택할 **연결 프로필 만들기**합니다. 이 단계에서는 SQL Server 인스턴스에 대 한 연결 프로필을 만듭니다.

4. 지시에 따라 새 연결 프로필에 대 한 연결 속성을 지정 합니다. 각 값을 지정한 후 눌러 **ENTER** 를 계속 합니다. 

   | 설정       | 제안 된 값 | 추가 정보 |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 이름** | 정규화 된 서버 이름 | 이 형식에 이름이 Azure SQL 데이터베이스 서버에 연결 하는 경우: `<server_name>.database.windows.net`합니다. |
   | **데이터베이스 이름** | **SSISDB** | 연결할 데이터베이스의 이름입니다. |
   | **인증** | SQL 로그인| 이 퀵 스타트의 SQL 인증을 사용 합니다. |
   | **사용자 이름** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호 (SQL 로그인)** | 서버 관리자 계정의 암호 | 이 서버를 만들 때 지정한 암호입니다. |
   | **암호를 저장 하 시겠습니까?** | Yes 또는 No | 암호를 입력 하려면 예를 선택 합니다. |
   | **이 프로필의 이름을 입력 합니다.** | 같은 프로필 이름 **mySSISServer** | 저장 된 프로필 이름에는 후속 로그인에 연결 속도가 빨라집니다. | 

5. 키를 눌러는 **ESC** 키 프로필 생성 되어 연결 된 사용자에 게 알려 주는 정보 메시지를 닫습니다.

6. 상태 표시줄에 대 한 연결을 확인 합니다.

## <a name="run-the-t-sql-code"></a>T-SQL 코드를 실행 합니다.
SSIS 패키지를 실행 하려면 다음 TRANSACT-SQL 코드를 실행 합니다.

1. 에 **편집기** 창의 빈 쿼리 창에서 다음 쿼리를 입력 합니다. (이 코드는에 의해 생성 된 코드는 **스크립트** 옵션에 **패키지 실행** SSMS의 대화 상자.)

2. 매개 변수 값을 업데이트는 `catalog.create_execution` 시스템에 대 한 프로시저를 저장 합니다.

3. 키를 눌러 **CTRL + SHIFT + E** 는 코드를 실행 하 여 패키지를 실행 합니다.

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx',
    @execution_id=@execution_id OUTPUT,
    @folder_name=N'Deployed Projects',
      @project_name=N'Integration Services Project1',
    @use32bitruntime=False,
      @reference_id=Null
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,
    @object_type=50,
      @parameter_name=N'LOGGING_LEVEL',
      @parameter_value=@var0
EXEC [SSISDB].[catalog].[start_execution] @execution_id
GO
```

## <a name="next-steps"></a>다음 단계
- 다른 방법으로 패키지를 실행 하는 것이 좋습니다.
    - [SSMS로는 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-ssms.md)
    - [Transact SQL (SSMS)를 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-tsql-ssms.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell에서 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#과 함께 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 

