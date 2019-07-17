---
title: sp_syscollector_update_collection_set (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collection_set_TSQL
- sp_syscollector_update_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_update_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 2dccc3cd-0e93-4e3e-a4e5-8fe89b31bd63
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0a351eaa746654d26d7f51536a41fc2677a2f67e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68010555"
---
# <a name="spsyscollectorupdatecollectionset-transact-sql"></a>sp_syscollector_update_collection_set(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용자 정의 컬렉션 집합의 속성을 수정하거나 사용자 정의 컬렉션 집합의 이름을 바꾸는 데 사용합니다.  
  
> [!WARNING]  
>  프록시로 구성된 Windows 계정이 아직 로그인하지 않은 비대화형 또는 대화형 사용자인 경우 프로필 디렉터리가 존재하지 않으며 준비 디렉터리 만들기가 실패합니다. 따라서 도메인 컨트롤러의 프록시 계정을 사용하는 경우 프로필 디렉터리가 만들어지도록 적어도 한 번은 사용된 대화형 계정을 지정해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_update_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    ,[ [ @schedule_uid = ] 'schedule_uid' ]  
    ,[ [ @schedule_name = ] 'schedule_uid' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @collection_set_id = ] collection_set_id` 컬렉션 집합에 대 한 고유한 로컬 식별자가입니다. *collection_set_id* 됩니다 **int** 하는 경우 값이 있어야 하 고 *이름* NULL입니다.  
  
`[ @name = ] 'name'` 컬렉션 집합의 이름이입니다. *이름* 됩니다 **sysname** 하는 경우 값이 있어야 하 고 *collection_set_id* NULL입니다.  
  
`[ @new_name = ] 'new_name'` 컬렉션 집합에 대 한 새 이름이입니다. *new_name* 됩니다 **sysname**, 및을 사용 하는 경우에 빈 문자열일 수 없습니다. *new_name* 고유 해야 합니다. 현재 컬렉션 집합 이름의 목록을 보려면 syscollector_collection_sets 시스템 뷰를 쿼리합니다.  
  
`[ @target = ] 'target'` 사용 하도록 예약 합니다.  
  
`[ @collection_mode = ] collection_mode` 사용 데이터 컬렉션의 형식이입니다. *collection_mode* 됩니다 **smallint** 다음 값 중 하나일 수 있습니다.  
  
 0 - 캐시된 모드. 데이터 컬렉션과 업로드가 별도의 일정에 속해 있습니다. 연속 컬렉션을 위해 캐시된 모드를 지정합니다.  
  
 1 - 캐시되지 않은 모드. 데이터 컬렉션과 업로드가 같은 일정에 속해 있습니다. 임시 컬렉션이나 스냅샷 컬렉션을 위해 캐시되지 않은 모드를 지정합니다.  
  
 캐시 되지 않은 모드에서 캐시 된 모드 (0)를 변경 하는 경우 지정 해야 하거나 *schedule_uid* 하거나 *schedule_name*합니다.  
  
`[ @days_until_expiration = ] days_until_expiration` 수집 된 데이터가 관리 데이터 웨어하우스에 저장 되는 일 수가입니다. *days_until_expiration* 됩니다 **smallint**합니다. *days_until_expiration* 0 또는 양의 정수 여야 합니다.  
  
`[ @proxy_id = ] proxy_id` 에 대 한 고유 식별자를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정. *proxy_id* 됩니다 **int**합니다.  
  
`[ @proxy_name = ] 'proxy_name'` 프록시의 이름이입니다. *proxy_name* 됩니다 **sysname** 이며 null을 허용 합니다.  
  
`[ @schedule_uid = ] 'schedule_uid'` 일정을 가리키는 GUID입니다. *schedule_uid* 됩니다 **uniqueidentifier**합니다.  
  
 가져오려고 *schedule_uid*, sysschedules 시스템 테이블을 쿼리 합니다.  
  
 때 *collection_mode* 0으로 설정 됩니다 *schedule_uid* 하거나 *schedule_name* 지정 해야 합니다. 때 *collection_mode* 1로 설정 됩니다 *schedule_uid* 하거나 *schedule_name* 지정 하면 무시 됩니다.  
  
`[ @schedule_name = ] 'schedule_name'` 일정의 이름이입니다. *schedule_name* 됩니다 **sysname** 이며 null을 허용 합니다. 를 지정 하는 경우 *schedule_uid* NULL 이어야 합니다. 가져오려고 *schedule_name*, sysschedules 시스템 테이블을 쿼리 합니다.  
  
`[ @logging_level = ] logging_level` 로깅 수준이입니다. *logging_level* 됩니다 **smallint** 다음 값 중 하나를 사용 하 여:  
  
 0 - 실행 정보 및 다음 항목을 추적하는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 이벤트 기록  
  
-   컬렉션 집합 시작/중지  
  
-   패키지 시작/중지  
  
-   오류 정보  
  
 1 - 수준 0 로깅 및 다음 항목  
  
-   실행 통계  
  
-   지속적으로 실행되는 컬렉션 프로세스  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)]의 경고 이벤트  
  
 2 - 수준 1 로깅 및 [!INCLUDE[ssIS](../../includes/ssis-md.md)]의 세부 이벤트 정보  
  
 에 대 한 기본값 *logging_level* 1입니다.  
  
`[ @description = ] 'description'` 컬렉션 집합의 설명이입니다. *설명을* 됩니다 **nvarchar(4000)** 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_syscollector_update_collection_set은 msdb 시스템 데이터베이스의 컨텍스트 내에서 실행되어야 합니다.  
  
 어느 *collection_set_id* 또는 *이름* 해야 값, 둘 다 NULL 일 수 없습니다. 이러한 값을 확인하려면 syscollector_collection_sets 시스템 뷰를 쿼리합니다.  
  
 컬렉션 집합을 실행 중인 경우만 업데이트할 수 있습니다 *schedule_uid* 하 고 *설명*합니다. 컬렉션 집합을 중지 하려면 사용 하 여 [sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행하려면 dc_admin 또는 dc_operator(EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버여야 합니다. dc_operator는 이 저장 프로시저를 실행할 수 있지만 이 역할의 멤버가 변경할 수 있는 속성은 제한적입니다. 다음 속성은 dc_admin만 변경할 수 있습니다.  
  
-   @new_name  
  
-   @target  
  
-   @proxy_id  
  
-   @description  
  
-   @collection_mode  
  
-   @days_until_expiration  
  
## <a name="examples"></a>예  
  
### <a name="a-renaming-a-collection-set"></a>A. 컬렉션 집합 이름 바꾸기  
 다음 예에서는 사용자 정의 컬렉션 집합의 이름을 바꿉니다.  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 1',  
@new_name = N'Collection set test 1 in cached mode';  
GO  
```  
  
### <a name="b-changing-the-collection-mode-from-non-cached-to-cached"></a>2\. 컬렉션 모드를 캐시되지 않은 모드에서 캐시된 모드로 변경  
 다음 예에서는 컬렉션 모드를 캐시되지 않은 모드에서 캐시된 모드로 변경합니다. 이렇게 변경하려면 일정 ID 또는 일정 이름을 지정해야 합니다.  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Collection set test 1 in cached mode',  
@collection_mode = 0,  
@schedule_uid = 'C7022AF3-51B8-4011-B159-64C47C88FF70';  
-- alternatively, use @schedule_name.  
-- @schedule_name = N'CollectorSchedule_Every_15min;  
GO  
```  
  
### <a name="c-changing-other-collection-set-parameters"></a>3\. 다른 컬렉션 집합 매개 변수 변경  
 다음 예에서는 "Simple collection set test 2"라는 컬렉션 집합의 다양한 속성을 업데이트합니다.  
  
```  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 2',  
@collection_mode = 1,  
@days_until_expiration = 5,  
@description = N'This is a test collection set that runs in noncached mode.',  
@logging_level = 0;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)   
 [dbo.sysschedules &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
