---
title: SSIS(SQL Server Integration Services)를 사용하여 SQL Server 또는 Azure SQL Database에 데이터 로드 | Microsoft Docs
description: SSIS(SQL Server Integration Services) 패키지를 만들어 다양한 데이터 원본에서 SQL Server 또는 Azure SQL Database로 데이터를 이동하는 방법을 보여 줍니다.
documentationcenter: NA
ms.prod: sql
ms.prod_service: integration-services
ms.technology: integration-services
ms.topic: conceptual
ms.custom: loading
ms.date: 08/20/2018
ms.author: chugu
author: chugugrace
ms.openlocfilehash: 8d78ab5befe5f95c07b6cb539d2629fdd9d003ae
ms.sourcegitcommit: 909b69dd1f918f00b9013bb43ea66e76a690400a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75924983"
---
# <a name="load-data-into-sql-server-or-azure-sql-database-with-sql-server-integration-services-ssis"></a>SSIS(SQL Server Integration Services)를 사용하여 SQL Server 또는 Azure SQL Database에 데이터 로드

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-xxxx-xxx.md)]

SSIS(SQL Server Integration Services) 패키지를 만들어 SQL Server 또는 [Azure SQL Database](/azure/sql-database/)에 데이터를 로드합니다. SSIS 데이터 흐름을 통해 전달될 때 필요에 따라 데이터를 재구성, 변형 및 정리할 수 있습니다.

이 아티클에서는 다음을 수행하는 방법을 보여줍니다.

* Visual Studio에서 새 Integration Services 프로젝트를 만듭니다.
* 원본에서 대상으로 데이터를 로드하는 SSIS 패키지를 디자인합니다.
* SSIS 패키지를 실행하여 데이터를 로드합니다.

## <a name="basic-concepts"></a>기본 개념

패키지는 SSIS의 작업 단위입니다. 관련된 패키지는 프로젝트에서 그룹화됩니다. SQL Server Data Tools를 사용하여 Visual Studio에서 프로젝트를 만들고 패키지를 디자인합니다. 디자인 프로세스는 도구 상자에서 디자인 화면으로 구성 요소를 끌어서 놓고, 연결하고, 해당 속성을 설정하는 시각적 프로세스입니다. 패키지를 완료한 후에 실행할 수 있고, 필요에 따라 포괄적인 관리, 모니터링 및 보안을 위해 SQL Server 또는 SQL Database에 배포할 수 있습니다.

SSIS에 대한 자세한 소개는 이 아티클의 범위를 벗어납니다. 자세히 알아보려면 다음 아티클을 참조하세요.

- [SQL Server Integration Services](sql-server-integration-services.md)

- [ETL 패키지를 만드는 방법](ssis-how-to-create-an-etl-package.md)

## <a name="about-the-solution"></a>솔루션 정보

솔루션은 원본 및 대상이 포함된 데이터 흐름 태스크를 사용하는 일반적인 패키지입니다. 이 방법은 SQL Server 및 Azure SQL Database를 포함하는 다양한 데이터 원본을 지원합니다.

이 자습서에서는 데이터 원본으로 SQL Server를 사용합니다. SQL Server는 온-프레미스 또는 Azure 가상 머신에서 실행됩니다.

SQL Server 및 SQL Database에 연결하려면 ADO.NET 연결 관리자와 원본 및 대상 또는 OLE DB 연결 관리자와 원본 및 대상을 사용할 수 있습니다. 이 자습서에서는 구성 옵션이 가장 적기 때문에 ADO.NET을 사용합니다. OLE DB는 ADO NET보다 약간 더 나은 성능을 제공할 수 있습니다.

바로 가기로 SQL Server 가져오기 및 내보내기 마법사를 사용하여 기본 패키지를 만들 수 있습니다. 그런 다음, 패키지를 저장하고 Visual Studio 또는 SSDT를 열어 보고 사용자 지정합니다. 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 단계별로 실행하려면 다음 항목이 필요합니다.

