---
title: "SSMS로 SSIS 패키지 실행 | Microsoft Docs"
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
ms.openlocfilehash: bbc17907311785ef98560493cb453b7b9b6d1556
ms.contentlocale: ko-kr
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)를 SSIS 패키지를 실행 합니다.
이 빠른 시작에는 SQL Server Management Studio (SSMS)를 사용 하 여 SSIS 카탈로그 데이터베이스에 연결 하 고 다음 SSMS의 개체 탐색기에서 SSIS 카탈로그에 저장 된 SSIS 패키지를 실행 하는 방법을 보여 줍니다.

SQL Server Management Studio는 SQL Server를 SQL 데이터베이스에서 모든 SQL 인프라를 관리 하기 위한 통합된 환경입니다. SSMS에 대 한 자세한 내용은 참조 하십시오. [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)합니다.

## <a name="prerequisites"></a>필수 구성 요소

시작 하기 전에 SQL Server Management Studio (SSMS)의 최신 버전 지정 했는지 확인 합니다. SSMS를 다운로드 하려면 [다운로드 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.

## <a name="connect-to-the-ssisdb-database"></a>SSISDB 데이터베이스에 연결

SQL Server Management Studio를 사용 하 여 SSIS 카탈로그에 대 한 연결을 설정 합니다. 

> [!NOTE]
> Azure SQL 데이터베이스 서버는 포트 1433에서 수신합니다. 회사 방화벽 내에서 Azure SQL 데이터베이스 서버에 연결 하려는 경우에이 포트에 성공적으로 연결 하면 회사 방화벽에서 열려 있어야 합니다.

1. SQL Server Management Studio를 엽니다.

2. 에 **서버에 연결** 대화 상자에서 다음 정보를 입력 합니다.

   | 설정       | 제안 된 값 | 추가 정보 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 유형** | 데이터베이스 엔진 | 이 값은 필수 사항입니다. |
   | **서버 이름** | 정규화 된 서버 이름 | 이 형식에 이름이 Azure SQL 데이터베이스 서버에 연결 하는 경우: `<server_name>.database.windows.net`합니다. |
   | **인증** | SQL Server 인증(SQL Server Authentication) | 이 퀵 스타트의 SQL 인증을 사용 합니다. |
   | **로그인** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호** | 서버 관리자 계정의 암호 | 이 서버를 만들 때 지정한 암호입니다. |

3. **연결**을 클릭합니다. SSMS에서 개체 탐색기 창이 열립니다. 

4. 개체 탐색기에서 확장 **Integration Services 카탈로그** 펼친 다음 **SSISDB** SSIS 카탈로그 데이터베이스에서 개체를 볼 수 있습니다.

## <a name="run-a-package"></a>패키지 실행

1. 개체 탐색기에서 패키지를 실행 하려면를 선택 합니다.

2. 마우스 오른쪽 단추로 클릭 하 고 선택 **Execute**합니다. **패키지 실행** 대화 상자가 열립니다.

3.  설정을 사용 하 여 패키지 실행을 구성 된 **매개 변수**, **연결 관리자**, 및 **고급** 패키지 실행 대화 상자에서 탭 합니다.

4.  패키지를 실행 하려면 확인을 클릭 합니다.

## <a name="next-steps"></a>다음 단계
- 다른 방법으로 패키지를 실행 하는 것이 좋습니다.
    - [Transact SQL (SSMS)를 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-sql (VS Code)는 SSIS 패키지를 실행 합니다.](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell에서 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#과 함께 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 

