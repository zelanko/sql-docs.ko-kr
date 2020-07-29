---
title: ALTER SECURITY POLICY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_SECURITY_POLICY_TSQL
- ALTER SECURITY POLICY
- ALTER_SECURITY_TSQL
- ALTER SECURITY
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER SECURITY POLICY statement
ms.assetid: a8efc37e-113d-489c-babc-b914fea2c316
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0696b96e83aac5ca66b43d38c11adceab702c10f
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87112562"
---
# <a name="alter-security-policy-transact-sql"></a>ALTER SECURITY POLICY(Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

보안 정책을 변경합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
ALTER SECURITY POLICY schema_name.security_policy_name   
    (  
        { ADD { FILTER | BLOCK } PREDICATE tvf_schema_name.security_predicate_function_name   
           ( { column_name | arguments } [ , ...n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ]  }   
        | { ALTER { FILTER | BLOCK } PREDICATE tvf_schema_name.new_security_predicate_function_name   
             ( { column_name | arguments } [ , ...n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ] }  
        | { DROP { FILTER | BLOCK } PREDICATE ON table_schema_name.table_name }   
        | [ <additional_add_alter_drop_predicate_statements> [ , ...n ] ]  
    )    [ WITH ( STATE = { ON | OFF } ) ]  
    [ NOT FOR REPLICATION ]  
[;]  
  
<block_dml_operation>  
    [ { AFTER { INSERT | UPDATE } }   
    | { BEFORE { UPDATE | DELETE } } ]  
```  

## <a name="arguments"></a>인수
security_policy_name  
보안 정책의 이름입니다. 보안 정책 이름은 식별자에 대한 규칙을 따라야 하며 데이터베이스에서 각 스키마별로 고유해야 합니다.  
  
schema_name  
보안 정책이 속한 스키마의 이름입니다. 스키마 바인딩 때문에 *schema_name*이 필요합니다.  
  
[ FILTER | BLOCK ]  
대상 테이블에 바인딩된 함수에 대한 보안 조건자의 형식입니다. FILTER 조건자는 읽기 작업에 사용 가능한 행을 자동으로 필터링합니다. BLOCK 조건자는 조건자 함수를 위반하는 쓰기 작업을 명시적으로 차단합니다.  
  
tvf_schema_name.security_predicate_function_name  
조건자로 사용하고 대상 테이블에 대해 쿼리를 적용하는 인라인 테이블 값 함수입니다. 특정 테이블에 대한 특정 DML 작업을 위해 최대 하나의 보안 조건자를 정의할 수 있습니다. SCHEMABINDING 옵션을 사용하여 인라인 테이블 값 함수를 만듭니다.  
  
{ column_name | arguments }  
보안 조건자 함수를 위한 매개 변수로 사용되는 열 이름 또는 식입니다. 대상 테이블에 있는 모든 열은 조건자 함수를 위한 인수로 사용할 수 있습니다. 리터럴과 기본 제공 항목, 산술 연산자를 사용하는 식을 포함하는 식을 사용할 수 있습니다.  
  
*table_schema_name.table_name*  
보안 조건자의 대상 테이블입니다. 사용되지 않도록 설정된 여러 보안 정책이 특정 DML 작업용 단일 테이블을 대상으로 할 수 있지만 지정된 시간에 하나만 사용할 수 있습니다.  
  
*\<block_dml_operation>*  
적용된 차단 조건자에 대한 특정 DML 작업입니다. AFTER는 DML 작업 수행(INSERT 또는 UPDATE) 후에 조건자가 행 값에 따라 평가되도록 지정합니다. BEFORE는 DML 작업 수행(UPDATE 또는 DELETE) 전에 조건자가 행 값에 따라 평가되도록 지정합니다. 작업이 지정되지 않은 경우 조건자는 모든 작업에 적용됩니다.  
  
작업은 조건자를 고유하게 식별하는 데 사용되기 때문에 적용된 차단 조건자에 대해 작업을 변경(ALTER)할 수 없습니다. 대신 조건자를 삭제하고 새 작업에 새 조건자를 추가해야 합니다.  
  
WITH ( STATE = { ON | OFF } )  
대상 테이블에 대해 해당 보안 조건자를 강제 적용하여 보안 정책을 사용하거나 사용하지 않도록 설정합니다. 지정되지 않으면 생성되는 보안 정책이 사용되도록 설정됩니다.  
  
NOT FOR REPLICATION  
복제 에이전트가 대상 개체를 수정할 때 보안 정책을 실행하면 안 됨을 나타냅니다. 자세한 내용은 [동기화하는 동안 트리거 및 제약 조건 동작 제어&#40;복제 Transact-SQL 프로그래밍&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)를 참조하세요.  
  
table_schema_name.table_name  
적용된 보안 조건자의 대상 테이블입니다. 사용되지 않도록 설정된 보안 정책은 여러 개가 단일 테이블을 대상으로 할 수 있지만 지정된 시간에 하나만 사용하도록 설정할 수 있습니다.  
  
## <a name="remarks"></a>설명  
ALTER SECURITY POLICY 문은 트랜잭션 범위 내에 있습니다. 트랜잭션이 롤백되면 이 문도 롤백됩니다.  
  
메모리 최적화 테이블에서 조건자 함수를 사용하는 경우, 보안 정책에 **SCHEMABINDING**를 포함하고 **WITH NATIVE_COMPILATION** 컴파일 힌트를 사용해야 합니다. SCHEMABINDING 인수는 모든 조건자에 적용되므로 ALTER 문으로 변경할 수 없습니다. 스키마 바인딩을 변경하려면 보안 정책을 삭제하고 다시 만들어야 합니다.  
  
차단 조건자는 해당 DML 작업이 실행된 후 평가됩니다. 따라서 READ UNCOMMITTED 쿼리는 롤백될 임시 값을 볼 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
ALTER ANY SECURITY POLICY 권한이 필요합니다.  
  
또한 추가된 각 조건자에는 다음 권한이 필요합니다.  
  
-   조건자로 사용 되는 함수에 대한 SELECT 및 REFERENCES 권한.  
-   정책에 바인딩되는 대상 테이블에 대한 REFERENCES 권한.  
-   인수로 사용하는 대상 테이블의 모든 열에 대한 REFERENCES 권한.  
  
## <a name="examples"></a>예제  
다음 예는 **ALTER SECURITY POLICY** 구문의 사용을 보여줍니다. 완벽한 보안 정책 시나리오의 예를 보려면 [행 수준 보안](../../relational-databases/security/row-level-security.md)을 참조하세요.  
  
### <a name="a-adding-an-additional-predicate-to-a-policy"></a>A. 정책에 추가적인 조건자 추가  
다음 구문은 `mytable` 테이블에서 필터 조건자를 추가하여 보안 정책을 변경합니다.  
  
```  
ALTER SECURITY POLICY pol1   
    ADD FILTER PREDICATE schema_preds.SecPredicate(column1)   
    ON myschema.mytable;  
```  
  
### <a name="b-enabling-an-existing-policy"></a>B. 기존 정책을 사용하도록 설정  
다음 예에서는 ALTER 구문을 사용하여 보안 정책을 사용하도록 설정합니다.  
  
```  
ALTER SECURITY POLICY pol1 WITH ( STATE = ON );  
```  
  
### <a name="c-adding-and-dropping-multiple-predicates"></a>C. 여러 조건자 추가 및 삭제  
다음 구문은 `mytable1` 및 `mytable3` 테이블에서 필터 조건자를 추가하고 `mytable2` 테이블에서 필터 조건자를 제거하여 보안 정책을 변경합니다.  
  
```  
ALTER SECURITY POLICY pol1  
ADD FILTER PREDICATE schema_preds.SecPredicate1(column1)   
    ON myschema.mytable1,  
DROP FILTER PREDICATE   
    ON myschema.mytable2,  
ADD FILTER PREDICATE schema_preds.SecPredicate2(column2, 1)   
    ON myschema.mytable3;  
```  
  
### <a name="d-changing-the-predicate-on-a-table"></a>D. 테이블의 조건자 변경  
다음 구문에서는 mytable 테이블의 기존 필터 조건자를 변경하여 SecPredicate2 함수가 되게 합니다.  
  
```  
ALTER SECURITY POLICY pol1  
    ALTER FILTER PREDICATE schema_preds.SecPredicate2(column1)  
        ON myschema.mytable;  
```  
  
### <a name="e-changing-a-block-predicate"></a>E. 차단 조건자 변경  
테이블 작업에 대한 차단 조건자 함수를 변경합니다.  
  
```  
ALTER SECURITY POLICY rls.SecPol  
    ALTER BLOCK PREDICATE rls.tenantAccessPredicate_v2(TenantId) 
    ON dbo.Sales AFTER INSERT;  
```  
  
## <a name="see-also"></a>참고 항목  
[행 수준 보안](../../relational-databases/security/row-level-security.md)   
[CREATE SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
[DROP SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
[sys.security_policies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
[sys.security_predicates&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  
