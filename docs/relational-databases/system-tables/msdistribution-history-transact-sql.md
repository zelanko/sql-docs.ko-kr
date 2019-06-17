---
title: MSdistribution_history (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistribution_history
- MSdistribution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_history system table
ms.assetid: 55665bd2-9e1d-4efc-8f60-c63a24f66b28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 305223fca45bb1916598f02c16cc4e38981e861d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62903700"
---
# <a name="msdistributionhistory-transact-sql"></a>MSdistribution_history(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSdistribution_history** 테이블은 로컬 배포자와 연결 된 배포 에이전트에 대 한 기록 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|배포 에이전트의 ID입니다.|  
|**runstatus**|**int**|실행 상태는 다음과 같습니다.<br /><br /> **1** = 시작 합니다.<br /><br /> **2** = 성공 합니다.<br /><br /> **3** = 진행 중입니다.<br /><br /> **4** = 유휴 상태입니다.<br /><br /> **5** = 다시 시도 합니다.<br /><br /> **6** = 실패.|  
|**start_time**|**datetime**|작업 실행을 시작할 시간입니다.|  
|**time**|**datetime**|메시지가 기록되는 시간입니다.|  
|**duration**|**int**|메시지 세션의 기간(초)입니다.|  
|**comments**|**nvarchar(4000)**|메시지 텍스트입니다.|  
|**xact_seqno**|**varbinary(16)**|마지막에 처리된 트랜잭션 시퀀스 번호입니다.|  
|**current_delivery_rate**|**float**|마지막 기록 항목 이후에 초당 전달된 평균 명령 수입니다.|  
|**current_delivery_latency**|**int**|마지막 기록 항목 이후 배포 데이터베이스를 시작하고 구독자에 적용될 때까지의 대기 시간입니다. 밀리초.|  
|**delivered_transactions**|**int**|세션 중에 전달된 총 트랜잭션 수입니다.|  
|**delivered_commands**|**int**|세션 중에 전달된 총 명령 수입니다.|  
|**average_commands**|**int**|세션 중에 전달된 평균 명령 수입니다.|  
|**delivery_rate**|**float**|초당 전달된 평균 명령 수입니다.|  
|**delivery_latency**|**int**|배포 데이터베이스를 시작하고 구독자에 적용될 때까지의 대기 시간입니다. 밀리초.|  
|**total_delivered_commands**|**bigint**|구독이 생성된 이후에 전달된 총 명령 수입니다.|  
|**error_id**|**int**|오류 메시지의 ID를 **MSrepl_error** 시스템 테이블입니다.|  
|**updateable_row**|**bit**|로 **1** 기록 행을 덮어쓸 수 있는 경우.|  
|**timestamp**|**timestamp**|이 테이블의 타임스탬프 열입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
