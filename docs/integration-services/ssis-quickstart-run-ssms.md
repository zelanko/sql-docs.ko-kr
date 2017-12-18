---
title: "SSMS를 사용하여 SSIS 패키지 실행 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7b35bade8769e3de11f60046375f082146da579d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="run-an-ssis-package-with-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)를 사용하여 SSIS 패키지 실행
이 빠른 시작에서는 SSMS(SQL Server Management Studio)를 사용하여 SSIS 카탈로그 데이터베이스에 연결한 다음, SSIS의 개체 탐색기에서 SSIS 카탈로그에 저장된 SSIS 패키지를 실행하는 방법을 보여 줍니다.

SQL Server Management Studio는 SQL Server에서 SQL Database까지 모든 SQL 인프라를 관리하기 위한 통합 환경입니다. SSMS에 대한 자세한 내용은 [SSMS(SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md)를 참조하세요.

## <a name="prerequisites"></a>필수 구성 요소

시작하기 전에 최신 버전의 SSMS(SQL Server Management Studio)가 설치되어 있는지 확인합니다. SSMS를 다운로드하려면 [SSMS(SQL Server Management Studio) 다운로드](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 참조하세요.

## <a name="connect-to-the-ssisdb-database"></a>SSISDB 데이터베이스에 연결

SQL Server Management Studio를 사용하여 SSIS 카탈로그에 대한 연결을 설정합니다. 

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

3. **연결**을 클릭합니다. SSMS에서 개체 탐색기 창이 열립니다. 

4. 개체 탐색기에서 **Integration Services 카탈로그**, **SSISDB**를 차례로 펼쳐 SSIS 카탈로그 데이터베이스의 개체를 봅니다.

## <a name="run-a-package"></a>패키지 실행

1. 개체 탐색기에서 실행하려는 패키지를 선택합니다.

2. 마우스 오른쪽 단추로 클릭하고 **실행**을 선택합니다. **패키지 실행** 대화 상자를 엽니다.

3.  패키지 실행 대화 상자의 **매개 변수**, **연결 관리자** 및 **고급** 탭의 설정을 사용하여 패키지 실행을 구성합니다.

4.  확인을 클릭하여 패키지를 실행합니다.

## <a name="next-steps"></a>다음 단계
- 패키지를 실행하는 다른 방법을 고려합니다.
    - [Transact-SQL(SSMS)을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL(VS Code)을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 
