---
title: "Transact-SQL(SSMS)을 사용하여 SSIS 패키지 실행 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: quick-start
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b5518a521154b37dc473eb700c3ff50d1a70d60
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="run-an-ssis-package-from-ssms-with-transact-sql"></a>Transact-SQL(SSMS)을 사용하여 SSIS 패키지 실행
이 빠른 시작에서는 SSMS(SQL Server Management Studio)를 사용하여 SSIS 카탈로그 데이터베이스에 연결한 다음, Transact-SQL 문을 사용하여 SSIS 카탈로그에 저장된 SSIS 패키지를 실행하는 방법을 보여 줍니다.

SQL Server Management Studio는 SQL Server에서 SQL Database까지 모든 SQL 인프라를 관리하기 위한 통합 환경입니다. SSMS에 대한 자세한 내용은 [SSMS(SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

시작하기 전에 최신 버전의 SSMS(SQL Server Management Studio)가 설치되어 있는지 확인합니다. SSMS를 다운로드하려면 [SSMS(SQL Server Management Studio) 다운로드](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 참조하세요.

## <a name="connect-to-the-ssisdb-database"></a>SSISDB 데이터베이스에 연결

SQL Server Management Studio를 사용하여 Azure SQL Database 서버의 SSIS 카탈로그에 대한 연결을 설정합니다. 

> [!NOTE]
> Azure SQL Database 서버는 1433 포트에서 수신 대기합니다. 회사 방화벽 내에서 Azure SQL Database 서버에 성공적으로 연결하려면 이 포트가 회사 방화벽에서 열려 있어야 합니다.

1. SQL Server Management Studio를 엽니다.

2. **서버에 연결** 대화 상자에 다음 정보를 입력합니다.

   | 설정       | 제안된 값 | 추가 정보 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 유형** | 데이터베이스 엔진 | 이 값은 필수 사항입니다. |
   | **서버 이름** | 정규화된 서버 이름 | Azure SQL Database 서버에 연결하는 경우 이름은 `<server_name>.database.windows.net` 형식입니다. |
   | **인증** | SQL Server 인증(SQL Server Authentication) | 이 빠른 시작에서는 SQL 인증을 사용합니다. |
   | **로그인** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호** | 서버 관리자 계정의 암호 | 서버를 만들 때 지정한 암호입니다. |

3.  **연결**을 클릭합니다. SSMS에서 개체 탐색기 창이 열립니다.

4. 개체 탐색기에서 **Integration Services 카탈로그**, **SSISDB**를 차례로 펼쳐 SSIS 카탈로그 데이터베이스의 개체를 봅니다.

## <a name="run-a-package"></a>패키지 실행
다음 Transact-SQL 코드를 실행하여 SSIS 패키지를 실행합니다.

1.  SSMS에서 새 쿼리 창을 열고 다음 코드를 붙여넣습니다. (이 코드는 SSMS **패키지 실행** 대화 상자의 **스크립트** 옵션에 의해 생성된 코드입니다.)

2.  시스템에 대한 `catalog.create_execution` 저장 프로시저의 매개 변수 값을 업데이트합니다.

3.  SSISDB가 현재 데이터베이스인지 확인합니다.

4.  스크립트를 실행합니다.

5. [개체 탐색기]에서 필요한 경우 **SSISDB**의 내용을 새로 고치고 배포한 프로젝트를 확인합니다.

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
    - [Transact-SQL(VS Code)을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 
