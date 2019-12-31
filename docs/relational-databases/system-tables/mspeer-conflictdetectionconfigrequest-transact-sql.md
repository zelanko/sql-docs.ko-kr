---
title: MSpeer_conflictdetectionconfigrequest (T-sql)
description: 피어 투 피어 게시에 대 한 토폴로지 전체 구성 요청을 추적 하는 데 사용 되는 MSPeer_conflictdetectionconfigurerequest 저장 프로시저에 대해 설명 합니다.
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigrequest_TSQL
- MSpeer_conflictdetectionconfigrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigurerequest
ms.assetid: 83afa0ca-707e-4468-a888-228268ed4e10
author: stevestein
ms.author: sstein
ms.openlocfilehash: 090236bd5e0bd0429985ff9c54039a576950ec84
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322100"
---
# <a name="mspeer_conflictdetectionconfigrequest-transact-sql"></a>MSpeer_conflictdetectionconfigrequest(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  피어 투 피어 복제에서 게시에 대한 토폴로지 차원 구성 요청을 추적하기 위해 사용됩니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|id|**int**|충돌 구성 요청을 식별합니다. [MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md) 의 request_id 열은이 값을 사용 합니다.|  
|publication|**sysname 이며**|충돌 구성 요청이 시작된 게시의 이름입니다.|  
|sent_date|**날짜**|충돌 구성 요청이 시작된 날짜와 시간입니다.|  
|시간 제한|**int**|모든 피어가 충돌 정보를 반환할 때까지 프로시저가 기다려야 하는 시간입니다.|  
|modified_date|**날짜**|단계가 완료된 날짜와 시간입니다.|  
|progress_phase|**nvarchar (32)**|다음 값 중 하나를 사용하여 현재 처리 단계를 식별합니다.<br /><br /> Started<br /><br /> Exploring topology<br /><br /> Collecting status<br /><br /> Status collected|  
|phase_timed_out|**bit**|현재 단계가 시간 초과되었는지 여부를 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
