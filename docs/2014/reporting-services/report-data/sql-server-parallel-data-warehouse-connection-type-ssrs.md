---
title: SQL Server 병렬 데이터 웨어하우스 연결 형식(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 3925fd3d-2aa1-4768-96ad-cfc2c0ba9283
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b0c8ada8e10ef0f1bc47e1655521acced6f0aa41
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106972"
---
# <a name="sql-server-parallel-data-warehouse-connection-type-ssrs"></a>SQL Server 병렬 데이터 웨어하우스 연결 형식(SSRS)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] 는 대규모 병렬 처리를 통해 성능 및 확장성을 제공 하는 확장 가능한 데이터 웨어하우스 어플라이언스입니다. [!INCLUDE[ssDW](../../../includes/ssdw-md.md)]는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 분산 처리 및 데이터 저장을 위해 데이터베이스를 사용 합니다.  
  
 이 어플라이언스는 고유한 인스턴스의 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]를 실행하는 각 노드로 구성된 여러 물리적 노드에서 큰 데이터베이스 테이블을 분할합니다. 보고서는 보고서 데이터를 검색하기 위해 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 에 연결될 때 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 어플라이언스에서 쿼리 처리를 관리하는 제어 노드에 연결됩니다. 연결이 설정되면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 환경이 아니더라도 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 인스턴스를 사용할 때와 아무런 차이가 없습니다.  
  
 보고서 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 에의 데이터를 포함 하려면 병렬 데이터 웨어하우스 유형의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 보고서 데이터 원본을 기반으로 하는 데이터 집합이 있어야 합니다. 이 기본 제공 데이터 원본 유형은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 병렬 데이터 웨어하우스 데이터 확장 프로그램을 기반으로 합니다. 이 데이터 원본 유형을 사용하여 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)]에 연결하고 데이터를 검색할 수 있습니다.  
  
 이 데이터 확장 프로그램은 다중값 매개 변수, 서버 집계 및 연결 문자열과 별개로 관리되는 자격 증명을 지원합니다.  
  
 자세한 내용은 [SQL Server 2008 R2 병렬 데이터 웨어하우스](https://go.microsoft.com/fwlink/?LinkId=150895)웹 사이트를 참조하십시오.  
  
 이 항목의 정보를 사용하여 데이터 원본을 작성할 수 있습니다. 단계별 지침은 [데이터 연결이 나 데이터 원본 &#40;추가 및 확인 보고서 작성기 및 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)를 참조 하세요.  
  
##  <a name="Connection"></a>연결 문자열  
 
  [!INCLUDE[ssDW](../../../includes/ssdw-md.md)]에 연결할 때 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 어플라이언스 내의 데이터베이스 개체에 연결됩니다. 쿼리 디자이너에서 사용할 데이터베이스 개체를 지정합니다. 연결 문자열에 데이터베이스를 지정하지 않을 경우 관리자가 할당한 기본 데이터베이스에 연결됩니다. 데이터 원본 연결에 사용할 자격 증명 및 연결 정보는 데이터베이스 관리자에게 문의하십시오. 다음 연결 문자열 예에서는 ** 어플라이언스에 있는 **CustomerSales[!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 예제 데이터베이스를 지정합니다.  
  
```  
HOST=<IP address>; database= CustomerSales; port=<port>  
```  
  
 또한 **데이터 원본 속성** 대화 상자를 사용하여 사용자 이름 및 암호와 같은 자격 증명을 제공합니다. `User Id` 및 `Password` 옵션은 연결 문자열에 자동으로 추가되므로 연결 문자열의 일부로 입력할 필요가 없습니다. 또한 사용자 인터페이스에서는 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 어플라이언스에 있는 제어 노드의 IP 주소 및 포트 번호를 지정할 수 있는 옵션이 제공됩니다. 기본적으로 포트는 17000입니다. 포트는 관리자가 구성할 수 있으며 연결 문자열에서 다른 포트 번호를 사용할 수도 있습니다.  
  
 연결 문자열 예제에 대한 자세한 내용은 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](../data-connections-data-sources-and-connection-strings-in-report-builder.md)을 참조하세요.  
  
##  <a name="Credentials"></a>자격 증명  
 
  [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 는 사용자 이름과 암호를 구현 및 저장하기 위한 고유한 보안 기술을 제공합니다. Windows 인증은 사용할 수 없습니다. Windows 인증을 사용하여 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 에 연결하려고 하면 오류가 발생합니다.  
  
 자격 증명에는 데이터베이스에 액세스할 수 있는 권한이 있어야 합니다. 쿼리에 따라 테이블 및 뷰에 액세스할 수 있는 권한과 같은 다른 사용 권한이 필요할 수 있습니다. 외부 데이터 원본의 소유자는 사용자에게 필요한 데이터베이스 개체에 대한 읽기 전용 권한을 제공할 수 있는 자격 증명을 구성해야 합니다.  
  
 보고서 작성 클라이언트에서는 다음 옵션을 사용하여 자격 증명을 지정할 수 있습니다.  
  
-   저장된 사용자 이름 및 암호 사용. 보고서 데이터를 포함하는 데이터베이스가 보고서 서버와 다른 경우 발생하는 이중 홉을 협상하려면 Windows 자격 증명을 자격 증명으로 사용하도록 옵션을 선택합니다. 데이터 원본에 연결한 후 인증된 사용자를 가장하도록 선택할 수도 있습니다.  
  
-   자격 증명 필요 없음 이 옵션을 사용하려면 보고서 서버에서 무인 실행 계정을 구성해야 합니다. 자세한 내용은 msdn.microsoft.com의 [Reporting Services 설명서](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)에서 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](https://go.microsoft.com/fwlink/?linkid=121312)을 참조하세요.  
  
 자세한 내용은 [Reporting Services의 데이터 연결, 데이터 원본 및 연결 문자열](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) 을 참조 하거나 [보고서 작성기에서 자격 증명을 지정](../specify-credentials-in-report-builder.md)하세요.  

##  <a name="Query"></a>쿼리  
 쿼리는 보고서 데이터 세트에 대해 검색할 데이터를 지정합니다.  
  
 쿼리 결과 집합의 열은 데이터 세트의 필드 컬렉션을 채웁니다. 쿼리가 여러 결과 집합을 반환할 경우 보고서는 쿼리가 검색한 첫 번째 결과 집합만 처리합니다. 기본적으로 그래픽 쿼리 디자이너에 나타낼 수 있는 새 쿼리를 만들거나 기존 쿼리를 열 경우 관계형 쿼리 디자이너를 사용할 수 있습니다. 다음과 같은 방법으로 쿼리를 지정할 수 있습니다.  
  
-   대화식으로 쿼리를 작성합니다. 관계형 쿼리 디자이너를 사용합니다. 관계형 쿼리 디자이너는 테이블, 뷰 및 기타 데이터베이스 항목을 데이터베이스 스키마별로 구성하여 계층 구조로 표시합니다. 테이블이나 뷰에서 열을 선택합니다. 필터 조건, 그룹 및 집계를 지정하여 검색할 데이터 행 수를 제한합니다. 매개 변수 옵션을 설정하여 보고서를 실행할 때 필터를 사용자 지정합니다.  
  
-   쿼리를 입력하거나 붙여넣습니다. 텍스트 기반 쿼리 디자이너를 사용하여 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 텍스트를 직접 입력하거나, 다른 원본에서 쿼리 텍스트를 붙여넣거나, 관계형 쿼리 디자이너를 사용하여 작성할 수 없는 복잡한 쿼리를 입력하거나, 쿼리 기반 식을 입력할 수 있습니다.  
  
-   파일 또는 보고서에서 기존 쿼리를 가져옵니다. 쿼리 디자이너에서 쿼리 **가져오기** 단추를 사용하여 .sql 파일 또는 .rdl 파일을 찾아서 쿼리를 가져옵니다.  
  
 자세한 내용은 [관계형 쿼리 디자이너 사용자 인터페이스&#40;보고서 작성기&#41;](relational-query-designer-user-interface-report-builder.md) 및 [텍스트 기반 쿼리 디자이너 사용자 인터페이스&#40;보고서 작성기&#41;](text-based-query-designer-user-interface-report-builder.md)를 참조하세요.  
  
 텍스트 기반 쿼리 디자이너는 [텍스트 모드](#QueryText) 를 지원하며 이 모드에서는 데이터 원본의 데이터를 선택하는 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 명령을 입력합니다.  
  
-   [본문](#QueryText)  
  
 
  [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 을 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 와 함께 사용하고 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 을 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]와 함께 사용합니다. 두 개의 SQL 언어는 매우 비슷합니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 원본 연결 형식에 맞게 작성된 쿼리는 일반적으로 [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] 데이터 원본 연결 형식에 사용할 수 있습니다.  
  
 
  [!INCLUDE[ssDW](../../../includes/ssdw-md.md)]등과 같은 데이터 웨어하우스를 비롯한 큰 데이터베이스에서 보고서 데이터를 검색하는 쿼리는 쿼리가 반환하는 행 수를 줄이기 위해 데이터를 집계 및 요약하지 않을 경우 매우 많은 수의 행을 가진 결과 집합을 생성할 수 있습니다. 그래픽 또는 텍스트 기반 쿼리 디자이너를 사용하여 집계 및 그룹화를 포함하는 쿼리를 작성할 수 있습니다.  
  
 
  [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 은 데이터를 요약하기 위해 쿼리 디자이너가 제공하는 집계, 절 및 키워드를 지원합니다.  
  
 
  [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 에서 사용하는 그래픽 쿼리 디자이너는 요약 데이터만 검색하는 쿼리를 작성하는 데 도움이 되는 그룹화 및 집계를 기본적으로 지원합니다. 
  [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 언어 기능은 GROUP BY 절, DISTINCT 키워드 및 SUM, COUNT 등과 같은 집계입니다. 텍스트 기반 쿼리 디자이너는 그룹화 및 집계를 비롯한 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 언어를 완벽하게 지원합니다.  
  
 
  [!INCLUDE[tsql](../../../includes/tsql-md.md)]에 대한 자세한 내용은 msdn.microsoft.com의 [](/sql/t-sql/language-reference)온라인 설명서에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [Transact-SQL 참조&#40;데이터베이스 엔진&#41;](https://go.microsoft.com/fwlink/?LinkId=141687)를 참조하세요.  
  
###  <a name="QueryText"></a>쿼리 유형 텍스트 사용  
 텍스트 기반 쿼리 디자이너에서는 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 명령을 입력하여 데이터 세트의 데이터를 정의합니다. 
  [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 에서 데이터를 검색하기 위해 사용하는 쿼리는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 애플리케이션 내에서 실행되지 않는 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 의 인스턴스에서 데이터를 검색하기 위해 사용하는 쿼리와 동일합니다. 예를 들어 다음 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 쿼리는 마케팅 지원을 담당하는 모든 직원의 이름을 선택합니다.  
  
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
  
 `WHERE HumanResources.Employee.JobTitle = (@JobTitle)`  
  
 쿼리를 실행하면 쿼리 매개 변수에 해당하는 보고서 매개 변수가 자동으로 만들어집니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [쿼리 매개 변수](#Parameters) 를 참조하십시오.  

##  <a name="Parameters"></a> 매개 변수  
 쿼리 텍스트에 입력 매개 변수가 있는 쿼리 변수 또는 저장 프로시저가 포함된 경우 데이터 세트에 대한 해당 쿼리 매개 변수와 보고서에 대한 해당 보고서 매개 변수가 자동으로 생성됩니다. 쿼리 텍스트는 각 쿼리 변수에 대한 DECLARE 문을 포함하지 않아야 합니다.  
  
 예를 들어 다음 SQL 쿼리는 `EmpID`라는 보고서 매개 변수를 만듭니다.  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 기본적으로 각 보고서 매개 변수는 데이터 형식이 Text이며 사용 가능한 값의 드롭다운 목록을 제공하기 위해 자동으로 작성된 데이터 세트를 가집니다. 보고서 매개 변수가 만들어진 후에는 기본값을 변경해야 할 수 있습니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)에 대해 자세히 알아봅니다.  

##  <a name="Remarks"></a> 주의 사항  
  
###### <a name="platform-and-version-information"></a>플랫폼 및 버전 정보  
 플랫폼 및 버전 지원에 대한 자세한 내용은 [](../create-deploy-and-manage-mobile-and-paginated-reports.md)온라인 설명서[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의  설명서에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](https://go.microsoft.com/fwlink/?linkid=121312).  

##  <a name="HowTo"></a> 방법 도움말 항목  
 이 섹션에서는 데이터 연결, 데이터 원본 및 데이터 세트를 사용하는 방법을 단계별로 설명합니다.  
  
 [데이터 연결이 나 데이터 원본 &#40;보고서 작성기 및 SSRS를 추가 하 고 확인&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [공유 데이터 집합 또는 포함 된 데이터 집합 &#40;보고서 작성기 및 SSRS를 만듭니다&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [데이터 집합 &#40;보고서 작성기 및 SSRS에 필터를 추가&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  

##  <a name="Related"></a>관련 섹션  
 설명서의 다음 섹션에서는 보고서 데이터에 대한 깊이 있는 개념 정보를 제공하며, 데이터와 관련된 보고서 부분을 정의, 사용자 지정 및 사용하는 방법을 절차적인 측면에서 소개합니다.  
  
 [보고서 &#40;보고서 작성기 및 SSRS&#41;에 데이터를 추가 합니다.](report-datasets-ssrs.md)  
 보고서의 데이터 액세스에 대한 개요를 제공합니다.  
  
 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 데이터 연결 및 데이터 원본에 대한 정보를 제공합니다.  
  
 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 포함된 데이터 세트 및 공유 데이터 세트에 대한 정보를 제공합니다.  
  
 [데이터 세트 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 쿼리에 의해 생성되는 데이터 세트 필드 컬렉션에 대한 정보를 제공합니다.  
  
 [Reporting Services &#40;SSRS에서 지 원하는 데이터 원본은](../create-deploy-and-manage-mobile-and-paginated-reports.md) 온라인 설명서 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 의 설명서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [](https://go.microsoft.com/fwlink/?linkid=121312)에서&#41;.  
 각 데이터 확장 프로그램의 플랫폼 및 버전 지원에 대한 자세한 정보를 제공합니다.  

## <a name="see-also"></a>참고 항목  
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
