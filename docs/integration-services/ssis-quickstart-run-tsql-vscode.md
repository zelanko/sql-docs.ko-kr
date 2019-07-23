---
title: Transact-SQL(VS Code)을 사용하여 SSIS 패키지 실행 | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 539df425bcdc5cb7dd60fe7d73574cfcec08a2c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068768"
---
# <a name="run-an-ssis-package-from-visual-studio-code-with-transact-sql"></a>Transact-SQL을 사용하여 Visual Studio Code에서 SSIS 패키지 실행

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


이 빠른 시작에서는 Visual Studio Code를 사용하여 SSIS 카탈로그 데이터베이스에 연결한 다음, Transact-SQL 문을 사용하여 SSIS 카탈로그에 저장된 SSIS 패키지를 실행하는 방법을 보여줍니다.

Visual Studio Code는 Microsoft SQL Server, Azure SQL Database 또는 Azure SQL Data Warehouse에 연결하기 위한 `mssql` 확장을 포함하여 확장을 지원하는 Windows, macOS 및 Linux용 코드 편집기입니다. VS Code에 대한 자세한 내용은 [Visual Studio Code](https://code.visualstudio.com/)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

시작하기 전에 최신 버전의 Visual Studio Code를 설치하고 `mssql` 확장을 로드했는지 확인합니다. 이러한 도구를 다운로드하려면 다음 페이지를 참조하세요.
-   [Visual Studio 코드 다운로드](https://code.visualstudio.com/Download)
-   [mssql 확장](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="supported-platforms"></a>지원 플랫폼

이 빠른 시작의 정보를 사용하여 다음과 같은 플랫폼에서 SSIS 패키지를 실행할 수 있습니다.

-   Windows의 SQL Server

-   Azure SQL Database Azure에서 패키지를 배포하고 실행하는 방법에 대한 자세한 내용은 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)를 참조하세요.

이 빠른 시작의 정보를 사용하여 Linux에서 SSIS 패키지를 실행할 수 없습니다. Linux에서 패키지를 실행하는 방법에 대한 자세한 내용은 [Linux에서 SSIS를 사용하여 데이터 추출, 변환 및 로드](../linux/sql-server-linux-migrate-ssis.md)를 참조하세요.

## <a name="set-language-mode-to-sql-in-vs-code"></a>VS Code에서 언어 모드를 SQL로 설정

`mssql` 명령과 T-SQL IntelliSense를 사용하도록 설정하려면 Visual Studio Code에서 언어 모드를 **SQL**로 설정합니다.

1. Visual Studio Code를 연 다음 새 창을 엽니다. 

2. 상태 표시줄의 오른쪽 아래 모서리에 있는 **일반 텍스트**를 클릭합니다.

3. 열리는 **언어 모드 선택** 드롭다운 메뉴에서 **SQL**을 선택하거나 입력한 다음 **Enter** 키를 눌러 언어 모드를 SQL로 설정합니다. 

## <a name="for-azure-sql-database-get-the-connection-info"></a>Azure SQL Database에서 연결 정보 가져오기

Azure SQL Database에서 패키지를 실행하려면 SSISDB(SSIS 카탈로그 데이터베이스)에 연결해야 하는 연결 정보를 가져옵니다. 다음 절차에는 정규화된 서버 이름과 로그인 정보가 필요합니다.

1. [Azure 포털](https://portal.azure.com/)에 로그인합니다.
2. 왼쪽 메뉴에서 **SQL Databases**를 선택한 다음, **SQL 데이터베이스** 페이지에서 SSISDB 데이터베이스를 선택합니다. 
3. 데이터베이스의 **개요** 페이지에서 정규화된 서버 이름을 검토합니다. **복사하려면 클릭** 옵션을 표시하려면 마우스로 서버 이름 위를 가리킵니다. 
4. Azure SQL Database 서버 로그인 정보를 잊은 경우, SQL Database 서버 페이지로 이동하여 서버 관리자 이름을 확인합니다. 필요한 경우 암호를 다시 설정할 수 있습니다.

## <a name="connect-to-the-ssis-catalog-database"></a>SSIS 카탈로그 데이터베이스에 연결

Visual Studio Code를 사용하여 SSIS 카탈로그에 대한 연결을 설정합니다.

> [!IMPORTANT]
> 계속하기 전에 서버, 데이터베이스 및 로그인 정보가 준비되어 있는지 확인합니다. 연결 프로필 정보를 입력하기 시작한 후에 Visual Studio Code에서 포커스를 변경하면 연결 프로필 만들기를 다시 시작해야 합니다.

1. VS Code에서 **Ctrl+Shift+P**(또는 **F1** 키)를 눌러 명령 팔레트를 엽니다.

2. **sqlcon**을 입력하고 **Enter** 키를 누릅니다.

3. **Enter** 키를 눌러 **연결 프로필 만들기**를 선택합니다. 이 단계는 SQL Server 인스턴스에 대한 연결 프로필을 만듭니다.

4. 프롬프트에 따라 새 연결 프로필에 대한 연결 속성을 지정합니다. 각 값을 지정한 후 **Enter** 키를 눌러 계속합니다. 

   | 설정       | 제안된 값 | 추가 정보 |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 이름** | 정규화된 서버 이름 | Azure SQL Database 서버에 연결하는 경우 이름은 `<server_name>.database.windows.net` 형식입니다. |
   | **데이터베이스 이름** | **SSISDB** | 연결할 데이터베이스의 이름입니다. |
   | **인증** | SQL 로그인 | SQL Server 인증을 사용하여 SQL Server나 Azure SQL Database에 연결할 수 있습니다. Azure SQL Database 서버에 연결하는 경우 Windows 인증을 사용할 수 없습니다. |
   | **User name** | 서버 관리자 계정 | 이 계정은 서버를 만들 때 지정한 계정입니다. |
   | **암호(SQL 로그인)** | 서버 관리자 계정의 암호 | 이 암호는 서버를 만들 때 지정한 암호입니다. |
   | **암호를 저장하시겠습니까?** | Yes 또는 No | 암호를 매번 입력하지 않으려면 'Yes'를 선택합니다. |
   | **이 프로필의 이름을 입력합니다.** | 프로필 이름(예: **mySSISServer**) | 저장된 프로필 이름은 후속 로그인에서 연결 속도를 높입니다. | 

5. **Esc** 키를 눌러 프로필이 만들어지고 연결되었음을 알리는 정보 메시지를 닫습니다.

6. 상태 표시줄에서 연결을 확인합니다.

## <a name="run-the-t-sql-code"></a>T-SQL 코드 실행
다음 Transact-SQL 코드를 실행하여 SSIS 패키지를 실행합니다.

1. **편집기** 창에서 빈 쿼리 창에 다음 쿼리를 입력합니다. (이 코드는 SSMS **패키지 실행** 대화 상자의 **스크립트** 옵션에 의해 생성된 코드입니다.)

2. 시스템에 대한 `catalog.create_execution` 저장 프로시저의 매개 변수 값을 업데이트합니다.

3. **Ctrl+Shift+E**를 눌러 코드를 실행하고 패키지를 실행합니다.

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
- 패키지를 실행하는 다른 방법을 고려합니다.
    - [SSMS를 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL(SSMS)을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-tsql-ssms.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 
