---
title: "인덱스 삭제 | Microsoft 문서"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing indexes
- deleting indexes
- dropping indexes
- indexes [SQL Server], dropping
- index deletions [SQL Server]
ms.assetid: fd38a0ed-26c4-4c76-9ef7-e0a16147329d
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 77d88bfd9ae9cb742bc9dc18f8baffdd32e5ac3e
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="delete-an-index"></a>인덱스 삭제
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 인덱스를 삭제하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **인덱스를 삭제하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
 PRIMARY KEY 또는 UNIQUE 제약 조건으로 생성된 인덱스는 이 방법으로 삭제할 수 없습니다. 대신 제약 조건을 삭제해야 합니다. 제약 조건과 해당 인덱스를 제거하려면 [에서](../../t-sql/statements/alter-table-transact-sql.md) ALTER TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)]에 DROP CONSTRAINT 절을 사용합니다. 자세한 내용은 [Delete Primary Keys](../../relational-databases/tables/delete-primary-keys.md)을 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다. 이 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_ddladmin** 및 **db_owner** 고정 데이터베이스 역할에 부여됩니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-delete-an-index-by-using-object-explorer"></a>개체 탐색기를 사용하여 인덱스를 삭제하려면  
  
1.  개체 탐색기에서 인덱스를 삭제할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블** 폴더를 확장합니다.  
  
3.  삭제할 인덱스가 포함된 테이블을 확장합니다.  
  
4.  **인덱스** 폴더를 확장합니다.  
  
5.  삭제할 인덱스를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.  
  
6.  **개체 삭제** 대화 상자에서 올바른 인덱스가 **삭제할 개체** 에 있는지 확인하고 **확인**을 클릭합니다.  
  
#### <a name="to-delete-an-index-using-table-designer"></a>테이블 디자이너를 사용하여 인덱스를 삭제하려면  
  
1.  개체 탐색기에서 인덱스를 삭제할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블** 폴더를 확장합니다.  
  
3.  삭제할 인덱스가 포함된 테이블을 마우스 오른쪽 단추로 클릭하고 디자인을 클릭합니다.  
  
4.  **테이블 디자이너** 메뉴에서 **인덱스/키**를 클릭합니다.  
  
5.  **인덱스/키** 대화 상자에서 삭제하려는 인덱스를 선택합니다.  
  
6.  **삭제**를 클릭합니다.  
  
7.  **닫기**를 클릭합니다.  
  
8.  **파일** 메뉴에서 *table_name* **저장**을 선택합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-delete-an-index"></a>인덱스를 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- delete the IX_ProductVendor_BusinessEntityID index  
    -- from the Purchasing.ProductVendor table  
    DROP INDEX IX_ProductVendor_BusinessEntityID   
        ON Purchasing.ProductVendor;  
    GO  
    ```  
  
 자세한 내용은 [DROP INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)를 참조하세요.  
  
  

