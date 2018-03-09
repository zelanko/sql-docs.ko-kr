---
title: sysarticleupdates (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysarticleupdates_TSQL
- sysarticleupdates
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticleupdates system table
ms.assetid: 11a53bcd-a215-4d0b-9db8-233981d3ef5d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad4980903794f4d721f5aed902d8efa65ae7c972
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
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
|**autogen**|**bit**|저장 프로시저가 자동으로 생성되는지 여부를 나타냅니다.<br /><br /> **0** = false, 자동이 아님.<br /><br /> **1** 자동 = true, 합니다.|  
|**sync_upd_trig**|**int**|아티클 테이블에서의 자동 버전 관리 트리거의 ID입니다.|  
|**conflict_tableid**|**int**|충돌 테이블의 ID입니다.|  
|**ins_conflict_proc**|**int**|작성 하 고 충돌 하는 데 사용 하는 프로시저의 ID는 **conflict_table**합니다.|  
|**identity_support**|**bit**|지연 업데이트를 사용할 때 자동 ID 범위 처리를 사용하는지 여부를 지정합니다. **0** 의미는 없는 id 범위 처리를 지원 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
