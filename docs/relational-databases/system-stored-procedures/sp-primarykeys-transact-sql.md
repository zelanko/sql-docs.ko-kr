---
title: sp_primarykeys (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_primarykeys_TSQL
- sp_primarykeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_primarykeys
ms.assetid: 0f76dd31-5b7b-4209-9e2e-b9ed5cac164d
author: stevestein
ms.author: sstein
ms.openlocfilehash: ccae0385ef8c9305f4972ff6dcbd7a7960200370
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68056307"
---
# <a name="sp_primarykeys-transact-sql"></a>sp_primarykeys(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 원격 테이블의 기본 키 열을 각 키 열당 한 개의 행으로 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_primarykeys [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @table_server = ] 'table_server'_`기본 키 정보를 반환할 연결 된 서버의 이름입니다. *table_server* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @table_name = ] 'table_name'`기본 키 정보를 제공할 테이블의 이름입니다. *table_name*는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @table_schema = ] 'table_schema'`테이블 스키마입니다. *table_schema* 는 **sysname**이며 기본값은 NULL입니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경에서는 테이블 소유자에 해당합니다.  
  
`[ @table_catalog = ] 'table_catalog'`지정 된 *table_name* 있는 카탈로그의 이름입니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경에서는 데이터베이스 이름에 해당합니다. *table_catalog* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 None  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|테이블 카탈로그입니다.|  
|**TABLE_SCHEM**|**sysname**|테이블 스키마입니다.|  
|**TABLE_NAME**|**sysname**|테이블 이름입니다.|  
|**COLUMN_NAME**|**sysname**|열의 이름입니다.|  
|**KEY_SEQ**|**int**|기본 키가 여러 열로 구성된 경우 열의 시퀀스 번호입니다.|  
|**PK_NAME**|**sysname**|기본 키 식별자입니다. 데이터 원본에 적용할 수 없을 경우에는 NULL을 반환합니다.|  
  
## <a name="remarks"></a>설명  
 **sp_primarykeys** 는 *table_server*에 해당 하는 OLE DB 공급자의 **IDBSchemaRowset** 인터페이스에 대 한 PRIMARY_KEYS 행 집합을 쿼리하여 실행 됩니다. *Table_name*, *table_schema*, *table_catalog*및 *열* 매개 변수는 반환 되는 행을 제한 하기 위해이 인터페이스에 전달 됩니다.  
  
 지정한 연결 된 서버의 OLE DB 공급자가 **IDBSchemaRowset** 인터페이스의 PRIMARY_KEYS 행 집합을 지원 하지 않는 경우 빈 결과 집합을 반환 합니다. **sp_primarykeys**  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LONDON1` 데이터베이스의 `HumanResources.JobCandidate` 테이블에 대해 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 서버에서 기본 키 열을 반환합니다.  
  
```  
EXEC sp_primarykeys @table_server = N'LONDON1',   
   @table_name = N'JobCandidate',  
   @table_catalog = N'AdventureWorks2012',   
   @table_schema = N'HumanResources';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;분산 쿼리 저장 프로시저](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_catalogs &#40;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [Transact-sql&#41;sp_column_privileges &#40;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [Transact-sql&#41;sp_foreignkeys &#40;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [Transact-sql&#41;sp_indexes &#40;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [Transact-sql&#41;sp_linkedservers &#40;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [Transact-sql&#41;sp_tables_ex &#40;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [Transact-sql&#41;sp_table_privileges &#40;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
