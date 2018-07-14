---
title: 기본 키 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- primary keys [SQL Server], creating
ms.assetid: 85c623ca-4656-4d70-a9db-ee4d897cd214
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9d4ba48188473aaa5286e8121bcbfcd3a9b50101
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177680"
---
# <a name="create-primary-keys"></a>기본 키 만들기
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 기본 키를 정의할 수 있습니다. 기본 키를 만들면 해당하는 고유 클러스터형 또는 비클러스터형 인덱스가 자동으로 만들어집니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **기본 키를 만들려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   테이블은 하나의 PRIMARY KEY 제약 조건만 포함할 수 있습니다.  
  
-   PRIMARY KEY 제약 조건 내에서 정의된 모든 열은 NOT NULL로 정의되어야 합니다. NULL 허용 여부를 지정하지 않은 경우에는 PRIMARY KEY 제약 조건에 참여하는 모든 열의 NULL 허용 여부가 NOT NULL로 설정됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 기본 키가 포함된 새 테이블을 만들려면 데이터베이스에서 CREATE TABLE 권한이 필요하고 테이블을 만들려는 스키마에 대한 ALTER 권한이 필요합니다.  
  
 기존 테이블에서 기본 키를 만들려면 해당 테이블에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-primary-key"></a>기본 키를 만들려면  
  
1.  개체 탐색기에서 UNIQUE 제약 조건을 추가하려는 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.  
  
2.  **테이블 디자이너**에서 기본 키로 정의하려는 데이터베이스 열의 행 선택기를 클릭합니다. 여러 열을 선택하려면 Ctrl 키를 누른 상태로 다른 열의 행 선택기를 클릭합니다.  
  
3.  열의 행 선택기를 마우스 오른쪽 단추로 클릭하고 **기본 키 설정**을 선택합니다.  
  
> [!CAUTION]  
>  기본 키를 다시 정의하려면 기존의 기본 키에 대한 관계를 모두 삭제한 다음 기본 키를 새로 만들어야 합니다. 이 과정에서 기존의 관계가 자동으로 삭제된다는 경고 메시지가 나타납니다.  
  
 기본 키 열을 구분하기 위해 해당 행 선택기에 기본 키 기호가 표시됩니다.  
  
 기본 키가 두 개 이상의 열로 구성되어 있는 경우 한 열에는 중복 값이 허용되지만 기본 키의 모든 열에 있는 값의 각 조합은 중복되지 않아야 합니다.  
  
 복합 키를 정의하는 경우 기본 키의 열 순서는 테이블에 표시되는 열 순서와 일치합니다. 기본 키를 만든 후에 이러한 열 순서를 변경할 수 있습니다. 자세한 내용은 [기본 키 수정](modify-primary-keys.md)을 참조하세요.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-primary-key-in-an-existing-table"></a>기존 테이블에 고유 키를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 `TransactionID`열에 기본 키를 만듭니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Production.TransactionHistoryArchive   
    ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID);  
    GO  
  
    ```  
  
#### <a name="to-create-a-primary-key-in-a-new-table"></a>새 테이블에 고유 키를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 테이블을 만들고 `TransactionID` 열에 고유 키를 정의합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive1  
    (  
       TransactionID int NOT NULL,  
       CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)  
    );  
    GO  
  
    ```  
  
     자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql), [CREATE TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql) 및 [table_constraint&#40;Transact-SQL&#41;](/sql/relational-databases/system-information-schema-views/table-constraints-transact-sql)를 참조하세요.  
  
###  <a name="TsqlExample"></a>  
