---
title: SSIS(SQL Server Integration Services)를 사용하여 Azure Synapse Analytics로 데이터 로드
description: SSIS(SQL Server Integration Services) 패키지를 만들어 다양한 데이터 원본에서 Azure Synapse Analytics의 전용 SQL 풀로 데이터를 이동하는 방법을 보여 줍니다.
documentationcenter: NA
ms.prod: sql
ms.prod_service: integration-services
ms.technology: integration-services
ms.topic: conceptual
ms.custom: loading
ms.date: 08/09/2018
ms.author: chugu
author: chugugrace
ms.openlocfilehash: 7b582e5722b19db3569aaa0f154f5b78864a2838
ms.sourcegitcommit: 985e2e8e494badeac6d6b652cd35765fd9c12d80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2020
ms.locfileid: "93328499"
---
# <a name="load-data-into-a-dedicated-sql-pool-in-azure-synapse-analytics-with-sql-server-integration-services-ssis"></a>SSIS(SQL Server Integration Services)를 사용하여 Azure Synapse Analytics의 전용 SQL 풀로 데이터 로드

[!INCLUDE[asa](../includes/applies-to-version/asa.md)]

SSIS(SQL Server Integration Services) 패키지를 만들어 Azure Synapse Analytics](/azure/sql-data-warehouse/index)의 전용 SQL 풀로 데이터를 로드합니다. SSIS 데이터 흐름을 통해 전달될 때 필요에 따라 데이터를 재구성, 변형 및 정리할 수 있습니다.

이 아티클에서는 다음을 수행하는 방법을 보여줍니다.

* Visual Studio에서 새 Integration Services 프로젝트를 만듭니다.
* 원본에서 대상으로 데이터를 로드하는 SSIS 패키지를 디자인합니다.
* SSIS 패키지를 실행하여 데이터를 로드합니다.

## <a name="basic-concepts"></a>기본 개념

패키지는 SSIS의 작업 단위입니다. 관련된 패키지는 프로젝트에서 그룹화됩니다. SQL Server Data Tools를 사용하여 Visual Studio에서 프로젝트를 만들고 패키지를 디자인합니다. 디자인 프로세스는 도구 상자에서 디자인 화면으로 구성 요소를 끌어서 놓고, 연결하고, 해당 속성을 설정하는 시각적 프로세스입니다. 패키지를 완료한 후에 실행할 수 있고, 필요에 따라 포괄적인 관리, 모니터링 및 보안을 위해 SQL Server 또는 SQL Database에 배포할 수 있습니다.

SSIS에 대한 자세한 소개는 이 아티클의 범위를 벗어납니다. 자세히 알아보려면 다음 아티클을 참조하세요.

- [SQL Server Integration Services](sql-server-integration-services.md)

- [ETL 패키지를 만드는 방법](ssis-how-to-create-an-etl-package.md)

## <a name="options-for-loading-data-into-azure-synapse-analytics-with-ssis"></a>SSIS를 사용하여 Azure Synapse Analytics로 데이터를 로드하기 위한 옵션
SSIS(SQL Server Integration Services)는 Azure Synapse Analytics에 연결하고 데이터를 로드하기 위한 다양한 옵션을 제공하는 유연한 도구 세트입니다.

1. 최상의 성능을 제공하는 기본 설정 메서드는 데이터를 로드하기 위해 [Azure SQL DW 업로드 태스크](control-flow/azure-sql-dw-upload-task.md)를 사용하는 패키지를 만드는 것입니다. 이 태스크는 원본 및 대상 정보를 모두 캡슐화합니다. 원본 데이터가 구분 기호로 분리된 텍스트 파일에 로컬로 저장된다고 가정합니다.

2. 또는 원본 및 대상이 포함된 데이터 흐름 태스크를 사용하는 패키지를 만들 수 있습니다. 이 방법은 SQL Server 및 Azure Synapse Analytics를 포함하는 다양한 데이터 원본을 지원합니다.

## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 단계별로 실행하려면 다음 항목이 필요합니다.

