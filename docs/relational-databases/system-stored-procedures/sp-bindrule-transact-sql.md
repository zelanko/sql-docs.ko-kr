---
title: sp_bindrule (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/25/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_bindrule_TSQL
- sp_bindrule
dev_langs: TSQL
helpviewer_keywords: sp_bindrule
ms.assetid: 2606073e-c52f-498d-a923-5026b9d97e67
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dbc90db869ea98ebfdf99bf9cbdf56d9019b28a8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spbindrule-transact-sql"></a>sp_bindrule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  열 또는 별칭 데이터 형식에 규칙을 바인딩합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]사용 하 여[Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md) 대신 합니다. CHECK 제약 조건을의 CHECK 키워드를 사용 하 여 생성 되는 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 또는 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 문.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_bindrule [ @rulename = ] 'rule' ,   
     [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>인수  
 [  **@rulename=**] **'***규칙***'**  
 CREATE RULE 문으로 작성된 규칙의 이름입니다. *규칙* 은 **nvarchar(776)**, 기본값은 없습니다.  
  
 [  **@objname=**] **'***object_name***'**  
 규칙을 바인딩할 테이블 및 열 또는 별칭 데이터 형식입니다. 규칙에 바인딩할 수 없습니다는 **텍스트**, **ntext**, **이미지**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, CLR 사용자 정의 형식 또는 **타임 스탬프**열입니다. 계산 열에 규칙을 바인딩할 수 없습니다.  
  
 *object_name* 은 **nvarchar(776)** 이며 기본값은 없습니다. 경우 *object_name* 은 한 부분, 별칭 데이터 형식으로 확인 됩니다. 두 부분이나 세 부분으로 된 이름이면 먼저 테이블 및 열로 확인된 다음 확인이 실패하면 별칭 데이터 형식으로 확인됩니다. 기본적으로 별칭 데이터 형식의 기존 열을 상속 *규칙* 열에 직접 규칙에 바인딩된 경우를 제외 합니다.  
  
> [!NOTE]  
>  *object_name* 대괄호 포함 될 수 있습니다 **[** 및 **]** 구분된 식별자 문자로 문자입니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
> [!NOTE]  
>  별칭 데이터 형식을 사용하는 식에 대해 만든 규칙을 열이나 별칭 데이터 형식에 바인딩할 수 있지만 이들 규칙을 참조할 때 컴파일할 수 없습니다. 별칭 데이터 형식에 대해 만든 규칙을 사용하지 마십시오.  
  
 [  **@futureonly=** ] **'***futureonly_flag***'**  
 규칙을 별칭 데이터 형식에 바인딩하는 경우에만 사용합니다. *future_only_flag* 은 **varchar(15)** 기본값은 NULL입니다. 로 설정 된 경우이 매개 변수 **futureonly** 새 규칙을 상속 별칭 데이터 형식의 기존 열을 방지 합니다. 경우 *futureonly_flag* 가 null 인 경우 새 규칙이 있는 현재 규칙이 없거나 별칭 데이터 형식의 기존 규칙을 사용 하는 별칭 데이터 형식의 열에 바인딩됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 (CHECK 제약 조건을 사용 하는 것이 좋습니다) 하지만 열에 새 규칙을 바인딩할 수 또는 별칭 데이터 형식으로 **sp_bindrule** 없이 기존 규칙을 바인딩 해제 합니다. 이 경우 이전 규칙은 무시됩니다. 기존의 CHECK 제약 조건으로 규칙이 열에 바인딩된 경우에는 모든 제한이 평가됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 규칙을 바인딩할 수 없습니다.  
  
 규칙은 바인딩 시점이 아니라 INSERT 문을 시도할 때 적용되며 열에 문자 규칙을 바인딩할 수 **숫자** 이 INSERT 작업이 유효 하지 않지만 데이터 형식입니다.  
  
 별칭 데이터 형식의 기존 열 하지 않는 한 새 규칙을 상속 *futureonly_flag* 로 지정 된 **futureonly**합니다. 별칭 데이터 형식으로 정의된 새 열은 항상 규칙을 상속합니다. 그러나 ALTER TABLE 문의 ALTER COLUMN 절이 열의 데이터 형식을 규칙에 바인딩된 별칭 데이터 형식으로 변경하는 경우에는 데이터 형식에 바인딩된 규칙이 열에 상속되지 않습니다. 규칙 특히 바인딩되어야 열에 사용 하 여 **sp_bindrule**합니다.  
  
 열에 규칙을 바인딩 관련된 정보에 추가 됩니다는 **sys.columns** 테이블입니다. 별칭 데이터 형식에 규칙을 바인딩 관련된 정보에 추가 됩니다는 **sys.types** 테이블입니다.  
  
## <a name="permissions"></a>Permissions  
 테이블 열에 규칙을 바인딩하려면 해당 테이블에 대한 ALTER 권한이 필요합니다. 별칭 데이터 형식에 규칙을 바인딩하려면 별칭 데이터 형식에 대한 CONTROL 권한 또는 그 형식이 속한 스키마에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-binding-a-rule-to-a-column"></a>1. 열에 규칙 바인딩  
 CREATE RULE 문을 사용하여 현재 데이터베이스에 `today`라는 규칙을 만들었다고 가정할 때 다음 예에서는 `HireDate` 테이블의 `Employee` 열에 이 규칙을 바인딩하는 방법을 보여 줍니다. 이제 `Employee`에 행을 추가하면 `HireDate` 열의 데이터가 `today` 규칙에 부합하는지 확인합니다.  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-rule-to-an-alias-data-type"></a>2. 별칭 데이터 형식에 규칙 바인딩  
 `rule_ssn`이라는 규칙과 `ssn`이라는 별칭 데이터 형식이 있다고 가정할 때 다음 예에서는 `rule_ssn`에 `ssn`을 바인딩하는 방법을 보여 줍니다. CREATE TABLE 문에서 `ssn` 형식의 열은 `rule_ssn` 규칙을 상속합니다. 형식의 기존 열 `ssn` 상속는 `rule_ssn` 규칙을 하지 않는 한 **futureonly** 에 대해 지정 된 *futureonly_flag*, 또는 `ssn` 에 직접 바인딩한 규칙이 있습니다. 데이터 형식에 바인딩한 규칙보다 열에 바인딩한 규칙이 항상 우선합니다.  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'rule_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>3. futureonly_flag 사용  
 다음 예에서는 `rule_ssn` 별칭 데이터 형식에 `ssn` 규칙을 바인딩하는 방법을 보여 줍니다. `futureonly`를 지정하였으므로 기존 `ssn` 형식의 열은 전혀 영향을 받지 않습니다.  
  
```  
USE master;  
GO  
EXEC sp_bindrule rule_ssn, 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>4. 구분 식별자 사용  
 다음 예제에서 구분된 식별자 사용을 보여 줍니다. *object_name* 매개 변수입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터베이스 엔진 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE&#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP 규칙 &#40; Transact SQL &#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_unbindrule &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
