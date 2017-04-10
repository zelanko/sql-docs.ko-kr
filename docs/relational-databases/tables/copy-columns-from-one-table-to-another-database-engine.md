---
title: "한 테이블에서 다른 테이블로 열 복사(데이터베이스 엔진) | Microsoft Docs"
ms.custom: ""
ms.date: "09/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "열 복사"
  - "열 [SQL Server], 복사"
ms.assetid: 5f5e70dc-69f9-44b8-bc48-b5d51ac20d77
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 한 테이블에서 다른 테이블로 열 복사(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 열 정의만 복사하거나 열 정의와 데이터를 모두 복사하여 테이블 간에 열을 복사하는 방법을 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 열을 복사하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
 별칭 데이터 형식의 열을 데이터베이스 간에 복사하면 대상 데이터베이스에서 별칭 데이터 형식을 사용하지 못할 수도 있습니다. 이 경우 해당 열에는 대상 데이터베이스에서 사용할 수 있는 가장 비슷한 기본 데이터 형식이 지정됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### 한 테이블에서 다른 테이블로 열 정의를 복사하려면  
  
1.  테이블을 마우스 오른쪽 단추로 클릭한 다음 **디자인**을 클릭하여 복사할 열이 있는 테이블과 이 열을 붙여 넣을 대상 테이블을 엽니다.  
  
2.  복사하려는 열이 포함된 테이블에 해당하는 탭을 클릭하고 복사할 열을 선택합니다.  
  
3.  **편집** 메뉴에서 **복사**를 클릭합니다.  
  
4.  열을 복사하여 넣으려는 대상 테이블에 해당하는 탭을 클릭합니다.  
  
5.  열을 삽입하려는 위치 바로 앞의 열을 선택하고 **편집** 메뉴에서 **붙여넣기**를 클릭합니다.  
  
#### 테이블 간에 데이터를 복사하려면  
  
1.  위에서 설명한 열 정의 복사 지침을 따릅니다.  
  
    > [!NOTE]  
    >  한 테이블에 다른 테이블로 데이터를 복사하려면 먼저 대상 열의 데이터 형식이 원본 열의 데이터 형식과 호환되는지 확인해야 합니다.  
  
2.  새 쿼리 편집기 창을 엽니다. 

3.  쿼리 편집기를 마우스 오른쪽 단추로 누른 다음 **편집기에서 쿼리 디자인**을 클릭합니다. 

4.  **테이블 추가** 대화 상자에서 원본 및 대상 테이블을 선택하고, **추가**를 클릭한 다음 **테이블 추가** 대화 상자를 닫습니다. 

5.  쿼리 편집기에서 열린 영역을 마우스 오른쪽 단추로 클릭하고 **형식 변경**을 가리킨 다음 **결과 삽입**을 클릭합니다.  

6.  **결과 삽입의 대상 테이블 선택** 대화 상자에서 대상 테이블을 선택합니다. 

7.  쿼리 디자이너 상단에서 원본 테이블의 원본 열을 클릭합니다.

8. 이제 쿼리 디자이너에서 INSERT 쿼리가 생성되었습니다. 원래 쿼리 편집기 창에 쿼리를 배치하려면 확인을 클릭합니다.  

9.  대상 테이블에 원본 테이블의 데이터를 삽입하려면 쿼리를 실행합니다.

  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### 한 테이블에서 다른 테이블로 열 정의를 복사하려면  
  
1.  Transact-SQL 문을 사용하여 한 테이블에서 다른 기존 테이블로 개별 열을 복사할 수 없습니다. 하지만 SELECT INTO를 사용하여 기본 파일 그룹에 새 테이블을 만들고 쿼리의 결과 행을 이 테이블에 삽입할 수 있습니다. 자세한 내용은 [INTO 절&#40;Transact-SQL&#41;](../Topic/INTO%20Clause%20\(Transact-SQL\).md)을 참조하세요.  
  
#### 테이블 간에 데이터를 복사하려면  
  
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
  
  