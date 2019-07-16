---
title: sp_syscollector_update_collection_item (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collection_item
- sp_syscollector_update_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_update_collection_item
ms.assetid: 7a0d36c8-c6e9-431d-a5a4-6c1802bce846
author: stevestein
ms.author: sstein
ms.openlocfilehash: 791c20214ff3eda4b5bb1f2bd3214b25ea972d74
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68010549"
---
# <a name="spsyscollectorupdatecollectionitem-transact-sql"></a>sp_syscollector_update_collection_item(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용자 정의 컬렉션 항목의 속성을 수정하거나 사용자 정의 컬렉션 항목의 이름을 바꾸는 데 사용합니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_update_collection_item   
      [ [ @collection_item_id = ] collection_item_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @frequency = ] frequency ]  
    , [ [ @parameters = ] 'parameters' ]  
```  
  
## <a name="arguments"></a>인수  
 [ @collection_item_id = ] *collection_item_id*  
 컬렉션 항목을 식별하는 고유한 식별자입니다. *collection_item_id* 됩니다 **int** 이며 기본값은 NULL입니다. *collection_item_id* 하는 경우 값이 있어야 *이름을* NULL입니다.  
  
 [ @name = ] '*name*'  
 컬렉션 항목의 이름입니다. *이름을* 됩니다 **sysname** 이며 기본값은 NULL입니다. *이름을* 하는 경우 값이 있어야 *collection_item_id* NULL입니다.  
  
 [ @new_name = ] '*new_name*'  
 컬렉션 항목의 새 이름입니다. *new_name* 됩니다 **sysname**, 및을 사용 하는 경우에 빈 문자열일 수 없습니다.  
  
 *new_name* 고유 해야 합니다. 현재 컬렉션 항목 이름의 목록을 보려면 syscollector_collection_items 시스템 뷰를 쿼리합니다.  
  
 [ @frequency = ] *frequency*  
 이 컬렉션 항목에 의해 데이터가 수집되는 빈도(초)입니다. *빈도* 됩니다 **int**, 기본값은 5 지정할 수 있는 최소값을 사용 하 여 합니다.  
  
 [ @parameters = ] '*parameters*'  
 컬렉션 항목의 입력 매개 변수입니다. *매개 변수* 됩니다 **xml** 이며 기본값은 NULL입니다. 합니다 *매개 변수* 스키마는 수집기 유형의 매개 변수 스키마와 일치 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 1 (실패)  
  
## <a name="remarks"></a>설명  
 컬렉션 집합이 캐시되지 않은 모드로 설정된 경우 이 모드에서는 데이터 컬렉션과 업로드가 모두 컬렉션 집합에 지정된 일정에 따라 발생하므로 빈도 변경이 무시됩니다. 컬렉션 집합의 상태를 보려면 다음 쿼리를 실행합니다. `<collection_item_id>`를 업데이트할 컬렉션 항목의 ID로 바꿉니다.  
  
```  
USE msdb;  
GO  
SELECT cs.collection_set_id, collection_set_uid, cs.name   
    ,'is running' = CASE WHEN is_running =  0 THEN 'No' ELSE 'Yes' END  
    ,'cache mode' = CASE WHEN collection_mode = 0 THEN 'Cached mode' ELSE 'Non-cached mode' END  
FROM syscollector_collection_sets AS cs  
JOIN syscollector_collection_items AS ci   
ON ci.collection_set_id = cs.collection_set_id  
WHERE collection_item_id = <collection_item_id>;  
```  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행하려면 dc_admin 또는 dc_operator(EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버여야 합니다. dc_operator는 이 저장 프로시저를 실행할 수 있지만 이 역할의 멤버가 변경할 수 있는 속성은 제한적입니다. 다음 속성은 dc_admin만 변경할 수 있습니다.  
  
-   @new_name  
  
-   @parameters  
  
## <a name="examples"></a>예  
 다음 예제에서 정의 된 예에서 만들어진 컬렉션 항목에 기반한 [sp_syscollector_create_collection_item &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)합니다.  
  
### <a name="a-changing-the-collection-frequency"></a>A. 컬렉션 빈도 변경  
 다음 예에서는 지정한 컬렉션 항목에 대한 컬렉션 빈도를 변경합니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@frequency = 3000;  
GO  
```  
  
### <a name="b-renaming-a-collection-item"></a>2\. 컬렉션 항목 이름 바꾸기  
 다음 예에서는 컬렉션 항목의 이름을 바꿉니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@new_name = N'My modified TSQL item';  
GO  
```  
  
### <a name="c-changing-the-parameters-of-a-collection-item"></a>3\. 컬렉션 항목의 매개 변수 변경  
 다음 예에서는 컬렉션 항목과 관련된 매개 변수를 변경합니다. `<Value>` 특성 내에 정의된 문이 변경되며 `UseSystemDatabases` 특성이 false로 설정됩니다. 이 항목의 현재 매개 변수를 보려면 syscollector_collection_items 시스템 뷰의 parameters 열을 쿼리합니다. `@collection_item_id`의 값을 수정해야 할 수 있습니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@collection_item_id = 9,   
@parameters = '  
    \<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
        <Query>  
            <Value>SELECT * FROM sys.dm_db_index_usage_stats</Value>  
            <OutputTable>MyOutputTable</OutputTable>  
        </Query>  
        <Databases>  
            <Database> UseSystemDatabases = "false"   
                       UseUserDatabases = "true"</Database>  
        </Databases>  
    \</ns:TSQLQueryCollector>';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_create_collection_item &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)   
 [syscollector_collection_items&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
