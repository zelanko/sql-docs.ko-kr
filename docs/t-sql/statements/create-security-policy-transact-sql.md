---
title: CREATE SECURITY POLICY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SECURITY_POLICY_TSQL
- CREATE SECURITY
- SECURITY
- CREATE_SECURITY_POLICY_TSQL
- CREATE_SECURITY_TSQL
- SECURITY POLICY
- SECURITY_TSQL
- CREATE SECURITY POLICY
dev_langs:
- TSQL
helpviewer_keywords:
- RLS
- CREATE SECURITY POLICY statement
- Row-Level Security
ms.assetid: d6ab70ee-0fa2-469c-96f6-a3c16d673bc8
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 53292dc3f9f5cbd36913276496084d4648f13520
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-security-policy-transact-sql"></a>CREATE SECURITY POLICY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  행 수준 보안에 대 한 보안 정책을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```     
CREATE SECURITY POLICY [schema_name. ] security_policy_name    
    { ADD [ FILTER | BLOCK ] } PREDICATE tvf_schema_name.security_predicate_function_name   
      ( { column_name | arguments } [ , …n] ) ON table_schema_name. table_name    
      [ <block_dml_operation> ] , [ , …n] 
    [ WITH ( STATE = { ON | OFF }  [,] [ SCHEMABINDING = { ON | OFF } ] ) ]  
    [ NOT FOR REPLICATION ] 
[;]  
  
<block_dml_operation>  
    [ { AFTER { INSERT | UPDATE } }   
    | { BEFORE { UPDATE | DELETE } } ]  
