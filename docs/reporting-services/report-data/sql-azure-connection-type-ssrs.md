---
title: "SQL Azure 연결 유형 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 02/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c84def6c-e8cf-43d9-9912-098171a7ce79
caps.latest.revision: 17
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d105eb2a7bacb70f93b3237c9a9134695cd13b59
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="sql-azure-connection-type-ssrs"></a>SQL Azure 연결 형식(SSRS)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술을 기반으로 작성된 클라우드 기반의 호스트되는 관계형 데이터베이스입니다. 보고서에 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 의 데이터를 포함하려면 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]유형의 보고서 데이터 원본을 기반으로 하는 데이터 집합이 있어야 합니다. 이 기본 제공 데이터 원본 유형은 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 데이터 확장 프로그램을 기반으로 합니다. 이 데이터 원본 유형을 사용하여 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 연결하고 데이터를 검색할 수 있습니다.  
  
 이 데이터 확장 프로그램은 다중값 매개 변수, 서버 집계 및 연결 문자열과 별개로 관리되는 자격 증명을 지원합니다.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 가 사용자 컴퓨터의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 비슷하기 때문에 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에서 데이터를 가져오는 방법은 몇 가지 예외를 제외하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 가져오는 방법과 동일합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 대한 연결을 열 때 연결 시간 제한을 30초로 설정하세요.  
  
 자세한 내용은 참조 [docs.microsoft.com의 Microsoft Azure SQL 데이터베이스](https://docs.microsoft.com/azure/sql-database/)합니다.  
  
 이 항목의 정보를 사용하여 데이터 원본을 작성할 수 있습니다. 단계별 지침은 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)유형의 보고서 데이터 원본에 기초하는 데이터 집합이 있어야 합니다.  
  
##  <a name="Connection"></a> 연결 문자열  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 연결하면 클라우드의 데이터베이스 개체에 연결하게 됩니다. 온사이트 데이터베이스와 마찬가지로 호스팅되는 데이터베이스에는 여러 테이블, 뷰 및 저장 프로시저가 있는 스키마가 여러 개 있을 수 있으므로 쿼리 디자이너에서 사용할 데이터베이스 개체를 지정합니다. 연결 문자열에 데이터베이스를 지정하지 않을 경우 관리자가 할당한 기본 데이터베이스에 연결됩니다.  
  
 데이터 원본 연결에 사용할 자격 증명 및 연결 정보는 데이터베이스 관리자에게 문의하십시오. 다음 연결 문자열 예에서는 AdventureWorks라는 호스팅되는 예제 데이터베이스를 지정합니다.  
  
```  
Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True;  
```  
  
 또한 **데이터 원본 속성** 대화 상자를 사용하여 사용자 이름과 암호 같은 자격 증명을 제공할 수 있습니다. 그러면 `User Id` 및 `Password` 옵션이 자동으로 연결 문자열에 추가되기 때문에 이러한 옵션을 연결 문자열의 일부로 입력할 필요가 없습니다.  
  
 자세한 내용 및 연결 문자열 예제는 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)을 참조하세요.  
  
##  <a name="Credentials"></a> 자격 증명  
 Windows 인증(통합 보안)이 지원되지 않기 때문에 Windows 인증을 사용하여 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 연결하려고 하면 오류가 발생합니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에서는 SQL Server 인증(사용자 이름 및 암호)만 지원하므로 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 연결할 때마다 자격 증명(로그인 및 암호)을 제공해야 합니다.  
  
 자격 증명에는 데이터베이스에 액세스할 수 있는 권한이 있어야 합니다. 쿼리에 따라 저장 프로시저를 실행하고 테이블 및 뷰에 액세스할 수 있는 권한과 같은 다른 사용 권한이 필요할 수 있습니다. 외부 데이터 원본의 소유자는 사용자에게 필요한 데이터베이스 개체에 대한 읽기 전용 권한을 제공할 수 있는 자격 증명을 구성해야 합니다.  
  
 보고서 작성 클라이언트에서는 다음 옵션을 사용하여 자격 증명을 지정할 수 있습니다.  
  
-   저장된 사용자 이름 및 암호 사용. 보고서 데이터를 포함하는 데이터베이스가 보고서 서버와 다른 경우 발생하는 이중 홉을 협상하려면 Windows 자격 증명을 자격 증명으로 사용하도록 옵션을 선택합니다. 데이터 원본에 연결한 후 인증된 사용자를 가장하도록 선택할 수도 있습니다.  
  
-   자격 증명 필요 없음. 이 옵션을 사용하려면 보고서 서버에서 무인 실행 계정을 구성해야 합니다. 자세한 내용은 msdn.microsoft.com의 [Reporting Services 설명서](http://go.microsoft.com/fwlink/?linkid=121312)에서 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)을 참조하세요.  
  
 자세한 내용은 [데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 또는 [보고서 작성기에 자격 증명 지정](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)을 참조하세요.  
  
  
##  <a name="Query"></a> 쿼리  
 쿼리는 보고서 데이터 집합에 대해 검색할 데이터를 지정합니다. 쿼리 결과 집합의 열은 데이터 집합의 필드 컬렉션을 채웁니다. 쿼리가 여러 결과 집합을 반환할 경우 보고서는 쿼리가 검색한 첫 번째 결과 집합만 처리합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 과(와) [!INCLUDE[ssSDS](../../includes/sssds-md.md)]은(는) 지원되는 데이터베이스 크기 등이 다를 수 있지만 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 대한 쿼리를 작성하는 방법과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 쿼리를 작성하는 방법은 비슷합니다. BACKUP과 같은 일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 지원되지 않지만 이러한 문은 보고서 쿼리에 사용하는 문이 아닙니다. 자세한 내용은 [SQL Server 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)을 참조하세요.  
  
 기본적으로 그래픽 쿼리 디자이너에 나타낼 수 있는 새 쿼리를 만들거나 기존 쿼리를 열 경우 관계형 쿼리 디자이너를 사용할 수 있습니다. 다음과 같은 방법으로 쿼리를 지정할 수 있습니다.  
  
-   대화식으로 쿼리를 작성합니다. 관계형 쿼리 디자이너를 사용합니다. 관계형 쿼리 디자이너는 테이블, 뷰, 저장 프로시저 및 기타 데이터베이스 항목을 데이터베이스 스키마별로 구성하여 계층 구조로 표시합니다. 테이블 또는 뷰에서 열을 선택하거나 저장 프로시저 또는 테이블 반환 함수를 지정합니다. 필터 조건을 지정하여 검색할 데이터 행 수를 제한합니다. 매개 변수 옵션을 설정하여 보고서를 실행할 때 필터를 사용자 지정합니다.  
  
-   쿼리를 입력하거나 붙여넣습니다. 텍스트 기반 쿼리 디자이너를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 텍스트를 직접 입력하거나, 다른 원본에서 쿼리 텍스트를 붙여넣거나, 관계형 쿼리 디자이너를 사용하여 작성할 수 없는 복잡한 쿼리를 입력하거나, 쿼리 기반 식을 입력할 수 있습니다.  
  
-   파일 또는 보고서에서 기존 쿼리를 가져옵니다. 쿼리 디자이너에서 쿼리 **가져오기** 단추를 사용하여 .sql 파일 또는 .rdl 파일을 찾아서 쿼리를 가져옵니다.  
  
 텍스트 기반 쿼리 디자이너에서는 다음과 같은 두 가지 모드를 지원합니다.  
  
-   [텍스트](#QueryText) 데이터 원본에서 데이터를 선택하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 입력합니다.  
  
-   [Stored Procedure](#QueryStoredProcedure) 저장 프로시저 목록에서 선택합니다.  
  
 자세한 내용은 [관계형 쿼리 디자이너 사용자 인터페이스&#40;보고서 작성기&#41;](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md) 및 [텍스트 기반 쿼리 디자이너 사용자 인터페이스&#40;보고서 작성기&#41;](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md)를 참조하세요.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 사용하는 그래픽 쿼리 디자이너는 요약 데이터만 검색하는 쿼리를 작성하는 데 도움이 되는 그룹화 및 집계를 기본적으로 지원합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어 기능은 GROUP BY 절, DISTINCT 키워드 및 SUM, COUNT 등과 같은 집계입니다. 텍스트 기반 쿼리 디자이너는 그룹화 및 집계를 비롯한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어를 완벽하게 지원합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]에 대한 자세한 내용은 msdn.microsoft.com의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?LinkId=141687)에서 [Transact-SQL 참조&#40;데이터베이스 엔진&#41;](../../t-sql/transact-sql-reference-database-engine.md)를 참조하세요.  
  
###  <a name="QueryText"></a> Text 쿼리 유형 사용  
 텍스트 기반 쿼리 디자이너에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 입력하여 데이터 집합의 데이터를 정의합니다. 예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리는 마케팅 지원을 담당하는 모든 직원의 이름을 선택합니다.  
  
```  
SELECT  
  HumanResources.Employee.BusinessEntityID  
  ,HumanResources.Employee.JobTitle  
  ,Person.Person.FirstName  
  ,Person.Person.LastName  
FROM  
  Person.Person  
  INNER JOIN HumanResources.Employee  
    ON Person.Person.BusinessEntityID = HumanResources.Employee.BusinessEntityID  
WHERE HumanResources.Employee.JobTitle = 'Marketing Assistant'   
```  
  
 쿼리를 실행하고 결과 집합을 표시하려면 도구 모음에서 **실행** 단추(**!**)를 클릭합니다.  
  
 이 쿼리에서 매개 변수를 사용하려면 쿼리 매개 변수를 추가합니다. 예를 들어 WHERE 절을 다음과 같이 변경합니다.  
  
```  
WHERE HumanResources.Employee.JobTitle = (@JobTitle)  
```  
  
 쿼리를 실행하면 쿼리 매개 변수에 해당하는 보고서 매개 변수가 자동으로 만들어집니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [쿼리 매개 변수](#Parameters) 를 참조하십시오.  
  
  
###  <a name="QueryStoredProcedure"></a> StoredProcedure 쿼리 유형 사용  
 다음 중 한 가지 방법으로 데이터 집합 쿼리에 대해 저장 프로시저를 지정할 수 있습니다.  
  
-   **데이터 집합 속성** 대화 상자에서 **저장 프로시저** 옵션을 설정합니다. 저장 프로시저 및 테이블 반환 함수 드롭다운 목록에서 원하는 항목을 선택합니다.  
  
-   관계형 쿼리 디자이너에서는 데이터베이스 뷰 창에서 저장 프로시저 또는 테이블 반환 함수를 선택합니다.  
  
-   텍스트 기반 쿼리 디자이너에서는 도구 모음에서 **StoredProcedure** 를 선택합니다.  
  
 저장 프로시저나 테이블 반환 함수를 선택한 후 쿼리를 실행할 수 있습니다. 입력 매개 변수 값을 입력하라는 메시지가 표시됩니다. 쿼리를 실행하면 입력 매개 변수에 해당하는 보고서 매개 변수가 자동으로 만들어집니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [쿼리 매개 변수](#Parameters) 를 참조하십시오.  
  
 저장 프로시저의 경우 첫 번째로 검색된 결과 집합만 지원됩니다. 저장 프로시저에서 여러 개의 결과 집합을 반환할 경우 첫 번째 결과 집합만 사용됩니다.  
  
 저장 프로시저에 기본값을 사용하는 매개 변수가 있는 경우 매개 변수의 값으로 DEFAULT 키워드를 사용하여 해당 값에 액세스할 수 있습니다. 쿼리 매개 변수가 보고서 매개 변수에 연결되어 있으면 사용자가 보고서 매개 변수의 입력란에 DEFAULT라는 단어를 입력하거나 선택할 수 있습니다.  
  
 저장 프로시저에 대한 자세한 내용은 msdn.microsoft.com의 [SQL Server 온라인 설명서](http://go.microsoft.com/fwlink/?linkid=98335) 에서 "저장 프로시저(데이터베이스 엔진)"를 참조하세요.  
  
  
##  <a name="Parameters"></a> 매개 변수  
 쿼리 텍스트에 입력 매개 변수가 있는 쿼리 변수 또는 저장 프로시저가 포함된 경우 데이터 집합에 대한 해당 쿼리 매개 변수와 보고서에 대한 해당 보고서 매개 변수가 자동으로 생성됩니다. 쿼리 텍스트는 각 쿼리 변수에 대한 DECLARE 문을 포함하지 않아야 합니다.  
  
 예를 들어 다음 SQL 쿼리는 **EmpID**라는 보고서 매개 변수를 만듭니다.  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 기본적으로 각 보고서 매개 변수는 데이터 형식이 Text이며 사용 가능한 값의 드롭다운 목록을 제공하기 위해 자동으로 작성된 데이터 집합을 가집니다. 보고서 매개 변수가 만들어진 후에는 기본값을 변경해야 할 수 있습니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)유형의 보고서 데이터 원본을 기반으로 하는 데이터 집합이 있어야 합니다.  
  
  
##  <a name="Remarks"></a> 주의  
  
###### <a name="alternate-data-extensions"></a>대체 데이터 확장 프로그램  
 OLE DB 데이터 원본 유형을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터를 검색할 수도 있습니다. OLE DB를 사용하여 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 연결할 수는 없습니다.  
  
 자세한 내용은 [ODBC 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/odbc-connection-type-ssrs.md)을 참조하세요.  
  
###### <a name="platform-and-version-information"></a>플랫폼 및 버전 정보  
 플랫폼 및 버전 지원에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서에서 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
  
##  <a name="HowTo"></a> 방법 도움말 항목  
 이 섹션에서는 데이터 연결, 데이터 원본 및 데이터 집합을 사용하는 방법을 단계별로 설명합니다.  
  
 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [공유 데이터 집합 또는 포함된 데이터 집합 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [데이터 집합에 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 관련 섹션  
 설명서의 다음 섹션에서는 보고서 데이터에 대한 깊이 있는 개념 정보를 제공하며, 데이터와 관련된 보고서 부분을 정의, 사용자 지정 및 사용하는 방법을 절차적인 측면에서 소개합니다.  
  
 [보고서 데이터 집합&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 보고서의 데이터 액세스에 대한 개요를 제공합니다.  
  
 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 데이터 연결 및 데이터 원본에 대한 정보를 제공합니다.  
  
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 포함된 데이터 집합 및 공유 데이터 집합에 대한 정보를 제공합니다.  
  
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 쿼리에 의해 생성되는 데이터 집합 필드 컬렉션에 대한 정보를 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서에서 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
 각 데이터 확장 프로그램의 플랫폼 및 버전 지원에 대한 자세한 정보를 제공합니다.  
  
  
## <a name="see-also"></a>관련 항목:  
[Docs.microsoft.com의 Microsoft Azure SQL 데이터베이스](https://docs.microsoft.com/azure/sql-database/)  
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
 문의: [Reporting Services 포럼을 시도 하십시오.](http://go.microsoft.com/fwlink/?LinkId=620231)
  
  

