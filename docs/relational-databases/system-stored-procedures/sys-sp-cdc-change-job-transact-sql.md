---
title: sys.sp_cdc_change_job (Transact SQL) | Microsoft Docs
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
- sys.sp_cdc_change_job_TSQL
- sys.sp_cdc_change_job
- sp_cdc_change_job_TSQL
- sp_cdc_change_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_change_job
ms.assetid: ea918888-0fc5-4cc1-b301-26b2a9fbb20d
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4878eeca70732ed5a7ab19e220eac60260e71ee9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysspcdcchangejob-transact-sql"></a>sys.sp_cdc_change_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 변경 데이터 캡처 정리 또는 캡처 작업의 구성을 수정합니다. 작업의 현재 구성을 쿼리는 [dbo.cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) 테이블을 쿼리하거나 [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@job_type=** ] **'***job_type***'**  
 수정할 작업 유형입니다. *job_type* 은 **nvarchar (20)** '캡처'의 기본값입니다. 올바른 입력 값은 'capture' 및 'cleanup'입니다.  
  
 [ **@maxtrans** ] **= * * * max_trans*  
 각 검색 주기에서 처리할 최대 트랜잭션 수입니다. *max_trans* 은 **int** 기본값 NULL이 매개이 변수에 대 한 변경 되지 않습니다 나타냅니다. 지정된 경우 값은 양의 정수여야 합니다.  
  
 *max_trans* 캡처 작업에 대해서만 유효 합니다.  
  
 [ **@maxscans** ] **= * * * max_scans*  
 로그에서 모든 행을 추출하기 위해 실행할 최대 검색 주기 수입니다. *max_scans* 은 **int** 기본값 NULL이 매개이 변수에 대 한 변경 되지 않습니다 나타냅니다.  
  
 *max_scan* 캡처 작업에 대해서만 유효 합니다.  
  
 [ **@continuous** ] **= * * * 연속*  
 캡처 작업을 계속 실행(1)할지, 아니면 한 번만 실행(0)할지를 나타냅니다. *연속* 은 **비트** 기본값 NULL이 매개이 변수에 대 한 변경 되지 않습니다 나타냅니다.  
  
 때 *연속* = 1는 [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) 작업의 로그를 검색 하 고 최대 처리 (*max_trans* \* *max_scans*) 트랜잭션입니다. 수에 지정 된 시간 (초) 동안 기다린 후 *polling_interval* 다음 로그 검색을 시작 하기 전에.  
  
 때 *연속* = 0는 **sp_cdc_scan** 작업이 최대 실행 *max_scans* 최대 처리 로그 스캔 *max_trans* 트랜잭션 동안 하며 각 검색 한 다음 종료 됩니다.  
  
 경우 **@continuous** 1에서 0으로 변경 **@pollinginterval** 자동으로 0으로 설정 됩니다. 값이 지정 **@pollinginterval** 제외 0은 무시 됩니다.  
  
 경우 **@continuous** 생략 되거나 NULL로 명시적으로 설정 하 고 **@pollinginterval** 명시적으로 값으로 설정 됩니다는 0 보다 큰 **@continuous** 자동으로 1로 설정 합니다.  
  
 *연속* 캡처 작업에 대해서만 유효 합니다.  
  
 [ **@pollinginterval** ] **= * * * polling_interval*  
 로그 검색 주기 사이의 시간(초)입니다. *polling_interval* 은 **bigint** 기본값 NULL이 매개이 변수에 대 한 변경 되지 않습니다 나타냅니다.  
  
 *polling_interval* 캡처에만 유효 되었을 때 작업 *연속* 1로 설정 됩니다.  
  
 [ **@retention** ] **= * * * 보존*  
 변경 테이블에 변경 행이 보관되는 시간(분)입니다. *보존* 은 **bigint** 기본값 NULL이 매개이 변수에 대 한 변경 되지 않습니다 나타냅니다. 최대값은 52494800(100년)입니다. 지정된 경우 값은 양의 정수여야 합니다.  
  
 *보존* 정리 작업에 대해서만 유효 합니다.  
  
 [  **@threshold=** ] **'***삭제 임계값***'**  
 정리 시 단일 문을 사용하여 삭제할 수 있는 삭제 항목의 최대 수입니다. *임계값을 삭제* 은 **bigint** 기본값 NULL이 매개이 변수에 대 한 변경 되지 않습니다 나타냅니다. *임계값을 삭제* 정리 작업에 대해서만 유효 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 매개 변수를 생략 하면 연결 된 값에는 [dbo.cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) 테이블이 업데이트 되지 않습니다. 명시적으로 NULL로 설정된 매개 변수는 매개 변수가 생략된 것으로 처리됩니다.  
  
 작업 유형에 잘못된 매개 변수를 지정할 경우 문이 실행되지 않습니다.  
  
 사용 하 여 작업이 중지 될 때까지 작업에 대 한 변경 내용이 적용 되지 않는 [sp_cdc_stop_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md) 를 사용 하 여 다시 시작 하 고 [sp_cdc_start_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **db_owner** 고정된 데이터베이스 역할입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-a-capture-job"></a>1. 캡처 작업 변경  
 다음 예에서는 업데이트 된 `@job_type`, `@maxscans`, 및 `@maxtrans` 에서 캡처 작업의 매개 변수는 `AdventureWorks2012` 데이터베이스입니다. 캡처 작업에 대한 다른 유효한 매개 변수인 `@continuous`와 `@pollinginterval`은 생략되며 해당 값은 수정되지 않습니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'capture',  
    @maxscans = 1000,  
    @maxtrans = 15;  
GO  
```  
  
### <a name="b-changing-a-cleanup-job"></a>2. 정리 작업 변경  
 다음 예에서는 `AdventureWorks2012` 데이터베이스에서 정리 작업을 업데이트합니다. 제외 하 고이 대 한 유효한 모든 매개 변수 작업 유형을 **@threshold**를 지정 합니다. 값 **@threshold** 수정 되지 않습니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'cleanup',  
    @retention = 2880;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [dbo.cdc_jobs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_add_job& #40; Transact SQL & #41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
