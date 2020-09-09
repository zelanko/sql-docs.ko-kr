---
description: sp_bindrule(Transact-SQL)
title: sp_bindrule (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_bindrule_TSQL
- sp_bindrule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindrule
ms.assetid: 2606073e-c52f-498d-a923-5026b9d97e67
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c7355f421701c5eb24da58dec5037b5fb1b8317c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548326"
---
# <a name="sp_bindrule-transact-sql"></a>sp_bindrule(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  열 또는 별칭 데이터 형식에 규칙을 바인딩합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신[Unique 제약 조건 및 Check 제약 조건을](../../relational-databases/tables/unique-constraints-and-check-constraints.md) 사용 해야 합니다. CHECK 제약 조건은 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 또는 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 문의 check 키워드를 사용 하 여 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_bindrule [ @rulename = ] 'rule' ,   
     [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @rulename = ] 'rule'` CREATE RULE 문에 의해 생성 된 규칙의 이름입니다. *rule* 은 **nvarchar (776)** 이며 기본값은 없습니다.  
  
`[ @objname = ] 'object_name'` 규칙을 바인딩할 테이블 및 열 또는 별칭 데이터 형식입니다. 규칙은 **text**, **ntext**, **image**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **xml**, CLR 사용자 정의 형식 또는 **timestamp** 열에 바인딩할 수 없습니다. 계산 열에 규칙을 바인딩할 수 없습니다.  
  
 *object_name* 은 **nvarchar (776)** 이며 기본값은 없습니다. *Object_name* 한 부분으로 구성 된 이름인 경우 별칭 데이터 형식으로 확인 됩니다. 두 부분이나 세 부분으로 된 이름이면 먼저 테이블 및 열로 확인된 다음 확인이 실패하면 별칭 데이터 형식으로 확인됩니다. 기본적으로 별칭 데이터 형식의 기존 열은 규칙이 열에 직접 바인딩된 경우를 제외 하 고 *규칙* 을 상속 합니다.  
  
> [!NOTE]  
>  *object_name* 은 대괄호 **[** 및 **]** 문자를 구분 식별자 문자로 포함할 수 있습니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
> [!NOTE]  
>  별칭 데이터 형식을 사용하는 식에 대해 만든 규칙을 열이나 별칭 데이터 형식에 바인딩할 수 있지만 이들 규칙을 참조할 때 컴파일할 수 없습니다. 별칭 데이터 형식에 대해 만든 규칙을 사용하지 마십시오.  
  
`[ @futureonly = ] 'futureonly_flag'` 는 규칙을 별칭 데이터 형식에 바인딩하는 경우에만 사용 됩니다. *future_only_flag* 는 **varchar (15)** 이며 기본값은 NULL입니다. 이 매개 변수를 **futureonly** 로 설정 하면 별칭 데이터 형식의 기존 열이 새 규칙을 상속 하지 않습니다. *FUTUREONLY_FLAG* NULL 인 경우에는 현재 규칙이 없거나 별칭 데이터 형식의 기존 규칙을 사용 하는 별칭 데이터 형식의 열에 새 규칙이 바인딩됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 CHECK 제약 조건을 사용 하는 경우에도 열에 새 규칙을 바인딩하거나 기존 규칙의 바인딩을 해제 하지 않고 **sp_bindrule** 를 사용 하 여 별칭 데이터 형식에 바인딩할 수 있습니다. 이 경우 이전 규칙은 무시됩니다. 기존의 CHECK 제약 조건으로 규칙이 열에 바인딩된 경우에는 모든 제한이 평가됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 규칙을 바인딩할 수 없습니다.  
  
 규칙은 바인딩 시점이 아니라 INSERT 문을 시도할 때 적용되며 **숫자** 데이터 형식의 열에 문자 규칙을 바인딩할 수 있지만 이러한 삽입 작업은 유효 하지 않습니다.  
  
 별칭 데이터 형식의 기존 열 *futureonly_flag* 이 **futureonly**로 지정 되지 않은 경우 새 규칙을 상속 합니다. 별칭 데이터 형식으로 정의된 새 열은 항상 규칙을 상속합니다. 그러나 ALTER TABLE 문의 ALTER COLUMN 절이 열의 데이터 형식을 규칙에 바인딩된 별칭 데이터 형식으로 변경하는 경우에는 데이터 형식에 바인딩된 규칙이 열에 상속되지 않습니다. 규칙은 특히 **sp_bindrule**를 사용 하 여 열에 바인딩되어야 합니다.  
  
 열에 규칙을 바인딩하면 관련 정보가 **sys. columns** 테이블에 추가 됩니다. 별칭 데이터 형식에 규칙을 바인딩하면 관련 정보가 **sys. types** 테이블에 추가 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 테이블 열에 규칙을 바인딩하려면 해당 테이블에 대한 ALTER 권한이 필요합니다. 별칭 데이터 형식에 규칙을 바인딩하려면 별칭 데이터 형식에 대한 CONTROL 권한 또는 그 형식이 속한 스키마에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-binding-a-rule-to-a-column"></a>A. 열에 규칙 바인딩  
 CREATE RULE 문을 사용하여 현재 데이터베이스에 `today`라는 규칙을 만들었다고 가정할 때 다음 예에서는 `HireDate` 테이블의 `Employee` 열에 이 규칙을 바인딩하는 방법을 보여 줍니다. 이제 `Employee`에 행을 추가하면 `HireDate` 열의 데이터가 `today` 규칙에 부합하는지 확인합니다.  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-rule-to-an-alias-data-type"></a>B. 별칭 데이터 형식에 규칙 바인딩  
 `rule_ssn`이라는 규칙과 `ssn`이라는 별칭 데이터 형식이 있다고 가정할 때 다음 예에서는 `rule_ssn`에 `ssn`을 바인딩하는 방법을 보여 줍니다. CREATE TABLE 문에서 `ssn` 형식의 열은 `rule_ssn` 규칙을 상속합니다. `ssn` `rule_ssn` *Futureonly_flag*에 대해 **futureonly** 를 지정 하지 않거나 `ssn` 해당 규칙에 직접 바인딩된 규칙을 포함 하는 경우에도 형식의 기존 열은 규칙을 상속 합니다. 데이터 형식에 바인딩한 규칙보다 열에 바인딩한 규칙이 항상 우선합니다.  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'rule_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonly_flag"></a>C. futureonly_flag 사용  
 다음 예에서는 `rule_ssn` 별칭 데이터 형식에 `ssn` 규칙을 바인딩하는 방법을 보여 줍니다. `futureonly`를 지정하였으므로 기존 `ssn` 형식의 열은 전혀 영향을 받지 않습니다.  
  
```  
USE master;  
GO  
EXEC sp_bindrule rule_ssn, 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 구분 식별자 사용  
 다음 예에서는 *object_name* 매개 변수에서 구분 식별자를 사용 하는 방법을 보여 줍니다.  
  
```  
USE master;  
GO  
CREATE TABLE [t.2] (c1 int) ;  
-- Notice the period as part of the table name.  
EXEC sp_bindrule rule1, '[t.2].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE&#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
