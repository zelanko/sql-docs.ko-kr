---
title: sp_column_privileges_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_ex
- sp_column_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges_ex
ms.assetid: 98cb6e58-4007-40fc-b048-449fb2e7e6be
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 822b017c41c9d7fbd205f25a8694e6a3ccd8d19d
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528005"
---
# <a name="spcolumnprivilegesex-transact-sql"></a>sp_column_privileges_ex(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 연결된 서버에 있는 지정한 테이블에 대한 열 권한을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_column_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @table_server = ] 'table_server'` 정보를 반환 하는 연결 된 서버의 이름이입니다. *table_server* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @table_name = ] 'table_name'` 지정 된 열이 포함 된 테이블의 이름이입니다. *table_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @table_schema = ] 'table_schema'` 테이블 스키마가입니다. *table_schema* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @table_catalog = ] 'table_catalog'` 데이터베이스의 이름이 지정 된 *table_name* 상주 합니다. *table_catalog* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @column_name = ] 'column_name'` 권한 정보를 제공할 대상 열의 이름이입니다. *column_name* 됩니다 **sysname**, 기본값은 NULL (모두 공통)를 사용 하 여 합니다.  
  
## <a name="result-sets"></a>결과 집합  
 다음 표에서는 결과 집합의 열을 보여 줍니다. 반환 된 결과 정렬 **TABLE_QUALIFIER**를 **TABLE_OWNER**를 **TABLE_NAME**를 **COLUMN_NAME**, 및  **권한**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|테이블 한정자 이름입니다. 다양 한 DBMS 제품에서는 테이블에 대해 세 부분으로 이루어진 이름 (_한정자_**.** _소유자_**.** _이름을_). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다. 이 필드는 NULL이 될 수 있습니다.|  
|**TABLE_SCHEM**|**sysname**|테이블 소유자 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 테이블을 만든 데이터베이스 사용자의 이름을 나타냅니다. 이 필드는 항상 값을 반환합니다.|  
|**TABLE_NAME**|**sysname**|테이블 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**COLUMN_NAME**|**sysname**|각 열에 대 한 열 이름에는 **TABLE_NAME** 반환 합니다. 이 필드는 항상 값을 반환합니다.|  
|**GRANTOR**|**sysname**|이에 대 한 권한을 부여한 데이터베이스 사용자 이름을 **COLUMN_NAME** 에 나열 된 **피부 여자에 게**합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],이 열은 항상 동일 합니다 **TABLE_OWNER**합니다. 이 필드는 항상 값을 반환합니다.<br /><br /> 합니다 **GRANTOR** 열은 데이터베이스 소유자를 지정할 수 있습니다 (**TABLE_OWNER**) 또는 데이터베이스 소유자 GRANT 문의 WITH GRANT OPTION 절을 사용 하 여 권한을 부여한에 게 부여한 사용자가 있습니다.|  
|**피부 여자에 게**|**sysname**|이에 대 한 권한을 부여 받은 데이터베이스 사용자 이름 **COLUMN_NAME** 나열 된 하 여 **GRANTOR**합니다. 이 필드는 항상 값을 반환합니다.|  
|**PRIVILEGE**|**varchar(** 32 **)**|사용할 수 있는 열 사용 권한 중 하나입니다. 열 사용 권한은 다음 값(또는 구현이 정의될 때 데이터 원본이 지원하는 다른 값) 중 하나일 수 있습니다.<br /><br /> 선택 = **피부 여자에 게** 열에 대 한 데이터를 검색할 수 있습니다.<br /><br /> 삽입 = **피부 여 자가** 새 행을 삽입 하는 경우이 열에 대 한 데이터를 제공할 수 있습니다 (여는 **피부 여자에 게**) 테이블로 합니다.<br /><br /> UPDATE = **피부 여자에 게** 열의 기존 데이터를 수정할 수 있습니다.<br /><br /> 참조 = **피부 여자에 게** 기본 키/외래 키 관계에서에 있는 외래 테이블의 열을 참조할 수 있습니다. 기본 키/외래 키 관계는 테이블 제약 조건으로 정의됩니다.|  
|**IS_GRANTABLE**|**varchar(** 3 **)**|나타냅니다 여부를 합니다 **피부 여자에 게** 가 ("권한 부여 권한"이 라고도 함) 다른 사용자에 게 권한을 부여할 수 있도록 합니다. YES, NO 또는 NULL이 될 수 있습니다. 알 수 없는 값 또는 NULL 값은 "권한 부여 권한"을 적용할 수 없는 데이터 원본을 의미합니다.|  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 연결된 서버 `HumanResources.Department`에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 `Seattle1` 테이블에 대한 열 권한 정보를 반환합니다.  
  
```  
EXEC sp_column_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Department',   
   @table_schema = 'HumanResources',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_table_privileges_ex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-ex-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
