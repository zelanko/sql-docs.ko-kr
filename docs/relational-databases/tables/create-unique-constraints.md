---
title: "UNIQUE 제약 조건 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "10/12/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "UNIQUE_TSQL"
helpviewer_keywords: 
  - "UNIQUE 제약 조건 [SQL Server], 만들기"
  - "제약 조건 [SQL Server], 만들기"
  - "제약 조건 [SQL Server], 고유"
ms.assetid: a86f9d6f-f242-43be-b65d-b3435b71b62a
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# UNIQUE 제약 조건 만들기
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하여 UNIQUE 제약 조건을 만들어서 기본 키에 참여하지 않는 특정 열에 입력하는 값이 중복되지 않도록 할 수 있습니다. UNIQUE 제약 조건을 만들면 해당하는 고유 인덱스가 자동으로 만들어집니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **UNIQUE 제약 조건을 만들려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### UNIQUE 제약 조건을 만들려면  
  
1.  **개체 탐색기**에서 UNIQUE 제약 조건을 추가하려는 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.  
  
2.  **테이블 디자이너** 메뉴에서 **인덱스/키**를 클릭합니다.  
  
3.  **인덱스/키** 대화 상자에서 **추가**를 클릭합니다.  
  
4.  **일반** 아래의 표에서 **형식**을 선택하고 속성 오른쪽에 있는 드롭다운 목록 상자에서 **고유 키**를 선택합니다.  
  
5.  **파일** 메뉴에서 **저장***table name*을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### UNIQUE 제약 조건을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 `TransactionHistoryArchive4` 테이블을 만들고 `TransactionID`열에 UNIQUE 제약 조건을 만듭니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive4  
     (  
       TransactionID int NOT NULL,   
       CONSTRAINT AK_TransactionID UNIQUE(TransactionID)   
    );   
    GO  
  
    ```  
  
#### 기존 테이블에 UNIQUE 제약 조건을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 `PasswordHash` 테이블에서 `PasswordSalt` 및 `Person.Password`열에 UNIQUE 제약 조건을 만듭니다.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    ALTER TABLE Person.Password   
    ADD CONSTRAINT AK_Password UNIQUE (PasswordHash, PasswordSalt);   
    GO  
  
    ```  
  
#### 새 테이블에 UNIQUE 제약 조건을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 테이블을 만들고 `TransactionID` 열에 UNIQUE 제약 조건을 정의합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive2  
    (  
       TransactionID int NOT NULL,  
       CONSTRAINT AK_TransactionID UNIQUE(TransactionID)  
    );  
    GO  
  
    ```  
  
     자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md), [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 및 [table_constraint&#40;Transact-SQL&#41;](../Topic/table_constraint%20\(Transact-SQL\).md)를 참조하세요.  
  
###  <a name="TsqlExample"></a>  