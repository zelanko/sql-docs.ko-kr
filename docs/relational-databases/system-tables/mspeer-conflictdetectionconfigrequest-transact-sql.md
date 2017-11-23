---
title: MSpeer_conflictdetectionconfigrequest (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSpeer_conflictdetectionconfigrequest_TSQL
- MSpeer_conflictdetectionconfigrequest
dev_langs: TSQL
helpviewer_keywords: MSpeer_conflictdetectionconfigurerequest
ms.assetid: 83afa0ca-707e-4468-a888-228268ed4e10
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7162681cd957f40a5da0e609124dc3c80624700d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mspeerconflictdetectionconfigrequest-transact-sql"></a>MSpeer_conflictdetectionconfigrequest(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  피어 투 피어 복제에서 게시에 대한 토폴로지 차원 구성 요청을 추적하기 위해 사용됩니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|id|**int**|충돌 구성 요청을 식별합니다. request_id 열에서 [MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md) 이 값을 사용 합니다.|  
|publication|**sysname**|충돌 구성 요청이 시작된 게시의 이름입니다.|  
|sent_date|**datetime**|충돌 구성 요청이 시작된 날짜와 시간입니다.|  
|timeout|**int**|모든 피어가 충돌 정보를 반환할 때까지 프로시저가 기다려야 하는 시간입니다.|  
|modified_date|**datetime**|단계가 완료된 날짜와 시간입니다.|  
|progress_phase|**nvarchar (32)**|다음 값 중 하나를 사용하여 현재 처리 단계를 식별합니다.<br /><br /> 시작됨<br /><br /> Exploring topology<br /><br /> Collecting status<br /><br /> Status collected|  
|phase_timed_out|**bit**|현재 단계가 시간 초과되었는지 여부를 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
