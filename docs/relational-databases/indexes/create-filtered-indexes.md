---
title: "필터링된 인덱스 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filtered indexes [SQL Server], about filtered indexes
- designing indexes [SQL Server], filtered
- filtered indexes [SQL Server]
- nonclustered indexes [SQL Server], filtered
- indexes [SQL Server], filtered
ms.assetid: 25e1fcc5-45d7-4c53-8c79-5493dfaa1c74
caps.latest.revision: 73
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de8d5ce869856d289b70b028ede2bc1009220a38
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="create-filtered-indexes"></a>필터링된 인덱스 만들기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 필터링된 인덱스를 만드는 방법에 대해 설명합니다. 필터링된 인덱스는 특히 데이터의 잘 정의된 하위 집합에서 선택하는 쿼리를 처리하는 데 적합한 최적화된 비클러스터형 인덱스입니다. 이 인덱스에서는 필터 조건자를 사용하여 테이블의 일부 행을 인덱싱합니다. 잘 디자인된 필터링된 인덱스는 전체 테이블 인덱스에 비해 쿼리 성능을 개선하고 인덱스 유지 관리 및 저장소 비용을 줄일 수 있습니다.  
  
 필터링된 인덱스는 전체 테이블 인덱스에 비해 다음과 같은 이점이 있습니다.  
  
-   **향상된 쿼리 성능 및 계획 품질**  
  
     잘 디자인된 필터링된 인덱스는 전체 테이블 비클러스터형 인덱스보다 크기가 작고 필터링된 통계가 있기 때문에 쿼리 성능 및 실행 계획 품질이 향상됩니다. 필터링된 통계는 필터링된 인덱스의 행만 처리하기 때문에 전체 테이블 통계보다 정확합니다.  
  
-   **줄어든 인덱스 유지 관리 비용**  
  
     인덱스의 DML(데이터 조작 언어) 문이 데이터에 영향을 줄 때에만 인덱스가 유지 관리됩니다. 필터링된 인덱스는 크기가 더 작고 인덱스의 데이터가 변경될 때에만 유지 관리되기 때문에 전체 테이블 비클러스터형 인덱스에 비해 인덱스 유지 관리 비용이 줄어듭니다. 자주 변경되지 않는 데이터를 포함하는 경우 필터링된 인덱스 수가 많을 수도 있습니다. 마찬가지로 필터링된 인덱스에 자주 수정되는 데이터만 들어 있을 경우 인덱스 크기가 작으므로 통계를 업데이트하는 비용이 줄어듭니다.  
  
-   **줄어든 인덱스 저장소 비용**  
  
     필터링된 인덱스를 만들면 전체 테이블 인덱스가 필요하지 않은 경우 비클러스터형 인덱스의 디스크 저장소를 줄일 수 있습니다. 저장소 요구 사항을 크게 증가시키지 않고 전체 테이블 비클러스터형 인덱스를 여러 필터링된 인덱스로 바꿀 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [디자인 고려 사항](#Design)  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **필터링된 인덱스를 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Design"></a> 디자인 고려 사항  
  
-   열에 적은 수의 쿼리 관련 값만 있는 경우 값의 하위 집합에 필터링된 인덱스를 만들 수 있습니다. 예를 들어 열에 있는 값이 대부분 NULL이고 쿼리는 NULL이 아닌 값에서만 선택하는 경우 NULL이 아닌 데이터 행에 대한 필터링된 인덱스를 만들 수 잇습니다. 결과 인덱스는 같은 키 열에서 정의된 전체 테이블 비클러스터형 인덱스에 비해 크기가 더 작고 유지 관리하는 비용이 더 적게 듭니다.  
  
-   테이블에 다른 유형의 데이터 행이 있는 경우 하나 이상의 데이터 범주에 대한 필터링된 인덱스를 만들 수 있습니다. 이렇게 하면 쿼리의 초점이 테이블의 특정 영역으로 제한되므로 이러한 데이터에 대한 쿼리 성능이 향상될 수 있습니다. 결과 인덱스는 전체 테이블 비클러스터형 인덱스에 비해 크기가 더 작고 유지 관리하는 비용이 더 적게 듭니다.  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   뷰에서 필터링된 인덱스를 만들 수 없습니다. 그러나 쿼리 최적화 프로그램에는 뷰에서 참조되는 테이블에 정의되는 필터링된 인덱스에 성능상 이점이 있습니다. 쿼리 최적화 프로그램에서는 쿼리 결과가 수정될 경우 뷰에서 선택하는 쿼리에 대한 필터링된 인덱스를 검토합니다.  
  
-   필터링된 인덱스에는 인덱싱된 뷰에 비해 다음과 같은 이점이 있습니다.  
  
    -   줄어든 인덱스 유지 관리 비용. 예를 들어 쿼리 프로세서에서 필터링된 인덱스를 업데이트하는 데 인덱싱된 뷰보다 적은 CPU 리소스를 사용합니다.  
  
    -   향상된 계획 품질. 예를 들어 쿼리 컴파일 중에 쿼리 최적화 프로그램이 인덱싱된 뷰보다 더 많은 경우에 필터링된 인덱스의 사용을 고려합니다.  
  
    -   온라인 인덱스 다시 작성. 필터링된 인덱스를 쿼리에 사용할 수 있는 동시에 다시 작성할 수 있습니다. 인덱싱된 뷰에 대해서는 온라인 인덱스 다시 작성이 지원되지 않습니다. 자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)에 대한 REBUILD 옵션을 참조하세요.  
  
    -   고유하지 않은 인덱스. 필터링된 인덱스는 고유하지 않아도 되지만 인덱싱된 뷰는 반드시 고유해야 합니다.  
  
