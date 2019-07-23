---
title: 테이블 이름 바꾸기(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 02/23/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table renaming [SQL Server]
- table names [SQL Server]
- tables [SQL Server], Visual Database Tools
- renaming tables
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c8a9fd43e62bda03b8f994e2a8639524b4bea645
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016328"
---
# <a name="rename-tables-database-engine"></a>테이블 이름 바꾸기(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

SQL Server 또는 Azure SQL Database에서 테이블의 이름을 바꿉니다.

Azure SQL Data Warehouse 또는 병렬 데이터 웨어하우스에서 테이블의 이름을 바꾸려면 t-sql [RENAME OBJECT](../../t-sql/statements/rename-transact-sql.md) 문을 사용합니다. 
  
> [!CAUTION]  
>  테이블 이름을 바꿀 때는 신중한 검토가 필요합니다. 기존의 쿼리, 뷰, 사용자 정의 함수, 저장 프로시저 또는 프로그램에서 해당 테이블을 참조하는 경우 이름 수정으로 인해 이러한 개체가 유효하지 않게 됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **테이블 이름을 바꾸려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 테이블 이름을 변경해도 해당 테이블에 대한 참조 이름은 자동으로 바뀌지 않습니다. 이름을 바꾼 테이블을 참조하는 개체는 수동으로 수정해야 합니다. 예를 들어 테이블 이름을 바꿨고 해당 테이블이 트리거에서 참조되는 경우 트리거를 수정하여 새로운 테이블 이름을 적용해야 합니다. 테이블 이름을 바꾸기 전에 테이블에 대한 종속성을 나열하려면 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 를 사용합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-rename-a-table"></a>테이블 이름을 바꾸려면  
  
1.  개체 탐색기에서 이름을 바꾸려는 테이블을 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **디자인** 을 선택합니다.  
  
2.  **보기** 메뉴에서 **속성**을 선택합니다.  
  
3.  **속성** 창의 **이름** 값 필드에 테이블의 새 이름을 입력합니다.  
  
4.  이 동작을 취소하려면 이 필드를 나가기 전에 Esc 키를 누릅니다.  
  
5.  **파일** 메뉴에서 **저장** _테이블 이름_을 선택합니다.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-rename-a-table"></a>테이블 이름을 바꾸려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예에서는 `SalesTerritory` 스키마에 있는 `SalesTerr` 테이블의 이름을 `Sales` 로 바꿉니다. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    EXEC sp_rename 'Sales.SalesTerritory', 'SalesTerr';  
    ```  
  
 추가 예제를 보려면 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)을 참조하세요.  
  
  
