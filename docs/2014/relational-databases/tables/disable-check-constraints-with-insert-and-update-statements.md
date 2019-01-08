---
title: INSERT 및 UPDATE 문에서 CHECK 제약 조건 해제 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, disabling
- constraints [SQL Server], disabling
- disabling constraints
- constraints [SQL Server], check
ms.assetid: c7287ad1-50d2-4e80-bc0c-b5570f7e5f69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bd49c3264857a92a9ca029a25894a5afdbeab381
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52798345"
---
# <a name="disable-check-constraints-with-insert-and-update-statements"></a>INSERT 및 UPDATE 문에서 CHECK 제약 조건 해제
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 INSERT 및 UPDATE 트랜잭션에 대해 CHECK 제약 조건을 해제할 수 있습니다. CHECK 제약 조건을 해제한 후에는 해당 열에 대한 이후 삽입 또는 업데이트 작업의 유효성을 해당 제약 조건에 따라 검사하지 않습니다. 새 데이터가 기존 제약 조건을 위반할지를 알고 있는 경우 또는 제약 조건이 데이터베이스에 이미 있는 데이터에만 적용될 경우 이 옵션을 사용합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **INSERT 및 UPDATE 문에 대해 CHECK 제약 조건을 해제하려면**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-disable-a-check-constraint-for-insert-and-update-statements"></a>INSERT 및 UPDATE 문에 대해 CHECK 제약 조건을 해제하려면  
  
1.  **개체 탐색기**에서 제약 조건을 포함하는 테이블을 확장하고 **제약 조건** 폴더를 확장합니다.  
  
2.  제약 조건을 마우스 오른쪽 단추로 클릭하고 **수정**을 선택합니다.  
  
3.  **테이블 디자이너**아래의 표에서 **INSERT 및 UPDATE에 적용** 을 클릭하고 드롭다운 메뉴에서 **아니요** 를 선택합니다.  
  
4.  **닫기**를 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-disable-a-check-constraint-for-insert-and-update-statements"></a>INSERT 및 UPDATE 문에 대해 CHECK 제약 조건을 해제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Purchasing.PurchaseOrderHeader  
    NOCHECK CONSTRAINT CK_PurchaseOrderHeader_Freight;   
    GO  
    ```  
  
 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)을 참조하세요.  
  
###  <a name="TsqlExample"></a>  
