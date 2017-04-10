---
title: "테이블 삭제(데이터베이스 엔진) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "테이블 삭제 [SQL Server]"
  - "테이블 삭제"
  - "테이블 제거"
  - "테이블 삭제"
ms.assetid: ca6aa3e9-9885-44c3-bafc-aec441fd97ec
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# 테이블 삭제(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 데이터베이스에서 테이블을 삭제할 수 있습니다.  
  
> [!CAUTION]  
>  테이블을 삭제할 때는 신중한 검토가 필요합니다. 기존의 쿼리, 뷰, 사용자 정의 함수, 저장 프로시저 또는 프로그램에서 해당 테이블을 참조하는 경우 테이블을 삭제하면 이 개체들은 유효하지 않게 됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **테이블을 삭제하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   FOREIGN KEY 제약 조건에 의해 참조되는 테이블은 삭제할 수 없습니다. 참조하는 FOREIGN KEY 제약 조건 또는 참조하는 테이블을 먼저 삭제해야 합니다. 참조하는 테이블과 기본 키를 포함하는 테이블이 하나의 DROP TABLE 문에서 삭제되는 경우 참조하는 테이블이 먼저 나열되어야 합니다.  
  
-   테이블을 삭제하면 해당 테이블에 있는 규칙이나 기본값의 바인딩이 해제되고 해당 테이블과 연결된 제약 조건이나 트리거가 자동으로 삭제됩니다. 테이블을 다시 만들려면 해당 규칙과 기본값을 다시 바인딩하고 트리거를 다시 만들어야 하며 필요한 제약 조건을 모두 추가해야 합니다.  
  
-   FILESTREAM 특성이 있는 **varbinary (max)** 열이 포함된 테이블을 삭제해도 파일 시스템에 저장된 데이터는 제거되지 않습니다.  
  
-   동일한 일괄 처리에서 동일한 테이블에 대해 DROP TABLE과 CREATE TABLE을 실행할 수는 없습니다. 이를 실행하면 예기치 않은 오류가 발생할 수 있습니다.  
  
-   삭제된 테이블을 참조하는 뷰나 저장 프로시저는 명시적으로 삭제하거나 테이블에 대한 참조를 제거하도록 수정해야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블이 속한 스키마에 대한 ALTER 권한, 테이블에 대한 CONTROL 권한 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### 데이터베이스에서 테이블을 삭제하려면  
  
1.  개체 탐색기에서 삭제하려는 테이블을 선택합니다.  
  
2.  테이블을 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **삭제**를 선택합니다.  
  
3.  삭제를 확인하는 메시지 상자가 나타나면 **예**를 클릭합니다.  
  
    > [!NOTE]  
    >  테이블을 삭제하면 테이블에 대한 모든 관계도 자동으로 제거됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### 쿼리 편집기에서 테이블을 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    DROP TABLE dbo.PurchaseOrderDetail;  
  
    ```  
  
 자세한 내용은 [DROP TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)을 참조하세요.  
  
  