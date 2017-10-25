---
title: "SSMS에서 SSIS 프로젝트 배포 | Microsoft Docs"
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
ms.openlocfilehash: b9729343ab14563ee6264795d6f098f3c22e91bf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)와 SSIS 프로젝트 배포
이 빠른 시작에는 SQL Server Management Studio (SSMS)를 사용 하 여 SSIS 카탈로그 데이터베이스에 연결 하 고 다음 SSIS 프로젝트를 SSIS 카탈로그에 배포 하려면 Integration Services 배포 마법사를 실행 하는 방법을 보여 줍니다. 

SQL Server Management Studio는 SQL Server를 SQL 데이터베이스에서 모든 SQL 인프라를 관리 하기 위한 통합된 환경입니다. SSMS에 대 한 자세한 내용은 참조 하십시오. [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)합니다.

## <a name="prerequisites"></a>필수 구성 요소

시작 하기 전에 SQL Server Management Studio의 최신 버전 지정 했는지 확인 합니다. SSMS를 다운로드 하려면 [다운로드 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.

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

## <a name="start-the-integration-services-deployment-wizard"></a>Integration Services 배포 마법사를 시작 합니다.
1. 개체 탐색기에서와 **Integration Services 카탈로그** 노드 및 **SSISDB** 프로젝트 폴더를 확장 하 고 확장 합니다.

2.  선택 된 **프로젝트** 노드.

3.  마우스 오른쪽 단추로 클릭는 **프로젝트** 노드 선택한 **배포 프로젝트**합니다. Integration Services 배포 마법사가 열립니다. 파일 시스템 또는 현재 카탈로그에서 프로젝트를 배포할 수 있습니다.

## <a name="deploy-a-project-with-the-wizard"></a>마법사를 사용 하 여 프로젝트를 배포 합니다.
1. 에 **소개** 페이지는 마법사의 소개를 검토 합니다. 클릭 **다음** 열려는 **원본 선택** 페이지.

2. 에 **원본 선택** 페이지에서 기존 SSIS 프로젝트 배포를 선택 합니다.
    -   만든 프로젝트 배포 파일을 배포하려면 **프로젝트 배포 파일** 을 선택하고 .ispac 파일에 대한 경로를 입력합니다.
    -   SSIS 카탈로그에 프로젝트를 배포 하려면 선택 **Integration Services 카탈로그**를 선택한 다음 카탈로그에 프로젝트를 서버 이름 및 경로 입력 합니다.
    **다음** 을 클릭하여 **대상 선택** 페이지를 표시합니다.
  
3.  에 **대상 선택** 페이지, 프로젝트에 대 한 대상을 선택 합니다.
    -   정규화 된 서버 이름을 입력 합니다. 이 형식 이름이 대상 서버에 Azure SQL 데이터베이스 서버 이면: `<server_name>.database.windows.net`합니다.
    -   클릭 **찾아보기** SSISDB에 대상 폴더를 선택 합니다.
    클릭 **다음** 열려는 **검토** 페이지.  
  
4.  에 **검토** 페이지에서 선택한 설정을 검토 합니다.
    -   **이전**을 클릭하거나 왼쪽 창의 단계 중 하나를 클릭하여 선택 항목을 변경할 수 있습니다.
    -   **배포** 를 클릭해 배포 프로세스를 시작합니다.
  
5.  배포 프로세스가 완료 된 후의 **결과** 페이지가 열립니다. 이 페이지는 각 동작의 성공 또는 실패 여부를 표시합니다.
    -   작업에 실패 한 경우 클릭 **실패** 에 **결과** 열 오류에 대 한 설명을 표시 합니다.
    -   필요에 따라 **보고서 저장...**  XML 파일로 결과 저장할 수 있습니다.
    -   클릭 **닫기** 여 마법사를 종료 합니다.

## <a name="next-steps"></a>다음 단계
- 패키지를 배포 하는 다른 방법을 고려 합니다.
    - [Transact SQL (SSMS)를 SSIS 패키지 배포](./ssis-quickstart-deploy-tsql-ssms.md)
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

