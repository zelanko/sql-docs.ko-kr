---
title: sys.sp_cdc_add_job (Transact SQL) | Microsoft Docs
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
- sp_cdc_add_job_TSQL
- sys.sp_cdc_add_job
- sys.sp_cdc_add_job_TSQL
- sp_cdc_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_add_job
ms.assetid: c4458738-ed25-40a6-8294-a26ca5a05bd9
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 58f17196962c2ca05ebf1c2e56ce78621dbb9ac7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysspcdcaddjob-transact-sql"></a>sys.sp_cdc_add_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 변경 데이터 캡처 정리 또는 캡처 작업을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_cdc_add_job [ @job_type = ] 'job_type'  
    [ , [ @start_job = ] start_job ]   
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ , [ @threshold ] = 'delete_threshold' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@job_type=** ] **'***job_type***'**  
 추가할 작업 유형입니다. *job_type* 은 **nvarchar (20)** NULL 일 수 없습니다. 유효한 입력은 **'캡처'** 및 **'정리'**합니다.  
  
 [  **@start_job=** ] *start_job*  
 작업이 추가된 후 바로 시작되어야 하는지 여부를 나타내는 플래그입니다. *start_job* 은 **비트** 기본값은 1입니다.  
  
 [ **@maxtrans** ] = *max_trans*  
 각 검색 주기에서 처리할 최대 트랜잭션 수입니다. *max_trans* 은 **int** 기본값은 500입니다. 지정된 경우 값은 양의 정수여야 합니다.  
  
 *max_trans* 캡처 작업에 대해서만 유효 합니다.  
  
 [ **@maxscans** ] **= * * * max_scans*  
 로그에서 모든 행을 추출하기 위해 실행할 최대 검색 주기 수입니다. *max_scans* 은 **int** 기본값은 10입니다.  
  
 *max_scan* 캡처 작업에 대해서만 유효 합니다.  
  
 [ **@continuous** ] **= * * * 연속*  
 캡처 작업을 계속 실행(1)할지, 아니면 한 번만 실행(0)할지를 나타냅니다. *연속* 은 **비트** 기본값은 1입니다.  
  
 때 *연속* = 1는 [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) 작업의 로그를 검색 하 고 최대 처리 (*max_trans* \* *max_scans*) 트랜잭션입니다. 수에 지정 된 시간 (초) 동안 기다린 후 *polling_interval* 다음 로그 검색을 시작 하기 전에.  
  
 때 *연속* = 0는 **sp_cdc_scan** 작업이 최대 실행 *max_scans* 최대 처리 로그 스캔 *max_trans* 트랜잭션 동안 하며 각 검색 한 다음 종료 됩니다.  
  
 *연속* 캡처 작업에 대해서만 유효 합니다.  
  
 [ **@pollinginterval** ] **= * * * polling_interval*  
 로그 검색 주기 사이의 시간(초)입니다. *polling_interval* 은 **bigint** 기본값은 5입니다.  
  
 *polling_interval* 캡처에만 유효 되었을 때 작업 *연속* 1로 설정 됩니다. 지정된 경우 값은 음수가 아니어야 하고 24시간을 초과할 수 없습니다. 값 0이 지정된 경우 로그 검색 간에 대기 시간이 없습니다.  
  
 [ **@retention** ] **= * * * 보존*  
 변경 테이블에 변경 데이터 행이 보관되는 시간(분)입니다. *보존* 은 **bigint** 기본값은 4320 (72 시간). 최대값은 52494800(100년)입니다. 지정된 경우 값은 양의 정수여야 합니다.  
  
 *보존* 정리 작업에 대해서만 유효 합니다.  
  
 [  **@threshold =** ] **'***delete_threshold***'**  
 정리 시 단일 문을 사용하여 삭제할 수 있는 삭제 항목의 최대 수입니다. *delete_threshold* 은 **bigint** 기본값은 5000입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 정리 작업은 데이터베이스의 첫 번째 테이블에 변경 데이터 캡처가 활성화된 경우 기본값을 사용하여 만들어집니다. 캡처 작업은 데이터베이스의 첫 번째 테이블에 변경 데이터 캡처가 활성화되고 데이터베이스에 대한 트랜잭션 게시가 없는 경우 기본값을 사용하여 만들어집니다. 트랜잭션 게시가 있는 경우 트랜잭션 로그 판독기를 사용하여 캡처 메커니즘을 구동하므로 별개의 캡처 작업이 필요 없고 허용되지도 않습니다.  
  
 정리 및 캡처 작업은 기본적으로 만들어지므로 이 저장 프로시저는 작업이 명시적으로 삭제되어 다시 만들어야 하는 경우에만 필요합니다.  
  
 작업 이름은 **cdc. ***< s e _ >***_cleanup으로 지정** 또는 **cdc. ***< s e _ >***_capture**여기서 *< s e _ >* 현재 데이터베이스의 이름입니다. 마침표로 이름이 추가 됩니다에 동일한 이름 가진 작업이 이미 존재 하는 경우 (**.**) 뒤에 고유 식별자가 경우가: **cdc. AdventureWorks_capture 합니다. A1ACBDED-13FC-428C-8302-10100EF74F52**합니다.  
  
 사용 하 여 정리 또는 캡처 작업의 현재 구성을 보려면 [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)합니다. 작업의 구성을 변경 하려면 [하면 sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **db_owner** 고정된 데이터베이스 역할입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-capture-job"></a>1. 캡처 작업 만들기  
 다음 예에서는 캡처 작업을 만듭니다. 이 예에서는 기존 정리 작업이 명시적으로 삭제되어 다시 만들어야 한다고 가정합니다. 작업은 기본값을 사용하여 만들어집니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job @job_type = N'capture';  
GO  
```  
  
### <a name="b-creating-a-cleanup-job"></a>2. 정리 작업 만들기  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 정리 작업을 만듭니다. 매개 변수 `@start_job`은 0으로, `@retention`은 5760분(96시간)으로 설정됩니다. 이 예에서는 기존 정리 작업이 명시적으로 삭제되어 다시 만들어야 한다고 가정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job  
     @job_type = N'cleanup'  
    ,@start_job = 0  
    ,@retention = 5760;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [dbo.cdc_jobs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [변경 데이터 캡처 정보&#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
