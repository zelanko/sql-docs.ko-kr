---
title: 테이블 이름 바꾸기(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table renaming [SQL Server]
- table names [SQL Server]
- tables [SQL Server], Visual Database Tools
- renaming tables
ms.assetid: 2f5c922d-4d71-4694-9fca-28dd99375799
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3fc62dc5f0e716273df257aba7fdc137391d3055
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68196734"
---
# <a name="rename-tables-database-engine"></a>테이블 이름 바꾸기(데이터베이스 엔진)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 테이블 이름을 바꿀 수 있습니다.  
  
> [!CAUTION]  
>  테이블 이름을 바꿀 때는 신중한 검토가 필요합니다. 기존의 쿼리, 뷰, 사용자 정의 함수, 저장 프로시저 또는 프로그램에서 해당 테이블을 참조하는 경우 이름 수정으로 인해 이러한 개체가 유효하지 않게 됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **테이블 이름을 바꾸려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
 테이블 이름을 변경해도 해당 테이블에 대한 참조 이름은 자동으로 바뀌지 않습니다. 이름을 바꾼 테이블을 참조하는 개체는 수동으로 수정해야 합니다. 예를 들어 테이블 이름을 바꿨고 해당 테이블이 트리거에서 참조되는 경우 트리거를 수정하여 새로운 테이블 이름을 적용해야 합니다. 테이블 이름을 바꾸기 전에 테이블에 대한 종속성을 나열하려면 [sys.sql_expression_dependencies](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql) 를 사용합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-rename-a-table"></a>테이블 이름을 바꾸려면  
  
1.  개체 탐색기에서 이름을 바꾸려는 테이블을 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **디자인** 을 선택합니다.  
  
2.  **보기** 메뉴에서 **속성**을 선택합니다.  
  
3.  **속성** 창의 **이름** 값 필드에 테이블의 새 이름을 입력합니다.  
  
4.  이 동작을 취소하려면 이 필드를 나가기 전에 Esc 키를 누릅니다.  
  
5.  **파일** 메뉴에서_테이블 이름_ **저장**을 선택 합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-rename-a-table"></a>테이블 이름을 바꾸려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예에서는 `SalesTerritory` 스키마에 있는 `SalesTerr` 테이블의 이름을 `Sales` 로 바꿉니다. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    EXEC sp_rename 'Sales.SalesTerritory', 'SalesTerr';  
    ```  
  
 추가 예제를 보려면 [sp_rename&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql)을 참조하세요.  
  
  
