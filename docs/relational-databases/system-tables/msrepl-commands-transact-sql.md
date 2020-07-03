---
title: MSrepl_commands (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_commands
- MSrepl_commands_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_commands system table
ms.assetid: 53b9f9cd-9429-47a0-aba2-908fc60e7036
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6d4dcbee03f1d5514e2b24520409804b1f27cefe
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889519"
---
# <a name="msrepl_commands-transact-sql"></a>MSrepl_commands(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSrepl_commands** 테이블에는 복제 된 명령의 행이 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|게시자 데이터베이스의 ID입니다.|  
|**xact_seqno**|**varbinary(16)**|트랜잭션 시퀀스 번호입니다.|  
|**type**|**int**|명령 유형입니다.|  
|**article_id**|**int**|아티클의 ID입니다.|  
|**originator_id**|**int**|원게시자의 ID입니다.|  
|**command_id**|**int**|명령의 ID입니다.|  
|**partial_command**|**bit**|부분 명령인지 여부를 나타냅니다.|  
|**command**|**varbinary (1024)**|명령 값입니다.|  
|**hashkey**|**int**|내부적으로만 사용됩니다.|  
|**originator_lsn**|**varbinary(16)**|원본 게시에서 명령의 LSN을 식별합니다. 피어 투 피어 트랜잭션 복제에 사용됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replcmds&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)  
  
  
