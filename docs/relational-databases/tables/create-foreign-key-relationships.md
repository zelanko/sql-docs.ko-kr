---
title: 외래 키 관계 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], creating
ms.assetid: 867a54b8-5be4-46e6-9702-49ae6dabf67c
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2fffbb19685087883d9b788e7dc894eb413f4b0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62516095"
---
# <a name="create-foreign-key-relationships"></a>외래 키 관계 만들기
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 외래 키 관계를 만드는 방법에 대해 설명합니다. 한 테이블의 행을 다른 테이블의 행과 연결하려면 두 테이블 사이에 관계를 만듭니다.    
     
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항 제한 사항
 
-   외래 키 제약 조건은 다른 테이블의 기본 키 제약 조건으로 연결될 수도 있고 다른 테이블에 있는 UNIQUE 제약 조건의 열을 참조하도록 정의할 수도 있습니다.    
    
-   FOREIGN KEY 제약 조건의 열에 NULL 외의 다른 값을 입력한 경우에는 그 값이 참조되는 열에 있어야 합니다. 그렇지 않은 경우에는 외래 키 위반 오류 메시지가 반환됩니다. 복합 외래 키 제약 조건의 모든 값에 대해 유효성을 검사하려면 관련된 모든 열에 NOT NULL을 지정합니다.    
    
-   FOREIGN KEY 제약 조건은 같은 서버의 같은 데이터베이스 내에 있는 테이블만 참조할 수 있습니다. 상호 데이터베이스 참조 무결성은 트리거를 통해 구현해야 합니다. 자세한 내용은 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)를 참조하세요.    
    
-   FOREIGN KEY 제약 조건은 같은 테이블에 있는 다른 열을 참조할 수 있습니다. 이것을 자체 참조라고 합니다.    
    
-   열 수준에서 지정된 외래 키 제약 조건은 참조 열을 하나만 나열할 수 있습니다. 이 열의 데이터 형식은 제약 조건이 정의된 열의 데이터 형식과 같아야 합니다.    
    
-   테이블 수준에서 지정된 외래 키 제약 조건에는 제약 조건 열 목록의 열 개수와 같은 수의 참조 열이 있어야 합니다. 각 참조 열의 데이터 형식도 열 목록의 해당 열과 같아야 합니다.    
    
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 테이블에 포함하여 다른 테이블을 참조하는 FOREIGN KEY 제약 조건의 수나 특정 테이블을 참조하는 다른 테이블 소유의 FOREIGN KEY 제약 조건의 수에 미리 한계를 정의하지 않습니다. 하지만 실제로 사용할 수 있는 FOREIGN KEY 제약 조건의 수는 하드웨어 구성 및 데이터베이스와 애플리케이션의 디자인에 따라 제한됩니다.  각 테이블은 최대 253개의 다른 테이블 및 열을 외래 키(나가는 참조)로 참조할 수 있습니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 에서는 단일 테이블의 열을 참조할 수 있는 다른 테이블 및 열의 수 제한이 253에서 10,000으로 증가합니다.  단, 호환성 수준이 130 이상이어야 합니다. 이러한 참조 가능 테이블 및 열 수의 증가에는 다음과 같은 제한이 적용됩니다.    
    
    -   253개를 초과하는 외래 키 참조는 DELETE 및 UPDATE DML 작업에서 지원됩니다. MERGE 작업은 지원되지 않습니다.    
    
    -   자기 자신에 대한 외래 키 참조가 포함된 테이블은 계속 253개의 외래 키 참조만 사용할 수 있습니다.    
    
    -   columnstore 인덱스, 메모리 최적화 테이블 또는 스트레치 데이터베이스에 대해서는 현재 253개보다 많은 외래 키 참조를 사용할 수 없습니다.    
    
-   임시 테이블에는 FOREIGN KEY 제약 조건이 적용되지 않습니다.    
    
-   CLR 사용자 정의 형식 열에 외래 키를 정의하는 경우 형식 구현이 이진 순서를 지원해야 합니다. 자세한 내용은 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)을 참조하세요.    
    
