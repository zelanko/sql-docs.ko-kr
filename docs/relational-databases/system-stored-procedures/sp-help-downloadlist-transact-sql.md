---
title: sp_help_downloadlist (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_downloadlist_TSQL
- sp_help_downloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_downloadlist
ms.assetid: 745b265b-86e8-4399-b928-c6969ca1a2c8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9dd52e6d2e4bf8a1a099ea2391a2c6ce2d6decdc
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827727"
---
# <a name="sp_help_downloadlist-transact-sql"></a>sp_help_downloadlist(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  제공 된 작업에 대 한 **sysdownloadlist** 시스템 테이블의 모든 행 또는 작업이 지정 되지 않은 경우 모든 행을 나열 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_downloadlist { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }   
     [ , [ @operation = ] 'operation' ]   
     [ , [ @object_type = ] 'object_type' ]   
     [ , [ @object_name = ] 'object_name' ]   
     [ , [ @target_server = ] 'target_server' ]   
     [ , [ @has_error = ] has_error ]   
     [ , [ @status = ] status ]   
     [ , [ @date_posted = ] date_posted ]  
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] job_id`정보를 반환할 작업 id입니다. *job_id* 은 **uniqueidentifier**이며 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'`작업의 이름입니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다.  
  
`[ @operation = ] 'operation'`지정 된 작업에 대 한 유효한 작업입니다. *연산은* **varchar (64)** 이며 기본값은 NULL이 고 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**제거**|마스터 **SQLServerAgent** 서비스에서 오류를 제거 하도록 대상 서버를 요청 하는 서버 작업입니다.|  
|**DELETE**|전체 작업을 제거하는 작업의 수행입니다.|  
|**INSERT**|전체 작업을 추가하거나 기존 작업을 새로 고치는 작업의 수행입니다. 여기에는 적용되는 모든 작업 단계 및 일정이 포함됩니다.|  
|**RE-ENLIST**|서버 작업이 대상 서버로 하여금 폴링 간격 및 다중 서버 도메인에 대한 표준 시간대를 포함하여 포함 정보를 다시 전달하도록 합니다. 또한 대상 서버는 **MSXOperator** 세부 정보를 다시 다운로드 합니다.|  
|**SET-POLL**|대상 서버가 다중 서버 도메인을 폴링하는 간격(초)을 설정하는 서버 작업입니다. 지정 된 경우 *값* 은 필수 간격 값으로 해석 되 고 **10** 에서 **28800**사이의 값이 될 수 있습니다.|  
|**시작**|작업 실행 시작을 요청하는 작업의 수행입니다.|  
|**막을**|작업 실행 중지를 요청하는 작업의 수행입니다.|  
|**SYNC-TIME**|대상 서버로 하여금 시스템 시계와 다중 서버 도메인을 동기화하도록 하는 서버 작업입니다. 이 작업은 비용이 많이 필요하므로 자주 실행하지 않고 제한적으로 실행합니다.|  
|**UPDATE**|작업 단계 나 일정이 아닌 작업에 대 한 **sysjobs** 정보만 업데이트 하는 작업 작업입니다. 는 **sp_update_job**에 의해 자동으로 호출 됩니다.|  
  
`[ @object_type = ] 'object_type'`지정 된 작업에 대 한 개체의 유형입니다. *object_type* 는 **varchar (64)** 이며 기본값은 NULL입니다. *object_type* 은 작업 또는 서버 중 하나일 수 있습니다. 유효한 *object_type*값에 대 한 자세한 내용은 [sp_add_category &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)를 참조 하세요.  
  
`[ @object_name = ] 'object_name'`개체의 이름입니다. *object_name* 는 **sysname**이며 기본값은 NULL입니다. *OBJECT_TYPE* 작업 인 경우 *object_name*은 작업 이름입니다. 서버 *object_type*인 경우 *object_name*서버 이름입니다.  
  
`[ @target_server = ] 'target_server'`대상 서버의 이름입니다. *target_server* 은 **nvarchar (128)** 이며 기본값은 NULL입니다.  
  
`[ @has_error = ] has_error`작업이 오류를 승인 해야 하는지 여부입니다. *has_error* 은 **tinyint**이며 기본값은 오류를 인정 하지 않아야 함을 나타내는 NULL입니다. **1** 은 모든 오류를 승인 해야 함을 나타냅니다.  
  
`[ @status = ] status`작업의 상태입니다. *status* 는 **tinyint**이며 기본값은 NULL입니다.  
  
`[ @date_posted = ] date_posted`지정 된 날짜 및 시간 이후의 모든 항목을 결과 집합에 포함 해야 하는 날짜와 시간입니다. *date_posted* 은 **datetime**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|명령의 고유한 정수 ID입니다.|  
|**source_server**|**nvarchar(30)**|명령을 발생시킨 서버의 컴퓨터 이름입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 7.0에서이는 항상 마스터 (MSX) 서버의 컴퓨터 이름입니다.|  
|**operation_code**|**nvarchar(4000)**|명령의 작업 코드입니다.|  
|**object_name**|**sysname**|명령이 적용되는 개체입니다.|  
|**object_id**|**uniqueidentifier**|명령의 영향을 받는 개체의 id 번호 (작업 개체에 대 한**job_id** 또는 서버 개체의 경우 0x00) 또는 **operation_code**특정 한 데이터 값입니다.|  
|**target_server**|**nvarchar(30)**|해당 명령이 다운로드될 대상 서버입니다.|  
|**error_message**|**nvarchar(1024)**|명령을 처리하는 동안 문제가 발생하는 경우 대상 서버에서 발행되는 오류 메시지입니다.<br /><br /> 참고: 모든 오류 메시지는 대상 서버에의 한 모든 추가 다운로드를 차단 합니다.|  
|**date_posted**|**datetime**|명령이 테이블에 게시된 날짜입니다.|  
|**date_downloaded**|**datetime**|대상 서버가 명령을 다운로드한 날짜입니다.|  
|**status**|**tinyint**|작업의 상태입니다.<br /><br /> **0** = 아직 다운로드 되지 않음<br /><br /> **1** = 성공적으로 다운로드 되었습니다.|  
  
## <a name="permissions"></a>권한  
 이 프로시저를 실행할 수 있는 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `sysdownloadlist` 작업에 대한 행을 `NightlyBackups`에 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_downloadlist  
    @job_name = N'NightlyBackups',  
    @operation = N'UPDATE',   
    @object_type = N'JOB',   
    @object_name = N'NightlyBackups',  
    @target_server = N'SEATTLE2',   
    @has_error = 1,   
    @status = NULL,   
    @date_posted = NULL ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
