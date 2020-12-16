---
description: 사용자 정의 함수 보기
title: 사용자 정의 함수 보기 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.udfproperties.general.f1
- sql13.swb.functionproperties.general.f1
helpviewer_keywords:
- displaying user-defined functions
- viewing user-defined functions
- user-defined functions [SQL Server], viewing
- status information [SQL Server], user-defined functions
ms.assetid: a45dfab5-6384-4311-b935-2e23a70c5c10
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e14a690cb844c17fb0851a88307cacf612cf489d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461524"
---
# <a name="view-user-defined-functions"></a>사용자 정의 함수 보기
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 사용자 정의 함수의 정의 또는 속성에 대한 정보를 얻을 수 있습니다. 함수 정의를 보면 어떻게 데이터가 원본 테이블에서 파생되었는지 알 수 있고 함수에서 정의한 데이터를 볼 수 있습니다.  
  
> [!IMPORTANT]  
>  함수가 참조하는 개체의 이름을 변경하려면 함수를 수정하여 함수의 텍스트에 새 이름이 적용되도록 해야 합니다. 따라서 개체 이름을 바꾸기 전에 먼저 개체의 종속성을 표시하여 영향을 받는 함수가 있는지 확인해야 합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **함수에 대한 정보를 얻으려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 **sys.sql_expression_dependencies** 를 사용하여 함수에 대한 모든 종속성을 찾으려면 데이터베이스에 대한 VIEW DEFINITION 권한과 데이터베이스의 **sys.sql_expression_dependencies** 에 대한 SELECT 권한이 있어야 합니다. OBJECT_DEFINITION에 반환되는 정의와 같은 시스템 개체 정의는 모두에게 표시됩니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-show-a-user-defined-functions-properties"></a>사용자 정의 함수의 속성을 표시하려면  
  
1.  **개체 탐색기** 에서 속성을 볼 함수가 포함된 데이터베이스 옆의 더하기 기호를 클릭한 다음 더하기 기호를 클릭하여 **프로그래밍 기능** 폴더를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **함수** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 속성을 볼 함수가 포함된 폴더를 확장합니다.  
  
    -   테이블 반환 함수  
  
    -   스칼라 반환 함수  
  
    -   Aggregate 함수  
  
4.  속성을 볼 함수를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택합니다.  

     다음 속성이 **함수 속성 –** _function_name_ 대화 상자에 표시됩니다.  
  
     **Database**  
     이 함수를 포함하는 데이터베이스의 이름입니다.  
  
     **Server**  
     현재 서버 인스턴스의 이름입니다.  
  
     **사용자**  
     이 연결을 사용하는 사용자의 이름입니다.  
  
     **만든 날짜**  
     함수를 만든 날짜를 표시합니다.  
  
     **다음으로 실행**  
     함수에 대한 실행 컨텍스트입니다.  
  
     **이름**  
     현재 함수의 이름입니다.  
  
     **스키마**  
     함수를 소유하는 스키마를 표시합니다.  
  
     **시스템 개체**  
     함수가 시스템 개체인지 여부를 나타냅니다. 사용 가능한 값은 True와 False입니다.  
  
     **ANSI NULL**  
     개체가 ANSI NULL 옵션으로 생성되었는지 여부를 나타냅니다.  
  
     **암호화됨**  
     함수를 암호화하는지 여부를 나타냅니다. 사용 가능한 값은 True와 False입니다.  
  
     **함수 유형**  
     사용자 정의 함수의 유형입니다.  
  
     **따옴표 붙은 식별자**  
     개체가 따옴표 붙은 식별자 옵션으로 생성되었는지 여부를 나타냅니다.  
  
     **스키마 바운드**  
     스키마 바운드 함수인지 여부를 나타냅니다. 사용 가능한 값은 True와 False입니다. 스키마 바운드 함수에 대한 자세한 내용은 [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)의 SCHEMABINDING 섹션을 참조하세요.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-get-the-definition-and-properties-of-a-function"></a>함수의 정의 및 속성을 가져오려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예 중 하나를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the function name, definition, and relevant properties  
    SELECT sm.object_id,   
       OBJECT_NAME(sm.object_id) AS object_name,   
       o.type,   
       o.type_desc,   
       sm.definition,  
       sm.uses_ansi_nulls,  
       sm.uses_quoted_identifier,  
       sm.is_schema_bound,  
       sm.execute_as_principal_id  
    -- using the two system tables sys.sql_modules and sys.objects  
    FROM sys.sql_modules AS sm  
    JOIN sys.objects AS o ON sm.object_id = o.object_id  
    -- from the function 'dbo.ufnGetProductDealerPrice'  
    WHERE sm.object_id = OBJECT_ID('dbo.ufnGetProductDealerPrice')  
    ORDER BY o.type;  
    GO  
  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the definition of the function dbo.ufnGetProductDealerPrice  
    SELECT OBJECT_DEFINITION (OBJECT_ID('dbo.ufnGetProductDealerPrice')) AS ObjectDefinition;  
    GO  
    ```  
  
 자세한 내용은 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 및 [OBJECT_DEFINITION&#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)을 참조하세요.  
  
#### <a name="to-get-the-dependencies-of-a-function"></a>함수의 종속성을 가져오려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get all of the dependency information  
    SELECT OBJECT_NAME(sed.referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(sed.referencing_id, sed.referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        sed.referencing_class_desc, sed.referenced_class_desc,  
        sed.referenced_server_name, sed.referenced_database_name, sed.referenced_schema_name,  
        sed.referenced_entity_name,   
        COALESCE(COL_NAME(sed.referenced_id, sed.referenced_minor_id), '(n/a)') AS referenced_column_name,  
        sed.is_caller_dependent, sed.is_ambiguous  
    -- from the two system tables sys.sql_expression_dependencies and sys.object  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    -- on the function dbo.ufnGetProductDealerPrice  
    WHERE sed.referencing_id = OBJECT_ID('dbo.ufnGetProductDealerPrice');  
    GO  
    ```  
  
 자세한 내용은 [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 및 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조하세요.  
  
  
