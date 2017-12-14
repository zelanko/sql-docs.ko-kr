---
title: "연습: SSIS 패키지를 SQL 뷰로 게시 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ssis.packagepublishwizard.f1
ms.assetid: d32d9761-93fb-4020-bf82-231439c6f3ac
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f0e5fa598ce47a95aafe11fd3f05c82eca79c064
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="walkthrough-publish-an-ssis-package-as-a-sql-view"></a>연습: SSIS 패키지를 SQL 뷰로 게시
  이 연습에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 SSIS 패키지를 SQL 뷰로 게시하는 자세한 단계를 제공합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 연습을 수행하려면 컴퓨터에 다음 소프트웨어를 설치해야 합니다.  
  
1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이상( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]포함)  
  
2.  [SQL Server Data Tools](../../ssdt/download-sql-server-data-tools-ssdt.md)  
  
## <a name="step-1-build-and-deploy-ssis-project-to-the-ssis-catalog"></a>1단계: SSIS 프로젝트 빌드 및 SSIS 카탈로그에 배포  
 이 단계에서는 SSIS 지원 데이터 원본(이 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 사용)에서 데이터를 추출하는 SSIS 패키지를 만들고 데이터 스트리밍 대상 구성 요소를 사용하여 데이터를 출력합니다. 그런 다음 SSIS 프로젝트를 빌드하고 SSIS 카탈로그에 배포합니다.  
  
1.  **SQL Server Data Tools**를 실행합니다. **시작** 메뉴에서 **모든 프로그램**, **Microsoft SQL Server**를 차례로 가리킨 다음 **SQL Server Data Tools**를 클릭합니다.  
  
2.  새 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 만듭니다.  
  
    1.  메뉴 모음에서 **파일** 을 클릭하고 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다.  
  
    2.  왼쪽 창에서 **비즈니스 인텔리전스** 를 확장하고 트리 뷰에서 **Integration Services** 를 선택합니다.  
  
    3.  **Integration Services 프로젝트** (아직 선택하지 않은 경우)를 선택합니다.  
  
    4.  **프로젝트 이름** 으로 **SSISPackagePublishing**을 지정합니다.  
  
    5.  프로젝트 위치를 지정합니다.  
  
    6.  **확인** 을 클릭하여 **새 프로젝트** 대화 상자를 닫습니다.  
  
3.  **SSIS 도구 상자** 에서 **제어 흐름** 탭의 디자인 화면으로 **데이터 흐름** 구성 요소를 끌어 옵니다.  
  
4.  **제어 흐름** 에서 **데이터 흐름** 구성 요소를 두 번 클릭하여 **데이터 흐름 디자이너**를 엽니다.  
  
5.  도구 상자에서 **데이터 흐름 디자이너** 로 **원본 구성 요소** 를 끌어 와 데이터 원본에서 데이터를 추출하도록 구성합니다.  
  
    1.  연습을 위해 **Employee** 테이블이 포함된 **TestDB**라는 테스트 데이터베이스를 만듭니다. **ID**, **FirstName** 및 **LastName**의 세 열이 있는 테이블을 만듭니다.  
  
    2.  **ID** 를 기본 키로 설정합니다.  
  
    3.  다음 데이터를 사용하여 두 개의 레코드를 삽입합니다.  
  
        |ID|FirstName|LastName|  
        |--------|---------------|--------------|  
        |1.|John|Doe|  
        |2|Jane|Doe|  
  
    4.  **SSIS 도구 상자** 에서 **데이터 흐름 디자이너** 로 **OLE DB 원본**구성 요소를 끌어 옵니다.  
  
    5.  **TestDB** 데이터베이스의 **Employee** 테이블에서 데이터를 추출하도록 구성 요소를 구성합니다. **OLE DB 연결 관리자** 에서 **(local).TestDB**, **데이터 액세스 모드** 에서 **테이블 또는 뷰**, **테이블 또는 뷰 이름** 에서 **[dbo].[Employee]**를 선택합니다.  
  
         ![데이터 스트리밍 대상 - OLE DB 연결](../../integration-services/data-flow/media/dsd-oledbconnectionmanager.jpg "데이터 스트리밍 대상 - OLE DB 연결")  
  
6.  이제 도구 상자에서 데이터 흐름으로 **데이터 스트리밍 대상** 을 끌어 옵니다. 도구 상자의 일반 섹션에서 이 구성 요소를 찾아야 합니다.  
  
