---
title: "배포, 실행 및 Azure에서 SSIS 패키지를 모니터링 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: c2dbdf818ef15dc97020dd7b35f88cfa080537d3
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---
# <a name="deploy-run-and-monitor-an-ssis-package-on-azure"></a>배포, 실행 및 Azure에서 SSIS 패키지를 모니터링 합니다.
이 자습서에서는 Azure SQL 데이터베이스에서 SSISDB 카탈로그 데이터베이스에 SQL Server Integration Services 프로젝트를 배포, Azure SSIS 통합 런타임에서 패키지를 실행 하 고, 실행 중인 패키지 모니터링 하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>필수 구성 요소

시작 하기 전에 17.2 SQL Server Management Studio의 이후 버전 지정 했는지 확인 합니다. 최신 버전의 SSMS 다운로드 하려면 [다운로드 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.

또한 SSISDB 데이터베이스를 설정 하 고 Azure SSIS 통합 런타임에서 사용자를 프로 비전 했는지 확인 합니다. Azure에서 SSIS 프로 비전 하는 방법에 대 한 정보를 참조 하십시오. [Azure에 SQL Server Integration Services (SSIS) 패키지 리프트 하 고 shift](https://docs.microsoft.com/en-us/azure/tutorial-deploy-ssis-packages-azure)합니다.

## <a name="connect-to-the-ssisdb-database"></a>SSISDB 데이터베이스에 연결

SQL Server Management Studio를 사용 하 여 Azure SQL 데이터베이스 서버의 SSIS 카탈로그에 연결할 수 있습니다. 자세한 내용은 참조 하십시오. [Azure에서 SSISDB 카탈로그 데이터베이스에 연결](ssis-azure-connect-to-catalog-database.md)합니다.

> [!IMPORTANT]
> Azure SQL 데이터베이스 서버는 포트 1433에서 수신합니다. 회사 방화벽 내에서 Azure SQL 데이터베이스 서버에 연결 하려는 경우에이 포트에 성공적으로 연결 하면 회사 방화벽에서 열려 있어야 합니다.

1. SQL Server Management Studio를 엽니다.

2. **서버에 연결**합니다. 에 **서버에 연결** 대화 상자에서 다음 정보를 입력 합니다.

   | 설정       | 제안 된 값 | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 유형** | 데이터베이스 엔진 | 이 값은 필수 사항입니다. |
   | **서버 이름** | 정규화 된 서버 이름 | 이 형식 이름 이어야 합니다: **mysqldbserver.database.windows.net**합니다. 서버 이름이 필요한 경우 참조 [Azure에서 SSISDB 카탈로그 데이터베이스에 연결](ssis-azure-connect-to-catalog-database.md)합니다. |
   | **인증** | SQL Server 인증(SQL Server Authentication) | 이 퀵 스타트의 SQL 인증을 사용 합니다. |
   | **로그인** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호** | 서버 관리자 계정의 암호 | 이 서버를 만들 때 지정한 암호입니다. |

3. **SSISDB 데이터베이스에 연결**합니다. 선택 **옵션** 확장 하 고 **서버에 연결** 대화 상자. 확장 된 **서버에 연결** 대화 상자는 **연결 속성** 탭 합니다. 에 **연결할 데이터베이스** 필드를 선택 하거나 입력 `SSISDB`합니다.

4. 그런 다음 선택 **연결**합니다. SSMS에서 개체 탐색기 창이 열립니다. 

5. 개체 탐색기에서 확장 **Integration Services 카탈로그** 펼친 다음 **SSISDB** SSIS 카탈로그 데이터베이스에서 개체를 볼 수 있습니다.

## <a name="deploy-a-project"></a>프로젝트 배포

### <a name="start-the-integration-services-deployment-wizard"></a>Integration Services 배포 마법사를 시작 합니다.
1. SSMS의 개체 탐색기에서와 **Integration Services 카탈로그** 노드 및 **SSISDB** 노드가 확장 프로젝트 폴더를 확장 합니다.

2.  선택 된 **프로젝트** 노드.

3.  마우스 오른쪽 단추로 클릭는 **프로젝트** 노드 선택한 **배포 프로젝트**합니다. Integration Services 배포 마법사가 열립니다. 파일 시스템 또는 SSIS 카탈로그 데이터베이스에서 프로젝트를 배포할 수 있습니다.

### <a name="deploy-a-project-with-the-deployment-wizard"></a>배포 마법사를 사용 하 여 프로젝트를 배포 합니다.
1. 에 **소개** 페이지는 배포 마법사의 소개를 검토 합니다. 선택 **다음** 열려는 **원본 선택** 페이지.

2. 에 **원본 선택** 페이지에서 기존 SSIS 프로젝트 배포를 선택 합니다.
    -   만든 프로젝트 배포 파일을 배포하려면 **프로젝트 배포 파일** 을 선택하고 .ispac 파일에 대한 경로를 입력합니다.
    -   SSIS 카탈로그에 프로젝트를 배포 하려면 선택 **Integration Services 카탈로그**를 선택한 다음 카탈로그에 프로젝트를 서버 이름 및 경로 입력 합니다.
    -   선택 **다음** 볼 수는 **대상 선택** 페이지.
  
3.  에 **대상 선택** 페이지, 프로젝트에 대 한 대상을 선택 합니다.
    -   형식에 정규화 된 서버 이름을 입력 `<server_name>.database.windows.net`합니다.
    -   다음 선택 **찾아보기** SSISDB에 대상 폴더를 선택 합니다.
    -   선택 **다음** 열려는 **검토** 페이지.  
  
4.  에 **검토** 페이지에서 선택한 설정을 검토 합니다.
    -   선택 하 여 선택 항목을 변경할 수 있습니다 **이전**, 왼쪽 창의 단계 중 하나를 선택 하 여 합니다.
    -   선택 **배포** 배포 프로세스를 시작 합니다.
  
5.  배포 프로세스가 완료 된 후의 **결과** 페이지가 열립니다. 이 페이지는 각 동작의 성공 또는 실패 여부를 표시합니다.
    -   작업에 실패 한 경우 선택 **실패** 에 **결과** 열 오류에 대 한 설명을 표시 합니다.
    -   필요에 따라 선택 **보고서 저장...**  XML 파일로 결과 저장할 수 있습니다.
    -   선택 **닫기** 여 마법사를 종료 합니다.

## <a name="run-a-package"></a>패키지 실행

1. SSMS의 개체 탐색기에서 패키지를 실행 하려면를 선택 합니다.

2. 마우스 오른쪽 단추로 클릭 하 고 선택 **Execute** 열려는 **패키지 실행** 대화 상자.

3.  에 **패키지 실행** 대화 상자에서 설정을 사용 하 여 패키지 실행을 구성을 **매개 변수**, **연결 관리자**, 및 **고급**  탭 합니다.

4.  선택 **확인** 패키지를 실행 합니다.

## <a name="monitor-the-running-package-in-ssms"></a>SSMS에서 실행 중인 패키지 모니터링

현재 실행 중인 배포, 유효성 검사 및 패키지 실행 예: Integration Services 서버에서 Integration Services 작업 상태를 보려면 사용 하 여는 **활성 작업** SSMS의 대화 상자. 열려는 **활성 작업** 대화 상자에서 마우스 오른쪽 단추로 클릭 **SSISDB**를 선택한 후 **활성 작업**합니다.

개체 탐색기, 마우스 오른쪽 단추 클릭 및 선택에서 패키지를 선택할 수도 있습니다 **보고서**, 다음 **표준 보고서**, 다음 **모든 실행**합니다.

SSMS에서 실행 중인 패키지를 모니터링 하는 방법에 대 한 자세한 내용은 참조 하십시오. [모니터 실행 중인 패키지 및 기타 작업](https://docs.microsoft.com/en-us/sql/integration-services/performance/monitor-running-packages-and-other-operations)합니다.

## <a name="monitor-the-azure-ssis-integration-runtime"></a>Azure SSIS 통합 런타임에서 모니터

Azure SSIS 통합 런타임에서는 실행 중인 패키지에 대 한 상태 정보를 가져오려면 다음 PowerShell 명령을 사용 하 여: 각 명령에 대 한 데이터 팩터리의 Azure SSIS IR 및 리소스 그룹의 이름을 입력 합니다.

### <a name="get-metadata-about-the-azure-ssis-integration-runtime"></a>Azure SSIS 통합 런타임에 대 한 메타 데이터 가져오기

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

### <a name="get-the-status-of-the-azure-ssis-integration-runtime"></a>Azure SSIS 통합 런타임 상태를 가져옵니다.

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntimeStatus -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

## <a name="next-steps"></a>다음 단계
- 패키지 실행을 예약 하는 방법에 알아봅니다. 자세한 내용은 참조 하십시오. [일정 SSIS 패키지를 Azure에서 실행](ssis-azure-schedule-packages.md)

