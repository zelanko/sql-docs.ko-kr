---
title: "행 수준 보안 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/29/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "액세스 제어 조건자"
  - "행 수준 보안"
  - "보안 [SQL Server], 조건자 기반 액세스 제어"
  - "행 수준 보안 설명됨"
  - "조건자 기반 보안"
ms.assetid: 7221fa4e-ca4a-4d5c-9f93-1b8a4af7b9e8
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# 행 수준 보안
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  ![Row level security graphic](../../relational-databases/security/media/row-level-security-graphic.png "Row level security graphic")  
  
 행 수준 보안(RLS)을 통해 고객은 쿼리(예: 그룹 멤버십 또는 실행 컨텍스트)를 실행하는 사용자의 특징을 기반으로 데이터베이스 테이블의 행에 대한 액세스를 제어할 수 있습니다.  
  
 행 수준 보안(RLS)은 응용 프로그램의 보안 설계 및 코딩을 간소화합니다. RLS를 사용하면 데이터 행 액세스에 제한을 둘 수 있습니다. 예를 들어, 작업자가 자신의 부서와 관련된 데이터 행에만 액세스할 수 있도록 하거나, 고객의 데이터 액세스를 회사와 관련된 데이터에만 액세스하도록 제한할 수 있습니다.  
  
 액세스 제한 논리는 다른 응용 프로그램 계층의 데이터와 다소 떨어진 데이터베이스 계층에 위치합니다. 데이터베이스 시스템은 모든 계층에서 데이터 액세스를 시도할 때마다 액세스를 제한합니다. 이로 인해 보안 시스템의 노출 영역이 감소되어 보안 시스템이 더 안정적이고 강력해집니다.  
  
 [CREATE SECURITY POLICY](../../t-sql/statements/create-security-policy-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하고 [인라인 테이블 반환 함수](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)로서 만들어진 조건자에 의해 RLS를 구현합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]~[현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]\([이해하기](http://azure.micosoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))|  
  
##  <a name="Top"></a> 항목 내용  
  
-   [설명](#Description)  
  
-   [사용 사례](#UseCases)  
  
-   [사용 권한](#Permissions)  
  
-   [최선의 구현 방법](#Best)  
  
-   [보안 정보: 사이드 채널 공격](#SecNote)  
  
-   [기능 간 호환성](#Limitations)  
  
-   [코드 예제](#CodeExamples)  
  
    -   [1. 직접 연결된 사용자의 시나리오](#Typical)  
  
    -   [2. 중간 계층 응용 프로그램 시나리오](#MidTier)  
  
##  <a name="Description"></a> 설명  
 RLS는 두 가지 유형의 보안 조건자를 지원합니다.  
  
-   필터 조건자는 읽기 작업(SELECT, UPDATE 및 DELETE)에 사용 가능한 행을 자동으로 필터링합니다.  
  
-   차단 조건자는 조건자를 위반하는 쓰기 작업(AFTER INSERT, AFTER UPDATE, BEFORE UPDATE, BEFORE DELETE)을 명시적으로 차단합니다.  
  
 테이블의 행 수준 데이터에 대한 액세스는 인라인 테이블 반환 함수로 정의된 보안 조건자에 의해 제한됩니다. 그런 다음 함수가 호출되고 보안 정책에 의해 적용됩니다. 필터 조건자의 경우 결과 집합으로부터 행이 필터링된 응용 프로그램에 대한 표시가 없습니다. 모든 행이 필터링되었으면 null 집합이 반환됩니다. 차단 조건자의 경우 조건자를 위반하는 모든 작업은 오류와 함께 실패합니다.  
  
 기본 테이블로부터 데이터를 읽는 동안 필터 조건이 적용되며, 모든 get 연산에 영향을 미칩니다. **SELECT**, **DELETE**(즉, 사용자가 필터링된 행을 삭제할 수 없음) 및 **UPDATE**(즉, 행이 이후 필터링되면서 업데이트될 수는 있어도 사용자가 필터링된 행을 업데이트할 수는 없음). 차단 조건자는 모든 쓰기 작업에 영향을 줍니다.  
  
-   AFTER INSERT 및 AFTER UPDATE 조건자는 사용자가 조건자를 위반하는 값으로 행을 업데이트하는 것을 방지할 수 있습니다.  
  
-   BEFORE UPDATE 조건자는 사용자가 현재 조건자를 위반하는 행을 업데이트하는 것을 방지할 수 있습니다.  
  
-   BEFORE DELETE 조건자는 삭제 작업을 차단할 수 있습니다.  
  
 필터 조건자와 차단 조건자 및 보안 정책 모두 다음 동작을 수행합니다.  
  
-   다른 테이블과 조인하거나 함수를 호출하는 조건자 함수를 정의할 수 있습니다. `SCHEMABINDING = ON`을 사용하여 보안 정책을 만든 경우에는 조인 또는 함수를 쿼리에서 액세스할 수 있으며, 다른 추가 권한 검사 없이 올바르게 작동 합니다. `SCHEMABINDING = OFF`를 사용하여 보안 정책을 만든 경우에는 대상 테이블을 쿼리하기 위해 이러한 추가 테이블 및 함수에 대해 **SELECT** 또는 **EXECUTE** 권한이 필요합니다.  
  
     다른 테이블과 조인하거나 함수를 호출하는 조건자 함수를 정의할 수 있습니다. 조인/함수는 쿼리로부터 액세스할 수 있으며, 다른 추가 권한 검사 없이 올바르게 작동합니다.  
  
-   정의되었지만 사용할 수 없는 보안 조건자가 있는 테이블에 대한 쿼리를 실행할 수 있습니다. 필터링되거나 차단된 행은 영향을 받지 않습니다.  
  
-   dbo 사용자, **db_owner** 역할의 멤버 또는 테이블 소유자가 보안 정책이 정의되고 사용되는 테이블에 대해 쿼리한 경우 행은 보안 정책에 의해 정의된 대로 필터링되거나 차단됩니다.  
  
-   스키마 바운드 보안 정책에 의해 바인딩된 테이블의 스키마를 변경하려 하면 오류가 발생합니다. 그러나 조건자에 의해 참조되지 않는 열은 변경할 수 있습니다.  
  
-   지정된 작업에 대해 정의된 조건자가 이미 있는 테이블에 조건자를 추가하려고 하면(사용 가능 여부에 관계없이) 오류가 발생합니다.  
  
-   스키마 바운드 보안 정책의 경우 보안 정책 내의 테이블에 있는 조건자로 사용되는 함수를 변경하려고 하면 오류가 발생합니다.  
  
-   겹치지 않는 조건자를 포함하는 복수의 활성 보안 정책 정의가 이어집니다.  
  
 필터 조건자는 다음 동작을 수행합니다.  
  
-   테이블의 행을 필터링하는 보안 정책을 정의합니다. 응용 프로그램은 모든 행이 필터링된 경우를 포함하여 **SELECT**, **UPDATE**및 **DELETE** 연산에 대해 필터링된 모든 행을 인식하지 못합니다. 응용 프로그램은 다른 연산 도중 필터링될지 여부에 관계없이 모든 행을 **INSERT** 할 수 있습니다.  
  
 차단 조건자는 다음 동작을 수행합니다.  
  
-   UPDATE에 대한 차단 조건자는 BEFORE 및 AFTER에 대해 별도의 작업으로 분할됩니다. 따라서 예를 들어 사용자가 행을 현재보다 큰 값으로 업데이트하는 것을 차단할 수 없습니다. 이러한 종류의 논리가 필요한 경우 DELETED 및 INSERTED 중간 테이블과 함께 트리거를 사용하여 이전 값과 새 값을 함께 참조해야 합니다.  
  
-   최적화 프로그램은 조건자 함수에서 사용하는 열이 변경되지 않은 경우 AFTER UPDATE 차단 조건자를 확인하지 않습니다. 예를 들어 Alice는 급여를 100,000보다 크게 변경할 수 없지만 급여가 이미 100,000을 초과하는(따라서 이미 조건자를 위반하는) 직원의 주소를 변경할 수는 있습니다.  
  
-   BULK INSERT를 포함하여 대량 API에 적용된 변경 내용은 없습니다. 따라서 일반적인 삽입 작업과 마찬가지로 차단 조건자 AFTER INSERT가 대량 삽입 작업에 적용됩니다.  
  
 [위쪽](#Top)  
  
##  <a name="UseCases"></a> 사용 사례  
 RLS 사용 방법에 대한 설계 예는 다음과 같습니다.  
  
-   병원에서 간호사가 담당 환자의 데이터 행만을 볼 수 있게 하는 보안 정책을 만들 수 있습니다.  
  
-   은행에서 직원의 업무 부서에 따라, 또는 회사 내에서 직원의 역할에 따라 금융 데이터 행에 대한 액세스를 제한하는 정책을 만들 수 있습니다.  
  
-   다중 테넌트 응용 프로그램은 모든 다른 테넌트 행으로부터 각 테넌트의 데이터 행의 논리적 분리를 적용하는 정책을 만들 수 있습니다. 여러 테넌트의 데이터를 하나의 테이블에 저장하여 효율성을 높일 수 있습니다. 물론 각 테넌트는 각자의 데이터 행만 볼 수 있습니다.  
  
 RLS 필터 조건자는 **WHERE** 절을 추가한 것과 기능적으로 동일합니다. 조건자는 업무 관례 명령처럼 복잡해질 수 있으며, 또는 절은 `WHERE TenantId = 42`처럼 간단해질 수 있습니다.  
  
 더 공식적인 용어로는, RLS는 조건자 기반 액세스 제어를 말합니다. 여기에는 유연하고, 중앙 집중적이며, 조건자 기반 평가가 있어 메타데이터 또는 관리자가 적절히 판단한 기타 기준을 고려할 수 있습니다. 조건자는 사용자 특성에 따라 사용자가 데이터에 적절하게 액세스하는지의 여부를 결정하는 기준으로 사용됩니다. 조건자 기반 액세스 제어를 사용하여 레이블 기반 액세스 제어를 구현할 수 있습니다.  
  
 [위쪽](#Top)  
  
##  <a name="Permissions"></a> 사용 권한  
 보안 정책을 만들거나, 변경하거나, 삭제하는 데에는 **ALTER ANY SECURITY POLICY** 권한이 필요합니다. 보안 정책을 만들거나 삭제하려면 스키마에 대한 **ALTER** 권한이 필요합니다.  
  
 또한 추가된 각 조건자에는 다음 권한이 필요합니다.  
  
-   조건자로 사용되는 함수에 대한**SELECT** 및 **REFERENCES** 권한.  
  
-   정책에 바인딩되는 대상 테이블에 대한**REFERENCES** 권한.  
  
-   인수로 사용하는 대상 테이블의 모든 열에 대한**REFERENCES** 권한.  
  
 보안 정책은 데이터베이스의 dbo 사용자를 포함한 모든 사용자에게 적용됩니다. Dbo 사용자는 보안 정책을 변경하거나 삭제할 수 있지만 해당 변경은 감사를 받을 수 있습니다. 높은 권한이 있는 사용자(예: sysadmin 또는 db_owner)가 문제를 해결하거나 데이터의 유효성을 검사하기 위해 모든 행을 볼 수 있어야 하는 경우 이를 허용하도록 보안 정책을 작성해야 합니다.  
  
 `SCHEMABINDING = OFF`를 사용하여 보안 정책을 만든 경우 대상 테이블을 쿼리하려면 조건자 함수에 대한 **SELECT** 또는 **EXECUTE** 권한과 조건자 함수 내에서 사용되는 추가 테이블, 뷰 또는 함수가 있어야 합니다. `SCHEMABINDING = ON`(기본값)을 사용하여 보안 정책을 만든 경우 사용자가 대상 테이블을 쿼리할 때 이러한 권한 검사는 무시됩니다.  
  
 [위쪽](#Top)  
  
##  <a name="Best"></a> 최선의 구현 방법  
  
-   RLS 개체(조건자 함수 및 보안 정책)에 대한 별도의 스키마를 만들 것을 적극 권장합니다.  
  
-   **ALTER ANY SECURITY POLICY** 권한은 보안 정책 관리자와 같은 높은 권한을 가진 사용자를 위한 것입니다. 보안 정책 관리자는 보호하는 테이블에 대한 **SELECT** 권한이 필요하지 않습니다.  
  
-   잠재적인 런타임 오류를 방지하려면 조건자 함수에서 형식을 변환하지 마십시오.  
  
-   성능 저하를 방지하려면 조건자 함수에서 가능한 재귀를 피하십시오. 쿼리 최적화 프로그램은 직접 재귀를 감지하지만 간접 재귀(즉, 두 번째 함수가 조건자 함수를 호출하는 경우)를 찾아낸다고 보장할 수는 없습니다.  
  
-   성능을 최대화하기 위해 조건자 함수에서 과도한 테이블 조인을 사용하지 마십시오.  
  
 세션별 [SET 옵션](../../t-sql/statements/set-statements-transact-sql.md)에 종속되는 조건자 논리 방지: 실제 응용 프로그램에서는 사용되지 않지만 해당 논리가 특정 세션별 **SET** 옵션에 종속되는 조건자 함수는 사용자가 임의 쿼리를 실행할 수 있는 경우 정보를 누출할 수 있습니다. 예를 들어 문자열을 암시적으로 **datetime** 으로 변환하는 조건자 함수는 현재 세션에 대해 **SET DATEFORMAT** 옵션을 기반으로 여러 행을 필터링할 수 있습니다. 일반적으로 조건자 함수는 다음과 같은 규칙을 준수해야 합니다.  
  
-   조건자 함수는 문자열을 암시적으로 **date**, **smalldatetime**, **datetime**, **datetime2** 또는 **datetimeoffset**으로 변환하거나 그 반대로 변환하지 않아야 합니다. 이러한 변환은 [SET DATEFORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md) 및 [SET LANGUAGE&#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md) 옵션의 영향을 받기 때문입니다. 대신 **CONVERT** 함수를 사용하여 스타일 매개 변수를 명시적으로 지정합니다.  
  
-   조건자 함수는 주의 첫 번째 요일 값에 의존하지 않아야 합니다. 이 값은 [SET DATEFIRST&#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md) 옵션의 영향을 받기 때문입니다.  
  
-   조건자 함수는 오류(예: 오버플로 또는 0으로 나누기)가 발생한 경우 **NULL**을 반환하는 산술 또는 집계 식을 사용하지 않아야 합니다. 이 동작은 [SET ANSI_WARNINGS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md), [SET NUMERIC_ROUNDABORT&#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md) 및 [SET ARITHABORT&#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md) 옵션의 영향을 받기 때문입니다.  
  
-   조건자 함수는 연결된 문자열을 **NULL**과 비교하지 않아야 합니다. 이 동작은 [SET CONCAT_NULL_YIELDS_NULL&#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md) 옵션의 영향을 받기 때문입니다.  
  
 [위쪽](#Top)  
  
##  <a name="SecNote"></a> 보안 정보: 사이드 채널 공격  
 **악의적인 보안 정책 관리자:** 중요한 열의 상단에 보안 정책을 만들 수 있는 권한과 인라인 테이블 반환 함수를 만들거나 변경할 수 있는 권한을 가지고, 데이터를 추론하기 위해 부채널 공격을 사용하도록 설계된 인라인 테이블 반환 함수를 악의적으로 만들어 데이터를 유출할 목적으로 테이블의 선택 권한을 가진 다른 사용자와 공모할 수 있는 악의적인 보안 정책 관리자를 관찰하는 것이 중요합니다. 이러한 공격에는 공모(또는 악의적인 사용자에게 부여된 과도한 권한)가 필요하고, 정책(스키마 바인딩을 중단하기 위해 조건자를 제거하는 데 권한 필요) 및 인라인 테이블 반환 함수를 여러 번 수정이 필요하며, 대상 테이블에서 select 문의 반복 실행이 필요합니다. 필요에 따라 권한을 제한하고 자주 변경되는 정책과 행 수준 보안과 관련된 인라인 테이블 반환 함수 등과 같은 의심스러운 활동을 모니터링하는 것을 매우 권장합니다.  
  
 **정교하게 만들어진 쿼리:** 정교하게 만들어진 쿼리를 통해 정보가 누출될 수 있습니다. 예를 들어, 악의적인 사용자가 `SELECT 1/(SALARY-100000) FROM PAYROLL WHERE NAME='John Doe'`을(를) 통해 John Doe의 급료가 $100,000임을 알게 됩니다. 악의적인 사용자가 타인의 급여를 직접 쿼리하는 것을 방지하기 위해 보안 조건자가 있더라도, 해당 사용자는 쿼리가 0으로 나누기 예외를 반환할 때 알아낼 수 있습니다.  
  
 [위쪽](#Top)  
  
##  <a name="Limitations"></a> 기능 간 호환성  
 일반적으로 행 수준 보안은 기능 간에 예상대로 작동합니다. 그러나 몇 가지 예외가 있습니다. 이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 특정 다른 기능과 함께 행 수준 보안을 사용할 대의 몇 가지 주의 사항을 설명합니다.  
  
-   **DBCC SHOW_STATISTICS**는 필터링되지 않은 데이터에 대한 통계치를 보고하기 때문에 보안 정책에 의해 보호되더라도 정보가 누출될 수 있습니다. 따라서 행 수준 보안 정책이 적용되는 테이블에 대한 통계 개체를 보려면 테이블의 소유자이거나 sysadmin 고정 서버 역할, db_owner 고정 데이터베이스 역할 또는 db_ddladmin 고정 데이터베이스 역할의 멤버여야 합니다.  
  
-   **Filestream** RLS는 Filestream과 호환되지 않습니다.  
  
-   **Polybase** RLS는 Polybase와 호환되지 않습니다.  
  
-   **메모리 액세스에 최적화된 테이블** 메모리에 최적화된 테이블에서 보안 조건자로 사용되는 인라인 테이블 반환 함수는 `WITH NATIVE_COMPILATION` 옵션을 사용하여 정의해야 합니다. 이 옵션을 사용하면 메모리에 최적화된 테이블에서 지원되지 않는 언어 기능이 차단되며 만들 때 해당 오류가 발생합니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블 소개](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md)의 **메모리 액세스에 최적화된 테이블의 행 수준 보안** 섹션을 참조하세요.  
  
-   **인덱싱된 뷰** 일반적으로 보안 정책은 뷰를 기반으로 만들 수 있으며 뷰는 보안 정책에 의해 바인딩된 테이블을 기반으로 만들 수 있습니다. 그러나 인덱스를 통한 행 조회는 정책을 무시하기 때문에 보안 정책이 있는 테이블을 기반으로 인덱싱된 뷰를 만들 수는 없습니다.  
  
-   **변경 데이터 캡처** 변경 데이터 캡처는 테이블에 CDC를 사용하도록 설정할 때 지정된 "제어" 역할의 멤버인 사용자 또는 **db_owner**의 멤버로 필터링해야 하는 전체 행을 누출할 수 있습니다(참고: 모든 사용자가 변경 데이터에 액세스할 수 있도록 이를 명시적으로 **NULL**로 설정할 수 있음). 실제로 **db_owner** 및 이 제어 역할의 멤버는 테이블에 대한 보안 정책이 있는 경우에도 테이블의 모든 데이터 변경 내용을 볼 수 있습니다.  
  
-   **변경 내용 추적** 변경 내용 추적은 **SELECT** 및 **VIEW CHANGE TRACKING** 권한이 있는 사용자로 필터링해야 하는 행의 기본 키를 누출할 수 있습니다. 실제 데이터 값은 누출되지 않습니다. 기본 키가 B인 행에 대해 열 A가 업데이트/삽입/삭제되었다는 사실만 누출됩니다. 이는 기본 키에 주민 등록 번호와 같은 기밀 요소가 포함된 경우 문제가 될 수 있습니다. 그러나 실제로 이 **CHANGETABLE** 은 최신 데이터를 가져오기 위해 거의 항상 원래 테이블과 조인됩니다.  
  
-   **전체 텍스트 검색** **CONTAINSTABLE**, **FREETEXTTABLE**, semantickeyphrasetable, semanticsimilaritydetailstable, semanticsimilaritytable 등의 전체 텍스트 검색 및 의미 체계 검색 함수를 사용하는 쿼리는 행 수준 보안을 적용하고 필터링해야 하는 행의 기본 키 누출을 방지하기 위해 추가 조인이 도입되므로 성능 저하가 예상됩니다.  
  
-   **Columnstore 인덱스** RLS는 클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스 모두와 호환됩니다. 그러나 행 수준 보안이 함수에 적용되기 때문에 최적화 프로그램에서 배치 모드를 사용하지 않도록 쿼리 계획을 수정할 수 있습니다.  
  
-   **분할 뷰** 분할 뷰에는 차단 조건자를 정의할 수 없으며, 차단 조건자를 사용하는 테이블을 기반으로 분할 뷰를 만들 수 없습니다. 필터 조건자는 분할 뷰와 호환됩니다.  
  
-   **임시 테이블** 은 RLS와 호환됩니다. 그러나 현재 테이블의 보안 조건자는 기록 테이블에 자동으로 복제되지 않습니다. 현재 및 기록 테이블 모두에 보안 정책을 적용하려면 각 테이블에서 개별적으로 보안 조건자를 추가해야 합니다.  
  
 [위쪽](#Top)  
  
##  <a name="CodeExamples"></a> 예  
  
###  <a name="Typical"></a> 1. 데이터베이스에 인증하는 사용자에 대한 시나리오  
 이 간단한 예에서는 3명의 사용자를 만들고 6개 행의 테이블을 만들어 채운 다음, 인라인 테이블 반환 함수와 테이블에 대한 보안 정책을 만듭니다. 예에서는 select 문이 다양한 사용자를 필터링하는 방법을 보여줍니다.  
  
 서로 다른 액세스 기능을 보여주는 3개의 사용자 계정을 만듭니다.  
  
```  
CREATE USER Manager WITHOUT LOGIN;  
CREATE USER Sales1 WITHOUT LOGIN;  
CREATE USER Sales2 WITHOUT LOGIN;  
```  
  
 데이터를 보유하는 간단한 테이블을 만듭니다.  
  
```  
CREATE TABLE Sales  
    (  
    OrderID int,  
    SalesRep sysname,  
    Product varchar(10),  
    Qty int  
    );  
```  
  
 각 영업 담당자별로 3개의 주문을 보여주는 6행의 데이터로 테이블을 채웁니다.  
  
```  
INSERT Sales VALUES   
(1, 'Sales1', 'Valve', 5),   
(2, 'Sales1', 'Wheel', 2),   
(3, 'Sales1', 'Valve', 4),  
(4, 'Sales2', 'Bracket', 2),   
(5, 'Sales2', 'Wheel', 5),   
(6, 'Sales2', 'Seat', 5);  
-- View the 6 rows in the table  
SELECT * FROM Sales;  
```  
  
 각 사용자에게 테이블에 읽기 액세스 권한을 부여합니다.  
  
```  
GRANT SELECT ON Sales TO Manager;  
GRANT SELECT ON Sales TO Sales1;  
GRANT SELECT ON Sales TO Sales2;  
```  
  
 새로운 스키마 및 인라인 테이블 반환 함수를 만듭니다. SalesRep 열이 사용자가 실행한 쿼리와 동일한 경우(`@SalesRep = USER_NAME()`) 또는 쿼리를 실행한 사용자가 Manager 사용자(`USER_NAME() = 'Manager'`)인 경우, 함수는 1을 반환합니다.  
  
```  
CREATE SCHEMA Security;  
GO  
  
CREATE FUNCTION Security.fn_securitypredicate(@SalesRep AS sysname)  
    RETURNS TABLE  
WITH SCHEMABINDING  
AS  
    RETURN SELECT 1 AS fn_securitypredicate_result   
WHERE @SalesRep = USER_NAME() OR USER_NAME() = 'Manager';  
```  
  
 필터 조건자로 함수를 추가하는 보안 정책을 만듭니다. 정책을 활성화하려면 상태는 ON으로 설정해야 합니다.  
  
```  
CREATE SECURITY POLICY SalesFilter  
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesRep)   
ON dbo.Sales  
WITH (STATE = ON);  
```  
  
 이제 각 사용자로 Sales 테이블에서 선택하여 필터링 조건자를 테스트합니다.  
  
```  
EXECUTE AS USER = 'Sales1';  
SELECT * FROM Sales;   
REVERT;  
  
EXECUTE AS USER = 'Sales2';  
SELECT * FROM Sales;   
REVERT;  
  
EXECUTE AS USER = 'Manager';  
SELECT * FROM Sales;   
REVERT;  
```  
  
 관리자는 6행 모두를 볼 수 있습니다. Sales1 및 Sales2 사용자는 자신의 판매 행만 볼 수 있습니다.  
  
 정책을 사용하지 않도록 보안 정책을 변경합니다.  
  
```  
ALTER SECURITY POLICY SalesFilter  
WITH (STATE = OFF);  
```  
  
 이제 Sales1 및 Sales2 사용자가 6 행 모두를 볼 수 있게 됩니다.  
  
 [위쪽](#Top)  
  
###  <a name="MidTier"></a> 2. 중간 계층 응용 프로그램을 통해 데이터베이스에 연결하는 사용자에 대한 시나리오  
 이 예는 중간 계층 응용 프로그램이 응용 프로그램 사용자(또는 테넌트)가 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자(응용 프로그램)을 공유하는 연결 필터링을 구현하는 방법을 보여줍니다. 데이터베이스에 연결한 후 응용 프로그램이 [SESSION_CONTEXT&#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)에서 현재 응용 프로그램 사용자 ID를 설정하면 보안 정책이 이 ID에 표시되지 않아야 하는 행을 투명하게 필터링하고 사용자가 잘못된 사용자 ID에 대한 행을 삽입하지 못하도록 차단합니다. 다른 응용 프로그램은 변경하지 않아도 됩니다.  
  
 데이터를 보유하는 간단한 테이블을 만듭니다.  
  
```  
CREATE TABLE Sales (  
    OrderId int,  
    AppUserId int,  
    Product varchar(10),  
    Qty int  
);  
```  
  
 각 응용 프로그램 사용자별로 3개의 주문을 보여주는 6행의 데이터로 테이블을 채웁니다.  
  
```  
INSERT Sales VALUES   
    (1, 1, 'Valve', 5),   
    (2, 1, 'Wheel', 2),   
    (3, 1, 'Valve', 4),  
    (4, 2, 'Bracket', 2),   
    (5, 2, 'Wheel', 5),   
    (6, 2, 'Seat', 5);  
```  
  
 응용 프로그램에서 연결하는 데 사용할 낮은 권한의 사용자를 만듭니다.  
  
```  
-- Without login only for demo  
CREATE USER AppUser WITHOUT LOGIN;   
GRANT SELECT, INSERT, UPDATE, DELETE ON Sales TO AppUser;  
  
-- Never allow updates on this column  
DENY UPDATE ON Sales(AppUserId) TO AppUser;  
```  
  
 행을 필터링하는 **SESSION_CONTEXT**에 저장된 응용 프로그램 사용자 ID를 사용할 새로운 스키마 및 조건자 함수를 만듭니다.  
  
```  
CREATE SCHEMA Security;  
GO  
  
CREATE FUNCTION Security.fn_securitypredicate(@AppUserId int)  
    RETURNS TABLE  
    WITH SCHEMABINDING  
AS  
    RETURN SELECT 1 AS fn_securitypredicate_result  
    WHERE  
        DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('AppUser')    
        AND CAST(SESSION_CONTEXT(N'UserId') AS int) = @AppUserId;   
GO  
```  
  
 `Sales`에 대한 필터 조건자 및 차단 조건자로서 이 함수를 추가하는 보안 정책을 만듭니다. 차단 조건자에는 **AFTER INSERT**만 필요합니다. **BEFORE UPDATE** 및 **BEFORE DELETE**는 이미 필터링되었고 **AFTER UPDATE**는 이전에 설정된 열 권한으로 인해 `AppUserId` 열을 다른 값으로 업데이트할 수 없어 필요 없기 때문입니다.  
  
```  
CREATE SECURITY POLICY Security.SalesFilter  
    ADD FILTER PREDICATE Security.fn_securitypredicate(AppUserId)   
        ON dbo.Sales,  
    ADD BLOCK PREDICATE Security.fn_securitypredicate(AppUserId)   
        ON dbo.Sales AFTER INSERT   
    WITH (STATE = ON);  
```  
  
 이제 **SESSION_CONTEXT**에서 다른 응용 프로그램 사용자 ID를 설정한 후 `Sales` 테이블에서 선택하여 연결 필터링을 시뮬레이트할 수 있습니다. 실제로 응용 프로그램은 연결을 연 후 **SESSION_CONTEXT**에서 현재 사용자 ID를 설정합니다.  
  
```  
EXECUTE AS USER = 'AppUser';  
EXEC sp_set_session_context @key=N'UserId', @value=1;  
SELECT * FROM Sales;  
GO  
  
--  Note: @read_only prevents the value from changing again   
--  until the connection is closed (returned to the connection pool)  
EXEC sp_set_session_context @key=N'UserId', @value=2, @read_only=1;   
  
SELECT * FROM Sales;  
GO  
  
INSERT INTO Sales VALUES (7, 1, 'Seat', 12); -- error: blocked from inserting row for the wrong user ID  
GO  
  
REVERT;  
GO  
```  
  
## 참고 항목  
 [CREATE SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [ALTER SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [SESSION_CONTEXT&#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)   
 [sp_set_session_context&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [sys.security_policies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [사용자 정의 함수 만들기&#40;데이터베이스 엔진&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)  
  
  