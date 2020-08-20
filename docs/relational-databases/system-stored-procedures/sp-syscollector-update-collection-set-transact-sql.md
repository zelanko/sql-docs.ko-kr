---
description: sp_syscollector_update_collection_set(Transact-SQL)
title: sp_syscollector_update_collection_set (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 00285e7f1e170a671cd38149098e485c90f710db
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485704"
---
# <a name="sp_syscollector_update_collection_set-transact-sql"></a>sp_syscollector_update_collection_set(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  사용자 정의 컬렉션 집합의 속성을 수정하거나 사용자 정의 컬렉션 집합의 이름을 바꾸는 데 사용합니다.  
  
> [!WARNING]  
>  프록시로 구성된 Windows 계정이 아직 로그인하지 않은 비대화형 또는 대화형 사용자인 경우 프로필 디렉터리가 존재하지 않으며 준비 디렉터리 만들기가 실패합니다. 따라서 도메인 컨트롤러의 프록시 계정을 사용하는 경우 프로필 디렉터리가 만들어지도록 적어도 한 번은 사용된 대화형 계정을 지정해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @collection_set_id = ] collection_set_id` 컬렉션 집합의 고유한 로컬 식별자입니다. *collection_set_id* 은 **int** 이며 *name* 이 NULL 인 경우 값이 있어야 합니다.  
  
`[ @name = ] 'name'` 컬렉션 집합의 이름입니다. *name* 은 **SYSNAME** 이며 *collection_set_id* NULL 인 경우 값이 있어야 합니다.  
  
`[ @new_name = ] 'new_name'` 컬렉션 집합의 새 이름입니다. *new_name* 는 **sysname**이며 사용 될 경우 빈 문자열일 수 없습니다. *new_name* 은 고유 해야 합니다. 현재 컬렉션 집합 이름의 목록을 보려면 syscollector_collection_sets 시스템 뷰를 쿼리합니다.  
  
`[ @target = ] 'target'` 나중에 사용 하도록 예약 되어 있습니다.  
  
`[ @collection_mode = ] collection_mode` 사용할 데이터 컬렉션의 유형입니다. *collection_mode* 은 **smallint** 이며 다음 값 중 하나를 사용할 수 있습니다.  
  
 0 - 캐시된 모드. 데이터 컬렉션과 업로드가 별도의 일정에 속해 있습니다. 연속 컬렉션을 위해 캐시된 모드를 지정합니다.  
  
 1 - 캐시되지 않은 모드. 데이터 컬렉션과 업로드가 같은 일정에 속해 있습니다. 임시 컬렉션이나 스냅샷 컬렉션을 위해 캐시되지 않은 모드를 지정합니다.  
  
 캐시 되지 않은 모드에서 캐시 된 모드 (0)로 변경 하는 경우 *schedule_uid* 또는 *schedule_name*도 지정 해야 합니다.  
  
`[ @days_until_expiration = ] days_until_expiration` 수집 된 데이터가 관리 데이터 웨어하우스에 저장 되는 일 수입니다. *days_until_expiration* 은 **smallint**입니다. *days_until_expiration* 는 0 또는 양의 정수 여야 합니다.  
  
`[ @proxy_id = ] proxy_id` 에이전트 프록시 계정의 고유 식별자입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *proxy_id* 은 **int**입니다.  
  
`[ @proxy_name = ] 'proxy_name'` 프록시의 이름입니다. *proxy_name* 는 **sysname** 이며 null을 허용 합니다.  
  
`[ @schedule_uid = ] 'schedule_uid'` 일정을 가리키는 GUID입니다. **uniqueidentifier** *schedule_uid* 입니다.  
  
 *Schedule_uid*를 얻으려면 sysschedules 시스템 테이블을 쿼리 합니다.  
  
 *Collection_mode* 를 0으로 설정 하면 *schedule_uid* 또는 *schedule_name* 를 지정 해야 합니다. *Collection_mode* 1로 설정 되 면 *schedule_uid* 또는 *schedule_name* 지정 된 경우 무시 됩니다.  
  
`[ @schedule_name = ] 'schedule_name'` 일정의 이름입니다. *schedule_name* 는 **sysname** 이며 null을 허용 합니다. 지정 하는 경우 *schedule_uid* 은 NULL 이어야 합니다. *Schedule_name*를 얻으려면 sysschedules 시스템 테이블을 쿼리 합니다.  
  
`[ @logging_level = ] logging_level` 로깅 수준입니다. *logging_level* 은 **smallint** 이며 다음 값 중 하나를 사용 합니다.  
  
 0 - 실행 정보 및 다음 항목을 추적하는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 이벤트 기록  
  
-   컬렉션 집합 시작/중지  
  
-   패키지 시작/중지  
  
-   오류 정보  
  
 1 - 수준 0 로깅 및 다음 항목  
  
-   실행 통계  
  
-   지속적으로 실행되는 컬렉션 프로세스  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)]의 경고 이벤트  
  
 2 - 수준 1 로깅 및 [!INCLUDE[ssIS](../../includes/ssis-md.md)]의 세부 이벤트 정보  
  
 *Logging_level* 의 기본값은 1입니다.  
  
`[ @description = ] 'description'` 컬렉션 집합에 대 한 설명입니다. *설명은* **nvarchar (4000)** 입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_syscollector_update_collection_set은 msdb 시스템 데이터베이스의 컨텍스트 내에서 실행되어야 합니다.  
  
 *Collection_set_id* 또는 *이름* 에는 값이 있어야 하며 둘 다 NULL 일 수 없습니다. 이러한 값을 확인하려면 syscollector_collection_sets 시스템 뷰를 쿼리합니다.  
  
 컬렉션 집합이 실행 되 고 있으면 *schedule_uid* 및 *설명*만 업데이트할 수 있습니다. 컬렉션 집합을 중지 하려면 [sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md)을 사용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행하려면 dc_admin 또는 dc_operator(EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버여야 합니다. dc_operator는 이 저장 프로시저를 실행할 수 있지만 이 역할의 멤버가 변경할 수 있는 속성은 제한적입니다. 다음 속성은 dc_admin만 변경할 수 있습니다.  
  
-   @new_name  
  
-   @target  
  
-   @proxy_id  
  
-   @description  
  
-   @collection_mode  
  
-   @days_until_expiration  
  
## <a name="examples"></a>예제  
  
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
  
### <a name="b-changing-the-collection-mode-from-non-cached-to-cached"></a>B. 컬렉션 모드를 캐시되지 않은 모드에서 캐시된 모드로 변경  
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
  
### <a name="c-changing-other-collection-set-parameters"></a>C. 다른 컬렉션 집합 매개 변수 변경  
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
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [Transact-sql&#41;syscollector_collection_sets &#40;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)   
 [ Transact-sql&#41;&#40;dbo.sys일정 ](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
