---
title: 한 테이블에서 다른 테이블로 열 복사(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- copying columns
- columns [SQL Server], copying
ms.assetid: 5f5e70dc-69f9-44b8-bc48-b5d51ac20d77
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67df7c541b0c664f200f6cf77affc0c809dbc719
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52794625"
---
# <a name="copy-columns-from-one-table-to-another-database-engine"></a>한 테이블에서 다른 테이블로 열 복사(데이터베이스 엔진)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 열 정의만 복사하거나 열 정의와 데이터를 모두 복사하여 테이블 간에 열을 복사하는 방법을 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 열을 복사하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 별칭 데이터 형식의 열을 데이터베이스 간에 복사하면 대상 데이터베이스에서 별칭 데이터 형식을 사용하지 못할 수도 있습니다. 이 경우 해당 열에는 대상 데이터베이스에서 사용할 수 있는 가장 비슷한 기본 데이터 형식이 지정됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>한 테이블에서 다른 테이블로 열 정의를 복사하려면  
  
1.  테이블을 마우스 오른쪽 단추로 클릭한 다음 **디자인**을 클릭하여 복사할 열이 있는 테이블과 이 열을 붙여 넣을 대상 테이블을 엽니다.  
  
2.  복사하려는 열이 포함된 테이블에 해당하는 탭을 클릭하고 복사할 열을 선택합니다.  
  
3.  **편집** 메뉴에서 **복사**를 클릭합니다.  
  
4.  열을 복사하여 넣으려는 대상 테이블에 해당하는 탭을 클릭합니다.  
  
5.  열을 삽입하려는 위치 바로 앞의 열을 선택하고 **편집** 메뉴에서 **붙여넣기**를 클릭합니다.  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>테이블 간에 데이터를 복사하려면  
  
1.  위에서 설명한 열 정의 복사 지침을 따릅니다.  
  
    > [!NOTE]  
    >  한 테이블에 다른 테이블로 데이터를 복사하려면 먼저 대상 열의 데이터 형식이 원본 열의 데이터 형식과 호환되는지 확인해야 합니다.  
  
2.  개체 탐색기에서 **뷰** 노드를 마우스 오른쪽 단추로 클릭한 다음 **새 뷰**를 클릭합니다.  
  
3.  **쿼리 디자이너** 메뉴에서 **형식 변경**을 가리킨 다음 **결과 삽입**을 클릭합니다.  
  
4.  **결과 삽입의 대상 테이블 선택** 대화 상자에서 데이터를 복사해 넣을 대상 테이블을 선택한 다음 **확인**을 클릭합니다.  
  
     테이블 내에서 행을 복사하는 경우 원본 테이블을 대상 테이블로 추가할 수 있습니다.  
  
    > [!NOTE]  
    >  **쿼리 디자이너** 에서는 업데이트 가능한 테이블과 뷰를 미리 확인할 수 없습니다. 따라서, **결과 삽입의 대상 테이블 선택** 대화 상자의 테이블 목록에는 쿼리하려는 데이터 연결에 사용 가능한 모든 테이블과 뷰가 표시됩니다. 여기에는 행을 복사해 넣을 수 없는 테이블이나 뷰도 포함됩니다.  
  
5.  다이어그램 창의 본문을 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **다이어그램에 테이블 추가**를 클릭합니다.  
  
6.  **테이블 추가** 대화 상자에서 데이터를 복사하려는 각 원본 테이블을 선택하고 **추가**를 클릭한 다음 **닫기**를 클릭합니다.  
  
     다이어그램 창에 테이블이 간략한 형태로 나타납니다.  
  
7.  간략한 테이블에서 데이터를 복사하려는 원본 열의 확인란을 모두 선택합니다.  
  
8.  조건 창의 **추가** 열에서 각 대상 열에 대해 데이터를 복사할 원본 열을 선택합니다.  
  
9. 조건 창에 검색 조건을 입력하여 복사할 행을 지정합니다. 자세한 내용은 [검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)을 참조하세요.  
  
     검색 조건을 지정하지 않으면 원본 테이블의 행 전체가 대상 테이블에 복사됩니다.  
  
10. 요약 정보를 복사하려면 **그룹화 방법** 옵션을 지정합니다. 자세한 내용은 [테이블에 있는 모든 행의 값 요약 또는 집계&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools.md)를 참조하세요.  
  
11. 쿼리를 실행하려면 **SQL 실행** 단추를 클릭합니다.  
  
     결과 삽입 쿼리를 실행해도 [결과 창](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)에는 결과가 보고되지 않습니다. 대신, 복사한 행의 수를 나타내는 메시지가 표시됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>한 테이블에서 다른 테이블로 열 정의를 복사하려면  
  
1.  Transact-SQL 문을 사용하여 한 테이블에서 다른 기존 테이블로 개별 열을 복사할 수 없습니다. 하지만 SELECT INTO를 사용하여 기본 파일 그룹에 새 테이블을 만들고 쿼리의 결과 행을 이 테이블에 삽입할 수 있습니다. 자세한 내용은 [INTO 절&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-into-clause-transact-sql)을 참조하세요.  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>테이블 간에 데이터를 복사하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.EmployeeSales  
    ( BusinessEntityID   varchar(11) NOT NULL,  
      SalesYTD money NOT NULL  
    );  
    GO  
    INSERT INTO dbo.EmployeeSales  
        SELECT BusinessEntityID, SalesYTD   
        FROM Sales.SalesPerson;  
    GO  
    ```  
  
  
