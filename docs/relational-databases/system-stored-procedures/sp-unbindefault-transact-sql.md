---
title: sp_unbindefault (Transact SQL) | Microsoft Docs
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
- sp_unbindefault_TSQL
- sp_unbindefault
dev_langs: TSQL
helpviewer_keywords: sp_unbindefault
ms.assetid: c96a6c5e-f3ca-4c1e-b64b-0d8ef6986af8
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d9389128a5056cc6a0dae7f54b4aad56c4f9a9f7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spunbindefault-transact-sql"></a>sp_unbindefault(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 열에서 또는 별칭 데이터 형식에서 기본값의 바인딩을 해제(제거)합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]DEFAULT 키워드를 사용 하 여 기본 정의 만드는 것이 좋습니다는 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 또는 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 문 대신 합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_unbindefault [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@objname=** ] **'***object_name***'**  
 바인딩 해제될 기본값이 있는 테이블 및 열의 이름 또는 별칭 데이터 형식입니다. *object_name* 은 **nvarchar(776)**, 기본값은 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 열 이름과 별칭 데이터 형식 순으로 두 부분의 식별자를 확인합니다.  
  
 별칭 데이터 형식에서 기본값의 바인딩을 해제하는 경우 같은 기본값을 가진 이 데이터 형식의 열에 대한 바인딩도 해제됩니다. 기본값을 직접 바인딩한 이 데이터 형식의 열은 영향을 받지 않습니다.  
  
> [!NOTE]  
>  *object_name* 괄호를 사용할 수 있습니다 **** 구분 식별자 문자로 합니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
 [  **@futureonly=** ] **'***futureonly_flag***'**  
 별칭 데이터 형식에서 기본값의 바인딩을 해제하는 경우에만 사용됩니다. *futureonly_flag* 은 **varchar(15)**, 기본값은 NULL입니다. 때 *futureonly_flag* 은 **futureonly**, 데이터 형식의 기존 열에 지정된 된 기본 손실 되지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 기본값의 텍스트를 표시 하려면 실행 **sp_helptext** 매개 변수 기본값의 이름으로 합니다.  
  
## <a name="permissions"></a>Permissions  
 테이블 열에서 기본값의 바인딩을 해제하려면 테이블에 대한 ALTER 사용 권한이 필요합니다. 별칭 데이터 형식에서 기본값의 바인딩을 해제하려면 유형에 대한 CONTROL 사용 권한 또는 유형이 속한 스키마에 대한 ALTER 사용 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-unbinding-a-default-from-a-column"></a>1. 열에서 기본값 바인딩 해제  
 다음 예에서는 `hiredate` 테이블의 `employees` 열에서 기본값의 바인딩을 해제합니다.  
  
```  
EXEC sp_unbindefault 'employees.hiredate';  
```  
  
### <a name="b-unbinding-a-default-from-an-alias-data-type"></a>2. 별칭 데이터 형식에서 기본값 바인딩 해제  
 다음 예에서는 `ssn` 별칭 데이터 형식에서 기본값의 바인딩을 해제합니다. 해당 형식의 기존 및 앞으로의 열에 대한 바인딩을 해제합니다.  
  
```  
EXEC sp_unbindefault 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>3. futureonly_flag 사용  
 다음 예에서는 기존 `ssn` 열에 영향을 주지 않고 앞으로 사용하는 `ssn` 별칭 데이터 형식에 대한  바인딩을 해제합니다.  
  
```  
EXEC sp_unbindefault 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>4. 구분 식별자 사용  
 다음 예제에서 구분된 식별자를 사용 하 여 *object_name* 매개 변수입니다.  
  
```  
CREATE TABLE [t.3] (c1 int); -- Notice the period as part of the table   
-- name.  
CREATE DEFAULT default2 AS 0;  
GO  
EXEC sp_bindefault 'default2', '[t.3].c1' ;  
-- The object contains two periods;  
-- the first is part of the table name and the second   
-- distinguishes the table name from the column name.  
EXEC sp_unbindefault '[t.3].c1';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터베이스 엔진 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT&#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [기본 &#40; 삭제 Transact SQL &#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_bindefault &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_helptext&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