7.  데이터 흐름의 **OLE DB 원본** 구성 요소를 **데이터 스트리밍 대상** 구성 요소에 연결합니다.  
  
8.  SSIS 프로젝트를 빌드하고 SSIS 카탈로그에 배포합니다.  
  
    1.  메뉴 모음에서 **프로젝트** 를 클릭한 다음 **배포**를 클릭합니다.  
  
    2.  마법사의 지침에 따라 로컬 데이터베이스 서버의 SSIS 카탈로그에 프로젝트를 배포합니다. 다음 예제에서는 **Power BI** 를 폴더 이름으로 사용하고, **SSISPackagePublishing** 을 SSIS 카탈로그의 프로젝트 이름으로 사용합니다.  
  
## <a name="step-2-use-the-ssis-data-feed-publishing-wizard-to-publish-ssis-package-as-a-sql-view"></a>2단계: SSIS 데이터 피드 게시 마법사를 사용하여 SSIS 패키지를 SQL 뷰로 게시  
 이 단계에서는 SSIS(SQL Server Integration Services) 데이터 피드 게시 마법사를 사용하여 SSIS 패키지를 SQL Server 데이터베이스의 뷰로 게시합니다. 이 뷰를 쿼리하여 패키지의 출력 데이터를 사용할 수 있습니다.  
  
 SSIS 데이터 피드 게시 마법사는 SSIS용 OLE DB 공급자(SSISOLEDB)를 사용하여 연결된 서버를 만든 다음 연결된 서버에 대한 쿼리로 구성된 SQL 뷰를 만듭니다. 이 쿼리에는 SSIS 카탈로그의 폴더 이름, 프로젝트 이름, 패키지 이름이 포함됩니다.  
  
 이 뷰는 런타임에 사용자가 만든 연결 서버를 통해 SSIS용 OLE DB 공급자에게 쿼리를 전송합니다. SSIS용 OLE DB 공급자는 쿼리에 지정된 패키지를 실행하고 탭 형식의 결과 집합을 쿼리로 반환합니다.  
  
1.  C:\Program Files\Microsoft SQL Server\130\DTS\Binn에서 ISDataFeedPublishingWizard.exe를 실행하거나 시작\모든 프로그램에서 Microsoft SQL Server 2016\SQL Server 2016 데이터 피드 게시 마법사를 클릭하여 **SSIS 데이터 피드 게시 마법사** 를 시작합니다.  
  
2.  **소개** 페이지에서 **다음** 을 클릭합니다.  
  
     ![데이터 피드 게시 마법사 - 소개 페이지](../../integration-services/data-flow/media/dsd-feedpublishingwizard-introductionpage.jpg "데이터 피드 게시 마법사 - 소개 페이지")  
  
3.  **패키지 설정** 페이지에서 다음 작업을 수행합니다.  
  
    1.  SSIS 카탈로그를 포함하는 SQL Server 인스턴스의 **이름** 을 입력하거나, **찾아보기** 를 클릭하여 서버를 선택합니다.  
  
         ![데이터 피드 게시 마법사 - 패키지 설정 페이지](../../integration-services/data-flow/media/dsd-feedpublishingwizard-packagesettingspage.jpg "데이터 피드 게시 마법사 - 패키지 설정 페이지")  
  
    2.  경로 필드 옆의 **찾아보기** 를 클릭하고 SSIS 카탈로그로 이동하여 게시할 SSIS 패키지를 선택(예: **SSISDB**->**SSISPackagePublishing**->**Package.dtsx**)한 다음 **확인**을 클릭합니다.  
  
         ![데이터 피드 게시 마법사 - 패키지 찾아보기](../../integration-services/data-flow/media/dsd-feedpublishingwizard-browseforpackage.jpg "데이터 피드 게시 마법사 - 패키지 찾아보기")  
  
    3.  페이지 아래쪽에 있는 패키지 매개 변수, 프로젝트 매개 변수 및 연결 관리자 탭을 사용하여 패키지 매개 변수, 프로젝트 매개 변수 또는 패키지에 대한 연결 관리자 설정 값을 입력합니다. 패키지 실행에 사용되는 환경 참조를 지정하고 프로젝트/패키지 매개 변수를 환경 변수에 바인딩할 수도 있습니다.  
  
         중요한 매개 변수를 환경 변수에 바인딩하는 것이 좋습니다. 그러면 중요한 매개 변수의 값이 마법사에서 만든 SQL 뷰에 일반 텍스트 형식으로 저장되지 않습니다.  
  
    4.  **다음** 을 클릭하여 **게시 설정** 페이지로 전환합니다.  
  
