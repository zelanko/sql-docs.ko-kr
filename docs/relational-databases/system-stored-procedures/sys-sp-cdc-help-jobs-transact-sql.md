---
description: sys.sp_cdc_help_jobs(Transact-SQL)
title: sys. sp_cdc_help_jobs (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_help_jobs
- sys.sp_cdc_help_jobs_TSQL
- sp_cdc_help_jobs_TSQL
- sys.sp_cdc_help_jobs
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_help_jobs
ms.assetid: 9399b4bc-8293-408f-b3cb-f904e0657fb5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6a051301d812b06ab2170519cb54ea6f528490b7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544719"
---
# <a name="syssp_cdc_help_jobs-transact-sql"></a>sys.sp_cdc_help_jobs(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스의 모든 변경 데이터 캡처 정리 또는 캡처 작업에 대한 정보를 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_cdc_help_jobs  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|작업의 ID입니다.|  
|**job_type**|**nvarchar (20)**|작업의 유형입니다.|  
|**maxtrans**|**int**|각 검색 주기에서 처리할 최대 트랜잭션 수입니다.<br /><br /> **maxtrans** 는 캡처 작업에 대해서만 사용할 수 있습니다.|  
|**maxscans**|**int**|로그에서 모든 행을 추출하기 위해 실행할 최대 검색 주기 수입니다.<br /><br /> **maxscans** 은 캡처 작업에 대해서만 유효 합니다.|  
|**주기가**|**bit**|캡처 작업이 지속적으로 실행(1)될지, 1회 모드로 실행(0)될지를 나타내는 플래그입니다. 자세한 내용은 [sp_cdc_add_job &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)을 참조 하십시오.<br /><br /> **연속** 은 캡처 작업에 대해서만 유효 합니다.|  
|**pollinginterval**|**bigint**|로그 검색 주기 사이의 시간(초)입니다.<br /><br /> **pollinginterval** 는 캡처 작업에 대해서만 사용할 수 있습니다.|  
|**보존**|**bigint**|변경 테이블에 변경 행이 보관되는 시간(분)입니다.<br /><br /> **보존** 은 정리 작업에 대해서만 유효 합니다.|  
|**threshold**|**bigint**|정리 시 단일 문을 사용하여 삭제할 수 있는 삭제 항목의 최대 수입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **Db_owner** 고정 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `AdventureWorks2012` 데이터베이스에 대해 정의된 캡처 및 정리 작업에 관한 정보를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_help_jobs;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [cdc_jobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_add_job&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