1. **SSIS(SQL Server Integration Services)** SSIS는 SQL Server의 구성 요소이며 SQL Server의 라이선스 버전 또는 개발자나 평가 버전이 필요합니다. SQL Server의 평가 버전을 가져오려면 [SQL Server 평가](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-rtm)를 참조하세요.
2. **Visual Studio**(선택 사항) Visual Studio Community Edition을 체험하려면 [Visual Studio Community][Visual Studio Community]를 참조하세요. Visual Studio를 설치하지 않으려는 경우 SSDT(SQL Server Data Tools)만을 설치할 수 있습니다. SSDT는 제한된 기능을 포함한 Visual Studio 버전을 설치합니다.
3. **Visual Studio용 SSDT(SQL Server Data Tools)** Visual Studio용 SQL Server Data Tools를 가져오려면 [SSDT(SQL Server Data Tools) 다운로드][Download SQL Server Data Tools (SSDT)]를 참조하세요.
4. 이 자습서에서는 SQL Server 또는 SQL Database 인스턴스에 연결하고 여기에 데이터를 로드합니다. 다음 중 하나에 연결하고, 테이블을 만들고, 데이터를 로드할 수 있는 권한이 있어야 합니다.
   - **Azure SQL Database 데이터베이스**. 자세한 내용은 [Azure SQL Database](/azure/sql-database/)를 참조하세요.  
      또는
   - **SQL Server 인스턴스**입니다. SQL Server는 온-프레미스 또는 Azure 가상 머신에서 실행됩니다. SQL Server의 평가판 또는 개발자 버전을 다운로드하려면 [SQL Server 다운로드](https://www.microsoft.com/sql-server/sql-server-downloads)를 참조하세요.

5. **샘플 데이터** 이 자습서에서는 원본 데이터로 AdventureWorks 샘플 데이터베이스의 SQL Server에 저장된 샘플 데이터를 사용합니다. AdventureWorks 샘플 데이터베이스를 가져오려면 [AdventureWorks 샘플 데이터베이스][AdventureWorks 2014 Sample Databases]를 참조하세요.
6. SQL Database에 데이터를 로드하는 경우 **방화벽 규칙**입니다. SQL Database에 데이터를 업로드하려면 먼저 로컬 컴퓨터의 IP 주소를 사용하여 SQL Database에 방화벽 규칙을 만들어야 합니다.

## <a name="create-a-new-integration-services-project"></a>새 Integration Services 프로젝트 만들기
1. Visual Studio를 시작합니다.
2. **파일** 메뉴에서 **새 | 프로젝트**를 선택합니다.
3. **설치된 | 템플릿 | 비즈니스 인텔리전스 | Integration Services** 프로젝트 형식으로 이동합니다.
4. **Integration Services 프로젝트**를 선택합니다. **이름** 및 **위치**에 대한 값을 제공한 다음, **확인**을 선택합니다.

Visual Studio가 열리고 새 Integration Services(SSIS) 프로젝트를 만듭니다. 그런 다음, Visual Studio에서 프로젝트에 단일 새 SSIS 패키지(Package.dtsx)에 대한 디자이너를 엽니다. 다음 화면 영역이 표시됩니다.

* 왼쪽은 SSIS 구성 요소의 **도구 상자**입니다.
* 중간은 여러 탭이 포함된 디자인 화면입니다. 일반적으로 최소한 **제어 흐름** 및 **데이터 흐름** 탭을 사용합니다.
* 오른쪽은 **솔루션 탐색기** 및 **속성** 창입니다.
  
    ![][01]

## <a name="create-the-basic-data-flow"></a>기본 데이터 흐름 만들기
1. 도구 상자에서 디자인 화면(**제어 흐름** 탭에서)의 가운데로 데이터 흐름 태스크를 끌어 옵니다.
   
    ![][02]
2. 데이터 흐름 태스크를 두 번 클릭하여 데이터 흐름 탭으로 전환합니다.
3. 도구 상자의 기타 원본 목록에서 ADO.NET 원본을 디자인 화면으로 끕니다. 원본 어댑터를 선택한 상태로 **속성** 창에서 해당 이름을 **SQL Server 원본**으로 변경합니다.
4. 도구 상자의 기타 대상 목록에서 ADO.NET 대상을 ADO.NET 원본 아래의 디자인 화면으로 끕니다. 대상 어댑터를 선택한 상태로 **속성** 창에서 해당 이름을 **SQL 대상**으로 변경합니다.
   
    ![][09]

## <a name="configure-the-source-adapter"></a>원본 어댑터 구성
1. 원본 어댑터를 두 번 클릭하여 **ADO.NET 원본 편집기**를 엽니다.
   
    ![][03]
2. **ADO.NET 원본 편집기**의 **연결 관리자** 탭에서 **ADO.NET 연결 관리자** 목록 옆의 **새로 만들기** 단추를 클릭하여 **ADO.NET 연결 관리자 구성** 대화 상자를 열고 이 자습서에서 데이터를 로드하는 SQL Server 데이터베이스에 대한 연결 설정을 만듭니다.
   
    ![][04]
3. **ADO.NET 연결 관리자 구성** 대화 상자에서 **새로 만들기** 단추를 클릭하여 **연결 관리자** 대화 상자를 열고 새 데이터 연결을 만듭니다.
   
    ![][05]
4. **연결 관리자** 대화 상자에서 다음을 수행합니다.
   
   1. **공급자**의 경우 SqlClient 데이터 공급자를 선택합니다.
   2. **서버 이름**의 경우 SQL Server 이름을 입력합니다.
   3. **서버에 로그온** 섹션에서 인증 정보를 선택하거나 입력합니다.
   4. **데이터베이스에 연결** 섹션에서 AdventureWorks 샘플 데이터베이스를 선택합니다.
   5. **연결 테스트**를 클릭합니다.
      
       ![][06]
   6. 연결 테스트의 결과를 보고하는 대화 상자에서 **확인**을 클릭하여 **연결 관리자** 대화 상자로 돌아갑니다.
   7. **연결 관리자** 대화 상자에서 **확인**을 클릭하여 **ADO.NET 연결 관리자 구성** 대화 상자로 돌아갑니다.
5. **ADO.NET 연결 관리자 구성** 대화 상자에서 **확인**을 클릭하여 **ADO.NET 원본 편집기**로 돌아갑니다.
6. **ADO.NET 원본 편집기**의 **테이블 또는 뷰 이름** 목록에서 **Sales.SalesOrderDetail** 테이블을 선택합니다.
   
    ![][07]
7. **미리 보기**를 클릭하여 **쿼리 결과 미리 보기** 대화 상자에서 원본 테이블의 처음 200개의 데이터 행을 봅니다.
   
    ![][08]
8. **쿼리 결과 미리 보기** 대화 상자에서 **닫기**를 클릭하여 **ADO.NET 원본 편집기**로 돌아갑니다.
9. **ADO.NET 원본 편집기**에서 **확인**을 클릭하여 데이터 원본 구성을 마칩니다.

## <a name="connect-the-source-adapter-to-the-destination-adapter"></a>대상 어댑터에 원본 어댑터 연결
1. 디자인 화면에서 원본 어댑터를 선택합니다.
2. 원본 어댑터에서 확장하는 파란색 화살표를 선택하고 제자리에 맞출 때까지 대상 편집기를 끕니다.
   
    ![][10]
   
    일반적인 SSIS 패키지에서 원본과 대상 간의 SSIS 도구 상자에서 다양한 구성 요소를 사용하여 SSIS 데이터 흐름을 통해 전달될 때 데이터를 재구성, 변형 및 정리합니다. 이 예제를 최대한 단순하게 유지하기 위해 원본을 대상에 직접 연결합니다.

## <a name="configure-the-destination-adapter"></a>대상 어댑터 구성
1. 대상 어댑터를 두 번 클릭하여 **ADO.NET 대상 편집기**를 엽니다.
   
    ![][11]
2. **ADO.NET 대상 편집기**의 **연결 관리자** 탭에서 **연결 관리자** 목록 옆의 **새로 만들기** 단추를 클릭하여 **ADO.NET 연결 관리자 구성** 대화 상자를 열고 이 자습서에서 데이터를 로드하는 데이터베이스에 대한 연결 설정을 만듭니다.
3. **ADO.NET 연결 관리자 구성** 대화 상자에서 **새로 만들기** 단추를 클릭하여 **연결 관리자** 대화 상자를 열고 새 데이터 연결을 만듭니다.
4. **연결 관리자** 대화 상자에서 다음을 수행합니다.
   1. **공급자**의 경우 SqlClient 데이터 공급자를 선택합니다.
   2. **서버 이름**의 경우 SQL Server 또는 SQL Database 서버의 이름을 입력합니다.
   3. **서버에 로그온** 섹션에서 **SQL Server 인증 사용**을 선택하고 인증 정보를 입력합니다.
   4. **데이터베이스에 연결** 섹션에서 기존 데이터베이스를 선택합니다.
    a. **연결 테스트**를 클릭합니다.
    b. 연결 테스트의 결과를 보고하는 대화 상자에서 **확인**을 클릭하여 **연결 관리자** 대화 상자로 돌아갑니다.
    다. **연결 관리자** 대화 상자에서 **확인**을 클릭하여 **ADO.NET 연결 관리자 구성** 대화 상자로 돌아갑니다.
5. **ADO.NET 연결 관리자 구성** 대화 상자에서 **확인**을 클릭하여 **ADO.NET 대상 편집기**로 돌아갑니다.
6. **ADO.NET 대상 편집기**에서 **테이블 또는 뷰 사용** 목록 옆의 **새로 만들기**를 클릭하여 **테이블 만들기** 대화 상자를 열고 원본 테이블과 일치하는 열 목록으로 새 대상 테이블을 만듭니다.
   
    ![][12a]
7. **테이블 만들기** 대화 상자에서 다음을 수행합니다.
   
   1. 대상 테이블의 이름을 **SalesOrderDetail**로 변경합니다.
      
       ![][12b]

   2. **확인**을 클릭하여 테이블을 만들고 **ADO.NET 대상 편집기**로 돌아갑니다.
8. **ADO.NET 대상 편집기**에서 **매핑** 탭을 선택하여 원본의 열이 대상의 열로 매핑되는 방법을 확인합니다.
   
    ![][13]
9. **확인**을 클릭하여 대상 구성을 완료합니다.

## <a name="run-the-package-to-load-the-data"></a>패키지를 실행하여 데이터 로드
도구 모음의 **시작** 단추를 클릭하거나 **디버그** 메뉴의 **실행** 옵션 중 하나를 선택하여 패키지를 실행합니다.

다음 단락에서는 이 아티클에 설명된 두 번째 옵션, 즉, 원본 및 대상이 포함된 데이터 흐름을 사용하여 패키지를 만든 경우 표시되는 내용에 대해 설명합니다.

패키지 실행을 시작하면 활동과 지금까지 처리된 행 수를 나타내는 데 노란색 회전 바퀴가 나타납니다.

![][14]

패키지가 실행을 마치면 성공과 원본에서 대상으로 로드된 데이터의 행 수를 나타내는 녹색 확인 표시가 나타납니다.

![][15]

축하합니다! SQL Server Integration Services를 사용하여 SQL Server 또는 Azure SQL Database에 데이터를 성공적으로 로드했습니다.

## <a name="next-steps"></a>다음 단계

- 디자인 환경에서 패키지 권한을 디버그하고 문제를 해결하는 방법을 알아봅니다. 여기에서 시작하세요. [패키지 배포 문제 해결 도구][Troubleshooting Tools for Package Development].

- SSIS 프로젝트와 패키지를 Integration Services 서버 또는 다른 스토리지 위치에 배포하는 방법에 대해 알아보세요. 여기에서 시작하세요. [프로젝트 및 패키지 배포][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/load-data-to-sql-database-with-ssis/ssis-designer-01.png
[02]:  ./media/load-data-to-sql-database-with-ssis/ssis-data-flow-task-02.png
[03]:  ./media/load-data-to-sql-database-with-ssis/ado-net-source-03.png
[04]:  ./media/load-data-to-sql-database-with-ssis/ado-net-connection-manager-04.png
[05]:  ./media/load-data-to-sql-database-with-ssis/ado-net-connection-05.png
[06]:  ./media/load-data-to-sql-database-with-ssis/test-connection-06.png
[07]:  ./media/load-data-to-sql-database-with-ssis/ado-net-source-07.png
[08]:  ./media/load-data-to-sql-database-with-ssis/preview-data-08.png
[09]:  ./media/load-data-to-sql-database-with-ssis/source-destination-09.png
[10]:  ./media/load-data-to-sql-database-with-ssis/connect-source-destination-10.png
[11]:  ./media/load-data-to-sql-database-with-ssis/ado-net-destination-11.png
[12a]: ./media/load-data-to-sql-database-with-ssis/destination-query-before-12a.png
[12b]: ./media/load-data-to-sql-database-with-ssis/destination-query-after-12b.png
[13]:  ./media/load-data-to-sql-database-with-ssis/column-mapping-13.png
[14]:  ./media/load-data-to-sql-database-with-ssis/package-running-14.png
[15]:  ./media/load-data-to-sql-database-with-ssis/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[Download SQL Server Data Tools (SSDT)]: ../ssdt/download-sql-server-data-tools-ssdt.md
[Data Flow]: ./data-flow/data-flow.md
[Troubleshooting Tools for Package Development]: ./troubleshooting/troubleshooting-tools-for-package-development.md
[Deployment of Projects and Packages]: ./packages/deploy-integration-services-ssis-projects-and-packages.md

<!--Other Web references-->
[Microsoft SQL Server 2017 Integration Services Feature Pack for Azure]: https://www.microsoft.com/download/details.aspx?id=54798
[SQL Server Evaluations]: https://www.microsoft.com/evalcenter/evaluate-sql-server-2017
[Visual Studio Community]: https://www.visualstudio.com/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks
