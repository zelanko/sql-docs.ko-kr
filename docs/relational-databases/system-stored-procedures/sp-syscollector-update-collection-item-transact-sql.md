---
title: sp_syscollector_update_collection_item (Transact-sql) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68010549"
---
# <a name="sp_syscollector_update_collection_item-transact-sql"></a>sp_syscollector_update_collection_item(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용자 정의 컬렉션 항목의 속성을 수정하거나 사용자 정의 컬렉션 항목의 이름을 바꾸는 데 사용합니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 컬렉션 항목을 식별하는 고유한 식별자입니다. *collection_item_id* 은 **int** 이며 기본값은 NULL입니다. *name* 이 NULL 인 경우 *collection_item_id* 에 값이 있어야 합니다.  
  
 [ @name = ] '*이름*'  
 컬렉션 항목의 이름입니다. *name* 은 **sysname** 이며 기본값은 NULL입니다. *collection_item_id* 가 NULL 이면 *이름* 에 값이 있어야 합니다.  
  
 [ @new_name = ] '*new_name*'  
 컬렉션 항목의 새 이름입니다. *new_name* 는 **sysname**이며 사용 될 경우 빈 문자열일 수 없습니다.  
  
 *new_name* 은 고유 해야 합니다. 현재 컬렉션 항목 이름의 목록을 보려면 syscollector_collection_items 시스템 뷰를 쿼리합니다.  
  
 [ @frequency = ] *빈도*  
 이 컬렉션 항목에 의해 데이터가 수집되는 빈도(초)입니다. *frequency* 는 **int**이며 기본값은 5이 고, 최소값은 지정할 수 있습니다.  
  
 [ @parameters = ] '*parameters*'  
 컬렉션 항목의 입력 매개 변수입니다. *매개 변수* 는 **xml** 이며 기본값은 NULL입니다. *Parameters* 스키마는 수집기 유형의 매개 변수 스키마와 일치 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 1 (실패)  
  
## <a name="remarks"></a>설명  
 컬렉션 집합이 캐시되지 않은 모드로 설정된 경우 이 모드에서는 데이터 컬렉션과 업로드가 모두 컬렉션 집합에 지정된 일정에 따라 발생하므로 빈도 변경이 무시됩니다. 컬렉션 집합의 상태를 보려면 다음 쿼리를 실행합니다. 
  `<collection_item_id>`를 업데이트할 컬렉션 항목의 ID로 바꿉니다.  
  
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
 다음 예는 [sp_syscollector_create_collection_item &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)에 정의 된 예제에서 만든 컬렉션 항목을 기반으로 합니다.  
  
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
  
### <a name="b-renaming-a-collection-item"></a>B. 컬렉션 항목 이름 바꾸기  
 다음 예에서는 컬렉션 항목의 이름을 바꿉니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@new_name = N'My modified TSQL item';  
GO  
```  
  
### <a name="c-changing-the-parameters-of-a-collection-item"></a>C. 컬렉션 항목의 매개 변수 변경  
 다음 예에서는 컬렉션 항목과 관련된 매개 변수를 변경합니다. 
  `<Value>` 특성 내에 정의된 문이 변경되며 `UseSystemDatabases` 특성이 false로 설정됩니다. 이 항목의 현재 매개 변수를 보려면 syscollector_collection_items 시스템 뷰의 parameters 열을 쿼리합니다. 
  `@collection_item_id`의 값을 수정해야 할 수 있습니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [Transact-sql&#41;sp_syscollector_create_collection_item &#40;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)   
 [Transact-sql&#41;syscollector_collection_items &#40;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
