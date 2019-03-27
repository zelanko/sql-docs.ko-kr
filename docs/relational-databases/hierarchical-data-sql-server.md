---
title: 계층적 데이터(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [SQL Server], tables to support
- hierarchyid [Database Engine], concepts
- hierarchical tables [Database Engine]
- SqlHierarchyId
- hierarchyid [Database Engine]
- hierarchical queries [SQL Server], using hierarchyid data type
ms.assetid: 19aefa9a-fbc2-4b22-92cf-67b8bb01671c
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7cf997219044de427ed968ca39928e1449f73e60
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51659488"
---
# <a name="hierarchical-data-sql-server"></a>계층적 데이터(SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  기본 제공 **hierarchyid** 데이터 형식을 사용하면 계층적 데이터를 더 쉽게 저장하고 쿼리할 수 있습니다. **hierarchyid** 는 계층적 데이터의 가장 일반적인 유형인 트리를 표시하는 데 최적화되어 있습니다.  
  
 계층적 데이터는 계층 관계를 통해 서로 관련된 데이터 항목 집합으로 정의됩니다. 계층 관계는 데이터의 한 항목이 다른 항목의 부모인 관계입니다. 데이터베이스에 일반적으로 저장되는 계층적 데이터는 다음과 같습니다.  
  
-   조직 구조  
  
-   파일 시스템  
  
-   프로젝트의 태스크 집합  
  
-   언어 용어의 분류  
  
-   웹 페이지 간 링크의 그래프  
  
 [hierarchyid](../t-sql/data-types/hierarchyid-data-type-method-reference.md) 를 데이터 형식으로 사용하여 계층 구조가 있는 테이블을 만들거나 다른 위치에 저장된 데이터의 계층 구조를 설명할 수 있습니다. [의](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06) hierarchyid 함수 [!INCLUDE[tsql](../includes/tsql-md.md)] 를 사용하면 계층적 데이터를 쿼리하고 관리할 수 있습니다.  
  
##  <a name="keyprops"></a> hierarchyid의 주요 속성  
 **hierarchyid** 데이터 형식의 값은 트리 계층에서의 위치를 나타냅니다. **hierarchyid** 값의 속성은 다음과 같습니다.  
  
-   높은 압축성  
  
     *n* 개 노드가 포함된 트리에서 노드를 나타내는 데 필요한 평균 비트 수는 평균 fanout(노드의 평균 자식 수)에 따라 달라집니다. 작은 fanout(0-7)의 경우 크기는 약 6\*logA*n* 비트입니다. 여기서 A는 평균 fanout입니다. 평균 fanout 수준이 6인 100,000명으로 구성된 조직 계층의 노드는 약 38비트를 사용합니다. 이는 스토리지를 위해 40비트나 5바이트로 반올림됩니다.  
  
-   깊이 우선 순서로 비교  
  
     두 개의 **hierarchyid** 값이 **a**와 **b**인 경우 **a<b**는 깊이 우선 트리 탐색에서 a가 b 앞에 온다는 의미입니다. **hierarchyid** 데이터 형식의 인덱스에는 깊이 우선 순서가 사용되며 깊이 우선 탐색에서 서로 가까이 있는 노드는 서로 가깝게 저장됩니다. 예를 들어 레코드의 자식은 해당 레코드에 인접하게 저장됩니다.  
  
-   임의 삽입 및 삭제 지원  
  
     [GetDescendant](../t-sql/data-types/getdescendant-database-engine.md) 메서드를 사용하면 지정한 노드의 오른쪽, 지정한 노드의 왼쪽 또는 두 형제 사이에 형제를 생성할 수 있습니다. 임의 개수의 노드를 계층에서 삽입하거나 삭제할 때 비교 속성이 유지됩니다. 대부분의 삽입 및 삭제 시 압축성 속성이 유지됩니다. 그러나 두 노드 간 삽입 시에는 약간 덜 압축된 표현으로 hierarchyid 값이 생성됩니다.  
  
  
##  <a name="limits"></a> hierarchyid의 제한 사항  
 **hierarchyid** 데이터 형식의 제한 사항은 다음과 같습니다.  
  
-   **hierarchyid** 형식의 열은 자동으로 트리를 나타내지 않습니다. 애플리케이션에 따라 원하는 행 간 관계가 값에 반영되도록 **hierarchyid** 값이 생성되어 할당됩니다. 일부 애플리케이션에는 다른 테이블에 정의된 계층에서의 위치를 나타내는 **hierarchyid** 형식의 열이 있을 수 있습니다.  
  
-   애플리케이션에 따라 **hierarchyid** 값이 생성되어 할당되는 작업에 대한 동시성이 달리 관리됩니다. 애플리케이션에서 UNIQUE KEY 제약 조건을 사용하거나 자체 논리를 통해 자체적으로 고유성을 적용하지 않는 한 열의 **hierarchyid** 값에 대한 고유성이 보장되지 않습니다.  
  
-   **hierarchyid** 값이 나타내는 계층 관계는 외래 키 관계와 같은 방식으로 적용되지 않습니다. A에 자식 B가 있는 상태에서 A를 삭제하여 B에 존재하지 않는 레코드에 대한 관계가 남게 되는 계층 관계를 만들 수 있으며 이러한 관계가 적절한 경우도 있습니다. 이 동작이 허용되지 않는 경우에는 애플리케이션에서 부모를 삭제하기 전에 하위 항목에 대해 쿼리해야 합니다.  
  
  
##  <a name="alternatives"></a> hierarchyid에 대한 대체 방법을 사용하는 경우  
 계층적 데이터를 나타내는 데 **hierarchyid** 외에 다음 두 가지 방법을 사용할 수 있습니다.  
  
-   부모/자식  
  
-   XML  
  
 **hierarchyid** 는 일반적으로 이러한 대체 방법보다 우수합니다. 그러나 대체 방법을 사용하는 것이 더 나은 상황도 있으며 아래에서는 이에 대해 설명합니다.  
  
### <a name="parentchild"></a>부모/자식  
 부모/자식 방법을 사용하면 각 행에 부모에 대한 참조가 포함됩니다. 다음 테이블에서는 하나의 부모/자식 관계에서 부모 및 자식 행을 포함하는 데 사용되는 일반적인 테이블을 정의합니다.  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE TABLE ParentChildOrg  
   (  
    BusinessEntityID int PRIMARY KEY,  
    ManagerId int REFERENCES ParentChildOrg(BusinessEntityID),  
    EmployeeName nvarchar(50)   
   ) ;  
GO  
```  
  
 일반 작업에 대한 부모/자식과 **hierarchyid** 비교  
  
-   **hierarchyid**를 사용하면 하위 트리 쿼리가 훨씬 더 빨라집니다.  
  
-   **hierarchyid**를 사용하면 직계 하위 항목 쿼리가 약간 더 느려집니다.  
  
-   **hierarchyid**를 사용하면 리프가 아닌 노드 이동이 더 느려집니다.  
  
-   **hierarchyid**를 사용할 경우 리프가 아닌 노드 삽입과 리프 노드의 삽입 및 이동의 복잡성은 동일합니다.  
  
 다음 경우 부모/자식이 더 우수할 수 있습니다.  
  
-   키의 크기가 중요한 경우. 노드 수가 같은 경우 **hierarchyid** 값은 정수 패밀리(**smallint**, **int**, **bigint**) 값보다 크거나 같습니다. **hierarchyid** 에서는 부모/자식 구조를 사용할 때 필요한 공통 테이블 식보다 I/O 및 CPU 복잡성의 효율이 훨씬 증가하므로 이 경우에 한해 부모/자식을 많이 사용합니다.  
  
-   계층의 섹션 간 쿼리를 거의 하지 않는 쿼리의 경우. 즉, 쿼리가 일반적으로 계층의 단일 지점만 다루는 경우입니다. 이러한 경우 같은 위치에 배치하는 작업이 중요하지 않습니다. 예를 들어 조직 테이블이 개별 직원에 대한 급여를 처리하는 데에만 사용되는 경우 부모/자식이 더 우수합니다.  
  
-   리프가 아닌 하위 트리가 자주 이동하며 성능이 매우 중요한 경우. 부모/자식 표현의 경우 한 계층에서 한 행의 위치를 변경하면 단일 행에 영향을 줍니다. 그러나 **hierarchyid** 사용 시 한 행의 위치를 변경하면 *n* 개의 행에 영향을 줍니다. 여기서 *n* 은 이동하는 하위 트리의 노드 수입니다.  
  
     리프가 아닌 하위 트리가 자주 이동하며 성능이 중요하지만 대부분의 이동이 잘 정의된 계층 수준에서 발생하는 경우에는 상위 수준과 하위 수준을 두 개의 계층으로 분할하십시오. 이렇게 하면 모든 트리가 상위 계층의 리프 수준으로 이동됩니다. 예를 들어 서비스에서 호스팅하는 웹 사이트 계층의 경우 사이트에는 계층으로 정렬된 많은 페이지가 있습니다. 호스팅된 사이트는 사이트 계층의 다른 위치로 이동될 수 있지만 하위 페이지는 거의 다시 정렬되지 않습니다. 이는 다음을 통해 나타낼 수 있습니다.  
  
    ```  
    CREATE TABLE HostedSites   
       (  
        SiteId hierarchyid, PageId hierarchyid  
       ) ;  
    GO  
    ```  
  
  
### <a name="xml"></a>XML  
 XML 문서는 트리이므로 단일 XML 데이터 형식 인스턴스가 전체 계층을 나타낼 수 있습니다. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] when an XML hierarchyid 함수dex is created, **hierarchyid** values are used hierarchyid 함수ternally to represent the position hierarchyid 함수 the hierarchy.  
  
 다음 경우 XML 데이터 형식이 더 우수할 수 있습니다.  
  
-   전체 계층이 항상 저장되고 검색되는 경우  
  
-   애플리케이션에서 데이터를 XML 형식으로 사용하는 경우  
  
-   조건자 검색이 매우 제한되어 있으며 성능이 중요하지 않은 경우  
  
 예를 들어 애플리케이션에서 여러 조직을 추적하고 전체 조직 계층을 항상 저장 및 검색하며 단일 조직만 쿼리하지 않는 경우 다음 형식의 테이블이 적합할 수 있습니다.  
  
```  
CREATE TABLE XMLOrg   
    (  
    Orgid int,  
    Orgdata xml  
    ) ;  
GO  
```  
  
  
##  <a name="indexing"></a> 계층적 데이터의 인덱싱 전략  
 계층적 데이터의 인덱싱 방법에는 두 가지가 있습니다.  
  
-   **깊이 우선**  
  
     깊이 우선 인덱스에서는 하위 트리의 행이 서로 가깝게 저장됩니다. 예를 들어 한 관리자를 통해 보고하는 모든 직원은 해당 관리자의 레코드에 가깝게 저장됩니다.  
  
     깊이 우선 인덱스에서는 노드의 하위 트리에 있는 모든 노드가 같은 위치에 배치됩니다. 따라서 "이 폴더 및 해당 하위 폴더에서 모든 파일 찾기"와 같은 하위 트리에 대한 쿼리에 답하는 데에는 깊이 우선 인덱스가 효율적입니다.  
  
-   **너비 우선**  
  
     너비 우선은 계층의 각 수준에 행을 함께 저장합니다. 예를 들어 같은 관리자에게 직접 보고하는 직원의 레코드는 서로 가깝게 저장됩니다.  
  
     너비 우선 인덱스에서는 노드의 모든 직계 자식이 같은 위치에 배치됩니다. 따라서 "이 관리자에게 직접 보고하는 모든 직원 찾기"와 같은 인접한 자식에 대한 쿼리에 답하는 데에는 너비 우선 인덱스가 효율적입니다.  
  
 깊이 우선을 사용할 것인지, 너비 우선을 사용할 것인지 또는 둘 다를 사용할 것인지 여부와 클러스터링 키(있는 경우)를 만들 인덱스는 위의 쿼리 형식에 대한 상대적 중요도와 SELECT 및 DML 작업의 상대적 중요도에 따라 달라집니다. 인덱싱 방법에 대한 자세한 예는 [Tutorial: Using the hierarchyid Data Type](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md)을 참조하십시오.  
  
  
### <a name="creating-indexes"></a>인덱스 만들기  
 GetLevel() 메서드를 사용하여 너비 우선 순서를 만들 수 있습니다. 다음 예에서는 너비 우선 인덱스와 깊이 우선 인덱스를 모두 만듭니다.  
  
```wmimof  
USE AdventureWorks2012 ;   
GO  
  
CREATE TABLE Organization  
   (  
    BusinessEntityID hierarchyid,  
    OrgLevel as BusinessEntityID.GetLevel(),   
    EmployeeName nvarchar(50) NOT NULL  
   ) ;  
GO  
  
CREATE CLUSTERED INDEX Org_Breadth_First   
ON Organization(OrgLevel,BusinessEntityID) ;  
GO  
  
CREATE UNIQUE INDEX Org_Depth_First   
ON Organization(BusinessEntityID) ;  
GO  
```  
  
  
## <a name="examples"></a>예  
  
### <a name="simple-example"></a>간단한 예  
 다음 예제는 시작하는 데 도움을 주기 위해 의도적으로 단순화된 것입니다. 먼저 일부 지리 데이터를 보유하는 테이블을 만듭니다.  
  
```  
CREATE TABLE SimpleDemo  
(Level hierarchyid NOT NULL,  
Location nvarchar(30) NOT NULL,  
LocationType nvarchar(9) NULL);  
```  
  
 이제 일부 대륙, 국가, 주 및 도시에 대한 데이터를 삽입합니다.  
  
```  
INSERT SimpleDemo  
VALUES   
('/1/', 'Europe', 'Continent'),  
('/2/', 'South America', 'Continent'),  
('/1/1/', 'France', 'Country'),  
('/1/1/1/', 'Paris', 'City'),  
('/1/2/1/', 'Madrid', 'City'),  
('/1/2/', 'Spain', 'Country'),  
('/3/', 'Antarctica', 'Continent'),  
('/2/1/', 'Brazil', 'Country'),  
('/2/1/1/', 'Brasilia', 'City'),  
('/2/1/2/', 'Bahia', 'State'),  
('/2/1/2/1/', 'Salvador', 'City'),  
('/3/1/', 'McMurdo Station', 'City');  
```  
  
 데이터를 선택하여 Level 데이터를 이해하기 쉬운 텍스트 값으로 변환하는 열을 추가합니다. 또한 이 쿼리는 **hierarchyid** 데이터 형식을 기준으로 결과를 정렬합니다.  
  
```  
SELECT CAST(Level AS nvarchar(100)) AS [Converted Level], *   
FROM SimpleDemo ORDER BY Level;  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
```  
Converted Level  Level     Location         LocationType  
/1/              0x58      Europe           Continent  
/1/1/            0x5AC0    France           Country  
/1/1/1/          0x5AD6    Paris            City  
/1/2/            0x5B40    Spain            Country  
/1/2/1/          0x5B56    Madrid           City  
/2/              0x68      South America    Continent  
/2/1/            0x6AC0    Brazil           Country  
/2/1/1/          0x6AD6    Brasilia         City  
/2/1/2/          0x6ADA    Bahia            State  
/2/1/2/1/        0x6ADAB0  Salvador         City  
/3/              0x78      Antarctica       Continent  
/3/1/            0x7AC0    McMurdo Station  City  
```  
  
 계층이 내부적으로 일관성이 없어도 계층의 구조는 유효합니다. Bahia는 유일한 주이며 도시 Brasilia의 피어로 계층에 나타납니다. 마찬가지로 McMurdo Station에는 부모 국가가 없습니다. 사용자는 이 유형의 계층이 사용하기에 적합한지 결정해야 합니다.  
  
 또 다른 행을 추가하고 결과를 선택합니다.  
  
```  
INSERT SimpleDemo  
VALUES ('/1/3/1/', 'Kyoto', 'City'), ('/1/3/1/', 'London', 'City');  
SELECT CAST(Level AS nvarchar(100)) AS [Converted Level], * FROM SimpleDemo ORDER BY Level;  
```  
  
 여기에서는 보다 가능한 문제를 보여 줍니다. Kyoto는 부모 수준 `/1/3/1/` 이 없어도 `/1/3/`수준으로 삽입될 수 있습니다. 그리고 London과 Kyoto의 **hierarchyid**값은 동일합니다. 여기에서도 사용자가 이 유형의 계층이 사용하기에 적합한지 결정해야 하고 사용하기에 적합하지 않은 값을 차단해야 합니다.  
  
 또한 이 테이블에서는 계층의 최상위( `'/'`)를 사용하지 않았습니다. 계층의 최상위는 모든 대륙의 공통 부모가 없기 때문에 생략되었습니다. 전체 지구를 추가하여 계층의 최상위를 추가할 수 있습니다.  
  
```  
INSERT SimpleDemo  
VALUES ('/', 'Earth', 'Planet');  
```  
  
##  <a name="tasks"></a> 관련 태스크  
  
###  <a name="migrating"></a> 부모/자식에서 hierarchyid로 마이그레이션  
 대부분의 트리는 부모/자식을 사용하여 표현됩니다. 부모/자식 구조를 **hierarchyid** 를 사용하는 테이블로 마이그레이션하는 가장 쉬운 방법은 임시 열이나 임시 테이블을 사용하여 계층의 각 수준에서 노드 수를 추적하는 것입니다. 부모/자식 테이블 마이그레이션의 예제는 [자습서: hierarchyid 데이터 형식 사용](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md)의 1단원을 참조하세요.  
  
  
###  <a name="BKMK_ManagingTrees"></a> hierarchyid를 사용하여 트리 관리  
 **hierarchyid** 열이 반드시 트리를 나타내는 것은 아니지만 응용 프로그램에서 손쉽게 해당 열이 트리를 나타내도록 만들 수 있습니다.  
  
-   새 값을 생성할 때 다음 중 하나를 수행합니다.  
  
    -   부모 행의 마지막 자식 번호를 추적합니다.  
  
    -   마지막 자식을 컴퓨팅합니다. 이 작업을 효율적으로 수행하려면 너비 우선 인덱스가 필요합니다.  
  
-   클러스터링 키의 일부 등으로 열에 대한 고유 인덱스를 만들어 고유성을 강제 적용합니다. 고유 값이 삽입되게 하려면 다음 중 하나를 수행합니다.  
  
    -   고유 키 위반 오류를 검색하고 다시 시도합니다.  
  
    -   새 자식 노드 각각의 고유성을 확인하고 직렬화 가능 트랜잭션의 일부로 해당 노드를 삽입합니다.  
  
  
#### <a name="example-using-error-detection"></a>오류 검색 사용 예  
 다음 예제의 샘플 코드는 새 자식 **EmployeeId** 값을 계산한 다음 키 위반을 검색하고 **INS_EMP** 표식으로 돌아와 새 행에 대해 **EmployeeId** 값을 다시 계산합니다.  
  
```  
USE AdventureWorks ;  
GO  
  
CREATE TABLE Org_T1  
   (  
    EmployeeId hierarchyid PRIMARY KEY,  
    OrgLevel AS EmployeeId.GetLevel(),  
    EmployeeName nvarchar(50)   
   ) ;  
GO  
  
CREATE INDEX Org_BreadthFirst ON Org_T1(OrgLevel, EmployeeId)  
GO  
  
CREATE PROCEDURE AddEmp(@mgrid hierarchyid, @EmpName nvarchar(50) )   
AS  
BEGIN  
    DECLARE @last_child hierarchyid  
INS_EMP:   
    SELECT @last_child = MAX(EmployeeId) FROM Org_T1   
    WHERE EmployeeId.GetAncestor(1) = @mgrid  
INSERT Org_T1 (EmployeeId, EmployeeName)  
SELECT @mgrid.GetDescendant(@last_child, NULL), @EmpName   
-- On error, return to INS_EMP to recompute @last_child  
IF @@error <> 0 GOTO INS_EMP   
END ;  
GO  
```  
  
  
#### <a name="example-using-a-serializable-transaction"></a>직렬화 가능 트랜잭션 사용 예  
 **Org_BreadthFirst** 인덱스를 사용하면 **@last_child** 확인 시 범위 검색이 사용됩니다. 애플리케이션에서 확인할 수 있는 다른 오류 상황뿐만 아니라 삽입 후의 중복 키 위반은 ID가 같은 여러 직원을 추가하려고 했음을 나타내므로 **@last_child** 를 다시 계산해야 합니다. 다음 코드에서는 직렬화 가능 트랜잭션과 너비 우선 인덱스를 사용하여 새 노드 값을 컴퓨팅합니다.  
  
```  
CREATE TABLE Org_T2  
    (  
    EmployeeId hierarchyid PRIMARY KEY,  
    LastChild hierarchyid,   
    EmployeeName nvarchar(50)   
    ) ;  
GO  
  
CREATE PROCEDURE AddEmp(@mgrid hierarchyid, @EmpName nvarchar(50))   
AS  
BEGIN  
DECLARE @last_child hierarchyid  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
BEGIN TRANSACTION   
  
UPDATE Org_T2   
SET @last_child = LastChild = EmployeeId.GetDescendant(LastChild,NULL)  
WHERE EmployeeId = @mgrid  
INSERT Org_T2 (EmployeeId, EmployeeName)   
    VALUES(@last_child, @EmpName)  
COMMIT  
END ;  
```  
  
 다음 코드에서는 테이블을 3개의 행으로 채우고 결과를 반환합니다.  
  
```  
INSERT Org_T2 (EmployeeId, EmployeeName)   
    VALUES(hierarchyid::GetRoot(), 'David') ;  
GO  
AddEmp 0x , 'Sariya'  
GO  
AddEmp 0x58 , 'Mary'  
GO  
SELECT * FROM Org_T2  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
```  
EmployeeId LastChild EmployeeName  
---------- --------- ------------  
0x        0x58       David  
0x58      0x5AC0     Sariya  
0x5AC0    NULL       Mary  
```  
  
  
###  <a name="BKMK_EnforcingTrees"></a> 트리 강제 적용  
 위 예에서는 애플리케이션에서 트리가 유지되도록 하는 방법을 보여 줍니다. 제약 조건을 사용하여 트리를 강제 적용하려면 기본 키 ID에 FOREIGN KEY 제약 조건을 다시 적용하여 각 노드의 부모를 정의하는 계산 열을 만듭니다.  
  
```  
CREATE TABLE Org_T3  
(  
   EmployeeId hierarchyid PRIMARY KEY,  
   ParentId AS EmployeeId.GetAncestor(1) PERSISTED    
      REFERENCES Org_T3(EmployeeId),  
   LastChild hierarchyid,   
   EmployeeName nvarchar(50)  
)  
GO  
```  
  
 계층적 트리를 유지하도록 트러스트되지 않은 코드에 해당 테이블에 대한 직접 DML 액세스가 있는 경우 관계를 이러한 방법으로 강제 적용하는 것이 좋습니다. 하지만 모든 DML 작업에서 제약 조건을 확인해야 하므로 이 방법은 성능을 저하시킬 수 있습니다.  
  
  
###  <a name="findclr"></a> CLR을 사용하여 상위 항목 찾기  
 한 계층의 두 노드를 사용하는 일반적인 작업에는 수준이 가장 낮은 공통 상위 항목을 찾는 작업이 있습니다. [!INCLUDE[tsql](../includes/tsql-md.md)] hierarchyid **형식을** 또는 CLR에서 모두 사용할 수 있으므로 두 방법을 모두 사용하여 이러한 작업을 코드로 작성할 수 있습니다. 그러나 성능이 향상되는 CLR을 사용하는 것이 좋습니다.  
  
 다음 CLR 코드를 사용하여 상위 항목을 나열하고 수준이 가장 낮은 공통 상위 항목을 찾을 수 있습니다.  
  
```  
using System;  
using System.Collections;  
using System.Text;  
using Microsoft.SqlServer.Server;  
using Microsoft.SqlServer.Types;  
  
public partial class HierarchyId_Operations  
{  
    [SqlFunction(FillRowMethodName = "FillRow_ListAncestors")]  
    public static IEnumerable ListAncestors(SqlHierarchyId h)  
    {  
        while (!h.IsNull)  
        {  
            yield return (h);  
            h = h.GetAncestor(1);  
        }  
    }  
    public static void FillRow_ListAncestors(Object obj, out SqlHierarchyId ancestor)  
    {  
        ancestor = (SqlHierarchyId)obj;  
    }  
  
    public static HierarchyId CommonAncestor(SqlHierarchyId h1, HierarchyId h2)  
    {  
        while (!h1.IsDescendant(h2))  
            h1 = h1.GetAncestor(1);  
  
        return h1;  
    }  
}  
```  
  
 다음 **예제에서** ListAncestor **및** CommonAncestor [!INCLUDE[tsql](../includes/tsql-md.md)] 메서드를 사용하려면 다음과 유사한 코드를 실행하여 **에서 DLL을 빌드하고** HierarchyId_Operations [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 어셈블리를 만듭니다.  
  
```  
CREATE ASSEMBLY HierarchyId_Operations   
FROM '<path to DLL>\ListAncestors.dll'  
GO  
```  
  
  
###  <a name="ancestors"></a> 상위 항목 나열  
 노드의 상위 항목 목록을 만드는 것은 조직에서의 위치 표시와 같은 일반적인 작업입니다. 이를 수행할 수 있는 한 가지 방법은 위에 정의된 **HierarchyId_Operations** 클래스를 사용하는 테이블 반환 함수를 사용하는 것입니다.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)]사용:  
  
```  
CREATE FUNCTION ListAncestors (@node hierarchyid)  
RETURNS TABLE (node hierarchyid)  
AS  
EXTERNAL NAME HierarchyId_Operations.HierarchyId_Operations.ListAncestors  
GO  
```  
  
 사용 예:  
  
```  
DECLARE @h hierarchyid  
SELECT @h = OrgNode   
FROM HumanResources.EmployeeDemo    
WHERE LoginID = 'adventure-works\janice0' -- /1/1/5/2/  
  
SELECT LoginID, OrgNode.ToString() AS LogicalNode  
FROM HumanResources.EmployeeDemo AS ED  
JOIN ListAncestors(@h) AS A   
   ON ED.OrgNode = A.Node  
GO  
```  
  
  
###  <a name="lowestcommon"></a> 수준이 가장 낮은 공통 상위 항목 찾기  
 위에 정의된 **HierarchyId_Operations** 클래스를 통해 다음 [!INCLUDE[tsql](../includes/tsql-md.md)] 함수를 만들어 한 계층의 두 노드를 사용하는 수준이 가장 낮은 공통 상위 항목을 찾습니다.  
  
```  
CREATE FUNCTION CommonAncestor (@node1 hierarchyid, @node2 hierarchyid)  
RETURNS hierarchyid  
AS  
EXTERNAL NAME HierarchyId_Operations.HierarchyId_Operations.CommonAncestor  
GO  
```  
  
 사용 예:  
  
```  
DECLARE @h1 hierarchyid, @h2 hierarchyid  
  
SELECT @h1 = OrgNode   
FROM  HumanResources.EmployeeDemo   
WHERE LoginID = 'adventure-works\jossef0' -- Node is /1/1/3/  
  
SELECT @h2 = OrgNode   
FROM HumanResources.EmployeeDemo    
WHERE LoginID = 'adventure-works\janice0' -- Node is /1/1/5/2/  
  
SELECT OrgNode.ToString() AS LogicalNode, LoginID   
FROM HumanResources.EmployeeDemo    
WHERE OrgNode = dbo.CommonAncestor(@h1, @h2) ;  
```  
  
 결과 노드는 /1/1/입니다.  
  
  
###  <a name="BKMK_MovingSubtrees"></a> 하위 트리 이동  
 다른 일반적인 작업은 하위 트리를 이동하는 것입니다. 아래 절차에서는 **@oldMgr** 의 하위 트리를 사용하여 이 하위 트리( **@oldMgr**포함)를 **@newMgr**를 사용하면 하위 트리 쿼리가 훨씬 더 빨라집니다.  
  
```  
CREATE PROCEDURE MoveOrg(@oldMgr nvarchar(256), @newMgr nvarchar(256) )  
AS  
BEGIN  
DECLARE @nold hierarchyid, @nnew hierarchyid  
SELECT @nold = OrgNode FROM HumanResources.EmployeeDemo WHERE LoginID = @oldMgr ;  
  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
BEGIN TRANSACTION  
SELECT @nnew = OrgNode FROM HumanResources.EmployeeDemo WHERE LoginID = @newMgr ;  
  
SELECT @nnew = @nnew.GetDescendant(max(OrgNode), NULL)   
FROM HumanResources.EmployeeDemo WHERE OrgNode.GetAncestor(1)=@nnew ;  
  
UPDATE HumanResources.EmployeeDemo    
SET OrgNode = OrgNode.GetReparentedValue(@nold, @nnew)  
WHERE OrgNode.IsDescendantOf(@nold) = 1 ;  
  
COMMIT TRANSACTION  
END ;  
GO  
```  
  
  
## <a name="see-also"></a>참고 항목  
 [hierarchyid 데이터 형식 메서드 참조](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)   
 [Tutorial: Using the hierarchyid Data Type](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md)   
 [hierarchyid&#40;Transact-SQL&#41;](../t-sql/data-types/hierarchyid-data-type-method-reference.md)  
  
  
