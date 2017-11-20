---
title: "Transact SQL (SSMS)를 SSIS 패키지 실행 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: 1c656661f645ac9f5d1659800893290819525f39
ms.contentlocale: ko-kr
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-ssms-with-transact-sql"></a>TRANSACT-SQL로 SSMS에서 SSIS 패키지를 실행 합니다.
이 빠른 시작에는 SQL Server Management Studio (SSMS)를 사용 하 여 SSIS 카탈로그 데이터베이스에 연결한 다음 TRANSACT-SQL 문을 사용 하 여 SSIS 카탈로그에 저장 하는 SSIS 패키지를 실행 하는 방법을 보여 줍니다.

SQL Server Management Studio는 SQL Server를 SQL 데이터베이스에서 모든 SQL 인프라를 관리 하기 위한 통합된 환경입니다. SSMS에 대 한 자세한 내용은 참조 하십시오. [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)합니다.

## <a name="prerequisites"></a>필수 구성 요소

시작 하기 전에 SQL Server Management Studio (SSMS)의 최신 버전 지정 했는지 확인 합니다. SSMS를 다운로드 하려면 [다운로드 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.

## <a name="connect-to-the-ssisdb-database"></a>SSISDB 데이터베이스에 연결

SQL Server Management Studio를 사용 하 여 Azure SQL 데이터베이스 서버의 SSIS 카탈로그에 대 한 연결을 설정 합니다. 

> [!NOTE]
> Azure SQL 데이터베이스 서버는 포트 1433에서 수신합니다. 회사 방화벽 내에서 Azure SQL 데이터베이스 서버에 연결 하려는 경우에이 포트에 성공적으로 연결 하면 회사 방화벽에서 열려 있어야 합니다.

1. SQL Server Management Studio를 엽니다.

2. 에 **서버에 연결** 대화 상자에서 다음 정보를 입력 합니다.

   | 설정       | 제안 된 값 | 추가 정보 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 유형** | 데이터베이스 엔진 | 이 값은 필수 사항입니다. |
   | **서버 이름** | 정규화 된 서버 이름 | 이 형식에 이름이 Azure SQL 데이터베이스 서버에 연결 하는 경우: `<server_name>.database.windows.net`합니다. |
   | **인증** | SQL Server 인증(SQL Server Authentication) | 이 퀵 스타트의 SQL 인증을 사용 합니다. |
   | **로그인** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호** | 서버 관리자 계정의 암호 | 이 서버를 만들 때 지정한 암호입니다. |

3.  **연결**을 클릭합니다. SSMS에서 개체 탐색기 창이 열립니다.

4. 개체 탐색기에서 확장 **Integration Services 카탈로그** 펼친 다음 **SSISDB** SSIS 카탈로그 데이터베이스에서 개체를 볼 수 있습니다.

## <a name="run-a-package"></a>패키지 실행
SSIS 패키지를 실행 하려면 다음 TRANSACT-SQL 코드를 실행 합니다.

1.  SSMS에서 새 쿼리 창을 열고 다음 코드를 붙여 넣습니다. (이 코드는에 의해 생성 된 코드는 **스크립트** 옵션에 **패키지 실행** SSMS의 대화 상자.)

2.  매개 변수 값을 업데이트는 `catalog.create_execution` 시스템에 대 한 프로시저를 저장 합니다.

3.  SSISDB가 현재 데이터베이스에 있는지 확인 합니다.

4.  스크립트를 실행합니다.

5. 개체 탐색기에서의 내용을 새로 고칩니다 **SSISDB** 필요한 경우 배포 된 프로젝트를 확인 합니다.

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
    - [Transact-sql (VS Code)는 SSIS 패키지를 실행 합니다.](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell에서 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#과 함께 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 

