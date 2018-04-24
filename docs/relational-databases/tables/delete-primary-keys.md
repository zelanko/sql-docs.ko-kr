---
title: 기본 키 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- removing primary keys
- deleting primary keys
- primary keys [SQL Server], deleting
ms.assetid: c472e465-7bdd-4d74-8fc9-e47fca007ccb
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cc07668d0fca77aad096bfba2da98e62315258d7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="delete-primary-keys"></a>기본 키 삭제
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 기본 키를 삭제할 수 있습니다. 기본 키를 삭제하면 해당 인덱스가 삭제됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **기본 키를 삭제하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-delete-a-primary-key-constraint-using-object-explorer"></a>개체 탐색기를 사용하여 PRIMARY KEY 제약 조건을 삭제하려면  
  
1.  개체 탐색기에서 기본 키가 포함된 테이블을 확장한 후 **키**를 확장합니다.  
  
2.  키를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.  
  
3.  **개체 삭제** 대화 상자에서 올바른 키가 지정되었는지 확인하고 **확인**을 클릭합니다.  
  
#### <a name="to-delete-a-primary-key-constraint-using-table-designer"></a>테이블 디자이너를 사용하여 PRIMARY KEY 제약 조건을 삭제하려면  
  
1.  개체 탐색기에서 기본 키가 있는 테이블을 마우스 오른쪽 단추로 클릭한 다음 **디자인**을 클릭합니다.  
  
2.  테이블 표에서 기본 키가 있는 행을 마우스 오른쪽 단추로 클릭하고 **기본 키 제거** 를 선택하여 기본 키 설정 또는 해제 여부를 전환할 수 있습니다.  
  
    > [!NOTE]  
    >  이 동작을 실행 취소하려면 변경 내용을 저장하지 않은 상태로 테이블을 닫습니다. 기본 키 삭제 작업을 취소하면 테이블에 대한 다른 모든 변경 내용이 손실됩니다.  
  
3.  **파일** 메뉴에서 *****테이블 이름 저장*을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-delete-a-primary-key-constraint"></a>PRIMARY KEY 제약 조건을 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 먼저 PRIMARY KEY 제약 조건의 이름을 식별한 후 해당 제약 조건을 삭제합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Return the name of primary key.  
    SELECT name  
    FROM sys.key_constraints  
    WHERE type = 'PK' AND OBJECT_NAME(parent_object_id) = N'TransactionHistoryArchive';  
    GO  
    -- Delete the primary key constraint.  
    ALTER TABLE Production.TransactionHistoryArchive  
    DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID;   
    GO  
    ```  
  
 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) 및 [sys.key_constraints&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)를 참조하세요.  
  
###  <a name="TsqlExample"></a>  
