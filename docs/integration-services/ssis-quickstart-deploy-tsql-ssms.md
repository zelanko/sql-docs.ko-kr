---
description: Transact-SQL을 사용하여 SSMS에서 SSIS 프로젝트 배포
title: Transact-SQL(SSMS)을 사용하여 SSIS 프로젝트 배포 | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a741612f0afd305edaf4cc289f1841eb9b353d8a
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195215"
---
# <a name="deploy-an-ssis-project-from-ssms-with-transact-sql"></a>Transact-SQL을 사용하여 SSMS에서 SSIS 프로젝트 배포

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



이 빠른 시작에서는 SSMS(SQL Server Management Studio)를 사용하여 SSIS 카탈로그 데이터베이스에 연결한 다음, Transact-SQL 문을 사용하여 SSIS 프로젝트를 SSIS 카탈로그에 배포하는 방법을 보여 줍니다. 

SQL Server Management Studio는 SQL Server에서 SQL Database까지 모든 SQL 인프라를 관리하기 위한 통합 환경입니다. SSMS에 대한 자세한 내용은 [SSMS(SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

시작하기 전에 최신 버전의 SQL Server Management Studio가 설치되어 있는지 확인합니다. SSMS를 다운로드하려면 [SSMS(SQL Server Management Studio) 다운로드](../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요.

## <a name="supported-platforms"></a>지원되는 플랫폼

이 빠른 시작의 정보를 사용하여 다음과 같은 플랫폼에 SSIS 프로젝트를 배포할 수 있습니다.

-   Windows의 SQL Server

이 빠른 시작의 정보를 사용하여 Azure SQL Database에 SSIS 패키지를 배포할 수 없습니다. `catalog.deploy_project` 저장 프로시저에는 로컬(온-프레미스) 파일 시스템의 `.ispac` 파일에 대한 경로가 필요합니다. Azure에서 패키지를 배포하고 실행하는 방법에 대한 자세한 내용은 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)를 참조하세요.

이 빠른 시작의 정보를 사용하여 SQL Server on Linux에 SSIS 패키지를 배포할 수 없습니다. Linux에서 패키지를 실행하는 방법에 대한 자세한 내용은 [Linux에서 SSIS를 사용하여 데이터 추출, 변환 및 로드](../linux/sql-server-linux-migrate-ssis.md)를 참조하세요.

## <a name="supported-authentication-method"></a>지원되는 인증 방법

[배포를 위한 인증 방법](ssis-quickstart-deploy-ssms.md#authentication-methods-for-deployment)을 참조하세요.

## <a name="connect-to-the-ssis-catalog-database"></a>SSIS 카탈로그 데이터베이스에 연결

SQL Server Management Studio를 사용하여 SSIS 카탈로그에 대한 연결을 설정합니다. 

1. SQL Server Management Studio를 엽니다.

2. **서버에 연결** 대화 상자에 다음 정보를 입력합니다.

   | 설정       | 제안 값 | 추가 정보 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 유형** | 데이터베이스 엔진 | 이 값은 필수입니다. |
   | **서버 이름** | 정규화된 서버 이름 |  |
   | **인증** | SQL Server 인증 | |
   | **로그인** | 서버 관리자 계정 | 이 계정은 서버를 만들 때 지정한 계정입니다. |
   | **암호** | 서버 관리자 계정의 암호 | 이 암호는 서버를 만들 때 지정한 암호입니다. |

3. **연결**을 클릭합니다. SSMS에서 개체 탐색기 창이 열립니다. 

4. 개체 탐색기에서 **Integration Services 카탈로그**, **SSISDB**를 차례로 펼쳐 SSIS 카탈로그 데이터베이스의 개체를 봅니다.


## <a name="run-the-t-sql-code"></a>T-SQL 코드 실행
다음 Transact-SQL 코드를 실행하여 SSIS 프로젝트를 배포합니다.

1.  SSMS에서 새 쿼리 창을 열고 다음 코드를 붙여넣습니다.

2.  시스템에 대한 `catalog.deploy_project` 저장 프로시저의 매개 변수 값을 업데이트합니다.

3.  **SSISDB**가 현재 데이터베이스인지 확인합니다.

4.  스크립트를 실행합니다.

5. [개체 탐색기]에서 필요한 경우 **SSISDB**의 내용을 새로 고치고 배포한 프로젝트를 확인합니다.

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
- 패키지를 배포하는 다른 방법을 고려합니다.
    - [SSMS를 사용하여 SSIS 패키지 배포](./ssis-quickstart-deploy-ssms.md)
    - [Transact-SQL(VS 코드)을 사용하여 SSIS 패키지 배포](ssis-quickstart-deploy-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 배포](./ssis-quickstart-deploy-cmdline.md)
    - [PowerShell을 사용하여 SSIS 패키지 배포](ssis-quickstart-deploy-powershell.md)
    - [C#을 사용하여 SSIS 패키지 배포](./ssis-quickstart-deploy-dotnet.md) 
- 배포된 패키지를 실행합니다. 패키지를 실행하려면 여러 도구와 언어 중에서 선택할 수 있습니다. 자세한 내용은 다음 문서를 참조하세요.
    - [SSMS를 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL(SSMS)을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL(VS Code)을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md)