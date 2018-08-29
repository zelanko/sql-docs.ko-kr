---
title: sys.sp_cdc_change_job (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7603f20095fa09bfcd574aeea1bcad5ca357cd40
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43018069"
---
# <a name="sysspcdcchangejob-transact-sql"></a>sys.sp_cdc_change_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 변경 데이터 캡처 정리 또는 캡처 작업의 구성을 수정합니다. 쿼리 작업의 현재 구성을 보려면 합니다 [dbo.cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) 테이블을 쿼리하거나 [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)합니다.  
  
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
 수정할 작업 유형입니다. *job_type* 됩니다 **nvarchar(20)** 이며 기본값은 '캡처' 합니다. 올바른 입력 값은 'capture' 및 'cleanup'입니다.  
  
 [ **@maxtrans** ] **= * max_trans*  
 각 검색 주기에서 처리할 최대 트랜잭션 수입니다. *max_trans* 됩니다 **int** 변하지가 매개이 변수에 대 한 기본값은 NULL 사용 하 여 나타냅니다. 지정된 경우 값은 양의 정수여야 합니다.  
  
 *max_trans* 캡처 작업에 대해서만 유효 합니다.  
  
 [ **@maxscans** ] **= * max_scans*  
 로그에서 모든 행을 추출하기 위해 실행할 최대 검색 주기 수입니다. *max_scans* 됩니다 **int** 변하지가 매개이 변수에 대 한 기본값은 NULL 사용 하 여 나타냅니다.  
  
 *max_scan* 캡처 작업에 대해서만 유효 합니다.  
  
 [ **@continuous** ] **= * 연속*  
 캡처 작업을 계속 실행(1)할지, 아니면 한 번만 실행(0)할지를 나타냅니다. *지속적인* 됩니다 **비트** 변하지가 매개이 변수에 대 한 기본값은 NULL 사용 하 여 나타냅니다.  
  
 때 *지속적인* = 1, 합니다 [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) 작업 로그를 검색 하 고 최대 처리 (*max_trans* \* *max_scans*) 트랜잭션입니다. 에 지정 된 초 기다립니다 *polling_interval* 다음 로그 검색을 시작 하기 전에 합니다.  
  
 때 *지속적인* = 0, 합니다 **sp_cdc_scan** 작업이 최대 실행 *max_scans* 최대 처리 로그를 검색 *max_trans* 트랜잭션 각 하며 검색 중 다음 종료 합니다.  
  
 하는 경우 **@continuous** 1에서 0으로 변경 되었을 **@pollinginterval** 자동으로 0으로 설정 됩니다. 값이 지정 **@pollinginterval** 외 0은 무시 됩니다.  
  
 하는 경우 **@continuous** 생략 되거나 NULL로 명시적으로 설정 하 고 **@pollinginterval** 명시적으로 설정할지를 값으로 0 보다 큰 **@continuous** 자동으로 1로 설정 합니다.  
  
 *연속* 캡처 작업에 대해서만 유효 합니다.  
  
 [ **@pollinginterval** ] **= * polling_interval*  
 로그 검색 주기 사이의 시간(초)입니다. *polling_interval* 됩니다 **bigint** 변하지가 매개이 변수에 대 한 기본값은 NULL 사용 하 여 나타냅니다.  
  
 *polling_interval* 는 캡처에만 사용할 경우 작업을 *연속* 1로 설정 됩니다.  
  
 [ **@retention** ] **= * 보존*  
 변경 테이블에 변경 행이 보관되는 시간(분)입니다. *보존* 됩니다 **bigint** 변하지가 매개이 변수에 대 한 기본값은 NULL 사용 하 여 나타냅니다. 최대값은 52494800(100년)입니다. 지정된 경우 값은 양의 정수여야 합니다.  
  
 *보존* 정리 작업에 대해서만 유효 합니다.  
  
 [  **@threshold=** ] **'***delete***'**  
 정리 시 단일 문을 사용하여 삭제할 수 있는 삭제 항목의 최대 수입니다. *임계값을 삭제* 됩니다 **bigint** 변하지가 매개이 변수에 대 한 기본값은 NULL 사용 하 여 나타냅니다. *delete* 정리 작업에 대해서만 유효 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 매개 변수를 생략 하면의 관련된 값을 [dbo.cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) 테이블이 업데이트 되지 않습니다. 명시적으로 NULL로 설정된 매개 변수는 매개 변수가 생략된 것으로 처리됩니다.  
  
 작업 유형에 잘못된 매개 변수를 지정할 경우 문이 실행되지 않습니다.  
  
 사용 하 여 작업이 중지 될 때까지 작업에 대 한 변경 내용이 적용 되지 않습니다 [sp_cdc_stop_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md) 사용 하 여 다시 시작 [sp_cdc_start_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **db_owner** 고정된 데이터베이스 역할.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-a-capture-job"></a>1. 캡처 작업 변경  
 다음 예에서는 업데이트를 `@job_type`, `@maxscans`, 및 `@maxtrans` 에서 캡처 작업의 매개 변수는 `AdventureWorks2012` 데이터베이스입니다. 캡처 작업에 대한 다른 유효한 매개 변수인 `@continuous`와 `@pollinginterval`은 생략되며 해당 값은 수정되지 않습니다.  
  
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
 다음 예에서는 `AdventureWorks2012` 데이터베이스에서 정리 작업을 업데이트합니다. 이 유효한 모든 매개 변수를 제외한 형식 작업 **@threshold**에 지정 됩니다. 변수의 **@threshold** 수정 되지 않습니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'cleanup',  
    @retention = 2880;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [dbo.cdc_jobs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_add_job&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
