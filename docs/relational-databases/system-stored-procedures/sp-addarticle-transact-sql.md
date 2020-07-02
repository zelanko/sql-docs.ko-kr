---
title: sp_addarticle (Transact-sql) | Microsoft Docs
description: 아티클을 만들어 게시에 추가합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행 됩니다.
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addarticle
- sp_addarticle_TSQL
helpviewer_keywords:
- sp_addarticle
ms.assetid: 0483a157-e403-4fdb-b943-23c1b487bef0
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 35aa02236cf3e8a11d03539042ccdaf9049dd8f9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731710"
---
# <a name="sp_addarticle-transact-sql"></a>sp_addarticle(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  아티클을 만들어 게시에 추가합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addarticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
    [ , [ @source_table = ] 'source_table' ]  
    [ , [ @destination_table = ] 'destination_table' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @type = ] 'type' ]   
    [ , [ @filter = ] 'filter' ]   
    [ , [ @sync_object= ] 'sync_object' ]   
        [ , [ @ins_cmd = ] 'ins_cmd' ]   
    [ , [ @del_cmd = ] 'del_cmd' ]   
        [ , [ @upd_cmd = ] 'upd_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @filter_clause = ] 'filter_clause' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @status = ] status ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @sync_object_owner = ] 'sync_object_owner' ]   
    [ , [ @filter_owner = ] 'filter_owner' ]   
    [ , [ @source_object = ] 'source_object' ]   
    [ , [ @artid = ] article_ID  OUTPUT ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @use_default_datatypes = ] use_default_datatypes  
    [ , [ @identityrangemanagementoption = ] identityrangemanagementoption ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @fire_triggers_on_snapshot = ] 'fire_triggers_on_snapshot' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`아티클이 포함 된 게시의 이름입니다. 이 이름은 데이터베이스에서 고유해야 합니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'`아티클의 이름입니다. 이름은 반드시 게시 내에서 고유해야 합니다. *article* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @source_table = ] 'source_table'`이 매개 변수는 더 이상 사용 되지 않습니다. 대신 *source_object* 를 사용 해야 합니다.  
  
 *이 매개 변수는 Oracle 게시자에 대해서는 지원되지 않습니다.*  
  
`[ @destination_table = ] 'destination_table'`*Source_table*또는 저장 프로시저와 다른 경우 대상 (구독) 테이블의 이름입니다. *destination_table* 는 **sysname**이며 기본값은 NULL입니다. 즉, *source_table* *destination_table * ** 와 같습니다.  
  
`[ @vertical_partition = ] 'vertical_partition'`테이블 아티클에 대해 열 필터링을 사용 하거나 사용 하지 않도록 설정 합니다. *vertical_partition* 은 **nchar (5)** 이며 기본값은 FALSE입니다.  
  
 **false** 는 수직 필터링이 없으며 모든 열을 게시 함을 나타냅니다.  
  
 **true로 설정** 하면 선언 된 기본 키를 제외한 모든 열을 지웁니다. 기본값은 없고 고유 키 열을 포함 하는 null 허용 열입니다. 열은 [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)를 사용 하 여 추가 됩니다.  
  
`[ @type = ] 'type'`아티클의 유형입니다. *형식은* **sysname**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**aggregate schema only**|스키마가 있는 집계 함수 전용입니다.|  
|**func schema only**|스키마가 있는 함수 전용입니다.|  
|**indexed view logbased**|로그 기반의 인덱싱된 뷰 아티클입니다. Oracle 게시자에 대해서는 지원되지 않습니다. 이 유형의 아티클은 기본 테이블을 별도로 게시할 필요가 없습니다.|  
|**indexed view logbased manualboth**|수동 필터 및 수동 뷰가 있는 로그 기반의 인덱싱된 뷰 아티클입니다. 이 옵션을 사용 하려면 *sync_object* 및 *필터* 매개 변수를 모두 지정 해야 합니다. 이 유형의 아티클은 기본 테이블을 별도로 게시할 필요가 없습니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
|**indexed view logbased manualfilter**|수동 필터가 있는 로그 기반의 인덱싱된 뷰 아티클입니다. 이 옵션을 사용 하려면 *sync_object* 및 *필터* 매개 변수를 모두 지정 해야 합니다. 이 유형의 아티클은 기본 테이블을 별도로 게시할 필요가 없습니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
|**indexed view logbased manualview**|수동 뷰가 있는 로그 기반의 인덱싱된 뷰 아티클입니다. 이 옵션을 사용 하려면 *sync_object* 매개 변수를 지정 해야 합니다. 이 유형의 아티클은 기본 테이블을 별도로 게시할 필요가 없습니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
|**indexed view schema only**|스키마가 있는 인덱싱된 뷰 전용입니다. 이 유형의 아티클은 기본 테이블도 게시해야 합니다.|  
|**logbased** (기본값)|로그 기반 아티클입니다.|  
|**logbased manualboth**|수동 필터 및 수동 뷰가 있는 로그 기반 아티클입니다. 이 옵션을 사용 하려면 *sync_object* 및 *필터* 매개 변수를 모두 지정 해야 합니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
|**logbased manualfilter**|수동 필터가 있는 로그 기반 아티클입니다. 이 옵션을 사용 하려면 *sync_object* 및 *필터* 매개 변수를 모두 지정 해야 합니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
|**logbased manualview**|수동 뷰가 있는 로그 기반 아티클입니다. 이 옵션을 사용 하려면 *sync_object* 매개 변수를 지정 해야 합니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
|**proc exec**|아티클의 모든 구독자로 저장 프로시저의 실행을 복제합니다. Oracle 게시자에 대해서는 지원되지 않습니다. **Proc exec**대신 **serializable proc exec** 옵션을 사용 하는 것이 좋습니다. 자세한 내용은 [트랜잭션 복제에서 저장 프로시저 실행 게시](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)의 "저장 프로시저 실행 아티클의 유형" 섹션을 참조 하세요. 변경 데이터 캡처가 설정된 경우 사용할 수 없습니다.|  
|**proc schema only**|스키마가 있는 프로시저 전용입니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
|**serializable proc exec**|직렬화할 수 있는 트랜잭션 컨텍스트 내에서 실행된 경우에만 저장 프로시저의 실행을 복제합니다. Oracle 게시자에 대해서는 지원되지 않습니다.<br /><br /> 또한 프로시저는 복제될 프로시저 실행에 대해 명시적 트랜잭션 내에서 실행되어야 합니다.|  
|**view schema only**|스키마가 있는 뷰 전용입니다. Oracle 게시자에 대해서는 지원되지 않습니다. 이 옵션을 사용할 때는 기본 테이블도 게시해야 합니다.|  
  
`[ @filter = ] 'filter'`테이블을 행 필터링 하는 데 사용 되는 저장 프로시저 (복제용으로 만듦)입니다. *filter* 는 **nvarchar (386)** 이며 기본값은 NULL입니다. 뷰 및 필터 저장 프로시저를 만들려면 [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 및 [sp_articlefilter](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 를 수동으로 실행 해야 합니다. NULL이 아닌 경우 저장 프로시저가 수동으로 생성되었다고 가정하여 필터 프로시저가 생성되지 않습니다.  
  
`[ @sync_object = ] 'sync_object'`이 아티클의 스냅숏을 나타내는 데 사용 되는 데이터 파일을 생성 하는 데 사용 되는 테이블 또는 뷰의 이름입니다. *sync_object* 은 **nvarchar (386)** 이며 기본값은 NULL입니다. NULL 인 경우 출력 파일을 생성 하는 데 사용 되는 뷰를 자동으로 만들기 위해 [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 가 호출 됩니다. 이는 [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)열을 추가한 후에 발생 합니다. NULL이 아닌 경우 뷰가 수동으로 생성된 것으로 가정하며 뷰가 생성되지 않습니다.  
  
`[ @ins_cmd = ] 'ins_cmd'`이 아티클에 대 한 삽입을 복제할 때 사용 되는 복제 명령 유형입니다. *ins_cmd* 는 **nvarchar (255)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**NONE**|아무 동작도 수행되지 않습니다.|  
|**CALL sp_MSins_**<br /> **_table_** (기본값)<br /><br /> 또는<br /><br /> **CALL custom_stored_procedure_name**|구독자에서 실행할 저장 프로시저를 호출합니다. 이 복제 방법을 사용 하려면 *schema_option* 를 사용 하 여 저장 프로시저를 자동으로 만들도록 지정 하거나 아티클에 있는 각 구독자의 대상 데이터베이스에 지정 된 저장 프로시저를 만듭니다. *custom_stored_procedure* 은 사용자가 만든 저장 프로시저의 이름입니다. <strong>sp_MSins_*테이블* </strong> 에는 매개 변수의 *_table* 부분 대신 대상 테이블의 이름이 포함 됩니다. *Destination_owner* 지정 된 경우 대상 테이블 이름 앞에 붙습니다. 예를 들어 구독자에서 **프로덕션** 스키마가 소유한 **제품 범주** 테이블의 경우 매개 변수는 `CALL sp_MSins_ProductionProductCategory` 입니다. 피어 투 피어 복제 토폴로지의 아티클의 경우 *_table* 에 GUID 값이 추가 됩니다. 구독자 업데이트에는 *custom_stored_procedure* 를 지정할 수 없습니다.|  
|**SQL** 또는 NULL|INSERT 문을 복제합니다. INSERT 문에는 아티클에 게시된 모든 열에 대한 값이 제공됩니다. 삽입에서 다음 명령이 복제됩니다.<br /><br /> `INSERT INTO <table name> VALUES (c1value, c2value, c3value, ..., cnvalue)`|  
  
 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
`[ @del_cmd = ] 'del_cmd'`이 아티클에 대 한 삭제를 복제할 때 사용 되는 복제 명령 유형입니다. *del_cmd* 는 **nvarchar (255)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**NONE**|아무 동작도 수행되지 않습니다.|  
|**CALLsp_MSdel_**<br /> **_table_** (기본값)<br /><br /> 또는<br /><br /> **CALL custom_stored_procedure_name**|구독자에서 실행할 저장 프로시저를 호출합니다. 이 복제 방법을 사용 하려면 *schema_option* 를 사용 하 여 저장 프로시저를 자동으로 만들도록 지정 하거나 아티클에 있는 각 구독자의 대상 데이터베이스에 지정 된 저장 프로시저를 만듭니다. *custom_stored_procedure* 은 사용자가 만든 저장 프로시저의 이름입니다. <strong>sp_MSdel_*테이블* </strong> 에는 매개 변수의 *_table* 부분 대신 대상 테이블의 이름이 포함 됩니다. *Destination_owner* 지정 된 경우 대상 테이블 이름 앞에 붙습니다. 예를 들어 구독자에서 **프로덕션** 스키마가 소유한 **제품 범주** 테이블의 경우 매개 변수는 `CALL sp_MSdel_ProductionProductCategory` 입니다. 피어 투 피어 복제 토폴로지의 아티클의 경우 *_table* 에 GUID 값이 추가 됩니다. 구독자 업데이트에는 *custom_stored_procedure* 를 지정할 수 없습니다.|  
|**XCALL sp_MSdel_**<br /> **_테이블_**<br /><br /> 또는<br /><br /> **XCALL custom_stored_procedure_name**|XCALL 스타일 매개 변수를 사용하는 저장 프로시저를 호출합니다. 이 복제 방법을 사용 하려면 *schema_option* 를 사용 하 여 저장 프로시저를 자동으로 만들도록 지정 하거나 아티클에 있는 각 구독자의 대상 데이터베이스에 지정 된 저장 프로시저를 만듭니다. 구독자 업데이트의 경우 사용자가 만든 저장 프로시저를 지정할 수 없습니다.|  
|**SQL** 또는 NULL|DELETE 문을 복제합니다. DELETE 문에는 모든 기본 키 열 값이 제공됩니다. 삭제에서 다음 명령이 복제됩니다.<br /><br /> `DELETE FROM <table name> WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
`[ @upd_cmd = ] 'upd_cmd'`이 아티클의 업데이트를 복제할 때 사용 되는 복제 명령 유형입니다. *upd_cmd* 는 **nvarchar (255)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**NONE**|아무 동작도 수행되지 않습니다.|  
|**CALL sp_MSupd_**<br /> **_테이블_**<br /><br /> 또는<br /><br /> **CALL custom_stored_procedure_name**|구독자에서 실행할 저장 프로시저를 호출합니다. 이 복제 방법을 사용 하려면 *schema_option* 를 사용 하 여 저장 프로시저를 자동으로 만들도록 지정 하거나 아티클에 있는 각 구독자의 대상 데이터베이스에 지정 된 저장 프로시저를 만듭니다.|  
|**MCALL sp_MSupd_**<br /> **_테이블_**<br /><br /> 또는<br /><br /> **MCALL custom_stored_procedure_name**|MCALL 스타일 매개 변수를 사용하는 저장 프로시저를 호출합니다. 이 복제 방법을 사용 하려면 *schema_option* 를 사용 하 여 저장 프로시저를 자동으로 만들도록 지정 하거나 아티클에 있는 각 구독자의 대상 데이터베이스에 지정 된 저장 프로시저를 만듭니다. *custom_stored_procedure* 은 사용자가 만든 저장 프로시저의 이름입니다. <strong>sp_MSupd_*테이블* </strong> 에는 매개 변수의 *_table* 부분 대신 대상 테이블의 이름이 포함 됩니다. *Destination_owner* 지정 된 경우 대상 테이블 이름 앞에 붙습니다. 예를 들어 구독자에서 **프로덕션** 스키마가 소유한 **제품 범주** 테이블의 경우 매개 변수는 `MCALL sp_MSupd_ProductionProductCategory` 입니다. 피어 투 피어 복제 토폴로지의 아티클의 경우 *_table* 에 GUID 값이 추가 됩니다. 구독자 업데이트의 경우 사용자가 만든 저장 프로시저를 지정할 수 없습니다.|  
|**SCALL sp_MSupd_**<br /> **_table_** (기본값)<br /><br /> 또는<br /><br /> **SCALL custom_stored_procedure_name**|SCALL 스타일 매개 변수를 사용하는 저장 프로시저를 호출합니다. 이 복제 방법을 사용 하려면 *schema_option* 를 사용 하 여 저장 프로시저를 자동으로 만들도록 지정 하거나 아티클에 있는 각 구독자의 대상 데이터베이스에 지정 된 저장 프로시저를 만듭니다. *custom_stored_procedure* 은 사용자가 만든 저장 프로시저의 이름입니다. <strong>sp_MSupd_*테이블* </strong> 에는 매개 변수의 *_table* 부분 대신 대상 테이블의 이름이 포함 됩니다. *Destination_owner* 지정 된 경우 대상 테이블 이름 앞에 붙습니다. 예를 들어 구독자에서 **프로덕션** 스키마가 소유한 **제품 범주** 테이블의 경우 매개 변수는 `SCALL sp_MSupd_ProductionProductCategory` 입니다. 피어 투 피어 복제 토폴로지의 아티클의 경우 *_table* 에 GUID 값이 추가 됩니다. 구독자 업데이트의 경우 사용자가 만든 저장 프로시저를 지정할 수 없습니다.|  
|**XCALL sp_MSupd_**<br /> **_테이블_**<br /><br /> 또는<br /><br /> **XCALL custom_stored_procedure_name**|XCALL 스타일 매개 변수를 사용하는 저장 프로시저를 호출합니다. 이 복제 방법을 사용 하려면 *schema_option* 를 사용 하 여 저장 프로시저를 자동으로 만들도록 지정 하거나 아티클에 있는 각 구독자의 대상 데이터베이스에 지정 된 저장 프로시저를 만듭니다. 구독자 업데이트의 경우 사용자가 만든 저장 프로시저를 지정할 수 없습니다.|  
|**SQL** 또는 NULL|UPDATE 문을 복제합니다. UPDATE 문에는 모든 열 값 및 기본 키 열 값이 제공됩니다. 업데이트에서 다음 명령이 복제됩니다.<br /><br /> `UPDATE <table name> SET c1 = c1value, SET c2 = c2value, SET cn = cnvalue WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
> [!NOTE]  
>  CALL, MCALL, SCALL 및 XCALL 구문에서 구독자에 전파되는 데이터 양은 각각 다릅니다. CALL 구문은 삽입 및 삭제한 모든 열의 모든 값을 전달합니다. SCALL 구문은 영향을 받은 열 값만 전달합니다. XCALL 구문은 열의 이전 값과 함께 변경 여부에 관계없이 모든 열의 값을 전달합니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
`[ @creation_script = ] 'creation_script'`구독 데이터베이스에서 아티클을 만드는 데 사용 되는 선택적 아티클 스키마 스크립트의 경로와 이름입니다. *creation_script* 는 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
`[ @description = ] 'description'`는 아티클에 대 한 설명 항목입니다. *description* 은 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
`[ @pre_creation_cmd = ] 'pre_creation_cmd'`이 아티클에 대 한 스냅숏을 적용할 때 구독자에서 같은 이름의 기존 개체가 검색 될 경우 시스템이 수행할 작업을 지정 합니다. *pre_creation_cmd* 은 **nvarchar (10)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**없음**|명령을 사용하지 않습니다.|  
|**delete**|스냅샷을 적용하기 전에 대상 테이블에서 데이터를 삭제합니다. 아티클이 행 필터링되면 필터 절에서 지정한 열에 있는 데이터만 삭제됩니다. 행 필터를 정의하면 Oracle 게시자에 대해서는 지원되지 않습니다.|  
|**drop** (기본값)|대상 테이블을 삭제합니다.|  
|**잘라내야**|대상 테이블을 자릅니다. ODBC 또는 OLE DB 구독자에는 유효하지 않습니다.|  
  
`[ @filter_clause = ] 'filter_clause'`는 가로 필터를 정의 하는 제한 (WHERE) 절입니다. 제약 조건 절을 입력할 때는 키워드인 WHERE를 생략합니다. *filter_clause* 는 **ntext**이며 기본값은 NULL입니다. 자세한 내용은 [게시된 데이터 필터링](../../relational-databases/replication/publish/filter-published-data.md)을 참조하세요.  
  
`[ @schema_option = ] schema_option`지정 된 아티클에 대 한 스키마 생성 옵션의 비트 마스크입니다. *schema_option* 는 **이진 (8)** 이며 [ (비트 or)](../../t-sql/language-elements/bitwise-or-transact-sql.md) 다음 값 중 하나 이상의 곱입니다.  
  
> [!NOTE]  
>  이 값이 NULL인 경우 시스템은 다른 아티클 속성에 따라 이 아티클에 대해 유효한 스키마 옵션을 자동으로 생성합니다. 설명에 제공 된 **기본 스키마 옵션** 표에서는 아티클 유형과 복제 유형의 조합을 기반으로 선택 되는 값을 보여 줍니다.  
  
|값|설명|  
|-----------|-----------------|  
|**0x00**|스냅숏 에이전트에서 스크립팅을 사용 하지 않도록 설정 하 고 *creation_script*을 사용 합니다.|  
|**0x01**|개체 만들기 스크립트(CREATE TABLE, CREATE PROCEDURE 등)를 생성합니다. 이 값은 저장 프로시저 아티클에 대한 기본값입니다.|  
|**제외한**|정의된 경우 아티클에 대한 변경 내용을 전파하는 저장 프로시저를 생성합니다.|  
|**0x04**|IDENTITY 속성을 사용하여 ID 열이 스크립팅됩니다.|  
|**0x08**|**타임 스탬프** 열을 복제 합니다. 설정 하지 않으면 **timestamp** 열이 **binary**로 복제 됩니다.|  
|**10**|해당 클러스터형 인덱스를 생성합니다. 이 옵션을 설정하지 않아도 게시된 테이블에 이미 정의되어 있으면 기본 키 및 UNIQUE 제약 조건과 관련된 인덱스가 생성됩니다.|  
|**0x20**|사용자 정의 데이터 형식(UDT)을 구독자에서의 기본 데이터 형식으로 변환합니다. UDT 열에 CHECK 또는 DEFAULT 제약 조건이 있거나 UDT 열이 기본 키의 일부이거나 계산 열이 UDT 열을 참조하는 경우 이 옵션을 사용할 수 없습니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*.|  
|**0x40**|해당 비클러스터형 인덱스를 생성합니다. 이 옵션을 설정하지 않아도 게시된 테이블에 이미 정의되어 있으면 기본 키 및 UNIQUE 제약 조건과 관련된 인덱스가 생성됩니다.|  
|**0x80**|PRIMARY KEY 제약 조건을 복제합니다. **0x10** 및 **0x40** 옵션을 사용 하도록 설정 하지 않은 경우에도 제약 조건과 관련 된 인덱스가 모두 복제 됩니다.|  
|**0x100**|정의된 경우 테이블 아티클에 사용자 트리거를 복제합니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*.|  
|**0x200**|FOREIGN KEY 제약 조건을 복제합니다. 참조되는 테이블이 게시되지 않는 경우 게시된 테이블의 모든 FOREIGN KEY 제약 조건은 복제되지 않습니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*.|  
|**0x400**|CHECK 제약 조건을 복제합니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*.|  
|**0x800**|기본값을 복제합니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*.|  
|**0x1000**|열 수준 데이터 정렬을 복제합니다.<br /><br /> **참고:** 대/소문자를 구분 하는 비교를 사용 하려면 Oracle 게시자에 대해이 옵션을 설정 해야 합니다.|  
|**0x2000**|게시된 아티클 원본 개체와 연관된 확장 속성을 복제합니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*.|  
|**0x4000**|UNIQUE 제약 조건을 복제합니다. **0x10** 및 **0x40** 옵션을 사용 하도록 설정 하지 않은 경우에도 제약 조건과 관련 된 인덱스가 모두 복제 됩니다.|  
|**0x8000**|이 옵션은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 게시자에 적합하지 않습니다.|  
|**0x10000**|동기화하는 동안 CHECK 조건이 강제 적용되지 않도록 해당 제약 조건을 NOT FOR REPLICATION으로 복제합니다.|  
|**0x20000**|동기화하는 동안 FOREIGN KEY 제약 조건이 강제 적용되지 않도록 해당 제약 조건을 NOT FOR REPLICATION으로 복제합니다.|  
|**0x40000**|분할된 테이블이나 인덱스와 연결된 파일 그룹을 복제합니다.|  
|**0x80000**|분할된 테이블에 대한 파티션 구성표를 복제합니다.|  
|**0x100000**|분할된 인덱스에 대한 파티션 구성표를 복제합니다.|  
|**0x200000**|테이블 통계를 복제합니다.|  
|**0x400000**|기본 바인딩|  
|**0x800000**|규칙 바인딩|  
|**0x1000000**|전체 텍스트 인덱스|  
|**0x2000000**|**Xml** 열에 바인딩된 xml 스키마 컬렉션은 복제 되지 않습니다.|  
|**0x4000000**|**Xml** 열에 인덱스를 복제 합니다.|  
|**0x8000000**|구독자에 없는 스키마를 만듭니다.|  
|**0x10000000**|구독자에서 **xml** 열을 **ntext** 로 변환 합니다.|  
|**0x20000000**|에서 도입 된 large object 데이터 형식 (**nvarchar (max)**, **varchar (max)** 및 **varbinary (max)**) [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 을에서 지원 되는 데이터 형식으로 변환 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 합니다.|  
|**0x40000000**|사용 권한을 복제합니다.|  
|**0x80000000**|게시의 일부가 아닌 개체에 대한 종속성을 삭제합니다.|  
|**0x100000000**|**Varbinary (max)** 열에 지정 된 경우이 옵션을 사용 하 여 FILESTREAM 특성을 복제 합니다. 테이블을 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 구독자에 복제할 경우에는 이 옵션을 지정하지 마십시오. FILESTREAM 열이 있는 테이블 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 은이 스키마 옵션이 설정 된 방법에 관계 없이 구독자에 복제할 수 없습니다.<br /><br /> 관련 옵션 **0x800000000**을 참조 하십시오.|  
|**0x200000000**|에서 도입 된 날짜 및 시간 데이터 형식 (**date**, **time**, **datetimeoffset**및 **datetime2**) [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 을 이전 버전의에서 지원 되는 데이터 형식으로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.|  
|**0x400000000**|데이터 및 인덱스에 대한 압축 옵션을 복제합니다. 자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하세요.|  
|**0x800000000**|FILESTREAM 데이터를 구독자에서 고유한 파일 그룹에 저장하려면 이 옵션을 설정합니다. 이 옵션을 설정하지 않으면 FILESTREAM 데이터는 기본 파일 그룹에 저장됩니다. 복제 기능에서는 파일 그룹을 만들지 않으므로 이 옵션을 설정할 경우 구독자에서 스냅샷을 적용하기 전에 파일 그룹을 만들어야 합니다. 스냅숏을 적용 하기 전에 개체를 만드는 방법에 대 한 자세한 내용은 [스냅숏 적용 전후에 스크립트 실행](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)을 참조 하세요.<br /><br /> 관련 옵션인 **0x100000000**을 참조 하십시오.|  
|**0x1000000000**|8000 바이트 보다 큰 CLR (공용 언어 런타임) Udt (사용자 정의 형식)를 **varbinary (max)** 로 변환 하 여를 실행 하는 구독자에 UDT 형식의 열을 복제할 수 있도록 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 합니다.|  
|**0x2000000000**|**Hierarchyid 데이터 형식을** **varbinary (max)** 로 변환 하 여 **hierarchyid** 형식의 열을를 실행 하는 구독자로 복제할 수 있습니다 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . 복제 된 테이블에서 **hierarchyid** 열을 사용 하는 방법에 대 한 자세한 내용은 [hierarchyid &#40;transact-sql&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)를 참조 하세요.|  
|**0x4000000000**|테이블의 필터링된 인덱스를 복제합니다. 필터링 된 인덱스에 대 한 자세한 내용은 [필터링 된 인덱스 만들기](../../relational-databases/indexes/create-filtered-indexes.md)를 참조 하세요.|  
|**0x8000000000**|**Geography** 및 **geometry** 데이터 형식을 **varbinary (max)** 로 변환 하 여 이러한 형식의 열을를 실행 하는 구독자로 복제할 수 있습니다 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .|  
|**0x10000000000**|**Geography** 및 **geometry**형식의 열에 대 한 인덱스를 복제 합니다.|  
|**0x20000000000**|열에 대한 SPARSE 특성을 복제합니다. 이 특성에 대 한 자세한 내용은 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)을 참조 하세요.|  
|**0x40000000000으로 설정**|구독자에서 메모리 최적화 테이블을 만들기 위해 스냅숏 에이전트에서 스크립팅을 사용 하도록 설정 합니다.|  
|**0x80000000000**|메모리 액세스에 최적화 된 아티클에 대해 클러스터형 인덱스를 비클러스터형 인덱스로 변환 합니다.|  
|**0x400000000000**|테이블에서 비클러스터형 columnstore 인덱스를 복제 합니다.|  
|**0x800000000000**|테이블에서 flitro비클러스터형 columnstore 인덱스를 복제 합니다.|  
|NULL|복제는 *schema_option* 를 기본값으로 자동 설정 하며, 값은 다른 아티클 속성에 따라 달라 집니다. 주의 섹션에 있는 “기본 스키마 옵션” 표에서는 아티클 유형과 복제 유형을 기반으로 하는 기본 스키마 옵션을 보여 줍니다.<br /><br /> 이외 게시의 기본값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **0X050d3**입니다.|  
  
 모든 복제 유형 및 아티클 유형에는 모든 *schema_option* 값이 유효 하지는 않습니다. 설명 섹션의 **유효한 스키마 옵션** 표에서는 아티클 유형과 복제 유형의 조합에 따라 선택할 수 있는 유효한 스키마 옵션을 보여 줍니다.  
  
`[ @destination_owner = ] 'destination_owner'`대상 개체의 소유자 이름입니다. *destination_owner* 는 **sysname**이며 기본값은 NULL입니다. *Destination_owner* 지정 하지 않으면 소유자는 다음 규칙에 따라 자동으로 지정 됩니다.  
  
|조건|대상 개체 소유자|  
|---------------|------------------------------|  
|게시는 기본 모드 대량 복사를 사용하여 초기 스냅샷을 생성하며 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자만 지원합니다.|기본값은 *source_owner*값입니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시자에서 게시합니다.|기본값은 대상 데이터베이스의 소유자입니다.|  
|게시는 문자 모드 대량 복사를 사용하여 초기 스냅샷을 생성하며 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자를 지원합니다.|할당되지 않습니다.|  
  
 이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자를 지원 하려면 *destination_owner* NULL 이어야 합니다.  
  
`[ @status = ] status`아티클이 활성 상태 인지 여부와 변경 내용을 전파 하는 방법에 대 한 추가 옵션을 지정 합니다. *status* 는 **tinyint**이며 다음이 될 수 있습니다. [| (비트 or)](../../t-sql/language-elements/bitwise-or-transact-sql.md) 이러한 값 중 하나 이상의 곱입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|아티클이 활성 상태입니다.|  
|**8**|INSERT 문에 열 이름을 포함합니다.|  
|**16** (기본값)|매개 변수가 있는 문을 사용합니다.|  
|**24**|INSERT 문에 열 이름도 포함하고 매개 변수가 있는 문도 사용합니다.|  
|**64**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 예를 들어 매개 변수가 있는 문을 사용하는 활성 아티클은 이 열의 값이 17이 되며 값이 **0** 이면 아티클이 비활성 상태이 고 추가 속성이 정의 되지 않았음을 의미 합니다.  
  
`[ @source_owner = ] 'source_owner'`원본 개체의 소유자입니다. *source_owner* 는 **sysname**이며 기본값은 NULL입니다. Oracle 게시자에 대해 *source_owner* 를 지정 해야 합니다.  
  
`[ @sync_object_owner = ] 'sync_object_owner'`게시 된 아티클을 정의 하는 뷰의 소유자입니다. *sync_object_owner* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @filter_owner = ] 'filter_owner'`필터의 소유자입니다. *filter_owner* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @source_object = ] 'source_object'`게시할 데이터베이스 개체입니다. *source_object* 는 **sysname**이며 기본값은 NULL입니다. *SOURCE_TABLE* null 이면 *source_object* null 일 수 없습니다. *source_table*대신 *source_object* 를 사용 해야 합니다. 스냅숏 또는 트랜잭션 복제를 사용 하 여 게시할 수 있는 개체 유형에 대 한 자세한 내용은 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)를 참조 하세요.  
  
`[ @artid = ] _article_ID_ OUTPUT`새 아티클의 아티클 ID입니다. *article_ID* 은 **int** 이며 기본값은 NULL이 고 OUTPUT 매개 변수입니다.  
  
`[ @auto_identity_range = ] 'auto_identity_range'`게시를 만들 때 자동 id 범위 처리를 사용 하거나 사용 하지 않도록 설정 합니다. *auto_identity_range* 은 **nvarchar (5)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**true**|자동 ID 범위 처리를 사용합니다.|  
|**false**|자동 ID 범위 처리를 사용하지 않습니다.|  
|NULL (기본값)|Id 범위 처리는 *identityrangemanagementoption*에 의해 설정 됩니다.|  
  
> [!NOTE]  
>  *auto_identity_range* 은 더 이상 사용 되지 않으며 이전 버전과의 호환성을 위해서만 제공 됩니다. Id 범위 관리 옵션을 지정 하려면 *identityrangemanagementoption* 을 사용 해야 합니다. 자세한 내용은 [ID 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)를 참조하세요.  
  
`[ @pub_identity_range = ] pub_identity_range`아티클의 *identityrangemanagementoption* 이 **auto** 로 설정 되어 있거나 *auto_identity_range* **true**로 설정 된 경우 게시자의 범위 크기를 제어 합니다. *pub_identity_range* 는 **bigint**이며 기본값은 NULL입니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*.  
  
`[ @identity_range = ] identity_range`아티클의 *identityrangemanagementoption* 가 **auto** 로 설정 되어 있거나 *auto_identity_range* **true**로 설정 된 경우 구독자의 범위 크기를 제어 합니다. *identity_range* 는 **bigint**이며 기본값은 NULL입니다. *Auto_identity_range* 이 **true**로 설정 된 경우 사용 됩니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*.  
  
`[ @threshold = ] threshold`배포 에이전트 새 id 범위를 할당 하는 시기를 제어 하는 백분율 값입니다. *임계값* 에 지정 된 값의 백분율을 사용 하는 경우 배포 에이전트 새 id 범위를 만듭니다. *threshold* 는 **bigint**이며 기본값은 NULL입니다. *Identityrangemanagementoption* 가 **auto** 로 설정 되거나 *auto_identity_range* 이 **true**로 설정 된 경우 사용 됩니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`이 저장 프로시저가 수행한 동작으로 인해 기존 스냅숏이 무효화 될 수 있음을 승인 합니다. *force_invalidate_snapshot* 은 **bit**이며 기본값은 0입니다.  
  
 **0** 은 아티클을 추가 해도 스냅숏이 무효화 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅샷을 필요로 하는 변경을 발견하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 아티클을 추가 하면 스냅숏이 무효화 될 수 있으며, 새 스냅숏이 필요한 구독이 있는 경우 기존 스냅숏이 사용 되지 않는 것으로 표시 되 고 새 스냅숏으로 생성 될 수 있는 권한을 부여 합니다.  
  
