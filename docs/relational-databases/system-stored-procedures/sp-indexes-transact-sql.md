---
title: sp_indexes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_indexes_TSQL
- sp_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sp_indexes
ms.assetid: 25469e72-9d95-463f-912a-193471c8f5e2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 625b1b5bca3c76a0433e0b887d2c291a714c6f54
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68139915"
---
# <a name="sp_indexes-transact-sql"></a>sp_indexes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 원격 테이블에 대한 인덱스 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_indexes [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_db' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
```  
  
## <a name="arguments"></a>인수  
 [ @table_server= ] '*table_server*'  
 테이블 정보가 요청된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 연결된 서버의 이름입니다. *table_server* 는 **sysname**이며 기본값은 없습니다.  
  
 [ @table_name= ] '*table_name*'  
 인덱스 정보를 제공할 원격 테이블의 이름입니다. *table_name* 는 **sysname**이며 기본값은 NULL입니다. NULL을 지정한 경우에는 지정된 데이터베이스의 모든 테이블이 반환됩니다.  
  
 [ @table_schema= ] '*table_schema*'  
 테이블 스키마를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경에서는 테이블 소유자에 해당합니다. *table_schema* 는 **sysname**이며 기본값은 NULL입니다.  
  
 [ @table_catalog= ] '*table_db*'  
 *Table_name* 있는 데이터베이스의 이름입니다. *table_db* 는 **sysname**이며 기본값은 NULL입니다. NULL 인 경우 *table_db* 기본값은 **master**입니다.  
  
 [ @index_name= ] '*index_name*'  
 정보가 요청되는 인덱스의 이름입니다. *index* 는 **sysname**이며 기본값은 NULL입니다.  
  
 [ @is_unique= ] '*is_unique*'  
 정보가 반환될 인덱스의 유형입니다. *is_unique* 은 **bit**이며 기본값은 NULL이 고 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|1|고유 인덱스에 관한 정보를 반환합니다.|  
|0|고유하지 않은 인덱스에 관한 정보를 반환합니다.|  
|NULL|모든 인덱스에 관한 정보를 반환합니다.|  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|TABLE_CAT|**sysname**|지정된 테이블이 있는 데이터베이스의 이름입니다.|  
|TABLE_SCHEM|**sysname**|테이블의 스키마입니다.|  
|TABLE_NAME|**sysname**|원격 테이블의 이름입니다.|  
|NON_UNIQUE|**smallint**|인덱스가 고유한지의 여부입니다.<br /><br /> 0 = 고유함<br /><br /> 1 = 고유하지 않음|  
|INDEX_QUALIFER|**sysname**|인덱스 소유자의 이름입니다. 일부 DBMS 제품은 테이블 소유자 이외의 사용자가 인덱스를 만들 수 있도록 허용합니다. 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이 열은 항상 **TABLE_NAME**와 동일 합니다.|  
|INDEX_NAME|**sysname**|인덱스의 이름입니다.|  
|TYPE|**smallint**|인덱스의 유형입니다.<br /><br /> 0 = 테이블에 대한 통계<br /><br /> 1 = 클러스터형<br /><br /> 2 = 해시됨<br /><br /> 3 = 기타|  
|ORDINAL_POSITION|**int**|인덱스에 있는 열의 서수 위치입니다. 인덱스의 첫 번째 열은 1입니다. 이 열은 항상 값을 반환합니다.|  
|COLUMN_NAME|**sysname**|반환된 TABLE_NAME의 각 열에 해당하는 열 이름입니다.|  
|ASC_OR_DESC|**varchar**|데이터 정렬에 사용되는 순서입니다.<br /><br /> A = 오름차순<br /><br /> D = 내림차순<br /><br /> NULL = 해당 사항 없음<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 항상 A를 반환합니다.|  
|CARDINALITY|**int**|테이블의 열 번호 또는 인덱스의 고유한 값입니다.|  
|PAGES|**int**|인덱스 또는 테이블을 저장할 페이지의 번호입니다.|  
|FILTER_CONDITION|**nvarchar (** 4000 **)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 값을 반환하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 연결된 서버 `Employees`에 있는 `AdventureWorks2012` 데이터베이스에서 `Seattle1` 테이블의 모든 인덱스 정보를 반환하는 방법을 보여 줍니다.  
  
```  
EXEC sp_indexes @table_server = 'Seattle1',   
   @table_name = 'Employee',   
   @table_schema = 'HumanResources',  
   @table_catalog = 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;분산 쿼리 저장 프로시저](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_catalogs &#40;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [Transact-sql&#41;sp_column_privileges &#40;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [Transact-sql&#41;sp_foreignkeys &#40;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [Transact-sql&#41;sp_linkedservers &#40;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [Transact-sql&#41;sp_tables_ex &#40;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [Transact-sql&#41;sp_table_privileges &#40;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
