---
title: MSreplication_queue (TRANSACT-SQL) | Microsoft Docs
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
- MSreplication_queue
- MSreplication_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_queue system table
ms.assetid: 664bf817-8021-4417-96d6-2bb1e4baabff
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 663a07279a7bfe0ba9afe8ce6dc37cd74c71434c
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102141"
---
# <a name="msreplicationqueue-transact-sql"></a>MSreplication_queue(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSreplication_queue** 테이블은 복제 프로세스에서 전달 하는 큐에 대기 중인된 명령을 모든 큐에 대기 되는 SQL 기반를 사용 하는 지연된 업데이트 구독을 저장 하는 데 사용 됩니다. 이 테이블은 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|게시자의 이름입니다.|  
|**publisher_db**|**sysname**|게시 데이터베이스의 이름입니다.|  
|**게시**|**sysname**|게시의 이름입니다.|  
|**tranid**|**sysname**|대기 중인 명령이 실행된 트랜잭션 ID입니다.|  
|**data**|**varbinary(8000)**|대기 중인 명령에 대한 정보를 저장한 압축된 바이트 스트림입니다.|  
|**datalen**|**int**|데이터의 길이(바이트)입니다.|  
|**commandtype**|**int**|대기 중인 명령의 유형입니다.<br /><br /> 1 = 트랜잭션의 사용자 명령<br /><br /> 2 = 구독 동기화 명령|  
|**insertdate**|**datetime**|삽입한 날짜입니다.|  
|**orderkey**|**bigint**|단순하게 증가하는 ID 열입니다.|  
|**cmdstate**|**bit**|명령 상태입니다.<br /><br /> 0 = 완료됨<br /><br /> 1 = 부분 완료됨|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
