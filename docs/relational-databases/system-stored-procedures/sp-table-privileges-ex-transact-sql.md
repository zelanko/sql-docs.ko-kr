---
title: sp_table_privileges_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_table_privileges_ex
- sp_table_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_table_privileges_ex
ms.assetid: b58d4a07-5c40-4f17-b66e-6d6b17188dda
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a11fb3f879336f5217abe138c91755154df868b5
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534275"
---
# <a name="sptableprivilegesex-transact-sql"></a>sp_table_privileges_ex(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 연결된 서버에서 지정한 테이블에 대한 권한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_table_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
     [ , [@fUsePattern =] 'fUsePattern']  
```  
  
## <a name="arguments"></a>인수  
`[ @table_server = ] 'table_server'` 정보를 반환 하는 연결 된 서버의 이름이입니다. *table_server* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @table_name = ] 'table_name']` 테이블 권한 정보를 제공 하는 테이블의 이름이입니다. *table_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @table_schema = ] 'table_schema'` 테이블 스키마가입니다. 일부 DBMS 환경에서는 테이블 소유자입니다. *table_schema* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @table_catalog = ] 'table_catalog'` 데이터베이스의 이름이 지정 된 *table_name* 상주 합니다. *table_catalog* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @fUsePattern = ] 'fUsePattern'` 확인 여부를 문자 '_', '%', ' [', 및 ']' 와일드 카드 문자로 해석 됩니다. 유효한 값은 0(패턴 일치 해제)과 1(패턴 일치 설정)입니다. *fUsePattern* 됩니다 **비트**, 기본값은 1입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|테이블 한정자 이름입니다. 다양 한 DBMS 제품에서는 테이블에 대해 세 부분으로 이루어진 이름 (_한정자_**.** _소유자_**.** _이름을_). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다. 이 필드는 NULL이 될 수 있습니다.|  
|**TABLE_SCHEM**|**sysname**|테이블 소유자 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 테이블을 만든 데이터베이스 사용자의 이름을 나타냅니다. 이 필드는 항상 값을 반환합니다.|  
|**TABLE_NAME**|**sysname**|테이블 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**GRANTOR**|**sysname**|이에 대 한 권한을 부여한 데이터베이스 사용자 **TABLE_NAME** 에 나열 된 **피부 여자에 게**합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],이 열은 항상 동일 합니다 **TABLE_OWNER**합니다. 이 필드는 항상 값을 반환합니다. 또한 GRANTOR 열은 데이터베이스 소유자를 수 있습니다 (**TABLE_OWNER**) 또는 부여한 사용자가 데이터베이스 소유자 권한 GRANT 문의 WITH GRANT OPTION 절을 사용 합니다.|  
|**피부 여자에 게**|**sysname**|이에 대 한 권한을 부여 받은 데이터베이스 사용자 이름 **TABLE_NAME** 나열 된 하 여 **GRANTOR**합니다. 이 필드는 항상 값을 반환합니다.|  
|**PRIVILEGE**|**varchar(** 32 **)**|사용할 수 있는 테이블 사용 권한 중의 하나입니다. 테이블 사용 권한은 다음 값 중 하나 또는 구현이 정의될 때 데이터 원본에 의해 지원되는 그 밖의 값이 될 수 있습니다.<br /><br /> 선택 = **피부 여자에 게** 하나 이상의 열에 대 한 데이터를 검색할 수 있습니다.<br /><br /> INSERT = **피부 여자에 게** 하나 이상의 열에 대 한 새 행에 대 한 데이터를 제공할 수 있습니다.<br /><br /> UPDATE = **피부 여자에 게** 하나 이상의 열에 대 한 기존 데이터를 수정할 수 있습니다.<br /><br /> 삭제 = **피부 여자에 게** 테이블에서 행을 제거할 수 있습니다.<br /><br /> 참조 = **피부 여자에 게** 기본 키/외래 키 관계에서에 있는 외래 테이블의 열을 참조할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기본 키/외래 키 관계는 테이블 제약 조건을 사용하여 정의됩니다.<br /><br /> 에 지정 된 동작의 범위는 **피부 여자에 게** 특정 테이블 권한은 데이터 원본에 따라 결정 됩니다. 예를 들어 UPDATE 권한을 활성화할 수는 **피부 여 자가** 는 하나의 데이터 원본에 테이블의 모든 열 및 열만 업데이트를 **GRANTOR** 다른 데이터 원본에 대 한 업데이트 권한이 합니다.|  
|**IS_GRANTABLE**|**varchar(** 3 **)**|나타냅니다 여부는 **피부 여자에 게** 가 다른 사용자에 게 권한을 부여할 수 있도록 합니다. 이것을 주로 "허가의 허가" 권한이라고 합니다. YES, NO 또는 NULL이 될 수 있습니다. 알 수 없는(또는 NULL) 값은 "허가의 허가"를 적용할 수 없는 데이터 원본을 의미합니다.|  
  
## <a name="remarks"></a>Remarks  
 반환 된 결과 정렬 **TABLE_QUALIFIER**를 **TABLE_OWNER**를 **TABLE_NAME**, 및 **권한**합니다.  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 지정한 연결된 서버 `Product`의 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 `Seattle1`로 시작되는 이름을 가진 테이블에 대한 권한 정보를 반환합니다. ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 된 서버로 가정).  
  
```  
EXEC sp_table_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Product%',   
   @table_schema = 'Production',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_column_privileges_ex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-ex-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [분산 쿼리 저장된 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
