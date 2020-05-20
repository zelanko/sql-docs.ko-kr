---
title: MSlogreader_history (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSlogreader_history_TSQL
- MSlogreader_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSlogreader_history system table
ms.assetid: 2e399fa1-3591-4c1c-96b7-7964fe82c7c4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5dfb1efc93efe8c4b59d649466f8b0c0af0a64a6
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82812829"
---
# <a name="mslogreader_history-transact-sql"></a>MSlogreader_history(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSlogreader_history** 테이블에는 로컬 배포자와 연결 된 로그 판독기 에이전트에 대 한 기록 행이 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|로그 판독기 에이전트의 ID입니다.|  
|**runstatus**|**int**|실행 상태는 다음과 같습니다.<br /><br /> 1 = 시작<br /><br /> 2 = 성공<br /><br /> 3 = 진행 중<br /><br /> 4 = 유휴 상태<br /><br /> 5 = 다시 시도<br /><br /> 6 = 실패|  
|**start_time**|**datetime**|작업 실행을 시작할 시간입니다.|  
|**time**|**datetime**|메시지가 기록되는 시간입니다.|  
|**duration**|**int**|메시지 세션의 기간(초)입니다.|  
|**주석만**|**nvarchar(255)**|메시지 텍스트입니다.|  
|**xact_seqno**|**varbinary(16)**|마지막에 처리된 트랜잭션 시퀀스 번호입니다.|  
|**delivery_time**|**int**|트랜잭션이 처음 전달된 시간입니다.|  
|**delivered_transactions**|**int**|세션 중에 전달된 총 트랜잭션 수입니다.|  
|**delivered_commands**|**int**|세션 중에 전달된 총 명령 수입니다.|  
|**average_commands**|**int**|세션 중에 전달된 평균 명령 수입니다.|  
|**delivery_rate**|**float**|초당 전달된 평균 명령 수입니다.|  
|**delivery_latency**|**int**|게시된 데이터베이스에 입력한 명령이 배포 데이터베이스에 입력될 때까지의 대기 시간입니다. 단위는 밀리초입니다.|  
|**error_id**|**int**|**MSrepl_error** 시스템 테이블에 있는 오류의 ID입니다.|  
|**timestamp**|**timestamp**|이 테이블의 타임스탬프 열입니다.|  
|**updateable_row**|**bit**|기록 행을 덮어쓸 수 있는 경우 **1** 로 설정 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
