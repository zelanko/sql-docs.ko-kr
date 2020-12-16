---
description: UNIQUE 제약 조건 삭제
title: UNIQUE 제약 조건 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 10/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- removing constraints
- UNIQUE constraints [SQL Server], deleting
- constraints [SQL Server], deleting
- deleting constraints
- constraints [SQL Server], unique
ms.assetid: 71e563fc-f5d7-4c2e-a42f-f0695a831f32
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0a2ad9953050271d42aa2770c6bd3a02d787f9d9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462614"
---
# <a name="delete-unique-constraints"></a>UNIQUE 제약 조건 삭제

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 UNIQUE 제약 조건을 삭제할 수 있습니다. UNIQUE 제약 조건을 삭제하면 제약 조건 식에 포함된 열 또는 열 조합에 입력한 값의 고유성 요구 사항이 제거되고 해당 고유 인덱스가 삭제됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **UNIQUE 제약 조건을 삭제하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-delete-a-unique-constraint-using-object-explorer"></a>개체 탐색기를 사용하여 UNIQUE 제약 조건을 삭제하려면  
  
1.  개체 탐색기에서 UNIQUE 제약 조건이 포함된 테이블을 확장한 후 **제약 조건** 을 확장합니다.  
  
2.  키를 마우스 오른쪽 단추로 클릭하고 **삭제** 를 선택합니다.  
  
3.  **개체 삭제** 대화 상자에서 올바른 키가 지정되었는지 확인하고 **확인** 을 클릭합니다.  
  
#### <a name="to-delete-a-unique-constraint-using-table-designer"></a>테이블 디자이너를 사용하여 UNIQUE 제약 조건을 삭제하려면  
  
1.  **개체 탐색기** 에서 UNIQUE 제약 조건이 있는 테이블을 마우스 오른쪽 단추로 클릭한 다음 **디자인** 을 클릭합니다.  
  
2.  **테이블 디자이너** 메뉴에서 **인덱스/키** 를 클릭합니다.  
  
3.  **인덱스/키** 대화 상자의 **선택한 기본/고유 키 및 인덱스** 목록에서 고유 키를 선택합니다.  
  
4.  **삭제** 를 클릭합니다.  
  
5.  **파일** 메뉴에서 ‘테이블 이름’ **저장을 클릭합니다.**   
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-delete-a-unique-constraint"></a>UNIQUE 제약 조건을 삭제하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    -- Return the name of unique constraint.  
    SELECT name  
    FROM sys.objects  
    WHERE type = 'UQ' AND OBJECT_NAME(parent_object_id) = N' DocExc';  
    GO  
    -- Delete the unique constraint.  
    ALTER TABLE dbo.DocExc   
    DROP CONSTRAINT UNQ_ColumnB_DocExc;  
    GO  
    ```  
  
 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) 및 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조하세요.  
  
###  <a name="TsqlExample"></a>  