1. **SSIS(SQL Server Integration Services)** SSIS는 SQL Server의 구성 요소이며 SQL Server의 라이선스 버전 또는 개발자나 평가 버전이 필요합니다. SQL Server의 평가 버전을 가져오려면 [SQL Server 평가](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-rtm)를 참조하세요.
2. **Visual Studio** (선택 사항) Visual Studio Community Edition을 체험하려면 [Visual Studio Community][Visual Studio Community]를 참조하세요. Visual Studio를 설치하지 않으려는 경우 SSDT(SQL Server Data Tools)만을 설치할 수 있습니다. SSDT는 제한된 기능을 포함한 Visual Studio 버전을 설치합니다.
3. **Visual Studio용 SSDT(SQL Server Data Tools)** Visual Studio용 SQL Server Data Tools를 가져오려면 [SSDT(SQL Server Data Tools) 다운로드][Download SQL Server Data Tools (SSDT)]를 참조하세요.
4. **Azure Synapse Analytics 데이터베이스 및 사용 권한**. 이 자습서는 Azure Synapse Analytics 인스턴스의 전용 SQL 풀에 연결하고 데이터를 로드합니다. 연결하고, 테이블을 만들고, 데이터를 로드하는 사용 권한이 있어야 합니다.

## <a name="create-a-new-integration-services-project"></a>새 Integration Services 프로젝트 만들기
1. Visual Studio를 시작합니다.
2. **파일** 메뉴에서 **새 | 프로젝트** 를 선택합니다.
3. **설치된 | 템플릿 | 비즈니스 인텔리전스 | Integration Services** 프로젝트 형식으로 이동합니다.
4. **Integration Services 프로젝트** 를 선택합니다. **이름** 및 **위치** 에 대한 값을 제공한 다음, **확인** 을 선택합니다.

Visual Studio가 열리고 새 Integration Services(SSIS) 프로젝트를 만듭니다. 그런 다음, Visual Studio에서 프로젝트에 단일 새 SSIS 패키지(Package.dtsx)에 대한 디자이너를 엽니다. 다음 화면 영역이 표시됩니다.

* 왼쪽은 SSIS 구성 요소의 **도구 상자** 입니다.
* 중간은 여러 탭이 포함된 디자인 화면입니다. 일반적으로 최소한 **제어 흐름** 및 **데이터 흐름** 탭을 사용합니다.
* 오른쪽은 **솔루션 탐색기** 및 **속성** 창입니다.
  
    ![도구 상자 창, 디자인 창, 솔루션 탐색기 창 및 속성 창이 표시된 Visual Studio의 스크린샷.][01]

## <a name="option-1---use-the-sql-dw-upload-task"></a>옵션 1 - SQL DW 업로드 태스크 사용

첫 번째 방법은 SQL DW 업로드 태스크를 사용하는 패키지입니다. 이 태스크는 원본 및 대상 정보를 모두 캡슐화합니다. 원본 데이터가 구분 기호로 분리된 텍스트 파일에 로컬로 저장되거나 Azure Blob Storage에 저장된다고 가정합니다.

### <a name="prerequisites-for-option-1"></a>옵션 1에 대한 필수 구성 요소

이 옵션을 사용하여 자습서를 계속하려면 다음 작업을 수행해야 합니다.

- [Azure용 Microsoft SQL Server Integration Services 기능 팩][Microsoft SQL Server 2017 Integration Services Feature Pack for Azure] SQL DW 업로드 태스크는 기능 팩의 구성 요소입니다.

- [Azure Blob Storage](https://docs.microsoft.com/azure/storage/) 계정 SQL DW 업로드 태스크는 Azure Blob Storage에서 Azure Synapse Analytics로 데이터를 로드합니다. Blob Storage에 이미 있는 파일을 로드할 수 있습니다. 또는 컴퓨터에서 파일을 로드할 수 있습니다. 컴퓨터에서 파일을 선택하면 SQL DW 업로드 작업은 먼저 준비를 위해 해당 파일을 Blob Storage에 업로드한 다음, 전용 SQL 풀로 로드합니다.

### <a name="add-and-configure-the-sql-dw-upload-task"></a>SQL DW 업로드 태스크 추가 및 구성

1. ( **제어 흐름** 탭에 있는) 도구 상자에서 디자인 화면의 가운데로 SQL DW 업로드 태스크를 끌어옵니다.

2. 열려는 태스크를 두 번 클릭하여 **SQL DW 업로드 태스크 편집기** 를 엽니다.

    ![SQL DW 업로드 태스크 편집기의 일반 페이지](media/load-data-to-sql-data-warehouse/azure-sql-dw-upload-task-editor.png)

3. [Azure SQL DW 업로드 태스크](control-flow/azure-sql-dw-upload-task.md) 아티클의 지침을 통해 태스크를 구성합니다. 이 태스크가 원본 및 대상 정보 모두와 원본 테이블과 대상 테이블 간의 매핑을 캡슐화하므로 작업 편집기에서는 여러 설정 페이지를 구성해야 합니다.

### <a name="create-a-similar-solution-manually"></a>수동으로 유사한 솔루션 만들기

추가 컨트롤의 경우 SQL DW 업로드 태스크에서 수행한 작업을 에뮬레이트하는 패키지를 수동으로 만들 수 있습니다. 

1. Azure Blob 업로드 태스크를 사용하여 Azure Blob Storage에 데이터를 저장합니다. Azure Blob 업로드 작업을 가져오려면 [Azure용 Microsoft SQL Server Integration Services 기능 팩][Microsoft SQL Server 2017 Integration Services Feature Pack for Azure]을 다운로드합니다.

2. 그런 다음, SSIS 실행 SQL 작업을 사용하여 전용 SQL 풀로 데이터를 로드하는 PolyBase 스크립트를 시작합니다. Azure Blob Storage에서 전용 SQL 풀로 데이터를 로드하는 예제(SSIS를 사용하지 않음)는 [자습서: Azure Synapse Analytics에 데이터 로드](/azure/sql-data-warehouse/load-data-wideworldimportersdw)를 참조하세요.

## <a name="option-2---use-a-source-and-destination"></a>옵션 2 - 원본 및 대상 사용

두 번째 방법은 원본 및 대상이 포함된 데이터 흐름 태스크를 사용하는 일반적인 패키지입니다. 이 방법은 SQL Server 및 Azure Synapse Analytics를 포함하는 다양한 데이터 원본을 지원합니다.

이 자습서에서는 데이터 원본으로 SQL Server를 사용합니다. SQL Server는 온-프레미스 또는 Azure 가상 머신에서 실행됩니다.

SQL Server 및 전용 SQL 풀에 연결하려면 ADO.NET 연결 관리자와 원본 및 대상 또는 OLE DB 연결 관리자와 원본 및 대상을 사용할 수 있습니다. 이 자습서에서는 구성 옵션이 가장 적기 때문에 ADO.NET을 사용합니다. OLE DB는 ADO NET보다 약간 더 나은 성능을 제공할 수 있습니다.

바로 가기로 SQL Server 가져오기 및 내보내기 마법사를 사용하여 기본 패키지를 만들 수 있습니다. 그런 다음, 패키지를 저장하고 Visual Studio 또는 SSDT를 열어 보고 사용자 지정합니다. 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조하세요.

### <a name="prerequisites-for-option-2"></a>옵션 2에 대한 필수 구성 요소

이 옵션을 사용하여 자습서를 계속하려면 다음 작업을 수행해야 합니다.

1. **샘플 데이터** 이 자습서에서는 AdventureWorks 예제 데이터베이스의 SQL Server에 저장된 샘플 데이터를 전용 SQL 풀로 로드할 원본 데이터로 사용합니다. AdventureWorks 샘플 데이터베이스를 가져오려면 [AdventureWorks 샘플 데이터베이스][AdventureWorks 2014 Sample Databases]를 참조하세요.

2. **방화벽 규칙** 전용 SQL 풀에 데이터를 업로드하려면 먼저 로컬 컴퓨터의 IP 주소를 사용하여 전용 SQL 풀에 방화벽 규칙을 만들어야 합니다.

### <a name="create-the-basic-data-flow"></a>기본 데이터 흐름 만들기
1. 도구 상자에서 디자인 화면( **제어 흐름** 탭에서)의 가운데로 데이터 흐름 태스크를 끌어 옵니다.
   
    ![데이터 흐름 태스크를 디자인 창의 제어 흐름 탭으로 끌어서 놓는 것을 보여 주는 Visual Studio의 스크린샷.][02]
2. 데이터 흐름 태스크를 두 번 클릭하여 데이터 흐름 탭으로 전환합니다.
3. 도구 상자의 기타 원본 목록에서 ADO.NET 원본을 디자인 화면으로 끕니다. 원본 어댑터를 선택한 상태로 **속성** 창에서 해당 이름을 **SQL Server 원본** 으로 변경합니다.
4. 도구 상자의 기타 대상 목록에서 ADO.NET 대상을 ADO.NET 원본 아래의 디자인 화면으로 끕니다. 대상 어댑터를 선택한 상태로 **속성** 창에서 해당 이름을 **SQL DW 대상** 으로 변경합니다.
   
    ![대상 어댑터를 원본 어댑터 바로 아래 위치로 끌어서 오는 것을 보여 주는 스크린샷.][09]

### <a name="configure-the-source-adapter"></a>원본 어댑터 구성
1. 원본 어댑터를 두 번 클릭하여 **ADO.NET 원본 편집기** 를 엽니다.
   
    ![ADO.NET 원본 편집기의 스크린샷. 연결 관리자 탭이 표시되어 있고 컨트롤을 사용하여 데이터 흐름 속성을 구성할 수 있습니다.][03]
2. **ADO.NET 원본 편집기** 의 **연결 관리자** 탭에서 **ADO.NET 연결 관리자** 목록 옆의 **새로 만들기** 단추를 클릭하여 **ADO.NET 연결 관리자 구성** 대화 상자를 열고 이 자습서에서 데이터를 로드하는 SQL Server 데이터베이스에 대한 연결 설정을 만듭니다.
   
    ![ADO.NET 연결 관리자 구성 대화 상자 스크린샷. 컨트롤을 사용하여 연결 관리자를 설정하고 구성할 수 있습니다.][04]
3. **ADO.NET 연결 관리자 구성** 대화 상자에서 **새로 만들기** 단추를 클릭하여 **연결 관리자** 대화 상자를 열고 새 데이터 연결을 만듭니다.
   
    ![연결 관리자 대화 상자 스크린샷. 컨트롤을 사용하여 데이터 연결을 구성할 수 있습니다.][05]
4. **연결 관리자** 대화 상자에서 다음을 수행합니다.
   
   1. **공급자** 의 경우 SqlClient 데이터 공급자를 선택합니다.
   2. **서버 이름** 의 경우 SQL Server 이름을 입력합니다.
   3. **서버에 로그온** 섹션에서 인증 정보를 선택하거나 입력합니다.
   4. **데이터베이스에 연결** 섹션에서 AdventureWorks 샘플 데이터베이스를 선택합니다.
   5. **연결 테스트** 를 클릭합니다.
      
       ![테스트 연결에 성공했음을 나타내는 확인 단추와 텍스트를 표시하는 대화 상자 스크린샷.][06]
   6. 연결 테스트의 결과를 보고하는 대화 상자에서 **확인** 을 클릭하여 **연결 관리자** 대화 상자로 돌아갑니다.
   7. **연결 관리자** 대화 상자에서 **확인** 을 클릭하여 **ADO.NET 연결 관리자 구성** 대화 상자로 돌아갑니다.
5. **ADO.NET 연결 관리자 구성** 대화 상자에서 **확인** 을 클릭하여 **ADO.NET 원본 편집기** 로 돌아갑니다.
6. **ADO.NET 원본 편집기** 의 **테이블 또는 뷰 이름** 목록에서 **Sales.SalesOrderDetail** 테이블을 선택합니다.
   
    ![ADO.NET 원본 편집기의 스크린샷. 테이블 또는 보기 목록 이름에서 Sales.SalesOrderDetail 테이블이 선택되어 있습니다.][07]
7. **미리 보기** 를 클릭하여 **쿼리 결과 미리 보기** 대화 상자에서 원본 테이블의 처음 200개의 데이터 행을 봅니다.
   
    ![쿼리 결과 미리 보기 대화 상자 스크린샷. 원본 테이블의 여러 판매 데이터 행을 볼 수 있습니다.][08]
8. **쿼리 결과 미리 보기** 대화 상자에서 **닫기** 를 클릭하여 **ADO.NET 원본 편집기** 로 돌아갑니다.
9. **ADO.NET 원본 편집기** 에서 **확인** 을 클릭하여 데이터 원본 구성을 마칩니다.

### <a name="connect-the-source-adapter-to-the-destination-adapter"></a>대상 어댑터에 원본 어댑터 연결
1. 디자인 화면에서 원본 어댑터를 선택합니다.
2. 원본 어댑터에서 확장하는 파란색 화살표를 선택하고 제자리에 맞출 때까지 대상 편집기를 끕니다.
   
    ![원본 및 대상 어댑터를 보여 주는 스크린샷. 파란색 화살표가 원본 어댑터에서 대상 어댑터를 가리키고 있습니다.][10]
   
    일반적인 SSIS 패키지에서 원본과 대상 간의 SSIS 도구 상자에서 다양한 구성 요소를 사용하여 SSIS 데이터 흐름을 통해 전달될 때 데이터를 재구성, 변형 및 정리합니다. 이 예제를 최대한 단순하게 유지하기 위해 원본을 대상에 직접 연결합니다.

### <a name="configure-the-destination-adapter"></a>대상 어댑터 구성
1. 대상 어댑터를 두 번 클릭하여 **ADO.NET 대상 편집기** 를 엽니다.
   
    ![ADO.NET 대상 편집기 스크린샷. 연결 관리자 탭이 표시되어 있고 컨트롤을 사용하여 데이터 흐름 속성을 구성할 수 있습니다.][11]
2. **ADO.NET 대상 편집기** 의 **연결 관리자** 탭에서 **연결 관리자** 목록 옆의 **새로 만들기** 단추를 클릭하여 **ADO.NET 연결 관리자 구성** 대화 상자를 열고 이 자습서에서 데이터를 로드하는 Azure Synapse Analytics 데이터베이스에 대한 연결 설정을 만듭니다.
3. **ADO.NET 연결 관리자 구성** 대화 상자에서 **새로 만들기** 단추를 클릭하여 **연결 관리자** 대화 상자를 열고 새 데이터 연결을 만듭니다.
4. **연결 관리자** 대화 상자에서 다음을 수행합니다.
   1. **공급자** 의 경우 SqlClient 데이터 공급자를 선택합니다.
   2. **서버 이름** 의 경우 전용 SQL 풀 이름을 입력합니다.
   3. **서버에 로그온** 섹션에서 **SQL Server 인증 사용** 을 선택하고 인증 정보를 입력합니다.
   4. **데이터베이스에 연결** 섹션에서 기존의 전용 SQL 풀 데이터베이스를 선택합니다.
   5. **연결 테스트** 를 클릭합니다.
   6. 연결 테스트의 결과를 보고하는 대화 상자에서 **확인** 을 클릭하여 **연결 관리자** 대화 상자로 돌아갑니다.
   7. **연결 관리자** 대화 상자에서 **확인** 을 클릭하여 **ADO.NET 연결 관리자 구성** 대화 상자로 돌아갑니다.
5. **ADO.NET 연결 관리자 구성** 대화 상자에서 **확인** 을 클릭하여 **ADO.NET 대상 편집기** 로 돌아갑니다.
6. **ADO.NET 대상 편집기** 에서 **테이블 또는 뷰 사용** 목록 옆의 **새로 만들기** 를 클릭하여 **테이블 만들기** 대화 상자를 열고 원본 테이블과 일치하는 열 목록으로 새 대상 테이블을 만듭니다.
   
    ![테이블 만들기 대화 상자 스크린샷. 대상 테이블을 만드는 S Q L 코드를 볼 수 있습니다.][12a]
7. **테이블 만들기** 대화 상자에서 다음을 수행합니다.
   
   1. 대상 테이블의 이름을 **SalesOrderDetail** 로 변경합니다.
   2. **rowguid** 열을 제거합니다. **uniqueidentifier** 데이터 형식은 전용 SQL 풀에서 지원되지 않습니다.
   3. **LineTotal** 열의 데이터 형식을 **money** 로 변경합니다. **10진** 데이터 형식은 전용 SQL 풀에서 지원되지 않습니다. 지원되는 데이터 형식에 대한 정보는 [테이블 만들기(Azure Synapse Analytics, 병렬 데이터 웨어하우스)][CREATE TABLE (Azure Synapse Analytics, Parallel Data Warehouse)]를 참조하세요.
      
       ![LineTotal이 money열이고 rowguid 열은 없는 SalesOrderDetail이라는 테이블을 만드는 코드를 포함하는 테이블 만들기 대화 상자 스크린샷.][12b]
   4. **확인** 을 클릭하여 테이블을 만들고 **ADO.NET 대상 편집기** 로 돌아갑니다.
8. **ADO.NET 대상 편집기** 에서 **매핑** 탭을 선택하여 원본의 열이 대상의 열로 매핑되는 방법을 확인합니다.
   
    ![ADO.NET 대상 편집기의 매핑 탭 스크린샷. 선들이 원본 및 대상 테이블에서 이름이 같은 열을 연결하고 있습니다.][13]
9. **확인** 을 클릭하여 대상 구성을 완료합니다.

## <a name="run-the-package-to-load-the-data"></a>패키지를 실행하여 데이터 로드
도구 모음의 **시작** 단추를 클릭하거나 **디버그** 메뉴의 **실행** 옵션 중 하나를 선택하여 패키지를 실행합니다.

다음 단락에서는 이 아티클에 설명된 두 번째 옵션, 즉, 원본 및 대상이 포함된 데이터 흐름을 사용하여 패키지를 만든 경우 표시되는 내용에 대해 설명합니다.

패키지 실행을 시작하면 활동과 지금까지 처리된 행 수를 나타내는 데 노란색 회전 바퀴가 나타납니다.

![각 어댑터 위에 노란색 회전 휠이 있고, 그 가운데에 “29916개 행”이라는 텍스트가 있는 원본 및 대상 어댑터를 보여 주는 스크린샷.][14]

패키지가 실행을 마치면 성공과 원본에서 대상으로 로드된 데이터의 행 수를 나타내는 녹색 확인 표시가 나타납니다.

![원본 및 대상 어댑터를 보여 주는 스크린샷. 각 어댑터 위에 녹색 확인 표시가 있고, 그 가운데에 “121317개 행”이라는 텍스트가 있습니다.][15]

축하합니다! SQL Server Integration Services를 사용하여 Azure Synapse Analytics로 데이터를 성공적으로 로드했습니다.

## <a name="next-steps"></a>다음 단계

- 디자인 환경에서 패키지 권한을 디버그하고 문제를 해결하는 방법을 알아봅니다. 여기에서 시작하세요. [패키지 배포 문제 해결 도구][Troubleshooting Tools for Package Development].

- SSIS 프로젝트와 패키지를 Integration Services 서버 또는 다른 스토리지 위치에 배포하는 방법에 대해 알아보세요. 여기에서 시작하세요. [프로젝트 및 패키지 배포][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/load-data-to-sql-data-warehouse/ssis-designer-01.png
[02]:  ./media/load-data-to-sql-data-warehouse/ssis-data-flow-task-02.png
[03]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-03.png
[04]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-manager-04.png
[05]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-05.png
[06]:  ./media/load-data-to-sql-data-warehouse/test-connection-06.png
[07]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-07.png
[08]:  ./media/load-data-to-sql-data-warehouse/preview-data-08.png
[09]:  ./media/load-data-to-sql-data-warehouse/source-destination-09.png
[10]:  ./media/load-data-to-sql-data-warehouse/connect-source-destination-10.png
[11]:  ./media/load-data-to-sql-data-warehouse/ado-net-destination-11.png
[12a]: ./media/load-data-to-sql-data-warehouse/destination-query-before-12a.png
[12b]: ./media/load-data-to-sql-data-warehouse/destination-query-after-12b.png
[13]:  ./media/load-data-to-sql-data-warehouse/column-mapping-13.png
[14]:  ./media/load-data-to-sql-data-warehouse/package-running-14.png
[15]:  ./media/load-data-to-sql-data-warehouse/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: ../relational-databases/polybase/polybase-guide.md
[Download SQL Server Data Tools (SSDT)]: ../ssdt/download-sql-server-data-tools-ssdt.md
[CREATE TABLE (Azure Synapse Analytics, Parallel Data Warehouse)]: ../t-sql/statements/create-table-azure-sql-data-warehouse.md
[Data Flow]: ./data-flow/data-flow.md
[Troubleshooting Tools for Package Development]: ./troubleshooting/troubleshooting-tools-for-package-development.md
[Deployment of Projects and Packages]: ./packages/deploy-integration-services-ssis-projects-and-packages.md

<!--Other Web references-->
[Microsoft SQL Server 2017 Integration Services Feature Pack for Azure]: https://www.microsoft.com/download/details.aspx?id=54798
[SQL Server Evaluations]: https://www.microsoft.com/evalcenter/evaluate-sql-server-2017
[Visual Studio Community]: https://www.visualstudio.com/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks