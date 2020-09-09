---
description: sys.sp_cdc_change_job(Transact-SQL)
title: sys. sp_cdc_change_job (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_change_job_TSQL
- sys.sp_cdc_change_job
- sp_cdc_change_job_TSQL
- sp_cdc_change_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_change_job
ms.assetid: ea918888-0fc5-4cc1-b301-26b2a9fbb20d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bf81cfb8cbd06602252e62b3c72bafe694c14ed8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545877"
---
# <a name="syssp_cdc_change_job-transact-sql"></a>sys.sp_cdc_change_job(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스의 변경 데이터 캡처 정리 또는 캡처 작업의 구성을 수정합니다. 작업의 현재 구성을 보려면 [dbo. cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) 테이블을 쿼리하거나 [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)를 사용 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_cdc_change_job [ [ @job_type = ] 'job_type' ]  
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ @threshold = ] 'delete threshold'  
```  
  
## <a name="arguments"></a>인수  
`[ @job_type = ] 'job_type'` 수정할 작업의 유형입니다. *job_type* 은 **nvarchar (20)** 이며 기본값은 ' capture '입니다. 올바른 입력 값은 'capture' 및 'cleanup'입니다.  
  
`[ @maxtrans ] = max_trans_` 각 검색 주기에서 처리할 최대 트랜잭션 수입니다. *max_trans* 은 **int** 이며 기본값은이 매개 변수에 대 한 변경 내용이 없음을 나타내는 NULL입니다. 지정된 경우 값은 양의 정수여야 합니다.  
  
 *max_trans* 는 캡처 작업에 대해서만 유효 합니다.  
  
`[ @maxscans ] = max_scans_` 로그에서 모든 행을 추출 하기 위해 실행할 최대 검색 주기 수입니다. *max_scans* 은 **int** 이며 기본값은이 매개 변수에 대 한 변경 내용이 없음을 나타내는 NULL입니다.  
  
 *max_scan* 는 캡처 작업에 대해서만 유효 합니다.  
  
`[ @continuous ] = continuous_` 캡처 작업을 계속 실행할지 (1), 아니면 한 번만 실행 (0) 할지를 나타냅니다. *연속* 은 **bit** 이며 기본값은이 매개 변수에 대 한 변경 내용이 없음을 나타내는 NULL입니다.  
  
 *연속* = 1 인 경우 [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) 작업은 로그를 검색 하 고 최대 (*max_trans* \* *max_scans*) 트랜잭션을 처리 합니다. 그런 다음, 다음 로그 검색을 시작 하기 전에 *polling_interval* 에 지정 된 시간 (초) 동안 대기 합니다.  
  
 *연속* = 0 인 경우 **sp_cdc_scan** 작업은 최대 *max_scans* 검색을 실행 하 여 각 검색 중에 *max_trans* 트랜잭션을 처리 한 다음 종료 됩니다.  
  
 ** \@ 연속** 이 1에서 0으로 변경 되 면 ** \@ pollinginterval** 가 자동으로 0으로 설정 됩니다. 0이 아닌 ** \@ pollinginterval** 에 대해 지정 된 값은 무시 됩니다.  
  
 ** \@ 연속** 이 생략 되거나 명시적으로 NULL로 설정 되 고 ** \@ pollinginterval** 가 0 보다 큰 값으로 명시적으로 설정 된 경우 ** \@ 연속** 은 자동으로 1로 설정 됩니다.  
  
 *연속* 은 캡처 작업에 대해서만 유효 합니다.  
  
`[ @pollinginterval ] = polling_interval_` 로그 검색 주기 사이의 시간 (초)입니다. *polling_interval* 는 **bigint** 이며 기본값은이 매개 변수에 대 한 변경 내용이 없음을 나타내는 NULL입니다.  
  
 *연속* 이 1로 설정 된 경우 *polling_interval* 는 캡처 작업에 대해서만 유효 합니다.  
  
`[ @retention ] = retention_` 변경 테이블에 변경 행이 보관 되는 시간 (분)입니다. *보존* 은 **bigint** 이며 기본값은이 매개 변수에 대 한 변경 내용이 없음을 나타내는 NULL입니다. 최대값은 52494800(100년)입니다. 지정된 경우 값은 양의 정수여야 합니다.  
  
 *보존* 은 정리 작업에 대해서만 유효 합니다.  
  
`[ @threshold = ] 'delete threshold'` 정리 시 단일 문을 사용 하 여 삭제할 수 있는 삭제 항목의 최대 수입니다. *delete 임계값* 은 **bigint** 이며 기본값은이 매개 변수에 대 한 변경 내용이 없음을 나타내는 NULL입니다. *delete 임계값* 은 정리 작업에 대해서만 유효 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 매개 변수가 생략 된 경우에는 [dbo. cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) 테이블의 연결 된 값이 업데이트 되지 않습니다. 명시적으로 NULL로 설정된 매개 변수는 매개 변수가 생략된 것으로 처리됩니다.  
  
 작업 유형에 잘못된 매개 변수를 지정할 경우 문이 실행되지 않습니다.  
  
 작업에 대 한 변경 내용은 [sp_cdc_stop_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md) 를 사용 하 여 중지 하 고 [sp_cdc_start_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md)를 사용 하 여 다시 시작할 때까지 적용 되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Db_owner** 고정 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-changing-a-capture-job"></a>A. 캡처 작업 변경  
 다음 예에서는 `@job_type` `@maxscans` `@maxtrans` 데이터베이스에서 캡처 작업의, 및 매개 변수를 업데이트 합니다 `AdventureWorks2012` . 캡처 작업에 대한 다른 유효한 매개 변수인 `@continuous`와 `@pollinginterval`은 생략되며 해당 값은 수정되지 않습니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'capture',  
    @maxscans = 1000,  
    @maxtrans = 15;  
GO  
```  
  
### <a name="b-changing-a-cleanup-job"></a>B. 정리 작업 변경  
 다음 예에서는 `AdventureWorks2012` 데이터베이스에서 정리 작업을 업데이트합니다. 이 작업 유형에 대 한 모든 유효한 매개 변수 ( ** \@ 임계값**제외)가 지정 됩니다. ** \@ Threshold** 값은 수정 되지 않습니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'cleanup',  
    @retention = 2880;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [cdc_jobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sp_cdc_enable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_add_job&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
