---
title: sp_table_privileges_ex (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: b40f7233bb3c50203a68c0b01cfcbdaf631e0098
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68096175"
---
# <a name="sp_table_privileges_ex-transact-sql"></a>sp_table_privileges_ex(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 연결된 서버에서 지정한 테이블에 대한 권한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_table_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
     [ , [@fUsePattern =] 'fUsePattern']  
```  
  
## <a name="arguments"></a>인수  
`[ @table_server = ] 'table_server'`정보를 반환할 연결 된 서버의 이름입니다. *table_server* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @table_name = ] 'table_name']`테이블 권한 정보를 제공할 테이블의 이름입니다. *table_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @table_schema = ] 'table_schema'`테이블 스키마입니다. 일부 DBMS 환경에서는 테이블 소유자입니다. *table_schema* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @table_catalog = ] 'table_catalog'`지정 된 *table_name* 이 있는 데이터베이스의 이름입니다. *table_catalog* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @fUsePattern = ] 'fUsePattern'`문자 ' _ ', '% ', ' [' 및 '] '가 와일드 카드 문자로 해석 되는지 여부를 결정 합니다. 유효한 값은 0(패턴 일치 해제)과 1(패턴 일치 설정)입니다. *fUsePattern* 는 **bit**이며 기본값은 1입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|테이블 한정자 이름입니다. 다양 한 DBMS 제품에서 테이블에 대해 세 부분으로 구성 되는 이름 (_한정자_)을 지원**합니다.** _소유자_**.** _이름_). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다. 이 필드는 NULL이 될 수 있습니다.|  
|**TABLE_SCHEM**|**sysname**|테이블 소유자 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 테이블을 만든 데이터베이스 사용자의 이름을 나타냅니다. 이 필드는 항상 값을 반환합니다.|  
|**TABLE_NAME**|**sysname**|테이블 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**GRANTOR**|**sysname**|나열 된 **피부 여자**에 대해이 **TABLE_NAME** 에 대 한 권한을 부여한 데이터베이스 사용자 이름입니다. 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이 열은 항상 **TABLE_OWNER**와 동일 합니다. 이 필드는 항상 값을 반환합니다. 또한 GRANTOR 열은 데이터베이스 소유자 (**TABLE_OWNER**) 이거나 데이터베이스 소유자가 GRANT 문의 WITH grant OPTION 절을 사용 하 여 사용 권한을 부여한 사용자가 될 수 있습니다.|  
|**GRANTEE**|**sysname**|나열 된 **GRANTOR**에 의해이 **TABLE_NAME** 에 대 한 권한이 부여 된 데이터베이스 사용자 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**PRIVILEGE**|**varchar (** 32 **)**|사용할 수 있는 테이블 사용 권한 중의 하나입니다. 테이블 사용 권한은 다음 값 중 하나 또는 구현이 정의될 때 데이터 원본에 의해 지원되는 그 밖의 값이 될 수 있습니다.<br /><br /> SELECT = **피부 여자** 는 하나 이상의 열에 대 한 데이터를 검색할 수 있습니다.<br /><br /> INSERT = **피부 여자** 는 하나 이상의 열에 대 한 새 행에 데이터를 제공할 수 있습니다.<br /><br /> UPDATE = **피부 여자** 는 하나 이상의 열에 대 한 기존 데이터를 수정할 수 있습니다.<br /><br /> DELETE = **피부 여자** 는 테이블에서 행을 제거할 수 있습니다.<br /><br /> REFERENCES = **피부 여자** 는 기본 키/외래 키 관계에 있는 외래 테이블의 열을 참조할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기본 키/외래 키 관계는 테이블 제약 조건을 사용하여 정의됩니다.<br /><br /> 특정 테이블 권한으로 **피부 여자** 에 지정 된 작업의 범위는 데이터 원본에 따라 다릅니다. 예를 들어 UPDATE 권한은 **피부 여자** 가 한 데이터 원본에 있는 테이블의 모든 열과 **GRANTOR** 가 다른 데이터 원본에 대 한 업데이트 권한을 가진 열만 업데이트할 수 있게 합니다.|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|**피부 여자** 에서 다른 사용자에 게 사용 권한을 부여할 수 있는지 여부를 나타냅니다. 이것을 주로 "허가의 허가" 권한이라고 합니다. YES, NO 또는 NULL이 될 수 있습니다. 알 수 없는(또는 NULL) 값은 "허가의 허가"를 적용할 수 없는 데이터 원본을 의미합니다.|  
  
## <a name="remarks"></a>설명  
 반환 되는 결과는 **TABLE_QUALIFIER**, **TABLE_OWNER**, **TABLE_NAME**및 **권한에**따라 정렬 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 지정한 연결된 서버 `Product`의 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 `Seattle1`로 시작되는 이름을 가진 테이블에 대한 권한 정보를 반환합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 연결 된 서버로 가정 됩니다.  
  
```  
EXEC sp_table_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Product%',   
   @table_schema = 'Production',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_column_privileges_ex &#40;](../../relational-databases/system-stored-procedures/sp-column-privileges-ex-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;분산 쿼리 저장 프로시저](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
