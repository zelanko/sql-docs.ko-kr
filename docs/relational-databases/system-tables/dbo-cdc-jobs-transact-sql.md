---
title: dbo. cdc_jobs (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc_jobs
- cdc_jobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.cdc_jobs
ms.assetid: 85e2d580-1c54-4b81-b7e6-2e12997199fd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 69c38cca8ab26691a155d11ad3afc88bdc2852d2
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827325"
---
# <a name="dbocdc_jobs-transact-sql"></a>dbo.cdc_jobs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  캡처 및 정리 작업에 대한 변경 데이터 캡처 구성 매개 변수를 저장합니다. 이 테이블은 **msdb**에 저장 됩니다.  
  
 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|작업이 실행되고 있는 데이터베이스의 ID입니다.|  
|**job_type**|**nvarchar (20)**|작업 유형으로 ‘캡처' 또는 '정리'입니다.|  
|**job_id**|**uniqueidentifier**|작업과 연결된 고유한 ID입니다.|  
|**maxtrans**|**int**|각 검색 주기에서 처리할 최대 트랜잭션 수입니다.<br /><br /> **maxtrans** 는 캡처 작업에 대해서만 사용할 수 있습니다.|  
|**maxscans**|**int**|로그에서 모든 행을 추출하기 위해 실행할 최대 검색 주기 수입니다.<br /><br /> **maxscans** 은 캡처 작업에 대해서만 유효 합니다.|  
|**주기가**|**bit**|캡처 작업이 지속적으로 실행(1)될지, 1회 모드로 실행(0)될지를 나타내는 플래그입니다. 자세한 내용은 [sp_cdc_add_job &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)을 참조 하십시오.<br /><br /> **연속** 은 캡처 작업에 대해서만 유효 합니다.|  
|**pollinginterval**|**bigint**|로그 검색 주기 사이의 시간(초)입니다.<br /><br /> **pollinginterval** 는 캡처 작업에 대해서만 사용할 수 있습니다.|  
|**보존**|**bigint**|변경 테이블에 변경 행이 보관되는 시간(분)입니다.<br /><br /> **보존** 은 정리 작업에 대해서만 유효 합니다.|  
|**고대비**|**bigint**|정리 시 단일 문을 사용하여 삭제할 수 있는 삭제 항목의 최대 수입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [sp_cdc_add_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)   
 [sp_cdc_change_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)   
 [sp_cdc_help_jobs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)   
 [sp_cdc_drop_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-drop-job-transact-sql.md)  
  
  
