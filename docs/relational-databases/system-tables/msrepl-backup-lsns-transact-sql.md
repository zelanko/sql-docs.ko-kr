---
title: MSrepl_backup_lsns (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSrepl_backup_lsns_TSQL
- MSrepl_backup_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_backup_Isns system table
ms.assetid: de06c349-82a8-48c6-b602-b5d6938514f6
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2978827ac47e46e7d9a5af7770101be52981b41f
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101441"
---
# <a name="msreplbackuplsns-transact-sql"></a>MSrepl_backup_lsns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSrepl_backup_lsns** 테이블 배포 데이터베이스의 'sync with backup' 옵션을 지원 하기 위한 트랜잭션 LSN (로그 시퀀스 번호)을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|게시자 데이터베이스의 ID입니다.|  
|**valid_xact_id**|**varbinary(16)**|로그를 잘라낼 지점을 표시하기 위해 게시자에게 보낼 트랜잭션의 ID입니다. 배포 데이터베이스가 'sync with backup' 모드인 경우에만 사용합니다. 백업된 배포 데이터베이스에 최근에 복제된 트랜잭션의 ID가 포함됩니다. 이 내용이 게시자에게 보내져 로그 판독기가 로그 트랜잭션을 잘라낼 지점을 표시하게 됩니다.|  
|**valid_xact_seqno**|**varbinary(16)**|게시자에게 보내져 로그를 잘라낼 지점을 표시할 트랜잭션의 시퀀스 번호입니다. 배포 데이터베이스가 'sync with backup' 모드인 경우에만 이를 사용합니다. 백업된 배포 데이터베이스에서 최근에 복제된 트랜잭션의 로그 시퀀스 번호입니다. 이 내용이 게시자에게 보내져 로그 판독기가 로그 트랜잭션을 잘라낼 지점을 표시하게 됩니다.|  
|**next_xact_id**|**varbinary(16)**|백업 작업에 사용되는 임시 로그 시퀀스 번호입니다.|  
|**nextx_xact_seqno**|**varbinary(16)**|백업 작업에 사용되는 임시 로그 시퀀스 번호입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
