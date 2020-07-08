---
title: 새 계획 지침 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.designer.newplanguide.f1
helpviewer_keywords:
- creating plan guides
- plan guides [SQL Server]. creating
ms.assetid: e1ad78bb-4857-40ea-a0c6-dcf5c28aef2f
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: c8301bfe9073a31020fe4481edfff24d89b68994
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85655642"
---
# <a name="create-a-new-plan-guide"></a>새 계획 지침 만들기
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
계획 지침은 쿼리 힌트나 정해진 쿼리 계획을 쿼리에 연결하여 쿼리 최적화에 영향을 미칩니다. 계획 지침에서 최적화하려는 문을 지정하고 사용할 쿼리 힌트가 들어 있는 OPTION 절이나 쿼리를 최적화하는 데 사용할 특정 쿼리 계획을 지정합니다. 쿼리가 실행하면 쿼리 최적화 프로그램이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 계획 지침과 비교하여 런타임에 쿼리에 OPTION 절을 추가하거나 지정된 쿼리 계획을 사용합니다.  

계획 지침에서는 해결된 쿼리 계획 및/또는 쿼리 힌트를 쿼리에 적용합니다.
  
##  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
-   sp_create_plan_guide 인수는 표시된 순서대로 제공해야 합니다. **sp_create_plan_guide**매개 변수 값을 제공하는 경우 모든 매개 변수 이름을 명시적으로 지정하거나 모두 지정하지 않아야 합니다. 예를 들어 **@name =** 을 지정한 경우 **@stmt =** , **@type =** 등도 지정해야 합니다. 마찬가지로 **@name =** 을 생략하고 매개 변수 값만 제공한 경우 나머지 매개 변수 이름도 생략하고 해당 값만 제공해야 합니다. 인수 이름은 구문 이해를 위한 설명 용도로만 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 지정된 매개 변수 이름과 해당 이름이 사용된 위치의 매개 변수 이름이 일치하는지 확인하지 않습니다.  
  
-   같은 쿼리 및 일괄 처리나 모듈에 대해 두 개 이상의 OBJECT 또는 SQL 계획 지침을 만들 수 있습니다. 그러나 지정된 시간에 한 개의 계획 지침만 사용할 수 있습니다.  
  
-   저장 프로시저, 함수 또는 WITH ENCRYPTION 절을 지정하거나 임시인 DML 트리거를 참조하는 @module_or_batch 값에 대해서는 OBJECT 유형의 계획 지침을 만들 수 없습니다.  
  
-   활성화 여부에 관계없이 계획 지침에서 참조하는 함수, 저장 프로시저 또는 DML 트리거를 삭제하거나 수정하려고 하면 오류가 발생합니다. 계획 지침에서 참조하는 트리거가 정의되어 있는 테이블을 삭제하려는 경우에도 오류가 발생합니다.  

##  <a name="permissions"></a><a name="Permissions"></a> 권한  
 OBJECT 유형의 계획 지침을 만들려면 참조된 개체에 ALTER 권한이 있어야 합니다. SQL 또는 TEMPLATE 유형의 계획 지침을 만들려면 현재 데이터베이스에 대한 ALTER 권한이 있어야 합니다.  
  
##  <a name="create-a-plan-guide-using-ssms"></a><a name="SSMSProcedure"></a> SSMS를 사용하여 계획 지침 만들기  
1.  더하기 기호를 클릭하여 계획 지침을 만들 데이터베이스를 확장한 다음 더하기 기호를 클릭하여 **프로그래밍 기능** 폴더를 확장합니다.  
  
2.  **계획 지침** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 계획 지침...** 을 선택합니다. ![select_plan_guide](../../relational-databases/performance/media/select-plan-guide.png)
  
3.  **새 계획 지침** 대화 상자의 **이름** 입력란에 계획 지침 이름을 입력합니다.  
  
4.  **문** 입력란에 계획 지침이 적용되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 입력합니다.  
  
5.  **범위 유형** 목록에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 나타나는 엔터티 유형을 선택합니다. 이것은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 계획 지침과 일치시키기 위한 컨텍스트를 제공합니다. 가능한 값은 **OBJECT**, **SQL**및 **TEMPLATE**입니다.  
  
6.  **범위 일괄 처리** 입력란에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 나타나는 일괄 처리 텍스트를 입력합니다. 일괄 처리 텍스트는 `USE`*database* 문을 포함할 수 없습니다. **범위 일괄 처리** 입력란은 **SQL** 이 범위 유형으로 선택되어 있는 경우에만 사용할 수 있습니다. 범위 유형이 SQL인 경우 범위 일괄 처리 입력란에 아무 것도 입력하지 않으면 일괄 처리 텍스트 값은 **문** 입력란의 값과 동일한 값으로 설정됩니다.  
  
7.  **범위 스키마 이름** 목록에 개체가 포함되는 스키마의 이름을 입력합니다. **범위 스키마 이름** 입력란은 **개체** 가 범위 유형으로 선택되어 있는 경우에만 사용할 수 있습니다.  
  
8.  **범위 개체 이름** 입력란에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 나타나는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저의 이름, 사용자 정의 스칼라 함수, 다중 문 테이블 반환 함수 또는 DML 트리거를 입력합니다. **범위 개체 이름** 입력란은 **개체** 가 범위 유형으로 선택되어 있는 경우에만 사용할 수 있습니다.  
  
9. **매개 변수** 입력란에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 포함된 모든 매개 변수의 데이터 형식과 매개 변수 이름을 입력합니다.  
  
   매개 변수는 다음 중 하나에 해당하는 경우에만 적용됩니다.  
  
   -   범위 유형이 **SQL** 또는 **TEMPLATE**인 경우. **TEMPLATE**일 경우 매개 변수는 NULL일 수 없습니다.  
  
   -   sp_executesql을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 전송되고 매개 변수에 대한 값이 지정된 경우 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 문을 매개 변수화한 후에 내부에서 전송하는 경우.  
  
10. **힌트** 입력란에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 적용되는 쿼리 힌트 또는 쿼리 계획을 입력합니다. 하나 이상의 쿼리 힌트를 지정하려면 유효한 OPTION 절을 입력합니다.  
  
11. **확인**을 클릭합니다.  

![plan_guide](../../relational-databases/performance/media/plan-guide.png)  

##  <a name="create-a-plan-guide-using-t-sql"></a><a name="TsqlProcedure"></a> T-SQL을 사용하여 계획 지침 만들기  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```sql  
    -- creates a plan guide named Guide1 based on a SQL statement  
    EXEC sp_create_plan_guide   
        @name = N'Guide1',   
        @stmt = N'SELECT TOP 1 *   
                  FROM Sales.SalesOrderHeader   
                  ORDER BY OrderDate DESC',   
        @type = N'SQL',  
        @module_or_batch = NULL,   
        @params = NULL,   
        @hints = N'OPTION (MAXDOP 1)';  
  
    ```  

자세한 내용은 [sp_create_plan_guide&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)를 참조하세요.  

  
