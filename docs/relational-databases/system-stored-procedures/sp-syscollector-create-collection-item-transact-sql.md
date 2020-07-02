---
title: sp_syscollector_create_collection_item (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collection_item
- sp_syscollector_create_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_create_collection_item
- data collector [SQL Server], stored procedures
ms.assetid: 60dacf13-ca12-4844-b417-0bc0a8bf0ddb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c5973cd5560f9c12bc38f58002cd6707fe71c714
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725613"
---
# <a name="sp_syscollector_create_collection_item-transact-sql"></a>sp_syscollector_create_collection_item(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  사용자 정의 컬렉션 집합에 컬렉션 항목을 만듭니다. 컬렉션 항목은 수집할 데이터와 데이터를 수집할 빈도를 정의합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_create_collection_item   
      [ @collection_set_id = ] collection_set_id   
    , [ @collector_type_uid = ] 'collector_type_uid'  
    , [ @name = ] 'name'   
    , [ [ @frequency = ] frequency ]  
    , [ @parameters = ] 'parameters'  
    , [ @collection_item_id = ] collection_item_id OUTPUT  
```  
  
## <a name="arguments"></a>인수  
 [ @collection_set_id =] *collection_set_id*  
 컬렉션 집합의 고유한 로컬 식별자입니다. *collection_set_id* 은 **int**입니다.  
  
 [ @collector_type_uid =] '*collector_type_uid*'  
 이 항목에 사용할 수집기 유형을 식별 하는 GUID 이며 기본값은 없는 **uniqueidentifier** *collector_type_uid* 입니다. 수집기 유형의 목록을 보려면 syscollector_collector_types 시스템 뷰를 쿼리합니다.  
  
 [ @name =] '*name*'  
 컬렉션 항목의 이름입니다. *name* 은 **sysname** 이며 빈 문자열 또는 NULL 일 수 없습니다.  
  
 *이름은* 고유 해야 합니다. 현재 컬렉션 항목 이름의 목록을 보려면 syscollector_collection_items 시스템 뷰를 쿼리합니다.  
  
 [ @frequency =] *빈도*  
 이 컬렉션 항목에서 데이터를 수집하는 빈도(초)를 지정하는 데 사용됩니다. *frequency* 는 **int**이며 기본값은 5입니다. 지정할 수 있는 최소값은 5초입니다.  
  
 컬렉션 집합이 캐시되지 않은 모드로 설정된 경우 이 모드에서는 데이터 컬렉션과 업로드가 모두 컬렉션 집합에 지정된 일정에 따라 발생하므로 빈도가 무시됩니다. 컬렉션 집합의 컬렉션 모드를 보려면 [syscollector_collection_sets](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md) 시스템 뷰를 쿼리 합니다.  
  
 [ @parameters =] '*parameters*'  
 수집기 유형의 입력 매개 변수입니다. *매개 변수* 는 **xml** 이며 기본값은 NULL입니다. *Parameters* 스키마는 수집기 유형의 매개 변수 스키마와 일치 해야 합니다.  
  
 [ @collection_item_id =] *collection_item_id*  
 컬렉션 집합 항목을 식별하는 고유한 식별자입니다. *collection_item_id* **int** 이며 출력이 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_syscollector_create_collection_item은 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
 컬렉션 항목을 추가할 컬렉션 집합은 컬렉션 항목을 만들기 전에 중지해야 합니다. 시스템 컬렉션 집합에는 컬렉션 항목을 추가할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행하려면 dc_admin(EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `Generic T-SQL Query Collector Type` 컬렉션 형식 기반의 컬렉션 항목을 만들어서 `Simple collection set test 2`라는 컬렉션 집합에 추가합니다. 지정 된 컬렉션 집합을 만들려면 [sp_syscollector_create_collection_set &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)에서 예제 B를 실행 합니다.  
  
```  
USE msdb;  
GO  
DECLARE @collection_item_id int;  
DECLARE @collection_set_id int = (SELECT collection_set_id   
                                  FROM syscollector_collection_sets  
                                  WHERE name = N'Simple collection set test 2');  
DECLARE @collector_type_uid uniqueidentifier =   
    (SELECT collector_type_uid  
     FROM syscollector_collector_types  
     WHERE name = N'Generic T-SQL Query Collector Type');  
DECLARE @params xml =   
    CONVERT(xml, N'\<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
                <Value>SELECT * FROM sys.objects</Value>  
                <OutputTable>MyOutputTable</OutputTable>  
            </Query>  
            <Databases>   
                <Database> UseSystemDatabases = "true"   
                           UseUserDatabases = "true"  
                </Database>  
            </Databases>  
         \</ns:TSQLQueryCollector>');  
  
EXEC sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid,  
    @name = 'My custom TSQL query collector item',  
    @frequency = 6000,  
    @parameters = @params,  
    @collection_item_id = @collection_item_id OUTPUT;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 수집](../../relational-databases/data-collection/data-collection.md)   
 [Transact-sql&#41;sp_syscollector_update_collection_item &#40;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)   
 [Transact-sql&#41;sp_syscollector_delete_collection_item &#40;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)   
 [Transact-sql&#41;syscollector_collector_types &#40;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)   
 [Transact-sql&#41;sp_syscollector_create_collection_set &#40;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)   
 [syscollector_collection_items&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
