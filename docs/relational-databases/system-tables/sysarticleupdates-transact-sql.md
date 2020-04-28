---
title: sysarticleupdates (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticleupdates_TSQL
- sysarticleupdates
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticleupdates system table
ms.assetid: 11a53bcd-a215-4d0b-9db8-233981d3ef5d
author: stevestein
ms.author: sstein
ms.openlocfilehash: d2e710bdbe8f026624ea71357afb6d204b333c91
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68130490"
---
# <a name="sysarticleupdates-transact-sql"></a>sysarticleupdates(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  즉시 업데이트 구독을 지원하는 각 아티클에 대해 한 행을 포함합니다. 이 테이블은 복제된 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|아티클에 대한 고유 ID를 제공하는 ID 열입니다.|  
|**pubid**|**int**|아티클이 속한 게시의 ID입니다.|  
|**sync_ins_proc**|**int**|삽입 동기화 트랜잭션을 처리하는 저장 프로시저의 ID입니다.|  
|**sync_upd_proc**|**int**|업데이트 동기화 트랜잭션을 처리하는 저장 프로시저의 ID입니다.|  
|**sync_del_proc**|**int**|삭제 동기화 트랜잭션을 처리하는 저장 프로시저의 ID입니다.|  
|**autogen**|**bit**|저장 프로시저가 자동으로 생성되는지 여부를 나타냅니다.<br /><br /> **0** = False, 자동이 아닙니다.<br /><br /> **1** = True, 자동.|  
|**sync_upd_trig**|**int**|아티클 테이블에서의 자동 버전 관리 트리거의 ID입니다.|  
|**conflict_tableid**|**int**|충돌 테이블의 ID입니다.|  
|**ins_conflict_proc**|**int**|**Conflict_table**충돌을 기록 하는 데 사용 되는 프로시저의 ID입니다.|  
|**identity_support**|**bit**|지연 업데이트를 사용할 때 자동 ID 범위 처리를 사용하는지 여부를 지정합니다. **0** 은 id 범위를 지원 하지 않음을 의미 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
