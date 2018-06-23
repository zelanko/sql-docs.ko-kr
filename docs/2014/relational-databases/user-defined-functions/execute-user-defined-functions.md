---
title: 사용자 정의 함수 실행 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-udf
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6961d8306ff4b5a5f5280d25e3657952d0890063
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082443"
---
# <a name="execute-user-defined-functions"></a>사용자 정의 함수 실행
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 사용자 정의 함수를 실행할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **사용자 지정을 실행 하려면 함수를 사용 하 여:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 Transact-SQL에서 *value* 또는 @*parameter_name*=*value*를 사용하여 매개 변수를 제공할 수 있습니다. 를 사용하여 제공할 수 있습니다. 매개 변수는 트랜잭션의 일부가 아니므로 나중에 롤백되는 트랜잭션에서 매개 변수가 변경된 경우 해당 매개 변수의 값은 이전 값으로 되돌아가지 않습니다. 호출자에게 반환되는 값은 항상 모듈이 반환되는 시점의 값입니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 EXECUTE 문을 실행하는 데에는 사용 권한이 필요하지 않습니다. 그러나 EXECUTE 문자열 내에서 참조되는 보안 개체에 대해서는 사용 권한이 필요합니다. 예를 들어 문자열에 INSERT 문이 있는 경우 EXECUTE 문의 호출자에게는 대상 테이블에 대한 INSERT 권한이 있어야 합니다. EXECUTE 문이 모듈 내에 포함된 경우에도 EXECUTE 문이 실행될 때는 사용 권한 검사가 수행됩니다. 자세한 내용은 [EXECUTE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)를 참조하세요.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-execute-a-user-defined-function"></a>사용자 정의 함수를 실행하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Declares a variable and sets it to zero.  
    -- This variable is used to return the results of the function.  
    DECLARE @ret nvarchar(15)= NULL;   
  
    -- Executes the dbo.ufnGetSalesOrderStatusText function.  
    --The function requires a value for one parameter, @Status.   
    EXEC @ret = dbo.ufnGetSalesOrderStatusText @Status= 5;   
    --Returns the result in the message tab.  
    PRINT @ret;  
    ```  
  
 자세한 내용은 [EXECUTE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)을 참조하세요.  
  
  
