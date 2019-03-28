---
title: sp_fulltext_table (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_table_TSQL
- sp_fulltext_table
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_table
ms.assetid: a765f311-07fc-4af3-b74c-e9a027fbecce
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 340d50725a13da4993ade63d890f2300ba38763b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527195"
---
# <a name="spfulltexttable-transact-sql"></a>sp_fulltext_table(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  테이블을 전체 텍스트 인덱싱에 표시하거나 표시하지 않습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md), [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)및 [DROP FULLTEXT INDEX](../../t-sql/statements/drop-fulltext-index-transact-sql.md) 를 사용하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_fulltext_table   
   [ @tabname= ] 'qualified_table_name'           
   , [ @action= ] 'action'   
   [   
   , [ @ftcat= ] 'fulltext_catalog_name'           
   , [ @keyname= ] 'unique_index_name'   
   ]  
```  
  
## <a name="arguments"></a>인수  
`[ @tabname = ] 'qualified_table_name'` 하나 또는 두 부분 구성 테이블 이름이입니다. 테이블은 반드시 현재 데이터베이스에 있어야 합니다. *qualified_table_name* 됩니다 **nvarchar(517)**, 기본값은 없습니다.  
  
`[ @action = ] 'action'` 수행할 동작이입니다. *작업* 됩니다 **nvarchar (50)** 이며 기본값은 없고 수 있습니다 이러한 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**만들기**|참조 하는 테이블에 대 한 전체 텍스트 인덱스에 대 한 메타 데이터를 만듭니다 *qualified_table_name* 하 고이 테이블에 대 한 전체 텍스트 인덱스 데이터에는 지정 *fulltext_catalog_name*합니다. 이 작업의 사용을 지정 합니다 *unique_index_name* 전체 텍스트 키 열으로 합니다. 이 고유한 인덱스는 반드시 이미 존재해야 하며, 테이블의 한 열에서 정의되어야 합니다.<br /><br /> 전체 텍스트 카탈로그가 채워질 때까지는 해당 테이블에 대해 전체 텍스트 검색을 수행할 수 없습니다.|  
|**Drop**|에 대 한 전체 텍스트 인덱스에서 메타 데이터 삭제 *qualified_table_name*합니다. 전체 텍스트 인덱스가 활성화된 경우에는 삭제되기 전에 자동으로 비활성화됩니다. 전체 텍스트 인덱스를 삭제하기 전에 열을 제거할 필요는 없습니다.|  
|**Activate**|전체 텍스트 인덱스 데이터를 수집 하는 기능을 활성화 *qualified_table_name*비활성화 된 후, 합니다. 활성화되기 전에 전체 텍스트 인덱스에 참여하는 열이 적어도 하나 이상 있어야 합니다.<br /><br /> 전체 텍스트 인덱스는 인덱스에 첫 번째 열이 추가된 직후 채우기가 자동으로 활성화됩니다. 마지막 열이 인덱스에서 삭제되면 해당 인덱스는 비활성화됩니다. 변경 내용 추적이 진행 중인 경우 비활성화된 인덱스를 활성화하면 채우기가 새로 시작됩니다.<br /><br /> 실제로 전체 텍스트 인덱스를 채우지 않은이 있지만 단순히 테이블 전체 텍스트 카탈로그에 있는 파일 시스템에 있도록 등록에서 행 *qualified_table_name* 다음 전체 텍스트 인덱스에 검색할 수 있습니다 채우기입니다.|  
|**비활성화**|에 대 한 전체 텍스트 인덱스를 비활성화 *qualified_table_name* 이상에 대 한 전체 텍스트 인덱스 데이터를 수집할 수 있도록 합니다 *qualified_table_name*합니다. 그러나 전체 텍스트 인덱스 메타데이터는 남아 있으며 테이블을 다시 활성화할 수 있습니다.<br /><br /> 변경 내용 추적이 진행 중인 경우 활성화된 인덱스를 비활성화하면 인덱스의 상태가 고정됩니다. 즉, 진행 중인 채우기가 모두 중지되고 변경 내용이 인덱스에 더 이상 전파되지 않습니다.|  
|**start_change_tracking**|전체 텍스트 인덱스의 증분 채우기를 시작합니다. 테이블에 타임스탬프가 없는 경우에는 전체 텍스트 인덱스의 전체 채우기를 시작합니다. 테이블의 변경 내용 추적을 시작합니다.<br /><br /> 전체 텍스트 변경 내용 추적 형식의 전체 텍스트 인덱싱된 열에서 수행 된 모든 WRITETEXT 또는 UPDATETEXT 작업을 추적 하지 않습니다 **이미지**하십시오 **텍스트**, 또는 **ntext**합니다.|  
|**stop_change_tracking**|테이블의 변경 내용 추적을 중단합니다.|  
|**update_index**|추적한 변경 내용의 현재 집합을 전체 텍스트 인덱스로 전파합니다.|  
|**start_background_updateindex**|변경될 때마다 추적한 변경 내용을 전체 텍스트 인덱스로 전파하기 시작합니다.|  
|**stop_background_updateindex**|변경될 때마다 추적한 변경 내용을 전체 텍스트 인덱스로 전파하는 것을 중단합니다.|  
|**start_full**|테이블에 대한 전체 텍스트 인덱스의 전체 채우기를 시작합니다.|  
|**start_incremental**|테이블에 대한 전체 텍스트 인덱스의 증분 채우기를 시작합니다.|  
|**중지**|전체 또는 증분 채우기를 중단합니다.|  
  
`[ @ftcat = ] 'fulltext_catalog_name'` 에 대 한 유효 하 고 기존 전체 텍스트 카탈로그 이름이 **만들** 작업. 다른 모든 동작에 대해서는 이 매개 변수가 반드시 NULL이어야 합니다. *fulltext_catalog_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @keyname = ] 'unique_index_name'` 에 유효한 단일 키 열, 고유한 null이 아닌 인덱스가 *qualified_table_name* 에 **만들기** 작업 합니다. 다른 모든 동작에 대해서는 이 매개 변수가 반드시 NULL이어야 합니다. *unique_index_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 기존 전체 텍스트 인덱스는 다음 전체 채우기; 일까 지 진행에서 됩니다 특정 테이블에 대 한 전체 텍스트 인덱스를 비활성화 되 면 그러나이 인덱스 하므로 사용 되지 않습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 비활성화 된 테이블에 대 한 쿼리를 차단 합니다.  
  
 테이블이 다시 활성화되고 인덱스가 다시 채워지지 않은 경우, 신규가 아닌 남아 있는 모든 전체 텍스트를 사용할 수 있는 열에 대해 쿼리할 때 여전히 이전 인덱스를 사용할 수 있습니다. 삭제된 열에서 가져온 데이터는 모든 전체 텍스트 열 검색을 지정하는 쿼리에서 짝을 찾습니다.  
  
 테이블이 전체 텍스트 인덱싱에 대해 정의된 이후, 전체를 다시 채우지 않고 해당 열의 데이터 형식을 변경하거나 한 열에서 다른 열로 전체 텍스트 고유 키 열을 변경하여 한 데이터 형식에서 다른 데이터 형식으로 전체 텍스트 고유 키 열을 변경하는 경우, 후속 쿼리 동안 실패가 발생하며, 다음과 같은 오류 메시지가 반환됩니다. "형식으로 변환 *data_type* 전체 텍스트 검색 키 값에 대 한 실패 *key_value*." 이 방지 하려면 사용 하 여이 테이블에 대 한 전체 텍스트 정의 삭제 합니다 **drop** 의 동작 **sp_fulltext_table** 를 사용 하 여 재정의 **sp_fulltext_table** 및 **sp_fulltext_column**합니다.  
  
 전체 텍스트 키 열은 900바이트 이하로 정의되어야 합니다. 키 열의 크기는 성능 향상을 위해 가능한 작은 것이 좋습니다.  
  
## <a name="permissions"></a>사용 권한  
 구성원만 합니다 **sysadmin** 고정 서버 역할 **db_owner** 하 고 **db_ddladmin** 수 있는 전체 텍스트 카탈로그에 대 한 참조 권한을 사용 하 여 고정 데이터베이스 역할 또는 사용자 실행할 **sp_fulltext_table**합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-enabling-a-table-for-full-text-indexing"></a>1. 테이블을 전체 텍스트 인덱싱에 사용  
 다음 예에서는 `Document` 데이터베이스의 `AdventureWorks` 테이블에 대한 전체 텍스트 인덱스 메타데이터를 만듭니다. `Cat_Desc`는 전체 텍스트 카탈로그이고, `PK_Document_DocumentID`는 `Document`의 고유한 단일 열 인덱스입니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'create', 'Cat_Desc', 'PK_Document_DocumentID';  
--Add some columns  
EXEC sp_fulltext_column 'Production.Document','DocumentSummary','add';  
-- Activate the full-text index  
EXEC sp_fulltext_table 'Production.Document','activate';  
GO  
```  
  
### <a name="b-activating-and-propagating-track-changes"></a>2. 변경 내용 추적 활성화 및 전파  
 다음 예에서는 변경될 때마다 추적한 변경 내용을 활성화하여 전체 텍스트 인덱스로 전파를 시작합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'Start_change_tracking';  
EXEC sp_fulltext_table 'Production.Document', 'Start_background_updateindex';  
GO  
```  
  
### <a name="c-removing-a-full-text-index"></a>3. 전체 텍스트 인덱스 제거  
 다음 예에서는 `Document` 데이터베이스의 `AdventureWorks` 테이블에 대한 전체 텍스트 인덱스 메타데이터를 제거합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'drop';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [INDEXPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_help_fulltext_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [sp_helpindex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [전체 텍스트 검색과 의미 체계 검색 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