-   **varchar(max)** 유형의 열은 자신이 참조하는 기본 키도 **varchar(max)** 유형으로 정의된 경우에만 FOREIGN KEY 제약 조건에 참여할 수 있습니다.    
    

    
##   <a name="permissions"></a>사용 권한    
 외래 키가 포함된 새 테이블을 만들려면 데이터베이스에서 CREATE TABLE 권한이 필요하고 테이블을 만들려는 스키마에 대한 ALTER 권한이 필요합니다.    
    
 기존 테이블에서 외래 키를 만들려면 해당 테이블에 대한 ALTER 권한이 필요합니다.    
       
    
## <a name="create-a-foreign-key-relationship-in-table-designer"></a>테이블 디자이너에서 외래 키 관계 만들기 
####  <a name="using-sql-server-management-studio"></a>SQL Server Management Studio 사용    
    
1.  개체 탐색기에서 관계의 외래 키 쪽에 표시할 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 클릭합니다.    
    
     **테이블 디자이너**에서 테이블이 열립니다.    
    
2.  **테이블 디자이너** 메뉴에서 **관계**를 클릭합니다.    
    
3.  **외래 키 관계** 대화 상자에서 **추가**를 클릭합니다.    
    
     **선택한 관계** 목록에 FK_\<*tablename*>_\<*tablename*> 형식의 시스템 제공 이름과 함께 관계가 표시됩니다. 여기에서 *tablename*은 외래 키 테이블의 이름입니다.    
    
4.  **선택한 관계** 목록에서 관계를 클릭합니다.    
    
5.  오른쪽에 있는 표에서 **테이블 및 열 사양**을 클릭한 다음, 속성의 오른쪽에 있는 줄임표( **…** )를 클릭합니다.    
    
6.  **테이블 및 열** 대화 상자의 **기본 키** 드롭다운 목록에서 관계의 기본 키 쪽에 사용할 테이블을 선택합니다.    
    
7.  아래 표에서 테이블의 기본 키로 사용할 열을 선택합니다. 각 열 바로 왼쪽에 있는 표의 셀에서 외래 키 테이블의 상응하는 외래 키 열을 선택합니다.    
    
     **테이블 디자이너** 에서 관계의 이름이 자동으로 지정됩니다. 이 이름을 변경하려면 **관계 이름** 입력란의 내용을 편집합니다.    
    
8.  **확인** 을 선택하여 관계를 만듭니다.    
       
## <a name="create-a-foreign-key-in-a-new-table"></a>새 테이블에서 외래 키 만들기  
####  <a name="using-transact-sql"></a>Transact-SQL 사용   
    
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.    
    
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.    
    
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 테이블을 만들고 `TempID` 테이블의 `SalesReasonID` 열을 참조하는 `Sales.SalesReason` 열의 외래 키 제약 조건을 정의합니다. ON DELETE CASCADE 및 ON UPDATE CASCADE 절을 사용하면 `Sales.SalesReason` 테이블에 대한 변경 내용이 `Sales.TempSalesReason` 테이블에 자동으로 전파되었는지 확인할 수 있습니다.    
    
    ```    
    USE AdventureWorks2012;    
    GO    
    CREATE TABLE Sales.TempSalesReason (TempID int NOT NULL, Name nvarchar(50),     
    CONSTRAINT PK_TempSales PRIMARY KEY NONCLUSTERED (TempID),     
    CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)     
        REFERENCES Sales.SalesReason (SalesReasonID)     
        ON DELETE CASCADE    
        ON UPDATE CASCADE    
    );
    GO    
    
    ```    
    
## <a name="create-a-foreign-key-in-an-existing-table"></a>기존 테이블에서 외래 키 만들기 
#### <a name="using-transact-sql"></a>Transact-SQL 사용   
    
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.    
    
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.    
    
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 `TempID` 열에 외래 키를 만들고 `SalesReasonID` 테이블의 `Sales.SalesReason` 열을 참조합니다.    
    
    ```    
    USE AdventureWorks2012;    
    GO    
    ALTER TABLE Sales.TempSalesReason     
    ADD CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)     
        REFERENCES Sales.SalesReason (SalesReasonID)     
        ON DELETE CASCADE    
        ON UPDATE CASCADE    
    ;    
    GO    
    
    ```    
    
     자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md), [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 및 [table_constraint&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)를 참조하세요.    
    
  