-   필터링된 인덱스는 하나의 테이블에서 정의되고 간단한 비교 논리만 지원합니다. 여러 테이블을 참조하거나 복잡한 논리를 사용하는 필터 식이 필요할 경우 뷰를 만들어야 합니다.  
  
-   필터링된 인덱스 식이 쿼리 조건자와 같고 쿼리가 쿼리 결과로 필터링된 인덱스 식의 열을 반환하지 않는다면 필터링된 인덱스 식의 열이 필터링된 인덱스 정의의 포괄 열 또는 키여야 할 필요는 없습니다.  
  
-   쿼리 조건자가 필터링된 인덱스 식과 다른 비교에 필터링된 인덱스 식의 열을 사용하면 해당 열은 필터링된 인덱스 정의의 포괄 열 또는 키여야 합니다.  
  
-   필터링된 인덱스 식의 열이 쿼리 결과 집합에 있으면 해당 열은 필터링된 인덱스 정의의 포괄 열 또는 키여야 합니다.  
  
-   테이블의 클러스터형 인덱스 키가 필터링된 인덱스 정의의 포괄 열 또는 키여야 할 필요는 없습니다. 클러스터형 인덱스 키는 필터링된 인덱스를 비롯하여 모든 비클러스터형 인덱스에 자동으로 포함됩니다.  
  
-   필터링된 인덱스의 필터링된 인덱스 식에 지정된 비교 연산자로 인해 암시적 또는 명시적 데이터 변환이 발생할 경우 비교 연산자의 왼쪽에서 변환이 일어나면 오류가 발생합니다. 이에 대한 해결 방법은 비교 연산자의 오른쪽에 데이터 변환 연산자(CAST 또는 CONVERT)를 사용하여 필터링된 인덱스 식을 작성하는 것입니다.  

- [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md) 구문에서 필터링된 인덱스를 만드는 데 필요한 SET 옵션을 검토합니다.
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다. 사용자는 **sysadmin** 고정 서버 역할의 멤버 또는 **db_ddladmin** 및 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다. 필터링된 인덱스를 수정하려면 CREATE INDEX WITH DROP_EXISTING을 사용합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-filtered-index"></a>필터링된 인덱스를 만들려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 필터링된 인덱스를 만들 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 필터링된 인덱스를 만들 테이블을 확장합니다.  
  
4.  **인덱스** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 인덱스**를 가리킨 다음 **비클러스터형 인덱스...**를 선택합니다.  
  
5.  **새 인덱스** 대화 상자의 **일반** 페이지에서 **인덱스 이름** 상자에 새 인덱스의 이름을 입력합니다.  
  
6.  **인덱스 키 열**아래에서 **추가...**를 클릭합니다.  
  
7.  **table_name***에서 열 선택* 대화 상자에서 고유 인덱스에 추가할 테이블 열의 확인란을 선택합니다.  
  
8.  **확인**을 클릭합니다.  
  
9. **필터** 페이지의 **필터 식**에 필터링된 인덱스를 만드는 데 사용할 SQL 식을 입력합니다.  
  
10. **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-filtered-index"></a>필터링된 인덱스를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Looks for an existing filtered index named "FIBillOfMaterialsWithEndDate"  
    -- and deletes it from the table Production.BillOfMaterials if found.   
    IF EXISTS (SELECT name FROM sys.indexes  
        WHERE name = N'FIBillOfMaterialsWithEndDate'  
        AND object_id = OBJECT_ID (N'Production.BillOfMaterials'))  
    DROP INDEX FIBillOfMaterialsWithEndDate  
        ON Production.BillOfMaterials  
    GO  
    -- Creates a filtered index "FIBillOfMaterialsWithEndDate"  
    -- on the table Production.BillOfMaterials   
    -- using the columms ComponentID and StartDate.  
  
    CREATE NONCLUSTERED INDEX FIBillOfMaterialsWithEndDate  
        ON Production.BillOfMaterials (ComponentID, StartDate)  
        WHERE EndDate IS NOT NULL ;  
    GO  
    ```  
  
     위 필터링된 인덱스 는 다음 쿼리에 적합합니다. 이 필터링된 인덱스가 쿼리 최적화 프로그램에서 사용되는지 확인하기 위해 쿼리 실행 계획을 표시할 수 있습니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT ProductAssemblyID, ComponentID, StartDate   
    FROM Production.BillOfMaterials  
    WHERE EndDate IS NOT NULL   
        AND ComponentID = 5   
        AND StartDate > '01/01/2008' ;  
    GO  
    ```  
  
#### <a name="to-ensure-that-a-filtered-index-is-used-in-a-sql-query"></a>필터링된 인덱스가 SQL 쿼리에 사용되도록 하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT ComponentID, StartDate FROM Production.BillOfMaterials  
        WITH ( INDEX ( FIBillOfMaterialsWithEndDate ) )   
    WHERE EndDate IN ('20000825', '20000908', '20000918');   
    GO  
    ```  
  
 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
  

