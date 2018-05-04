---
title: sp_column_privileges (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_TSQL
- sp_column_privileges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges
ms.assetid: a3784301-2517-4b1d-bbd9-47404483fad0
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 41f6cc18687e6491295e2843632e0bd6badbc95a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spcolumnprivileges-transact-sql"></a>sp_column_privileges(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 환경 내의 단일 테이블에 대한 열 권한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_column_privileges [ @table_name = ] 'table_name'   
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @column_name = ] 'column' ]  
```  
  
## <a name="arguments"></a>인수  
 [ @table_name=] '*table_name*'  
 카탈로그 정보를 반환하는 데 사용되는 테이블입니다. *table_name* 은 **sysname**, 기본값은 없습니다. 와일드카드 패턴 일치는 지원되지 않습니다.  
  
 [ @table_owner=] '*table_owner*'  
 카탈로그 정보를 반환하는 데 사용하는 테이블의 소유자입니다. *table_owner* 은 **sysname**, 기본값은 NULL입니다. 와일드카드 패턴 일치는 지원되지 않습니다. 경우 *table_owner* 을 지정 하지 않으면 기본 데이터베이스 관리 시스템 (DBMS)의 기본 테이블 표시 규칙이 적용 됩니다.  
  
 현재 사용자가 지정한 이름의 테이블을 소유하고 있는 경우 해당 테이블의 열이 반환됩니다. 경우 *table_owner* 지정 하지 않으면 현재 사용자가 지정 된 테이블을 소유 하지 및 *table_name*, sp_column_privileges 지정 된 테이블을 찾습니다 *table_name* 데이터베이스 소유자가 소유 합니다. 테이블이 있으면 테이블의 열이 반환됩니다.  
  
 [ @table_qualifier=] '*table_qualifier*'  
 테이블 한정자의 이름입니다. *table_qualifier* 은 *sysname*, 기본값은 NULL입니다. 다양 한 DBMS 제품에서는 테이블에 대 한 세 부분으로 구성 된 이름 (*한정자 ***.*** 소유자 ***.*** 이름*). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다.  
  
 [ @column_name=] '*열*'  
 카탈로그 정보 중 한 열만 확보될 때 사용되는 단일 열입니다. *열* 은 **nvarchar (** 384 **)**, 기본값은 NULL입니다. 경우 *열* 은 지정 하지 않으면 모든 열 반환 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], *열* sys.columns 테이블에 나열 된 열 이름을 나타냅니다. *열* 일치 패턴은 기본 DBMS의 와일드 카드를 사용 하 여 와일드 카드 문자를 포함할 수 있습니다. 상호 운용성을 극대화하려면 게이트웨이 클라이언트에서 ISO 표준 패턴 일치(% 및 _ 와일드카드 문자)만 사용해야 합니다.  
  
## <a name="result-sets"></a>결과 집합  
 sp_column_privileges는 ODBC의 SQLColumnPrivileges와 같습니다. 반환된 결과는 TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME, COLUMN_NAME 및 PRIVILEGE 순으로 정렬됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|테이블 한정자 이름입니다. 이 필드는 NULL이 될 수 있습니다.|  
|TABLE_OWNER|**sysname**|테이블 소유자 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|TABLE_NAME|**sysname**|테이블 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|COLUMN_NAME|**sysname**|반환된 TABLE_NAME의 각 열 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|GRANTOR|**sysname**|나열된 GRANTEE에게 해당 COLUMN_NAME에 대한 권한을 부여한 데이터베이스 사용자 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 항상 TABLE_OWNER와 같습니다. 이 필드는 항상 값을 반환합니다.<br /><br /> GRANTOR 열은 데이터베이스 소유자(TABLE_OWNER)이거나 또는 데이터베이스 소유자가 GRANT 문에 WITH GRANT OPTION 절을 사용하여 권한을 부여한 사용자가 될 수 있습니다.|  
|GRANTEE|**sysname**|나열된 GRANTOR에 의해 해당 COLUMN_NAME에 대한 권한을 부여받은 데이터베이스 사용자 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 항상 sysusers 테이블의 한 명의 데이터베이스 사용자를 포함합니다. 이 필드는 항상 값을 반환합니다.|  
|PRIVILEGE|**varchar(** 32 **)**|사용할 수 있는 열 사용 권한 중 하나입니다. 열 사용 권한은 다음 값(또는 구현이 정의될 때 데이터 원본이 지원하는 다른 값) 중 하나일 수 있습니다.<br /><br /> SELECT = GRANTEE는 열에 대한 데이터를 검색할 수 있습니다<br /><br /> INSERT = GRANTEE는 GRANTEE에 의해 새 행이 테이블에 삽입될 때 이 열에 대한 데이터를 제공할 수 있습니다.<br /><br /> UPDATE = GRANTEE는 열의 기존 데이터를 수정할 수 있습니다.<br /><br /> REFERENCES = GRANTEE는 기본 키/외래 키 관계에 있는 외래 테이블의 열을 참조할 수 있습니다. 기본 키/외래 키 관계는 테이블 제약 조건을 사용하여 정의됩니다.|  
|IS_GRANTABLE|**varchar (** 3 **)**|GRANTEE가 다른 사용자에게 권한을 부여할 수 있도록 허용할지 여부를 나타냅니다. 이것을 "권한 부여 권한"이라고도 합니다. YES, NO 또는 NULL이 될 수 있습니다. 알 수 없는 값(또는 NULL)은 "권한 부여 권한"을 적용할 수 없는 데이터 원본을 의미합니다.|  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 경우 GRANT 문으로 사용 권한을 부여하고 REVOKE 문으로 사용 권한을 제거합니다.  
  
## <a name="permissions"></a>Permissions  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 특정 열에 대한 열 권한 정보를 반환하는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_column_privileges @table_name = 'Employee'   
    ,@table_owner = 'HumanResources'  
    ,@table_qualifier = 'AdventureWorks2012'  
    ,@column_name = 'SalariedFlag';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
