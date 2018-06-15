---
title: MSreplication_queue (Transact SQL) | Microsoft Docs
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1230ab84f1d5082fd1f8b9482702a9361b7b9f2e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33005510"
---
# <a name="msreplicationqueue-transact-sql"></a>MSreplication_queue(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_queue** 복제 프로세스를 전달 하는 큐에 대기 중인된 명령을 모든 SQL 기반을 사용 하는 지연된 업데이트 구독 큐에 대기를 저장할 테이블을 사용 합니다. 이 테이블은 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|게시자의 이름입니다.|  
|**publisher_db**|**sysname**|게시 데이터베이스의 이름입니다.|  
|**게시**|**sysname**|게시의 이름입니다.|  
|**Tranid**|**sysname**|대기 중인 명령이 실행된 트랜잭션 ID입니다.|  
|**data**|**varbinary(8000)**|대기 중인 명령에 대한 정보를 저장한 압축된 바이트 스트림입니다.|  
|**datalen**|**int**|데이터의 길이(바이트)입니다.|  
|**commandtype**|**int**|대기 중인 명령의 유형입니다.<br /><br /> 1 = 트랜잭션의 사용자 명령<br /><br /> 2 = 구독 동기화 명령|  
|**insertdate**|**datetime**|삽입한 날짜입니다.|  
|**orderkey**|**bigint**|단순하게 증가하는 ID 열입니다.|  
|**cmdstate**|**bit**|명령 상태입니다.<br /><br /> 0 = 완료됨<br /><br /> 1 = 부분 완료됨|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
