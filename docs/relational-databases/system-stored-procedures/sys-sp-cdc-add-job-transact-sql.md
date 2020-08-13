---
title: sys. sp_cdc_add_job (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 53bc390e3e95ac49554826ad6ed96b8c4138ca10
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88172902"
---
# <a name="syssp_cdc_add_job-transact-sql"></a>sys.sp_cdc_add_job(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스의 변경 데이터 캡처 정리 또는 캡처 작업을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @job_type = ] 'job\_type'`추가할 작업 유형입니다. *job_type* 은 **nvarchar (20)** 이며 NULL 일 수 없습니다. 유효한 입력은 **' capture '** 및 **' cleanup '** 입니다.  
  
`[ @start_job = ] start_job`작업을 추가한 직후에 작업을 시작할지 여부를 나타내는 플래그입니다. *start_job* 은 **bit** 이며 기본값은 1입니다.  
  
`[ @maxtrans ] = max_trans`각 검색 주기에서 처리할 최대 트랜잭션 수입니다. *max_trans* 는 **int** 이며 기본값은 500입니다. 지정된 경우 값은 양의 정수여야 합니다.  
  
 *max_trans* 는 캡처 작업에 대해서만 유효 합니다.  
  
`[ @maxscans ] = max\_scans_`로그에서 모든 행을 추출 하기 위해 실행할 최대 검색 주기 수입니다. *max_scans* 은 **int** 이며 기본값은 10입니다.  
  
 *max_scan* 는 캡처 작업에 대해서만 유효 합니다.  
  
`[ @continuous ] = continuous_`캡처 작업을 계속 실행할지 (1), 아니면 한 번만 실행 (0) 할지를 나타냅니다. *연속* 은 **bit** 이며 기본값은 1입니다.  
  
 *연속* = 1 인 경우 [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) 작업은 로그를 검색 하 고 최대 (*max_trans* \* *max_scans*) 트랜잭션을 처리 합니다. 그런 다음, 다음 로그 검색을 시작 하기 전에 *polling_interval* 에 지정 된 시간 (초) 동안 대기 합니다.  
  
 *연속* = 0 인 경우 **sp_cdc_scan** 작업은 최대 *max_scans* 검색을 실행 하 고 각 검색 중에 *max_trans* 트랜잭션을 처리 한 다음 종료 됩니다.  
  
 *연속* 은 캡처 작업에 대해서만 유효 합니다.  
  
`[ @pollinginterval ] = polling\_interval_`로그 검색 주기 사이의 시간 (초)입니다. *polling_interval* 는 **bigint** 이며 기본값은 5입니다.  
  
 *연속* 이 1로 설정 된 경우 *polling_interval* 는 캡처 작업에 대해서만 유효 합니다. 지정 된 경우 값은 0 보다 크거나 같고 24 시간 (최대: 86399 초) 보다 작아야 합니다. 값 0이 지정된 경우 로그 검색 간에 대기 시간이 없습니다.  
  
`[ @retention ] = retention_`변경 테이블에 변경 데이터 행이 보관 되는 시간 (분)입니다. *보존* 은 **bigint** 이며 기본값은 4320 (72 시간)입니다. 최대값은 52494800(100년)입니다. 지정된 경우 값은 양의 정수여야 합니다.  
  
 *보존* 은 정리 작업에 대해서만 유효 합니다.  
  
`[ @threshold = ] 'delete\_threshold'`정리 시 단일 문을 사용 하 여 삭제할 수 있는 삭제 항목의 최대 수입니다. *delete_threshold* 는 **bigint** 이며 기본값은 5000입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 정리 작업은 데이터베이스의 첫 번째 테이블에 변경 데이터 캡처가 활성화된 경우 기본값을 사용하여 만들어집니다. 캡처 작업은 데이터베이스의 첫 번째 테이블에 변경 데이터 캡처가 활성화되고 데이터베이스에 대한 트랜잭션 게시가 없는 경우 기본값을 사용하여 만들어집니다. 트랜잭션 게시가 있는 경우 트랜잭션 로그 판독기를 사용하여 캡처 메커니즘을 구동하므로 별개의 캡처 작업이 필요 없고 허용되지도 않습니다.  
  
 정리 및 캡처 작업은 기본적으로 만들어지므로 이 저장 프로시저는 작업이 명시적으로 삭제되어 다시 만들어야 하는 경우에만 필요합니다.  
  
 작업 이름이 **cdc입니다.** _\<database\_name\>_ ** \_ 정리** 또는 **cdc.** _\<database\_name\>_ ** \_ capture**, 여기서 *<database_name>* 는 현재 데이터베이스의 이름입니다. 이름이 같은 작업이 이미 있으면 이름에 마침표 (**.**)와 고유 식별자 (예: cdc)가 추가 됩니다. ** AdventureWorks_capture. A1ACBDED-13FC-428C-8302-10100EF74F52)**.  
  
 정리 또는 캡처 작업의 현재 구성을 보려면 [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)를 사용 합니다. 작업의 구성을 변경 하려면 [sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)을 사용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Db_owner** 고정 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-capture-job"></a>A. 캡처 작업 만들기  
 다음 예에서는 캡처 작업을 만듭니다. 이 예에서는 기존 정리 작업이 명시적으로 삭제되어 다시 만들어야 한다고 가정합니다. 작업은 기본값을 사용하여 만들어집니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job @job_type = N'capture';  
GO  
```  
  
### <a name="b-creating-a-cleanup-job"></a>B. 정리 작업 만들기  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 정리 작업을 만듭니다. 매개 변수 `@start_job`은 0으로, `@retention`은 5760분(96시간)으로 설정됩니다. 이 예에서는 기존 정리 작업이 명시적으로 삭제되어 다시 만들어야 한다고 가정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job  
     @job_type = N'cleanup'  
    ,@start_job = 0  
    ,@retention = 5760;  
```  
  
## <a name="see-also"></a>참고 항목  
 [cdc_jobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sp_cdc_enable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [변경 데이터 캡처 정보&#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