```  
  
## <a name="arguments"></a>인수  
 *security_policy_name*  
 보안 정책의 이름입니다. 보안 정책 이름은 식별자에 대한 규칙을 따라야 하며 데이터베이스에서 각 스키마별로 고유해야 합니다.  
  
 *schema_name*  
 보안 정책이 속한 스키마의 이름입니다. *schema_name* 가 스키마 바인딩 때문에 필요 합니다.  
  
 [필터 | 블록]  
 대상 테이블에 바인딩되어 함수에 대 한 보안 조건자의 형식입니다. 필터 조건자는 자동으로 읽기 작업에 사용할 수 있는 행을 필터링 합니다. 블록 조건자 명시적으로 조건자 함수를 위반 하는 블록 쓰기 작업입니다.  
  
 *tvf_schema_name.security_predicate_function_name*  
 조건자로 사용되고 대상 테이블에 대한 쿼리 시 적용될 인라인 테이블 값 함수입니다. 특정 테이블에 대한 특정 DML 작업을 위해 최대 하나의 보안 조건자를 정의할 수 있습니다. 인라인 테이블 값 함수는 SCHEMABINDING 옵션을 사용하여 생성했어야 합니다.  
  
 { *column_name* | *인수* }  
 보안 조건자 함수를 위한 매개 변수로 사용되는 열 이름 또는 식입니다. 대상 테이블에 있는 모든 열은 조건자 함수를 위한 인수로 사용할 수 있습니다. 리터럴과 builtin, 산술 연산자를 사용하는 식을 포함하는 식을 사용할 수 있습니다.  
  
 *table_schema_name.table_name*  
 보안 조건자를 적용할 대상 테이블입니다. 사용할 수 없는 보안 정책은 여러 개가 단일 테이블에 대 한 특정 DML 작업을 대상으로 지정할 수 있지만 하나만 지정된 된 시간에 사용 하도록 설정할 수 있습니다.  
  
 *\<block_dml_operation >* 블록 조건자를 적용할 특정 DML 작업입니다. DML 작업 수행 (삽입 또는 업데이트) 한 후 조건자 행의 값에 평가 될 지정 후 합니다. 이전 조건자 DML 작업이 수행 된 (업데이트 또는 삭제) 되기 전에 행의 값에 대해 평가 됩니다 지정 합니다. 작업이 지정 된 경우 조건자는 모든 작업에 적용 됩니다.  
  
 [상태 = {ON | **OFF** }]  
 대상 테이블에 대해 해당 보안 조건자를 강제 적용하여 보안 정책을 사용하거나 사용하지 않도록 설정합니다. 지정되지 않으면 생성되는 보안 정책이 사용되도록 설정됩니다.  
  
 [SCHEMABINDING = {ON | OFF}]  
 SCHEMABINDING 옵션으로 정책에서 모든 조건자 함수를 생성 해야 하는지 여부를 나타냅니다. 기본적으로 모든 함수가 SCHEMABINDING으로 만들어야 합니다.  
  
 NOT FOR REPLICATION  
 복제 에이전트가 대상 개체를 수정할 때 보안 정책을 실행하면 안 됨을 나타냅니다. 자세한 내용은 [동기화하는 동안 트리거 및 제약 조건 동작 제어&#40;복제 Transact-SQL 프로그래밍&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)를 참조하세요.  
  
 [*table_schema_name*.] *table_name*  
 보안 조건자를 적용할 대상 테이블입니다. 사용되지 않도록 설정된 보안 정책은 여러 개가 단일 테이블을 대상으로 할 수 있지만 지정된 시간에 하나만 사용하도록 설정할 수 있습니다.  
  
## <a name="remarks"></a>주의  
 조건자 함수를 사용 하 여 메모리 액세스에 최적화 된 테이블을 포함 해야 **SCHEMABINDING** 사용 하는 **WITH NATIVE_COMPILATION** 컴파일 힌트입니다.  
  
 차단 조건자는 해당 DML 작업이 실행 된 후 평가 됩니다. 따라서 READ UNCOMMITTED 쿼리 롤백할 수는 임시 값을 볼 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 스키마에 대한 ALTER ANY SECURITY POLICY 권한 및 ALTER 권한이 필요합니다.  
  
 또한 추가된 각 조건자에는 다음 권한이 필요합니다.  
  
-   조건자로 사용 되는 함수에 대한 SELECT 및 REFERENCES 권한.  
  
-   정책에 바인딩되는 대상 테이블에 대한 REFERENCES 권한.  
  
-   인수로 사용하는 대상 테이블의 모든 열에 대한 REFERENCES 권한.  
  
## <a name="examples"></a>예  
 다음 예는 **CREATE SECURITY POLICY** 구문의 사용을 보여 줍니다. 완벽 한 보안 정책 시나리오의 예제를 보려면 [행 수준 보안](../../relational-databases/security/row-level-security.md)합니다.  
  
### <a name="a-creating-a-security-policy"></a>1. 보안 정책 만들기  
 다음 구문은 Customer 테이블에 대한 필터 조건자가 있는 보안 정책을 만들고 보안 정책을 사용하지 않도록 설정해 둡니다.  
  
```  
CREATE SECURITY POLICY [FederatedSecurityPolicy]   
ADD FILTER PREDICATE [rls].[fn_securitypredicate]([CustomerId])   
ON [dbo].[Customer];  
```  
  
### <a name="b-creating-a-policy-that-affects-multiple-tables"></a>2. 여러 테이블에 영향을 주는 정책 만들기  
 다음 구문은 서로 다른 세 테이블에서 3개의 필터 조건자를 사용하여 보안 정책을 만들고 보안 정책을 사용하도록 설정합니다.  
  
```  
CREATE SECURITY POLICY [FederatedSecurityPolicy]   
ADD FILTER PREDICATE [rls].[fn_securitypredicate1]([CustomerId])   
    ON [dbo].[Customer],  
ADD FILTER PREDICATE [rls].[fn_securitypredicate1]([VendorId])   
    ON [dbo].[ Vendor],  
ADD FILTER PREDICATE [rls].[fn_securitypredicate2]([WingId])   
    ON [dbo].[Patient]  
WITH (STATE = ON);  
```  
  
### <a name="c-creating-a-policy-with-multiple-types-of-security-predicates"></a>3. 여러 종류의 보안 조건자 정책 만들기  
 Sales 테이블에 필터 조건자와 차단 조건자를 추가 합니다.  
  
```  
CREATE SECURITY POLICY rls.SecPol  
    ADD FILTER PREDICATE rls.tenantAccessPredicate(TenantId) ON dbo.Sales,  
    ADD BLOCK PREDICATE rls.tenantAccessPredicate(TenantId) ON dbo.Sales AFTER INSERT;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [행 수준 보안](../../relational-databases/security/row-level-security.md)   
 [ALTER SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [sys.security_policies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  


