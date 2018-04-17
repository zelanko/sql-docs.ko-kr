---
title: sp_syscollector_create_collection_set (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collection_set_TSQL
- sp_syscollector_create_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_create_collection_set
ms.assetid: 69e9ff0f-c409-43fc-89f6-40c3974e972c
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e2aa88ff030e3fb938fdd00808d10c3c8b6cac9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="spsyscollectorcreatecollectionset-transact-sql"></a>sp_syscollector_create_collection_set(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  새 컬렉션 집합을 만듭니다. 이 저장 프로시저를 사용하여 데이터 컬렉션용 사용자 지정 컬렉션 집합을 만들 수 있습니다.  
  
> [!WARNING]  
>  프록시로 구성된 Windows 계정이 아직 로그인하지 않은 비대화형 또는 대화형 사용자인 경우 프로필 디렉터리가 존재하지 않으며 준비 디렉터리 만들기가 실패합니다. 따라서 도메인 컨트롤러의 프록시 계정을 사용하는 경우 프로필 디렉터리가 만들어지도록 적어도 한 번은 사용된 대화형 계정을 지정해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_create_collection_set   
      [ @name = ] 'name'  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    , [ [ @schedule_uid = ] 'schedule_uid' ]  
    , [ [ @schedule_name = ] 'schedule_name' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
    , [ @collection_set_id = ] collection_set_id OUTPUT   
    , [ [ @collection_set_uid = ] 'collection_set_uid' OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@name =** ] '*이름*'  
 컬렉션 집합의 이름입니다. *이름* 은 **sysname** 이며 빈 문자열 이거나 NULL 일 수 없습니다.  
  
 *이름* 고유 해야 합니다. 현재 컬렉션 집합 이름의 목록을 보려면 syscollector_collection_sets 시스템 뷰를 쿼리합니다.  
  
 [  **@target =** ] '*대상*'  
 나중에 사용하도록 예약되어 있습니다. *이름* 은 **nvarchar (128)** 이며 기본값은 NULL입니다.  
  
 [  **@collection_mode =** ] *collection_mode*  
 데이터를 수집하고 저장하는 방식을 지정합니다. *collection_mode* 은 **smallint** 다음 값 중 하나일 수 있습니다.  
  
 0 - 캐시된 모드. 데이터 컬렉션과 업로드가 별도의 일정에 속해 있습니다. 연속 컬렉션을 위해 캐시된 모드를 지정합니다.  
  
 1 - 캐시되지 않은 모드. 데이터 컬렉션과 업로드가 같은 일정에 속해 있습니다. 임시 컬렉션이나 스냅숏 컬렉션을 위해 캐시되지 않은 모드를 지정합니다.  
  
 에 대 한 기본값 *collection_mode* 은 0입니다. 때 *collection_mode* 은 0으로, *schedule_uid* 또는 *schedule_name* 지정 해야 합니다.  
  
 [  **@days_until_expiration =** ] *days_until_expiration*  
 수집된 데이터가 관리 데이터 웨어하우스에 저장되는 일 수입니다. *days_until_expiration* 은 **smallint** 기본값은 730 (2 년)입니다. *days_until_expiration* 0 또는 양의 정수 여야 합니다.  
  
 [ **@proxy_id =** ] *proxy_id*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정의 고유 식별자입니다. *proxy_id* 은 **int** 이며 기본값은 NULL입니다. 를 지정 하는 경우 *proxy_name* NULL 이어야 합니다. 얻으려고 *proxy_id*, sysproxies 시스템 테이블을 쿼리 합니다. dc_admin 고정 데이터베이스 역할에는 프록시에 액세스할 권한이 있어야 합니다. 자세한 내용은 참조 [SQL Server 에이전트 프록시 만들기](http://msdn.microsoft.com/library/142e0c55-a8b9-4669-be49-b9dc602d5988)합니다.  
  
 [ **@proxy_name =** ] '*proxy_name*'  
 프록시 계정의 이름입니다. *proxy_name* 은 **sysname** 이며 기본값은 NULL입니다. 를 지정 하는 경우 *proxy_id* NULL 이어야 합니다. 얻으려고 *proxy_name*, sysproxies 시스템 테이블을 쿼리 합니다.  
  
 [  **@schedule_uid =** ] '*schedule_uid*'  
 일정을 가리키는 GUID입니다. *schedule_uid* 은 **uniqueidentifier** 이며 기본값은 NULL입니다. 를 지정 하는 경우 *schedule_name* NULL 이어야 합니다. 얻으려고 *schedule_uid*, sysschedules 시스템 테이블을 쿼리 합니다.  
  
 때 *collection_mode* 0으로 설정 *schedule_uid* 또는 *schedule_name* 지정 해야 합니다. 때 *collection_mode* 1로 설정 되어 *schedule_uid* 또는 *schedule_name* 지정 해도 무시 됩니다.  
  
 [  **@schedule_name =** ] '*schedule_name*'  
 일정의 이름입니다. *schedule_name* 은 **sysname** 이며 기본값은 NULL입니다. 를 지정 하는 경우 *schedule_uid* NULL 이어야 합니다. 얻으려고 *schedule_name*, sysschedules 시스템 테이블을 쿼리 합니다.  
  
 [  **@logging_level =** ] *logging_level*  
 로깅 수준입니다. *logging_level* 은 **smallint** 다음 값 중 하나를 사용 합니다.  
  
 0 - 실행 정보 및 다음 항목을 추적하는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 이벤트 기록  
  
-   컬렉션 집합 시작/중지  
  
-   패키지 시작/중지  
  
-   오류 정보  
  
 1 - 수준 0 로깅 및 다음 항목  
  
-   실행 통계  
  
-   지속적으로 실행되는 컬렉션 프로세스  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)]의 경고 이벤트  
  
 2 - 수준 1 로깅 및 [!INCLUDE[ssIS](../../includes/ssis-md.md)]의 세부 이벤트 정보  
  
 에 대 한 기본값 *logging_level* 는 1입니다.  
  
 [  **@description =** ] '*설명*'  
 컬렉션 집합에 대한 설명입니다. *설명* 은 **nvarchar (4000)** 이며 기본값은 NULL입니다.  
  
 [ **@collection_set_id =** ] *collection_set_id*  
 컬렉션 집합의 고유한 로컬 식별자입니다. *collection_set_id* 은 **int** 출력을 제공 하며 필요 합니다.  
  
 [  **@collection_set_uid =** ] '*collection_set_uid*'  
 컬렉션 집합의 GUID입니다. *collection_set_uid* 은 **uniqueidentifier** 이며 기본값은 NULL 출력을 제공 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 sp_syscollector_create_collection_set은 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
## <a name="permissions"></a>Permissions  
 이 프로시저를 실행하려면 dc_admin(EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-collection-set-by-using-default-values"></a>1. 기본값을 사용하여 컬렉션 집합 만들기  
 다음 예에서는 필수 매개 변수만 지정하여 컬렉션 집합을 만듭니다. `@collection_mode`는 필수 사항은 아니지만 기본 컬렉션 모드(캐시된 모드)를 사용하려면 일정 ID 또는 일정 이름을 지정해야 합니다.  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
EXECUTE dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 1',  
    @description = N'This is a test collection set that runs in non-cached mode.',  
    @collection_mode = 1,  
    @collection_set_id = @collection_set_id OUTPUT;  
GO  
```  
  
### <a name="b-creating-a-collection-set-by-using-specified-values"></a>2. 지정된 값을 사용하여 컬렉션 집합 만들기  
 다음 예에서는 여러 매개 변수에 값을 지정하는 방식으로 컬렉션 집합을 만듭니다.  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier;  
SET @collection_set_uid = NEWID();  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 2',  
    @collection_mode = 0,  
    @days_until_expiration = 365,  
    @description = N'This is a test collection set that runs in cached mode.',  
    @logging_level = 2,  
    @schedule_name = N'CollectorSchedule_Every_30min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [일반 T-SQL 쿼리 수집기 유형을 사용하는 사용자 지정 컬렉션 집합 만들기&#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_collection_sets&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
