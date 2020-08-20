---
description: sp_bindefault(Transact-SQL)
title: sp_bindefault (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_bindefault
- sp_bindefault_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindefault
ms.assetid: 3da70c10-68d0-4c16-94a5-9e84c4a520f6
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5f72269bbeef0954cff5a312909c55797d82b8f8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493475"
---
# <a name="sp_bindefault-transact-sql"></a>sp_bindefault(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  열 또는 별칭 데이터 형식에 기본값을 바인딩합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 또는 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 문의 default 키워드를 사용 하 여 기본 정의를 만드는 것이 좋습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_bindefault [ @defname = ] 'default' ,   
    [ @objname = ] 'object_name'   
    [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @defname = ] 'default'` 기본값 만들기로 생성 된 기본값의 이름입니다. *기본값* 은 **nvarchar (776)** 이며 기본값은 없습니다.  
  
`[ @objname = ] 'object_name'` 기본값을 바인딩할 테이블 및 열의 이름 또는 별칭 데이터 형식입니다. *object_name* 은 **nvarchar (776)** 이며 기본값은 없습니다. *object_name* 는 **varchar (max)**, **nvarchar (max)**, **VARBINARY (max)**, **xml**또는 CLR 사용자 정의 형식으로 정의할 수 없습니다.  
  
 *Object_name* 한 부분으로 구성 된 이름인 경우 별칭 데이터 형식으로 확인 됩니다. 두 부분이나 세 부분으로 된 이름이면 먼저 테이블 및 열로 확인된 다음 확인이 실패하면 별칭 데이터 형식으로 확인됩니다. 기본적으로 별칭 데이터 형식의 기존 열은 기본값이 열에 직접 바인딩된 경우를 제외 하 고는 *기본값*을 상속 합니다. 기본값은 **text**, **ntext**, **image**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, **timestamp**또는 CLR 사용자 정의 형식 열, IDENTITY 속성이 있는 열, 계산 열 또는 이미 default 제약 조건이 있는 열에 바인딩할 수 없습니다.  
  
> [!NOTE]  
>  *object_name* 대괄호 **([])** 를 구분 식별자로 사용할 수 있습니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
`[ @futureonly = ] 'futureonly_flag'` 는 기본값을 별칭 데이터 형식에 바인딩하는 경우에만 사용 됩니다. *futureonly_flag* 는 **varchar (15)** 이며 기본값은 NULL입니다. 이 매개 변수를 **futureonly**로 설정 하면 해당 데이터 형식의 기존 열이 새 기본값을 상속할 수 없습니다. 이 매개 변수는 열에 기본값을 바인딩할 때는 절대 사용되지 않습니다. *FUTUREONLY_FLAG* NULL 이면 새 기본값은 현재 기본값이 없거나 별칭 데이터 형식의 기존 기본값을 사용 하는 별칭 데이터 형식의 열에 바인딩됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 기본 제약 조건을 사용 하거나 기존 기본값의 바인딩을 해제 하지 않고 별칭 데이터 형식에 새 기본값을 바인딩하는 대신 **sp_bindefault** 를 사용 하 여 새 기본값을 열에 바인딩할 수 있습니다. 이전의 기본값은 무시됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식 또는 CLR 사용자 정의 형식에는 기본값을 바인딩할 수 없습니다. 기본값을 바인딩한 열과 기본값이 호환되지 않는 경우에는 바인딩할 때가 아니라 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]가 기본값을 삽입하려고 시도할 때 오류 메시지를 반환합니다.  
  
 별칭 데이터 형식의 기존 열은 기본값이 자신에 게 직접 바인딩되어 있거나 *futureonly_flag* **futureonly**로 지정 되지 않은 경우 새 기본값을 상속 합니다. 별칭 데이터 형식의 새 열은 항상 기본값을 상속합니다.  
  
 기본값을 열에 바인딩하면 관련 정보가 **sys. columns** 카탈로그 뷰에 추가 됩니다. 별칭 데이터 형식에 기본값을 바인딩하면 관련 정보가 **sys. types** 카탈로그 뷰에 추가 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 테이블을 소유 하거나 **sysadmin** 고정 서버 역할의 멤버 이거나 고정 데이터베이스 역할을 **db_ddladmin** **db_owner** 합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-binding-a-default-to-a-column"></a>A. 열에 기본값 바인딩  
 `today`라는 기본값이 CREATE DEFAULT에 의해 현재 데이터베이스에 정의되었으며, 다음 예에서는 이 기본값을 `HireDate` 테이블의 `Employee` 열에 바인딩합니다. `Employee` 열의 데이터가 제공되지 않은 채로 `HireDate` 테이블에 행이 추가될 때마다 열은 `today`라는 기본값을 할당받게 됩니다.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-default-to-an-alias-data-type"></a>B. 별칭 데이터 형식에 기본값 바인딩  
 `def_ssn`이라는 이름의 기본값과 `ssn`이라는 이름의 별칭 데이터 형식이 이미 존재합니다. 다음 예에서는 기본값 `def_ssn`을 `ssn`에 바인딩합니다. 테이블을 작성할 때 별칭 데이터 형식인 `ssn`으로 할당된 모든 열은 기본값을 상속합니다. **Futureonly** 가 *futureonly_flag* 값에 대해 지정 되지 않은 경우 또는 열에 직접 바인딩된 기본값이 있는 경우가 아니면 **ssn** 형식의 기존 열도 기본 **def_ssn**를 상속 합니다. 열에 바인딩된 기본값은 데이터 형식에 바인딩된 값보다 항상 우선합니다.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonly_flag"></a>C. futureonly_flag 사용  
 다음 예에서는 기본값 `def_ssn`을 별칭 데이터 형식 `ssn`에 바인딩합니다. **Futureonly** 가 지정 되었으므로 형식의 기존 열 `ssn` 은 영향을 받지 않습니다.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 구분 식별자 사용  
 다음 예제에서는 object_name에서 구분 식별자를 사용 하는 방법을 보여 줍니다 `[t.1]` . *object_name*  
  
```  
USE master;  
GO  
CREATE TABLE [t.1] (c1 int);   
-- Notice the period as part of the table name.  
EXEC sp_bindefault 'default1', '[t.1].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name,   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>관련 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT&#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-sql&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [Transact-sql&#41;sp_unbindefault &#40;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
