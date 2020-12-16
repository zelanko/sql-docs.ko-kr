---
description: UNIQUE 제약 조건 만들기
title: UNIQUE 제약 조건 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- UNIQUE_TSQL
helpviewer_keywords:
- UNIQUE constraints [SQL Server], creating
- constraints [SQL Server], creating
- constraints [SQL Server], unique
ms.assetid: a86f9d6f-f242-43be-b65d-b3435b71b62a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 06f465d3c4ff6086d74c155c4f810730eca50742
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484485"
---
# <a name="create-unique-constraints"></a>UNIQUE 제약 조건 만들기

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하여 UNIQUE 제약 조건을 만들어서 기본 키에 참여하지 않는 특정 열에 입력하는 값이 중복되지 않도록 할 수 있습니다. UNIQUE 제약 조건을 만들면 해당하는 고유 인덱스가 자동으로 만들어집니다.  
  
> [!NOTE]    
> Azure Synapse Analytics의 UNIQUE 제약 조건에 대한 자세한 내용은 [Azure Synapse Analytics의 기본 키, 외래 키 및 고유 키](/azure/sql-data-warehouse/sql-data-warehouse-table-constraints)를 참조하세요.
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **UNIQUE 제약 조건을 만들려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-unique-constraint"></a>UNIQUE 제약 조건을 만들려면  
  
1.  **개체 탐색기** 에서 UNIQUE 제약 조건을 추가하려는 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인** 을 선택합니다.  
  
2.  **테이블 디자이너** 메뉴에서 **인덱스/키** 를 클릭합니다.  
  
3.  **인덱스/키** 대화 상자에서 **추가** 를 클릭합니다.  
  
4.  **일반** 아래의 그리드에서 **형식** 을 선택하고 속성 오른쪽에 있는 드롭다운 목록 상자에서 **고유 키** 를 선택한 다음 **닫기** 를 클릭합니다.  
  
5.  **파일** 메뉴에서 ‘테이블 이름’ **저장을 클릭합니다.**   

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-unique-constraint"></a>UNIQUE 제약 조건을 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 이 예에서는 `TransactionHistoryArchive4` 테이블을 만들고 `TransactionID`열에 UNIQUE 제약 조건을 만듭니다.  
  
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
  
#### <a name="to-create-a-unique-constraint-on-an-existing-table"></a>기존 테이블에 UNIQUE 제약 조건을 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 이 예에서는 `PasswordHash` 테이블에서 `PasswordSalt` 및 `Person.Password`열에 UNIQUE 제약 조건을 만듭니다.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    ALTER TABLE Person.Password   
    ADD CONSTRAINT AK_Password UNIQUE (PasswordHash, PasswordSalt);   
    GO  
  
    ```  
  
#### <a name="to-create-a-unique-constraint-on-a-new-table"></a>새 테이블에 고유 제약 조건을 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 이 예에서는 테이블을 만들고 `TransactionID`열에 UNIQUE 제약 조건을 정의합니다.  
  
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
  
     자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md), [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 및 [table_constraint&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)를 참조하세요.  
  
###  <a name="TsqlExample"></a>