---
title: dbo.cdc_jobs (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- cdc_jobs
- cdc_jobs_TSQL
dev_langs: TSQL
helpviewer_keywords: dbo.cdc_jobs
ms.assetid: 85e2d580-1c54-4b81-b7e6-2e12997199fd
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1c455f083d0cb635d62e67a9b8e03e7bdda0b106
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="dbocdcjobs-transact-sql"></a>dbo.cdc_jobs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  캡처 및 정리 작업에 대한 변경 데이터 캡처 구성 매개 변수를 저장합니다. 이 테이블에 저장 됩니다 **msdb**합니다.  
  
 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|작업이 실행되고 있는 데이터베이스의 ID입니다.|  
|**job_type**|**nvarchar (20)**|작업 유형으로 ‘캡처' 또는 '정리'입니다.|  
|**job_id**|**uniqueidentifier**|작업과 연결된 고유한 ID입니다.|  
|**maxtrans**|**int**|각 검색 주기에서 처리할 최대 트랜잭션 수입니다.<br /><br /> **maxtrans** 캡처 작업에 대해서만 유효 합니다.|  
|**maxscans**|**int**|로그에서 모든 행을 추출하기 위해 실행할 최대 검색 주기 수입니다.<br /><br /> **maxscans** 캡처 작업에 대해서만 유효 합니다.|  
|**연속**|**bit**|캡처 작업이 지속적으로 실행(1)될지, 1회 모드로 실행(0)될지를 나타내는 플래그입니다. 자세한 내용은 참조 [sys.sp_cdc_add_job&#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md).<br /><br /> **연속** 캡처 작업에 대해서만 유효 합니다.|  
|**pollinginterval**|**bigint**|로그 검색 주기 사이의 시간(초)입니다.<br /><br /> **pollinginterval** 캡처 작업에 대해서만 유효 합니다.|  
|**보존**|**bigint**|변경 테이블에 변경 행이 보관되는 시간(분)입니다.<br /><br /> **보존** 정리 작업에 대해서만 유효 합니다.|  
|**임계값**|**bigint**|정리 시 단일 문을 사용하여 삭제할 수 있는 삭제 항목의 최대 수입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [sys.sp_cdc_add_job&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)   
 [sys.sp_cdc_change_job &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)   
 [sys.sp_cdc_help_jobs &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)   
 [sys.sp_cdc_drop_job &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-drop-job-transact-sql.md)  
  
  
