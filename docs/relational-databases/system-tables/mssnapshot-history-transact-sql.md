---
title: MSsnapshot_history (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSsnapshot_history
- MSsnapshot_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_history system table
ms.assetid: 56bf4128-1689-4963-9343-432dd0898d31
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c5360a12d9606df310fe5e6e46c6aaaaf34f6f37
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mssnapshothistory-transact-sql"></a>MSsnapshot_history(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsnapshot_history** 테이블은 로컬 배포자와 연관 된 스냅숏 에이전트에 대 한 기록 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|스냅숏 에이전트의 ID입니다.|  
|**runstatus**|**int**|실행 상태는 다음과 같습니다.<br /><br /> **1** = 시작 합니다.<br /><br /> **2** = 성공 합니다.<br /><br /> **3** = 진행 중입니다.<br /><br /> **4** = 유휴 상태입니다.<br /><br /> **5** = 다시 시도 합니다.<br /><br /> **6** = 실패.|  
|**start_time**|**datetime**|작업 실행을 시작할 시간입니다.|  
|**time**|**datetime**|메시지가 기록되는 시간입니다.|  
|**duration**|**int**|메시지 세션의 기간(초)입니다.|  
|**주석**|**nvarchar(255)**|메시지 텍스트입니다.|  
|**delivered_transactions**|**int**|세션 중에 전달된 총 트랜잭션 수입니다.|  
|**delivered_commands**|**int**|초당 전달된 명령 수입니다.|  
|**delivery_rate**|**float(53)**|초당 전달된 평균 명령 수입니다.|  
|**error_id**|**int**|오류 메시지의 ID는 [MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md) 시스템 테이블입니다.|  
|**timestamp**|**timestamp**|이 테이블의 타임스탬프 열입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
