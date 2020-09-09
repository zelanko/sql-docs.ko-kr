---
description: sp_tables_ex(Transact-SQL)
title: sp_tables_ex (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_tables_ex
- sp_tables_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tables_ex
ms.assetid: 33755c33-7e1e-4ef7-af14-a9cebb1e2ed4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0156f75940cf5e0d2186625d148850dcfb181ad0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544739"
---
# <a name="sp_tables_ex-transact-sql"></a>sp_tables_ex(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  지정한 연결된 서버에서 테이블에 대한 테이블 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_tables_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]  
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @table_type = ] 'table_type' ]   
     [ , [@fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @table_server = ] 'table_server'` 테이블 정보를 반환할 연결 된 서버의 이름입니다. *table_server* 는 **sysname**이며 기본값은 없습니다.  
  
``[ , [ @table_name = ] 'table_name']`` 데이터 형식 정보를 반환할 테이블의 이름입니다. *table_name*는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @table_schema = ] 'table_schema']` 테이블 스키마입니다. *table_schema*는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @table_catalog = ] 'table_catalog'` 지정 된 *table_name* 이 있는 데이터베이스의 이름입니다. *table_catalog* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @table_type = ] 'table_type'` 반환할 테이블의 유형입니다. *table_type* 는 **sysname**이며 기본값은 NULL이 고 다음 값 중 하나를 사용할 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**앤티앨리어스**|별칭 이름입니다.|  
|**GLOBAL TEMPORARY**|시스템 전반적으로 사용 가능한 임시 테이블 이름입니다.|  
|**LOCAL TEMPORARY**|현재 작업에만 사용 가능한 임시 테이블 이름입니다.|  
|**SYNONYM**|동의어 이름입니다.|  
|**시스템 테이블**|시스템 테이블 이름입니다.|  
|**시스템 뷰**|시스템 뷰 이름입니다.|  
|**TABLE**|사용자 테이블 이름입니다.|  
|**VIEW**|뷰 이름입니다.|  
  
`[ @fUsePattern = ] 'fUsePattern'`**_**, **%** , **[** 및 **]** 문자를 와일드 카드 문자로 해석할지 여부를 결정 합니다. 유효한 값은 0(패턴 일치 해제)과 1(패턴 일치 설정)입니다. *fUsePattern* 는 **bit**이며 기본값은 1입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 None  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|테이블 한정자 이름입니다. 다양 한 DBMS 제품에서 테이블에 대해 세 부분으로 구성 되는 이름 (_한정자_)을 지원**합니다.** _소유자_**.** _이름_). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 다른 제품에서는 테이블이 있는 데이터베이스 환경의 서버 이름을 나타냅니다. 이 필드는 NULL이 될 수 있습니다.|  
|**TABLE_SCHEM**|**sysname**|테이블 소유자 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 테이블을 만든 데이터베이스 사용자의 이름을 나타냅니다. 이 필드는 항상 값을 반환합니다.|  
|**TABLE_NAME**|**sysname**|테이블 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**TABLE_TYPE**|**varchar(32)**|테이블, 시스템 테이블 또는 뷰입니다.|  
|**설명**|**varchar (254)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이 열의 값을 반환하지 않습니다.|  
  
## <a name="remarks"></a>설명  
 **sp_tables_ex** 는 *table_server*에 해당 하는 OLE DB 공급자의 **IDBSchemaRowset** 인터페이스의 tables 행 집합을 쿼리하여 실행 됩니다. *Table_name*, *table_schema*, *table_catalog*및 *열* 매개 변수는 반환 되는 행을 제한 하기 위해이 인터페이스에 전달 됩니다.  
  
 지정한 연결 된 서버의 OLE DB 공급자가 **IDBSchemaRowset** 인터페이스의 tables 행 집합을 지원 하지 않는 경우 빈 결과 집합을 반환 합니다. **sp_tables_ex**  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 연결된 서버 `HumanResources`에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 `LONDON2` 스키마에 포함되어 있는 테이블에 관한 정보를 반환합니다.  
  
```  
EXEC sp_tables_ex @table_server = 'LONDON2',   
@table_catalog = 'AdventureWorks2012',   
@table_schema = 'HumanResources',   
@table_type = 'TABLE';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;분산 쿼리 저장 프로시저 ](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_catalogs &#40;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [Transact-sql&#41;sp_columns_ex &#40;](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [Transact-sql&#41;sp_column_privileges &#40;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [Transact-sql&#41;sp_foreignkeys &#40;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [Transact-sql&#41;sp_indexes &#40;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [Transact-sql&#41;sp_table_privileges &#40;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
