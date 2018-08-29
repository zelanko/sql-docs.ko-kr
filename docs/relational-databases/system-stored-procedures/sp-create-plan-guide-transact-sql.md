---
title: sp_create_plan_guide (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_create_plan_guide
- sp_create_plan_guide_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_plan_guide
ms.assetid: 5a8c8040-4f96-4c74-93ab-15bdefd132f0
caps.latest.revision: 82
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b33a8b9f5090d0e2d14467bc7fc9cb2a73c34b87
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038745"
---
# <a name="spcreateplanguide-transact-sql"></a>sp_create_plan_guide(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  쿼리 힌트 또는 실제 쿼리 계획을 데이터베이스의 쿼리와 연결하기 위한 계획 지침을 만듭니다. 계획 지침에 대한 자세한 내용은 [Plan Guides](../../relational-databases/performance/plan-guides.md)를 참조하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_create_plan_guide [ @name = ] N'plan_guide_name'  
    , [ @stmt = ] N'statement_text'  
    , [ @type = ] N'{ OBJECT | SQL | TEMPLATE }'  
    , [ @module_or_batch = ]  
      {   
                    N'[ schema_name. ] object_name'  
        | N'batch_text'  
        | NULL  
      }  
    , [ @params = ] { N'@parameter_name data_type [ ,...n ]' | NULL }   
    , [ @hints = ] { N'OPTION ( query_hint [ ,...n ] )'   
                 | N'XML_showplan'  
                 | NULL }  
```  
  
## <a name="arguments"></a>인수  
 [ \@이름 =] N'*plan_guide_name*'  
 계획 지침의 이름입니다. 계획 지침 이름은 현재 데이터베이스 범위에 적용됩니다. *plan_guide_name* 에 대 한 규칙을 따라야 [식별자](../../relational-databases/databases/database-identifiers.md) 하며 숫자 기호를 사용 하 여 시작할 수 없습니다 (#). 최대 길이인 *plan_guide_name* 는 124 자입니다.  
  
 [ \@stmt =] N'*statement_text*'  
 계획 지침을 만들 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 일치 하는 쿼리를 인식할 *statement_text*를 *plan_guide_name* 적용 됩니다. 성공 하는 계획 지침을 만들 *statement_text* 하 여 지정 된 컨텍스트에 나타나야 합니다 합니다 \@형식 \@module_or_batch, 및 \@params 매개 변수입니다.  
  
 *statement_text* 쿼리 최적화 프로그램에서 식별 된 모듈 또는 일괄 처리 내에서 제공 하는 해당 문을 사용 하 여 일치 시킬 수 있는 방식으로 제공 되어야 합니다 \@module_or_batch 및 \@매개 변수입니다. 자세한 내용은 "주의" 섹션을 참조하십시오. 크기인 *statement_text* 서버의 사용 가능한 메모리 크기로 제한 됩니다.  
  
 [\@유형 =] N'{개체 | SQL | 템플릿}'  
 엔터티 형식인 *statement_text* 나타납니다. 일치 하는 컨텍스트를 지정 하는이 *statement_text* 하 *plan_guide_name*합니다.  
  
 OBJECT  
 나타냅니다 *statement_text* 의 컨텍스트에서 표시 되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저, 스칼라 함수, 다중 문 테이블 반환 함수 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 현재 데이터베이스에서 DML 트리거.  
  
 SQL  
 나타냅니다 *statement_text* 독립 실행형 문 또는 일괄 처리를 전송할 수 있는 컨텍스트에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 임의 메커니즘을 통해. [!INCLUDE[tsql](../../includes/tsql-md.md)] 공용 언어 런타임 (CLR) 개체 또는 확장된 저장된 프로시저 또는 EXEC N을 사용 하 여 제출 된 문에 '*sql_string*', 서버에서 일괄적으로 처리 됩니다 하 고, 따라서로 식별 되어야 합니다 \@ 형식**=** 'SQL'. 쿼리 매개 변수화 힌트 SQL을 지정한 경우 {FORCED | 간단한}에 지정할 수는 \@매개 변수 힌트입니다.  
  
 TEMPLATE  
 계획 지침에 지정 된 형식으로 매개 변수화 되는 모든 쿼리에 적용 됨을 나타냅니다 *statement_text*합니다. 템플릿이 지정 된 경우 PARAMETERIZATION {FORCED | SIMPLE} 쿼리 힌트에 지정할 수는 \@매개 변수 힌트입니다. TEMPLATE 계획 지침에 대 한 자세한 내용은 참조 하세요. [계획 지침 사용 하 여 쿼리 매개 변수화 동작 지정](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)합니다.  
  
 [\@module_or_batch =] {N'[ *schema_name*합니다. ] *object_name*' | N'*batch_text*' | NULL }  
 개체의 이름을 지정 *statement_text* 나타나면 또는는 일괄 처리 텍스트 *statement_text* 나타납니다. 일괄 처리 텍스트를 사용 하 여 포함할 수 없습니다*데이터베이스* 문입니다.  
  
 응용 프로그램에서 전송한 일괄 처리를 일치 하는 계획 지침에 대 한 *batch_tex*t 동일한 형식으로 제공 되어야 합니다-문자를에 전송 된 것과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이 일치 작업을 더 효과적으로 처리하기 위해 내부 변환은 수행되지 않습니다. 자세한 내용은 주의 섹션을 참조하세요.  
  
 [*schema_name*.] *object_name* 의 이름을 지정 된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저, 스칼라 함수, 다중 문 테이블 반환 함수 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 포함 하는 DML 트리거 *statement_text*. 하는 경우 *schema_name* 지정 하지 않으면 *schema_name* 현재 사용자의 스키마를 사용 합니다. NULL을 지정 하는 경우 및 \@유형 = 'SQL', 값 \@module_or_batch의 값으로 설정 되어 \@stmt 합니다. 하는 경우 \@유형 = ' 템플릿을 **'**, \@module_or_batch는 NULL 이어야 합니다.  
  
 [ \@params =] {N'*\@parameter_name data_type* [합니다 *...n* ]' | NULL}  
 에 포함 된 모든 매개 변수의 정의 지정 합니다 *statement_text*합니다. \@params 인 경우에 다음 중 하나가 true 적용 됩니다.  
  
-   \@형식 = 'SQL' 또는 'TEMPLATE'. 경우 'TEMPLATE' \@params NULL 이어야 합니다.  
  
-   *statement_text* sp_executesql 및 값을 사용 하 여 제출 되는 \@params 매개 변수를 지정 하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부적으로 매개 변수화 한 후 전송 합니다. 데이터베이스 API(ODBC, OLE DB, ADO.NET 등)에서 매개 변수가 있는 쿼리의 전송은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 sp_executesql 또는 API 서버 커서 루틴에 대한 호출로 나타나므로 SQL 또는 TEMPLATE 계획 지침으로 일치시킬 수도 있습니다.  
  
 *\@parameter_name data_type* 에 전송 된 것과 정확히 같은 형식에 제공 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_executesql을 사용 하 여 매개 변수화 한 후 내부에서 전송한 또는 합니다. 자세한 내용은 주의 섹션을 참조하세요. 일괄 처리에 매개 변수가 없는 경우 NULL이 지정되어야 합니다. 크기 \@매개 변수는 서버의 사용 가능한 메모리 크기로 제한 됩니다.  
  
 [\@힌트 =] {N'OPTION (*query_hint* [합니다 *...n* ])' | N'*XML_showplan*' | NULL}  
 N'OPTION (*쿼리 힌트* [합니다 *...n* ])  
 일치 하는 쿼리에 연결할 OPTION 절을 지정 \@stmt. \@힌트 이어야 구문상 SELECT 문의 OPTION 절과 동일 하며 쿼리 힌트의 유효한 시퀀스를 포함할 수 있습니다.  
  
 N'*XML_showplan*'  
 힌트로 적용할 XML 형식의 쿼리 계획입니다.  
  
 XML 실행 계획을 변수에 할당하는 것이 좋습니다. 그렇지 않으면 실행 계획의 작은따옴표 앞에 다른 작은따옴표를 붙여 이스케이프 처리해야 합니다. 예 5를 참조하십시오.  
  
 NULL  
 쿼리의 OPTION 절에 지정된 기존 힌트는 쿼리에 적용되지 않음을 나타냅니다. 자세한 내용은 [OPTION 절 &#40;TRANSACT-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md)합니다.  
  
## <a name="remarks"></a>Remarks  
 sp_create_plan_guide 인수는 표시된 순서대로 제공해야 합니다. **sp_create_plan_guide**매개 변수 값을 제공하는 경우 모든 매개 변수 이름을 명시적으로 지정하거나 모두 지정하지 않아야 합니다. 예를 들어 경우  **\@이름 =** 을 지정한 경우  **\@stmt =** 를  **\@유형 =**, 등도 지정 해야 합니다. 마찬가지로, 하는 경우  **\@이름 =** 을 생략 하 고 유일한 매개 변수 값을 제공한 경우 나머지 매개 변수 이름도 생략 해야, 하 고 해당 값만 제공 합니다. 인수 이름은 구문 이해를 위한 설명 용도로만 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 지정된 매개 변수 이름과 해당 이름이 사용된 위치의 매개 변수 이름이 일치하는지 확인하지 않습니다.  
  
 같은 쿼리 및 일괄 처리나 모듈에 대해 두 개 이상의 OBJECT 또는 SQL 계획 지침을 만들 수 있습니다. 그러나 지정된 시간에 한 개의 계획 지침만 사용할 수 있습니다.  
  
 에 대 한 개체를 만들 수 없습니다 유형의 계획 지침을 \@저장된 프로시저, 함수 또는 WITH ENCRYPTION 절 또는 임시 인지 지정 하는 DML 트리거를 참조 하는 module_or_batch 값입니다.  
  
 활성화 여부에 관계없이 계획 지침에서 참조하는 함수, 저장 프로시저 또는 DML 트리거를 삭제하거나 수정하려고 하면 오류가 발생합니다. 계획 지침에서 참조하는 트리거가 정의되어 있는 테이블을 삭제하려는 경우에도 오류가 발생합니다.  
  
> [!NOTE]  
>  계획 지침은 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 일부 버전에서 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요. 계획 지침은 모든 버전에 표시됩니다. 계획 지침이 포함된 데이터베이스를 모든 버전에 추가할 수 있습니다. 업그레이드된 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 데이터베이스를 복원하거나 첨부해도 계획 지침은 그대로 유지됩니다. 서버를 업그레이드한 후에는 각 데이터베이스의 계획 지침을 원활하게 사용할 수 있는지 확인해야 합니다.  
  
## <a name="plan-guide-matching-requirements"></a>계획 지침 일치 요구 사항  
 지정 하는 계획 지침이 \@형식 = 'SQL' 또는 \@유형 = 'TEMPLATE' 값에 대 한 쿼리를 성공적으로 일치 *batch_text* 하 고  *\@parameter_name data_type*[,*...n* ] 응용 프로그램에서 전송 된 해당 부분과 정확히 같은 형식에 제공 되어야 합니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴파일러가 수신한 것과 정확히 같게 일괄 처리 텍스트를 제공해야 함을 의미합니다. 실제 일괄 처리 및 매개 변수 텍스트를 캡처하기 위해 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용할 수 있습니다. 자세한 내용은 [만들기 및 테스트 계획 지침을 사용 하 여 SQL Server Profiler](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md)합니다.  
  
 때 \@유형 = 'SQL' 및 \@module_or_batch의 값을 NULL로 설정 됩니다 \@module_or_batch의 값으로 설정 되어 \@stmt 합니다. 즉, 값 *statement_text* 정확히 같은 형식으로 제공 되어야 합니다-문자를에 전송 된 것과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이 일치 작업을 더 효과적으로 처리하기 위해 내부 변환은 수행되지 않습니다.  
  
 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값과 일치 *statement_text* 하려면 *batch_text* 하 고  *\@parameter_name data_type* [,*....n* ], 이거나 \@유형 = **'** 개체 ', 내에서 해당 쿼리를 텍스트로 *object_name*, 다음 문자열 요소가 고려 되지 않습니다:  
  
-   문자열 안에 있는 공백 문자(탭, 공백, 캐리지 리턴 또는 줄 바꿈)  
  
-   주석 (**--** 하거나 **/ \* \* /**).  
  
-   후행 세미콜론  
  
 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 매칭 합니다 *statement_text* 문자열 `N'SELECT * FROM T WHERE a = 10'` 다음과 *batch_text*:  
  
 `N'SELECT *`  
  
 `FROM T`  
  
 `WHERE a=10'`  
  
 그러나 동일한 문자열을이 일치 하지는 *batch_text*:  
  
 `N'SELECT * FROM T WHERE b = 10'`  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 첫째 쿼리 안에 있는 캐리지 리턴, 줄 바꿈 및 공백 문자를 무시합니다. 둘째 쿼리에서 `WHERE b = 10` 시퀀스는 `WHERE a = 10`과 다르게 해석됩니다. 일치 작업은 대/소문자를 구분하지 않는 키워드의 경우를 제외하고 데이터베이스의 데이터 정렬이 대/소문자를 구분하지 않는 경우에도 대/소문자와 액센트 기호를 구분합니다. 일치 작업은 키워드의 축약 형식을 구분하지 않습니다. 예를 들어 `EXECUTE`, `EXEC` 및 `execute` 키워드는 동일하게 간주됩니다.  
  
## <a name="plan-guide-effect-on-the-plan-cache"></a>계획 캐시의 계획 지침 효과  
 모듈에 대한 계획 지침을 만들면 계획 캐시에서 해당 모듈에 대한 쿼리 계획이 제거되고, 일괄 처리에 OBJECT 또는 SQL 유형의 계획 지침을 만들면 같은 해시 값을 가진 일괄 처리에 대한 쿼리 계획이 제거되며, TEMPLATE 유형의 계획 지침을 만들면 해당 데이터베이스 내의 계획 캐시에서 단일 문 일괄 처리가 모두 제거됩니다.  
  
## <a name="permissions"></a>사용 권한  
 OBJECT 유형의 계획 지침을 만들려면 참조된 개체에 ALTER 권한이 있어야 합니다. SQL 또는 TEMPLATE 유형의 계획 지침을 만들려면 현재 데이터베이스에 대한 ALTER 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-plan-guide-of-type-object-for-a-query-in-a-stored-procedure"></a>1. 저장 프로시저에 있는 쿼리에 대해 OBJECT 유형의 계획 지침 만들기  
 다음 예에서는 응용 프로그램 기반 저장 프로시저의 컨텍스트에서 실행된 쿼리와 일치하는 계획 지침을 만들고 해당 쿼리에 대해 `OPTIMIZE FOR` 힌트를 적용합니다.  
  
 저장 프로시저는 다음과 같습니다.  
  
```  
IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetSalesOrderByCountry;  
GO  
CREATE PROCEDURE Sales.GetSalesOrderByCountry   
    (@Country_region nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t   
        ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country_region;  
END  
GO  
```  
  
 저장 프로시저에 있는 쿼리에 대해 생성된 계획 지침은 다음과 같습니다.  
  
```  
EXEC sp_create_plan_guide   
    @name =  N'Guide1',  
    @stmt = N'SELECT *  
              FROM Sales.SalesOrderHeader AS h   
              INNER JOIN Sales.Customer AS c   
                 ON h.CustomerID = c.CustomerID  
              INNER JOIN Sales.SalesTerritory AS t   
                 ON c.TerritoryID = t.TerritoryID  
              WHERE t.CountryRegionCode = @Country_region',  
    @type = N'OBJECT',  
    @module_or_batch = N'Sales.GetSalesOrderByCountry',  
    @params = NULL,  
    @hints = N'OPTION (OPTIMIZE FOR (@Country_region = N''US''))';  
```  
  
### <a name="b-creating-a-plan-guide-of-type-sql-for-a-stand-alone-query"></a>2. 독립 실행형 쿼리에 대해 SQL 유형의 계획 지침 만들기  
 다음 예에서는 sp_executesql 시스템 저장 프로시저를 사용하는 응용 프로그램에서 전송한 일괄 처리에 있는 쿼리와 일치하는 계획 지침을 만듭니다.  
  
 일괄 처리는 다음과 같습니다.  
  
```  
SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC;  
```  
  
 병렬 실행 계획이 이 쿼리에서 생성되지 않도록 하려면 다음 계획 지침을 만드십시오.  
  
```  
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
  
### <a name="c-creating-a-plan-guide-of-type-template-for-the-parameterized-form-of-a-query"></a>3. 매개 변수가 있는 쿼리 형식에 대해 TEMPLATE 유형의 계획 지침 만들기  
 다음 예에서는 지정된 형식으로 매개 변수화되는 쿼리와 일치하는 계획 지침을 만들고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 쿼리를 매개 변수화하도록 지정합니다. 다음 두 개의 쿼리는 구문이 같고 상수 리터럴 값만 다릅니다.  
  
```  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45639;  
  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45640;  
```  
  
 매개 변수가 있는 쿼리 형식에 대한 계획 지침은 다음과 같습니다.  
  
```  
EXEC sp_create_plan_guide   
    @name = N'TemplateGuide1',  
    @stmt = N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
              INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
                  ON h.SalesOrderID = d.SalesOrderID  
              WHERE h.SalesOrderID = @0',  
    @type = N'TEMPLATE',  
    @module_or_batch = NULL,  
    @params = N'@0 int',  
    @hints = N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 앞의 예에서 `@stmt` 매개 변수의 값은 매개 변수가 있는 쿼리 형식입니다. sp_create_plan_guide에서 사용하기 위해 이 값을 얻는 안정적인 한 가지 방법은 [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) 시스템 저장 프로시저를 사용하는 것입니다. 다음 스크립트는 매개 변수가 있는 쿼리를 얻고 이에 대한 계획 지침을 만들기 위해 사용할 수 있습니다.  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
      INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
          ON h.SalesOrderID = d.SalesOrderID  
      WHERE h.SalesOrderID = 45639;',  
    @stmt OUTPUT,   
    @params OUTPUT  
EXEC sp_create_plan_guide N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
> [!IMPORTANT]  
>  sp_get_query_template에 전달된 `@stmt` 매개 변수에 있는 상수 리터럴 값은 리터럴을 대체하는 변수에 대해 선택한 데이터 형식에 영향을 미칠 수 있습니다. 이는 계획 지침 일치에도 영향을 미칩니다. 둘 이상의 계획 지침을 만들어 서로 다른 매개 변수 값 범위를 처리해야 할 수도 있습니다.  
  
### <a name="d-creating-a-plan-guide-on-a-query-submitted-by-using-an-api-cursor-request"></a>4. API 커서 요청을 사용하여 전송한 쿼리에 대해 계획 지침 만들기  
 계획 지침을 API 서버 커서 루틴에서 전송된 쿼리에 일치시킬 수 있습니다. 이러한 루틴에는 sp_cursorprepare, sp_cursorprepexec 및 sp_cursoropen이 있습니다. ADO, OLE DB 및 ODBC API를 사용하는 응용 프로그램은 API 서버 커서를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 자주 상호 작용합니다. RPC:Starting 프로파일러 추적 이벤트를 보고 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 추적에서 API 서버 커서 루틴의 호출을 확인할 수 있습니다.  
  
 계획 지침으로 튜닝하려는 쿼리에 대해 다음 데이터가 RPC:Starting 프로파일러 추적 이벤트에 표시된다고 가정합니다.  
  
```  
DECLARE @p1 int;  
SET @p1=-1;  
DECLARE @p2 int;  
SET @p2=0;  
DECLARE @p5 int;  
SET @p5=4104;  
DECLARE @p6 int;  
SET @p6=8193;  
DECLARE @p7 int;  
SET @p7=0;  
EXEC sp_cursorprepexec @p1 output,@p2 output,N'@P1 varchar(255),@P2 varchar(255)',N'SELECT * FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID WHERE h.OrderDate BETWEEN @P1 AND @P2',@p5 OUTPUT,@p6 OUTPUT,@p7 OUTPUT,'20040101','20050101'  
SELECT @p1, @p2, @p5, @p6, @p7;  
```  
  
 `SELECT`의 호출에서 `sp_cursorprepexec` 쿼리의 계획은 병합 조인을 사용하지만 사용자는 해시 조인을 사용하려고 합니다. `sp_cursorprepexec`를 사용하여 전송된 쿼리가 쿼리 문자열과 매개 변수 문자열 모두를 포함하여 매개 변수화됩니다. `sp_cursorprepexec`의 호출에서 문자 수준까지 정확히 일치하는 쿼리 및 매개 변수 문자열을 사용하여 계획의 선택 사항을 변경하기 위해 다음 계획 지침을 만들 수 있습니다.  
  
```  
EXEC sp_create_plan_guide   
    @name = N'APICursorGuide',  
    @stmt = N'SELECT * FROM Sales.SalesOrderHeader AS h   
              INNER JOIN Sales.SalesOrderDetail AS d   
                ON h.SalesOrderID = d.SalesOrderID   
              WHERE h.OrderDate BETWEEN @P1 AND @P2',  
    @type = N'SQL',  
    @module_or_batch = NULL,  
    @params = N'@P1 varchar(255),@P2 varchar(255)',  
    @hints = N'OPTION(HASH JOIN)';  
```  
  
 응용 프로그램에서 수행하는 이 쿼리의 후속 실행은 이 계획 지침의 영향을 받으며 쿼리를 처리하는 데 해시 조인이 사용됩니다.  
  
### <a name="e-creating-a-plan-guide-by-obtaining-the-xml-showplan-from-a-cached-plan"></a>5. 캐시된 계획에서 XML 실행 계획을 가져와 계획 지침 만들기  
 다음 예에서는 간단한 임시 SQL 문에 대한 계획 지침을 만듭니다. `@hints` 매개 변수에 직접 쿼리에 대한 XML 실행 계획을 지정하여 이 문에 대해 원하는 쿼리 계획을 계획 지침에 제공합니다. 예에서는 먼저 SQL 문을 실행하여 계획 캐시에 계획을 생성합니다. 이 예를 위해 생성된 계획이 원하는 계획이며 추가 쿼리 튜닝이 필요하지 않다고 가정합니다. 쿼리에 대한 XML 실행 계획은 `sys.dm_exec_query_stats`, `sys.dm_exec_sql_text`및 `sys.dm_exec_text_query_plan` 동적 관리 뷰를 쿼리하여 가져오고 `@xml_showplan` 변수에 할당됩니다. 그런 다음 `@xml_showplan` 변수는 `sp_create_plan_guide` 매개 변수의 `@hints` 문에 전달됩니다. 또는 [sp_create_plan_guide_from_handle](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md) 저장 프로시저를 사용하여 계획 캐시의 쿼리 계획에서 계획 지침을 만들 수 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;  
GO  
DECLARE @xml_showplan nvarchar(max);  
SET @xml_showplan = (SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%');  
  
EXEC sp_create_plan_guide   
    @name = N'Guide1_from_XML_showplan',   
    @stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints =@xml_showplan;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [계획 지침](../../relational-databases/performance/plan-guides.md)   
 [sp_control_plan_guide&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)   
 [sys.plan_guides&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_cached_plans &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md)   
 [sp_get_query_template &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md)  
  
  
