---
title: MSqreader_history (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSqreader_history
- MSqreader_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSqreader_history system table
ms.assetid: c5c91d39-513c-4a77-870b-c8ef74a1cd6b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a1d179cbef19e652472714b8010edcaeb12ebcc6
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52779695"
---
# <a name="msqreaderhistory-transact-sql"></a>MSqreader_history(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSqreader_history** 테이블은 로컬 배포자와 연결 된 큐 판독기 에이전트에 대 한 기록 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|큐 판독기 에이전트의 ID입니다.|  
|**publication_id**|**int**|게시의 ID입니다.|  
|**runstatus**|**int**|에이전트의 실행 상태입니다.<br /><br /> **1** = 시작 합니다.<br /><br /> **2** = 성공 합니다.<br /><br /> **3** = 진행 중입니다.<br /><br /> **4** = 유휴 상태입니다.<br /><br /> **5** = 다시 시도 합니다.<br /><br /> **6** = 실패.|  
|**start_time**|**datetime**|에이전트 세션이 시작된 날짜 및 시간입니다.|  
|**time**|**datetime**|마지막으로 메시지가 기록된 날짜 및 시간입니다.|  
|**duration**|**int**|기록된 세션 동작의 경과 시간(초) 입니다.|  
|**주석**|**nvarchar(255)**|설명 텍스트입니다.|  
|**transaction_id**|**nvarchar(40)**|해당되는 경우, 메시지와 함께 저장된 트랜잭션 ID입니다.|  
|**transaction_status**|**int**|트랜잭션의 상태입니다.|  
|**transactions_processed**|**int**|세션에서 처리된 트랜잭션의 총 수입니다.|  
|**commands_processed**|**int**|세션에서 처리된 명령의 총 수입니다.|  
|**delivery_rate**|**float(53)**|전달된 명령의 초 당 평균 수입니다.|  
|**transaction_rate**|**float(53)**|처리된 트랜잭션 비율입니다.|  
|**subscriber**|**sysname**|구독자 이름입니다.|  
|**subscriberdb**|**sysname**|구독 데이터베이스의 이름입니다.|  
|**error_id**|**int**|0이 아닌 경우 숫자 나타내는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 메시지입니다.|  
|**timestamp**|**timestamp**|테이블의 타임스탬프 열입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
