---
description: MSrepl_backup_lsns(Transact-SQL)
title: MSrepl_backup_lsns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_backup_lsns_TSQL
- MSrepl_backup_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_backup_Isns system table
ms.assetid: de06c349-82a8-48c6-b602-b5d6938514f6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 743657bad9cf4c0bd1611e7f00f1d410753583ce
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540264"
---
# <a name="msrepl_backup_lsns-transact-sql"></a>MSrepl_backup_lsns(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSrepl_backup_lsns** 테이블에는 배포 데이터베이스의 ' sync with backup ' 옵션을 지원 하기 위한 트랜잭션 LSN (로그 시퀀스 번호)이 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|게시자 데이터베이스의 ID입니다.|  
|**valid_xact_id**|**varbinary(16)**|로그를 잘라낼 지점을 표시하기 위해 게시자에게 보낼 트랜잭션의 ID입니다. 배포 데이터베이스가 'sync with backup' 모드인 경우에만 사용합니다. 백업된 배포 데이터베이스에 최근에 복제된 트랜잭션의 ID가 포함됩니다. 이 내용이 게시자에게 보내져 로그 판독기가 로그 트랜잭션을 잘라낼 지점을 표시하게 됩니다.|  
|**valid_xact_seqno**|**varbinary(16)**|게시자에게 보내져 로그를 잘라낼 지점을 표시할 트랜잭션의 시퀀스 번호입니다. 배포 데이터베이스가 'sync with backup' 모드인 경우에만 이를 사용합니다. 백업된 배포 데이터베이스에서 최근에 복제된 트랜잭션의 로그 시퀀스 번호입니다. 이 내용이 게시자에게 보내져 로그 판독기가 로그 트랜잭션을 잘라낼 지점을 표시하게 됩니다.|  
|**next_xact_id**|**varbinary(16)**|백업 작업에 사용되는 임시 로그 시퀀스 번호입니다.|  
|**nextx_xact_seqno**|**varbinary(16)**|백업 작업에 사용되는 임시 로그 시퀀스 번호입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