`[ @use_default_datatypes = ] use_default_datatypes`Oracle 게시자에서 아티클을 게시할 때 기본 열 데이터 형식 매핑을 사용할지 여부입니다. *use_default_datatypes* 은 bit 이며 기본값은 1입니다.  
  
 **1** = 기본 아티클 열 매핑이 사용 됩니다. 기본 데이터 형식 매핑은 [sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)를 실행 하 여 표시할 수 있습니다.  
  
 **0** = 사용자 지정 아티클 열 매핑이 정의 되므로 **sp_addarticle**에 의해 [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 호출 되지 않습니다.  
  
 *Use_default_datatypes* 를 **0**으로 설정 하면 기본값에서 변경 되는 각 열 매핑에 대해 한 번씩 [sp_changearticlecolumndatatype](../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md) 실행 해야 합니다. 모든 사용자 지정 열 매핑을 정의한 후 [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)를 실행 해야 합니다.  
  
> [!NOTE]  
>  이 매개 변수는 Oracle 게시자에 대해서만 사용해야 합니다. 게시자에 대해 *use_default_datatypes* **0** 으로 설정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하면 오류가 생성 됩니다.  
  
`[ @identityrangemanagementoption = ] identityrangemanagementoption`아티클에 대해 id 범위 관리를 처리 하는 방법을 지정 합니다. *identityrangemanagementoption* 은 **nvarchar (10)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**없음**|복제에서 ID 범위 관리를 명시적으로 수행하지 않습니다. 이 옵션은 이전 버전 SQL Server와의 호환성을 위해서만 사용하는 것이 좋습니다. 피어 복제에 대해서는 허용되지 않습니다.|  
|**수동**|수동 ID 범위 처리를 사용하려면 NOT FOR REPLICATION을 사용하여 ID 열을 표시합니다.|  
|**auto**|ID 범위의 자동 관리를 지정합니다.|  
|NULL (기본값)|*Auto_identity_range* 값이 **true**가 아니면 기본값은 **none** 입니다. 피어 투 피어 토폴로지에서 기본값은 **수동으로** 설정 됩니다 (*auto_identity_range* 는 무시 됨).|  
  
 이전 버전과의 호환성을 위해 *identityrangemanagementoption* 의 값이 NULL 이면 *auto_identity_range* 의 값이 선택 됩니다. 그러나 *identityrangemanagementoption* 의 값이 NULL이 아닌 경우 *auto_identity_range* 값은 무시 됩니다.  
  
 자세한 내용은 [ID 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)를 참조하세요.  
  
`[ @publisher = ] 'publisher'`이외 게시자를 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  게시자에 아티클을 추가할 때 *게시자* 를 사용 하면 안 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
`[ @fire_triggers_on_snapshot = ] 'fire_triggers_on_snapshot'`초기 스냅숏을 적용할 때 복제 된 사용자 트리거를 실행할지 여부입니다. *fire_triggers_on_snapshot* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다. **true** 는 스냅숏이 적용 될 때 복제 된 테이블의 사용자 트리거가 실행 됨을 의미 합니다. 트리거를 복제 하려면 *schema_option* 의 비트 마스크 값에 **0x100**값이 포함 되어야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addarticle** 는 스냅숏 복제 또는 트랜잭션 복제에 사용 됩니다.  
  
 기본적으로 복제는 열 데이터 형식이 복제에서 지원되지 않으면 원본 테이블의 어떤 열도 게시하지 않습니다. 이러한 열을 게시 해야 하는 경우에는 [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 를 실행 하 여 열을 추가 해야 합니다.  
  
 피어 투 피어 트랜잭션 복제를 지원하는 게시에 아티클을 추가하는 경우 다음 제한이 적용됩니다.  
  
-   모든 logbased 아티클에 대해 매개 변수가 있는 문을 지정해야 하며 *상태* 값에 **16** 을 포함 해야 합니다.  
  
-   대상 테이블의 이름 및 소유자는 원본 테이블과 일치해야 합니다.  
  
-   아티클을 행 또는 열 필터링할 수 없습니다.  
  
-   자동 ID 범위 관리는 지원되지 않습니다. *Identityrangemanagementoption*의 값을 manual로 지정 해야 합니다.  
  
-   테이블에 **타임 스탬프** 열이 있는 경우 *schema_option* 에 0x08를 포함 하 여 열을 **timestamp**로 복제 해야 합니다.  
  
-   *Ins_cmd*, *upd_cmd*및 *del_cmd*에 대해 **SQL** 값을 지정할 수 없습니다.  
  
 자세한 내용은 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)을 참조하세요.  
  
 개체를 게시하면 해당 정의가 구독자로 복사됩니다. 하나 이상의 다른 개체에 종속된 데이터베이스 개체를 게시하는 경우 참조되는 개체를 모두 게시해야 합니다. 예를 들어 테이블에 종속된 뷰를 게시하는 경우 테이블도 게시해야 합니다.  
  
 *Vertical_partition* **true**로 설정 된 경우 **sp_addarticle** [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 를 호출할 때까지 (마지막 [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 추가 된 후) 뷰가 생성 되는 것을 지연 시킵니다.  
  
 게시에서 구독 업데이트를 허용 하 고 게시 된 테이블에 **uniqueidentifier** 열이 없으면 테이블에 **uniqueidentifier** 열이 자동으로 추가 **sp_addarticle** .  
  
 인스턴스가 아닌 구독자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (다른 유형의 복제)로 복제 하는 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] **INSERT**, **UPDATE**및 **DELETE** 명령에 대해서만 문이 지원 됩니다.  
  
 로그 판독기 에이전트가 실행 중인 경우 아티클을 피어 투 피어 게시에 추가할 경우 로그 판독기 에이전트와 아티클을 추가하는 프로세스 간에 교착 상태가 발생할 수 있습니다. 이 문제를 방지하려면 아티클을 피어 투 피어 게시에 추가하기 전에 복제 모니터를 사용하여 아티클을 추가 중인 노드에서 로그 판독기를 중지합니다. 아티클을 추가한 후 로그 판독기 에이전트를 다시 시작합니다.  
  
 또는를 설정 하는 경우 `@del_cmd = 'NONE'` `@ins_cmd = 'NONE'` 제한 된 업데이트가 발생할 때 이러한 명령을 보내지 않으면 **업데이트** 명령의 전파가 영향을 받을 수도 있습니다. 바인딩된 업데이트는 구독자에 대한 DELETE/INSERT 쌍으로 복제되는 게시자의 UPDATE 문입니다.  
  
## <a name="default-schema-options"></a>기본 스키마 옵션  
 이 표에서는 사용자가 *schema_options* 지정 하지 않은 경우 복제에 의해 설정 되는 기본값을 설명 합니다. 여기서이 값은 복제 유형 (맨 위에 표시) 및 아티클 유형 (첫 번째 열에 표시 됨)에 따라 달라 집니다.  
  
|아티클 유형|복제 유형||  
|------------------|----------------------|------|  
||트랜잭션|스냅샷|  
|**aggregate schema only**|**0x01**|**0x01**|  
|**func schema only**|**0x01**|**0x01**|  
|**indexed view schema only**|**0x01**|**0x01**|  
|**indexed view logbased**|**0x30F3**|**0x3071**|  
|**indexed view logbase manualboth**|**0x30F3**|**0x3071**|  
|**indexed view logbased manualfilter**|**0x30F3**|**0x3071**|  
|**indexed view logbased manualview**|**0x30F3**|**0x3071**|  
|**logbased**|**0x30F3**|**0x3071**|  
|**logbased manualfilter**|**0x30F3**|**0x3071**|  
|**logbased manualview**|**0x30F3**|**0x3071**|  
|**proc exec**|**0x01**|**0x01**|  
|**proc schema only**|**0x01**|**0x01**|  
|**serializable proc exec**|**0x01**|**0x01**|  
|**view schema only**|**0x01**|**0x01**|  
  
> [!NOTE]
>  게시가 지연 업데이트를 사용 하도록 설정 된 경우에는 테이블에 표시 된 기본값에 **0x80** 의 *schema_option* 값이 추가 됩니다. 이외 게시 *schema_option* 에 대 한 기본 Schema_option [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 **0x050d3**입니다.  
  
## <a name="valid-schema-options"></a>유효한 스키마 옵션  
 다음 표에서는 복제 유형 (위에 표시 됨)과 아티클 유형 (첫 번째 열에 표시 됨)에 따라 *schema_option* 의 허용 가능한 값에 대해 설명 합니다.  
  
|아티클 유형|복제 유형||  
|------------------|----------------------|------|  
||트랜잭션|스냅샷|  
|**logbased**|모든 옵션|**0x02** 를 제외한 모든 옵션|  
|**logbased manualfilter**|모든 옵션|**0x02** 를 제외한 모든 옵션|  
|**logbased manualview**|모든 옵션|**0x02** 를 제외한 모든 옵션|  
|**indexed view logbased**|모든 옵션|**0x02** 를 제외한 모든 옵션|  
|**indexed view logbased manualfilter**|모든 옵션|**0x02** 를 제외한 모든 옵션|  
|**indexed view logbased manualview**|모든 옵션|**0x02** 를 제외한 모든 옵션|  
|**indexed view logbase manualboth**|모든 옵션|**0x02** 를 제외한 모든 옵션|  
|**proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x800000**, **0x10000000**, **0x20000000**, **0x40000000**및 **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x800000**, **0x10000000**, **0x20000000**, **0x40000000**및 **0x80000000**|  
|**serializable proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x800000**, **0x10000000**, **0x20000000**, **0x40000000**및 **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x800000**, **0x10000000**, **0x20000000**, **0x40000000**및 **0x80000000**|  
|**proc schema only**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x800000**, **0x10000000**, **0x20000000**, **0x40000000**및 **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x800000**, **0x10000000**, **0x20000000**, **0x40000000**및 **0x80000000**|  
|**view schema only**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**, **0x200000**, **0x800000**, **0x40000000**및 **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**, **0x200000**, **0x800000**, **0x40000000**및 **0x80000000**|  
|**func schema only**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x800000**, **0x10000000**, **0x20000000**, **0x40000000**및 **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x800000**, **0x10000000**, **0x20000000**, **0x40000000**및 **0x80000000**|  
|**indexed view schema only**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**, **0x200000**, **0x800000**, **0x40000000**및 **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**, **0x200000**, **0x800000**, **0x40000000**및 **0x80000000**|  
  
> [!NOTE]
>  지연 업데이트 게시의 경우 **0x8000** 및 **0x80** 의 *schema_option* 값을 사용 하도록 설정 해야 합니다. 이외 게시에 대해 지원 되는 *schema_option* 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **0x01**, **0x02**, **0x10**, **0x40**, **0x80**, **0x1000**, **0x4000** 및 **0x8000**입니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-addarticle-transact-sql_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addarticle**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [아티클 정의](../../relational-databases/replication/publish/define-an-article.md)   
 [Transact-sql&#41;sp_articlecolumn &#40;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [Transact-sql&#41;sp_articlefilter &#40;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [Transact-sql&#41;sp_articleview &#40;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [Transact-sql&#41;sp_changearticle &#40;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [Transact-sql&#41;sp_droparticle &#40;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [Transact-sql&#41;sp_helparticle &#40;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Transact-sql&#41;sp_helparticlecolumns &#40;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [Transact-sql&#41;를 &#40;하는 복제 저장 프로시저](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
