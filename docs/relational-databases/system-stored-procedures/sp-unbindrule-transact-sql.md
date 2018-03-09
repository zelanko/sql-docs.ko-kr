---
title: sp_unbindrule (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_unbindrule_TSQL
- sp_unbindrule
dev_langs: TSQL
helpviewer_keywords: sp_unbindrule
ms.assetid: f54ee155-c3c9-4f1a-952e-632a8339f0cc
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 587578e7b9133b5323557b6cd1b5246a148bcb6e
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="spunbindrule-transact-sql"></a>sp_unbindrule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 열에서 또는 별칭 데이터 형식에서 규칙을 바인딩 해제합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]DEFAULT 키워드를 사용 하 여 기본 정의 만드는 것이 좋습니다는 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 또는 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 문 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_unbindrule [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@objname=** ] **'***object_name***'**  
 바인딩이 해제된 규칙이 있는 테이블 및 열의 이름 또는 별칭 데이터 형식입니다. *object_name* 은 **nvarchar(776)**, 기본값은 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 열 이름과 별칭 데이터 형식 순으로 두 부분의 식별자를 확인합니다. 별칭 데이터 형식에서 규칙을 바인딩 해제하는 경우 같은 규칙을 가진 데이터 형식의 열 또한 바인딩 해제됩니다. 규칙이 직접 바인딩된 이 데이터 형식의 열은 영향을 받지 않습니다.  
  
> [!NOTE]  
>  *object_name* 괄호를 사용할 수 있습니다 **[]** 구분 식별자 문자로 합니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
 [  **@futureonly=** ] **'***futureonly_flag***'**  
 별칭 데이터 형식에서 규칙의 바인딩을 해제하는 경우에만 사용됩니다. *futureonly_flag* 은 **varchar(15)**, 기본값은 NULL입니다. 때 *futureonly_flag* 은 **futureonly**, 해당 데이터 형식의 기존 열에 지정된 된 규칙 손실 되지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 실행 규칙의 텍스트를 표시 하려면 **sp_helptext** 규칙 이름을 매개 변수로 사용 합니다.  
  
 규칙 바인딩 해제 하는 바인딩에 대 한 정보에서 제거 됩니다는 **sys.columns** 규칙이 바인딩된 열을 들어오고 경우 테이블은 **sys.types** 규칙이 별칭 데이터 형식에 바인딩된 경우 테이블입니다.  
  
 규칙이 별칭 데이터 형식에서 바인딩 해제되면 해당 규칙은 이 별칭 데이터 형식을 가진 열에서도 바인딩 해제됩니다. 데이터 형식이 ALTER TABLE 문의 ALTER COLUMN 절에 의해 나중에 변경 된 열에 규칙을 바인딩할 수 여전히, 사용 하 여 해당이 열에서 규칙을 언바인딩 특히 해야 **sp_unbindrule** 지정 하는 열 이름입니다.  
  
## <a name="permissions"></a>Permissions  
 테이블 열에서 규칙을 바인딩 해제하려면 테이블에 대한 ALTER 권한이 필요합니다. 별칭 데이터 형식에서 규칙을 바인딩 해제하려면 형식에 대한 CONTROL 권한 또는 형식이 속한 스키마에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-unbinding-a-rule-from-a-column"></a>1. 열에서 규칙 바인딩 해제  
 다음 예에서는 `startdate` 테이블의 `employees` 열에서 규칙을 바인딩 해제합니다.  
  
```  
EXEC sp_unbindrule 'employees.startdate';  
```  
  
### <a name="b-unbinding-a-rule-from-an-alias-data-type"></a>2. 별칭 데이터 형식에서 규칙 바인딩 해제  
 다음 예에서는 `ssn` 별칭 데이터 형식에서 규칙을 바인딩 해제합니다. 해당 형식의 기존 열 및 향후 열에서 규칙을 바인딩 해제합니다.  
  
```  
EXEC sp_unbindrule ssn;  
```  
  
### <a name="c-using-futureonlyflag"></a>3. futureonly_flag 사용  
 다음 예에서는 기존 `ssn` 열에 영향을 주지 않고 `ssn` 별칭 데이터 형식에서 규칙을 바인딩 해제합니다.  
  
```  
EXEC sp_unbindrule 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>4. 구분 식별자 사용  
 다음 예제에서 구분된 식별자를 사용 하는 *object_name* 매개 변수입니다.  
  
```  
CREATE TABLE [t.4] (c1 int); -- Notice the period as part of the table   
-- name.  
GO  
CREATE RULE rule2 AS @value > 100;  
GO  
EXEC sp_bindrule rule2, '[t.4].c1' -- The object contains two   
-- periods; the first is part of the table name and the second   
-- distinguishes the table name from the column name.  
GO  
EXEC sp_unbindrule '[t.4].c1';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터베이스 엔진 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE&#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP 규칙 &#40; Transact SQL &#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_bindrule &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_helptext&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
