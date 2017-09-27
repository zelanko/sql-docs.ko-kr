---
title: "Transact SQL (SSMS)와 SSIS 프로젝트 배포 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: e97fb20f5b0ee10aa3e5de690676b7e0bb797b4c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-from-ssms-with-transact-sql"></a>TRANSACT-SQL로 SSMS에서 SSIS 프로젝트 배포

이 빠른 시작에는 SQL Server Management Studio (SSMS)를 사용 하 여 SSIS 카탈로그 데이터베이스에 연결한 다음 TRANSACT-SQL 문을 사용 하 여 SSIS 카탈로그에 SSIS 프로젝트를 배포 하는 방법을 보여 줍니다. 

> [!NOTE]
> SSMS로 Azure SQL 데이터베이스 서버에 연결 하는 경우에이 문서에 설명 된 메서드는 사용할 수 없습니다. `catalog.deploy_project` 프로시저에 대 한 경로 저장된 프로시저는 `.ispac` (온-프레미스) 로컬 파일 시스템의 파일입니다.

SQL Server Management Studio는 SQL Server를 SQL 데이터베이스에서 모든 SQL 인프라를 관리 하기 위한 통합된 환경입니다. SSMS에 대 한 자세한 내용은 참조 하십시오. [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)합니다.

## <a name="prerequisites"></a>필수 구성 요소

시작 하기 전에 SQL Server Management Studio의 최신 버전 지정 했는지 확인 합니다. SSMS를 다운로드 하려면 [다운로드 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.

## <a name="connect-to-the-ssis-catalog-database"></a>SSIS 카탈로그 데이터베이스에 연결

SQL Server Management Studio를 사용 하 여 SSIS 카탈로그에 대 한 연결을 설정 합니다. 

> [!NOTE]
> Azure SQL 데이터베이스 서버는 포트 1433에서 수신합니다. 회사 방화벽 내에서 Azure SQL 데이터베이스 서버에 연결 하려는 경우에이 포트에 성공적으로 연결 하면 회사 방화벽에서 열려 있어야 합니다.

1. SQL Server Management Studio를 엽니다.

2. 에 **서버에 연결** 대화 상자에서 다음 정보를 입력 합니다.

   | 설정       | 제안 된 값 | 추가 정보 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 유형** | 데이터베이스 엔진 | 이 값은 필수 사항입니다. |
   | **서버 이름** | 정규화 된 서버 이름 |  |
   | **인증** | SQL Server 인증(SQL Server Authentication) | 이 퀵 스타트의 SQL 인증을 사용 합니다. |
   | **로그인** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호** | 서버 관리자 계정의 암호 | 이 서버를 만들 때 지정한 암호입니다. |

3. **연결**을 클릭합니다. SSMS에서 개체 탐색기 창이 열립니다. 

4. 개체 탐색기에서 확장 **Integration Services 카탈로그** 펼친 다음 **SSISDB** SSIS 카탈로그 데이터베이스에서 개체를 볼 수 있습니다.

## <a name="run-the-t-sql-code"></a>T-SQL 코드를 실행 합니다.
SSIS 프로젝트를 배포 하려면 다음 TRANSACT-SQL 코드를 실행 합니다.

1.  SSMS에서 새 쿼리 창을 열고 다음 코드를 붙여 넣습니다.

2.  매개 변수 값을 업데이트는 `catalog.deploy_project` 시스템에 대 한 프로시저를 저장 합니다.

3.  SSISDB가 현재 데이터베이스에 있는지 확인 합니다.

4.  스크립트를 실행합니다.

5. 개체 탐색기에서의 내용을 새로 고칩니다 **SSISDB** 필요한 경우 배포 된 프로젝트를 확인 합니다.

```sql
DECLARE @ProjectBinary AS varbinary(max)
DECLARE @operation_id AS bigint
SET @ProjectBinary =
    (SELECT * FROM OPENROWSET(BULK '<project_file_path>.ispac', SINGLE_BLOB) AS BinaryData)

EXEC catalog.deploy_project @folder_name = '<target_folder>',
    @project_name = '<project_name',
    @Project_Stream = @ProjectBinary,
    @operation_id = @operation_id out
```

## <a name="next-steps"></a>다음 단계
- 패키지를 배포 하는 다른 방법을 고려 합니다.
    - [SSMS로 SSIS 패키지 배포](./ssis-quickstart-deploy-ssms.md)
    - [TRANSACT-SQL (VS Code)를 SSIS 패키지 배포](ssis-quickstart-deploy-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 배포](./ssis-quickstart-deploy-cmdline.md)
    - [PowerShell과 함께 SSIS 패키지 배포](ssis-quickstart-deploy-powershell.md)
    - [C#과 함께 SSIS 패키지 배포](./ssis-quickstart-deploy-dotnet.md) 
- 배포 된 패키지를 실행 합니다. 패키지를 실행 하려면 여러 가지 도구와 언어를 선택할 수 있습니다. 자세한 내용은 다음 문서를 참조 합니다.
    - [SSMS로는 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-ssms.md)
    - [Transact SQL (SSMS)를 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-sql (VS Code)는 SSIS 패키지를 실행 합니다.](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell에서 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#과 함께 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 

