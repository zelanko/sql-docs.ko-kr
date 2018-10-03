---
title: MSrepl_commands (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSrepl_commands
- MSrepl_commands_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_commands system table
ms.assetid: 53b9f9cd-9429-47a0-aba2-908fc60e7036
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 44b9b1868959b744bf0d24300f828b351b521f54
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47834521"
---
# <a name="msreplcommands-transact-sql"></a>MSrepl_commands(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSrepl_commands** 테이블 복제 된 명령의 행이 포함 됩니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|게시자 데이터베이스의 ID입니다.|  
|**xact_seqno**|**varbinary(16)**|트랜잭션 시퀀스 번호입니다.|  
|**type**|**int**|명령 유형입니다.|  
|**article_id**|**int**|아티클의 ID입니다.|  
|**originator_id**|**int**|원게시자의 ID입니다.|  
|**command_id**|**int**|명령의 ID입니다.|  
|**partial_command**|**bit**|부분 명령인지 여부를 나타냅니다.|  
|**명령**|**varbinary(1024)**|명령 값입니다.|  
|**hashkey**|**int**|내부적으로만 사용됩니다.|  
|**originator_lsn**|**varbinary(16)**|원본 게시에서 명령의 LSN을 식별합니다. 피어 투 피어 트랜잭션 복제에 사용됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replcmds &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)  
  
  