4.  **게시 설정** 페이지에서 다음 작업을 수행합니다.  
  
    1.  뷰를 만들 **데이터베이스** 를 선택합니다.  
  
         ![데이터 피드 게시 마법사 - 게시 설정 페이지](../../integration-services/data-flow/media/dsd-feedpublishingwizard-publishsettingspage.jpg "데이터 피드 게시 마법사 - 게시 설정 페이지")  
  
    2.  **뷰** **이름**을 입력합니다. 드롭다운 목록에서 기존 뷰를 선택할 수도 있습니다.  
  
    3.  **설정** 목록에서 뷰와 연결할 **연결된 서버** 의 **이름** 을 지정합니다. 연결된 서버가 아직 없는 경우 마법사에서 뷰를 만들기 전에 먼저 연결된 서버를 만듭니다. 여기에서 **User32BitRuntime** 및 **Timeout** 값을 설정할 수도 있습니다.  
  
    4.  **고급** 단추를 클릭합니다. **고급 설정** 대화 상자가 표시됩니다.  
  
    5.  **고급 설정** 대화 상자에서 다음을 수행합니다.  
  
        1.  뷰를 만들 데이터베이스 스키마를 지정합니다(스키마 필드).  
  
        2.  데이터를 네트워크를 통해 보내기 전에 암호화해야 하는지 여부를 지정합니다(암호화 필드). 이 설정 및 TrustServerCertificate 설정에 대한 자세한 내용은 [유효성 검사 없이 암호화 사용](http://msdn.microsoft.com/library/ms131691.aspx) 항목을 참조하세요.  
  
        3.  암호화 설정을 사용하는 경우 자체 서명된 서버 인증서를 사용할 수 있는지 여부를 지정합니다(**TrustServerCertificate** 필드).  
  
        4.  **확인** 을 클릭하여 **고급 설정** 대화 상자를 닫습니다.  
  
    6.  **다음** 을 클릭하여 **유효성 검사** 페이지로 전환합니다.  
  
5.  **유효성 검사** 페이지에서 모든 설정 값의 유효성 검사 결과를 검토합니다. 다음 예제에서는 연결된 서버 존재에 대한 **경고** 를 볼 수 있습니다. 선택한 SQL Server 인스턴스에 연결된 서버가 없기 때문입니다. **결과** 에 **오류**가 표시되는 경우 **오류** 위로 마우스를 가져가면 오류에 대한 세부 정보가 표시됩니다. 예를 들어 SSISOLEDB 공급자에 대한 Inprocess 허용 옵션을 활성화하지 않은 경우 연결된 서버 구성 작업에서 오류가 발생합니다.  
  
     ![데이터 피드 게시 마법사 - 유효성 검사 페이지](../../integration-services/data-flow/media/dsd-feedpublishingwizard-validationpage.jpg "데이터 피드 게시 마법사 - 유효성 검사 페이지")  
  
6.  이 보고서를 XML 파일로 저장하려면 보고서 저장을 클릭합니다.  
  
7.  **유효성 검사** 페이지에서 **다음** 을 클릭하여 **요약** 페이지로 전환합니다.  
  
8.  **요약** 페이지에서 선택 항목을 검토하고 **게시** 를 클릭하여 게시 프로세스를 시작합니다. 이 프로세스는 연결된 서버를 만든 다음(서버에 연결된 서버가 없는 경우) 연결된 서버를 사용하여 뷰를 만듭니다.  
  
     ![데이터 피드 게시 마법사 - 요약 페이지](../../integration-services/data-flow/media/dsd-feedpublishingwizard-summarypage.jpg "데이터 피드 게시 마법사 - 요약 페이지")  
  
     이제 TestDB 데이터베이스에 대해 SELECT * FROM [SSISPackageView] SQL 문을 실행하여 패키지의 출력 데이터를 쿼리할 수 있습니다.  
  
9. 이 보고서를 XML 파일로 저장하려면 **보고서 저장**을 클릭합니다.  
  
10. 게시 프로세스의 결과를 검토하고 **마침** 을 클릭하여 마법사를 닫습니다.  
  
    > [!NOTE]  
    >  텍스트, ntext, 이미지, nvarchar(max), varchar(max) 및 varbinary(max) 데이터 형식은 지원되지 않습니다.  
  
## <a name="step-3-test-the-sql-view"></a>3단계: SQL 뷰 테스트  
 이 단계에서는 SSIS 데이터 피드 게시 마법사에서 만든 SQL 뷰를 실행합니다.  
  
1.  SQL Server Management Studio를 실행합니다.  
  
2.  \<**컴퓨터 이름**>, **데이터베이스**, \<**마법사에서 선택한 데이터베이스**> 및 **뷰**를 확장합니다.  
  
3.  마법사에서 만든 \<**마법사에서 만든 뷰**>를 마우스 오른쪽 단추로 클릭하고 **상위 1000개 행 선택**을 클릭합니다.  
  
4.  SSIS 패키지의 결과가 표시되는지 확인합니다.  
  
## <a name="step-4-verify-the-ssis-package-execution"></a>4단계: SSIS 패키지 실행 확인  
 이 단계에서는 SSIS 패키지가 실행되었는지 확인합니다.  
  
1.  SQL Server Management Studio에서 **Integration Services 카탈로그**, **SSISDB**, SSIS 프로젝트가 있는 **폴더** , **프로젝트**, 프로젝트 노드, **패키지**를 차례로 확장합니다.  
  
2.  SSIS 패키지를 마우스 오른쪽 단추로 클릭하고 **보고서**, **표준 보고서**를 차례로 가리킨 다음 **모든 실행**을 클릭합니다.  
  
3.  SSIS 패키지 실행이 보고서에 표시됩니다.  
  
    > [!NOTE]  
    >  Windows Vista 서비스 팩 2 컴퓨터에서는 성공한 실행과 실패한 실행의 두 가지 SSIS 패키지 실행이 보고서에 표시될 수 있습니다. 실패한 실행은 이 릴리스의 알려진 문제로 인한 것이므로 무시합니다.  
  
## <a name="more-info"></a>추가 정보  
 데이터 피드 게시 마법사는 다음과 같은 중요한 단계를 수행합니다.  
  
1.  연결된 서버를 만들고 SSIS용 OLE DB 공급자를 사용하도록 구성합니다.  
  
2.  지정된 데이터베이스에서 선택한 패키지에 대한 카탈로그 정보를 사용하여 연결된 서버를 쿼리하는 SQL 뷰를 만듭니다.  
  
 이 섹션에서는 데이터 피드 게시 마법사를 사용하지 않고 연결된 서버와 SQL 뷰를 만드는 절차를 제공합니다. 또한 SSIS용 OLE DB 공급자와 함께 OPENQUERY 함수를 사용하는 방법에 대한 추가 정보를 제공합니다.  
  
### <a name="create-a-linked-server-using-the-ole-db-provider-for-ssis"></a>SSIS용 OLE DB 공급자를 사용하여 연결된 서버 만들기  
 SQL Server Management Studio에서 다음 쿼리를 실행하여 SSIS용 OLE DB 공급자를 통해 연결된 서버를 만듭니다.  
  
```sql 
  
USE [master]  
GO  
  
EXEC sp_addlinkedserver  
@server = N'SSISFeedServer',  
@srvproduct = N'Microsoft',  
@provider = N'SSISOLEDB',  
@datasrc = N'.'  
GO  
  
```  
  
### <a name="create-a-view-using-linked-server-and-ssis-catalog-information"></a>연결된 서버 및 SSIS 카탈로그 정보를 사용하여 뷰 만들기  
 이 단계에서는 이전 섹션에서 만든 연결된 서버에서 쿼리를 실행하는 SQL 뷰를 만듭니다. 쿼리에는 SSIS 카탈로그의 폴더 이름, 프로젝트 이름, 패키지 이름이 포함됩니다.  
  
 런타임에 뷰를 실행하면 뷰에 정의된 연결된 서버 쿼리가 쿼리에 지정된 SSIS 패키지를 시작하고 패키지 출력을 테이블 형식 결과 집합으로 받습니다.  
  
1.  뷰를 만들기 전에 새 쿼리 창에서 다음 쿼리를 입력하고 실행합니다. OPENQUERY는 SQL Server에서 지원되는 행 집합 함수입니다. 연결된 서버에 연결된 OLE DB 공급자를 사용하여 지정된 연결된 서버에서 지정된 통과 쿼리를 실행합니다. OPENQUERY는 테이블 이름처럼 쿼리의 FROM 절에서 참조될 수 있습니다. 자세한 내용은 [MSDN 라이브러리의 OPENQUERY 설명서](http://msdn.microsoft.com/library/ms188427.aspx) 를 참조하세요.  
  
    ```sql
    SELECT * FROM OPENQUERY(SSISFeedServer,N'Folder=Eldorado;Project=SSISPackagePublishing;Package=Package.dtsx')   
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  필요한 경우 폴더 이름, 프로젝트 이름 및 패키지 이름을 업데이트합니다. OPENQUERY 함수가 실패한 경우 **SQL Server Management Studio**에서 **서버 개체**, 확장 **연결된 서버**, **공급자**를 차례로 확장하고 **SSISOLEDB** 공급자를 두 번 클릭하여 **Inprocess 허용** 옵션이 사용하도록 설정되었는지 확인합니다.  
  
2.  다음 쿼리를 실행하여 **TestDB** 데이터베이스에서 뷰를 만듭니다.  
  
    ```sql
  
    USE [TestDB]   
    GO   
  
    CREATE VIEW SSISPackageView AS   
    SELECT * FROM OPENQUERY(SSISFeedServer, 'Folder=Eldorado;Project=SSISPackagePublishing;Package=Package.dtsx')   
    GO  
  
    ```  
  
3.  다음 쿼리를 실행하여 뷰를 테스트합니다.  
  
    ```sql
    SELECT * FROM SSISPackageView  
    ```  
  
### <a name="openquery-function"></a>OPENQUERY 함수  
 OPENQUERY 함수에 대한 구문은 다음과 같습니다.  
  
```sql 
SELECT * FROM OPENQUERY(<LinkedServer Name>, N’Folder=<Folder Name from SSIS Catalog>; Project=<SSIS Project Name>; Package=<SSIS Package Name>; Use32BitRuntime=[True | False];Parameters=”<parameter_name_1>=<value1>; parameter_name_2=<value2>”;Timeout=<Number of Seconds>;’)  
```  
  
 폴더, 프로젝트 및 패키지 매개 변수는 필수입니다. Use32BitRuntime, Timeout 및 Parameters는 선택 사항입니다.  
  
 Use32BitRuntime의 값은 0, 1, true 또는 false일 수 있습니다. SQL Server의 플랫폼이 64비트인 경우 패키지에서 32비트 런타임(1 또는 true)을 사용해야 할지 여부를 나타냅니다.  
  
 Timeout은 SSIS용 OLE DB 공급자가 SSIS 패키지에서 새 데이터가 도착할 때까지 대기할 수 있는 시간(초)입니다. 기본적으로 제한 시간은 60초입니다. 20에서 32000 사이의 정수를 시간 제한 값으로 지정할 수 있습니다.  
  
 Parameters는 패키지 매개 변수 값과 프로젝트 매개 변수 값을 모두 포함합니다. 매개 변수에 대한 규칙은 [DTExec](http://msdn.microsoft.com/library/hh231187.aspx)의 매개 변수와 동일합니다.  
  
 다음 목록은 쿼리 절에 허용되는 특수 문자를 지정합니다.  
  
-   작은따옴표(') – 표준 OPENQUERY에서 지원됩니다. 쿼리 절에 작은따옴표를 사용하려는 경우 큰따옴표(")를 사용합니다.  
  
-   큰따옴표(") - 쿼리의 매개 변수 부분을 큰따옴표로 묶어야 합니다. 매개 변수 값 자체에 큰따옴표가 포함된 경우에는 이스케이프 문자를 사용합니다. 예를 들면 \"와 같습니다.  
  
-   왼쪽 및 오른쪽 대괄호([ 및 ]) – 이러한 문자는 선행/후행 공백을 나타내는 데 사용됩니다. 예를 들어, "[ 일부 공간 ]"은 선행 공백과 후행 공백이 하나씩 있는 " 일부 공간 " 문자열을 나타냅니다. 이러한 문자 자체가 쿼리 절에 사용되는 경우에는 이스케이프되어야 합니다. 예를 들어 \\[ 및 \\]입니다.  
  
-   슬래시(\\) - 쿼리 절에 사용되는 모든 \는 이스케이프 문자를 사용해야 합니다. 예를 들어 \\\는 쿼리 절에서 \로 평가됩니다.  
  
 슬래시(\\) - 쿼리 절에 사용되는 모든 \는 이스케이프 문자를 사용해야 합니다. 예를 들어 \\\는 쿼리 절에서 \로 평가됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 스트리밍 대상](../../integration-services/data-flow/data-streaming-destination.md)   
 [데이터 스트리밍 대상 구성](../../integration-services/data-flow/configure-data-streaming-destination.md)  
  
  
