---
title: MSpeer_lsns (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- MSpeer_lsns
- MSpeer_lsns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_lsns system table
ms.assetid: 0ba33907-601b-4c3d-8099-2663f680a161
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e4c68b32d5b6c86fad158962deb360e64fa129d0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33006831"
---
# <a name="mspeerlsns-transact-sql"></a>MSpeer_lsns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Mspeer_lsns** 각 트랜잭션에 피어 투 피어 복제 토폴로지에서 구독에 매핑할 테이블을 사용 합니다. 이 테이블은 피어 투 피어 복제 토폴로지 내의 모든 게시 데이터베이스와 피어 투 피어 게시에 대한 모든 구독자의 구독 데이터베이스에 저장됩니다. 이 유형의 트랜잭션 복제 토폴로지에 대 한 자세한 내용은 참조 하십시오. [피어 투 피어 트랜잭션 복제](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)합니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|피어 투 피어 LSN을 식별합니다.|  
|**last_updated**|**datetime**|**datetime** 에서 마지막 행 업데이트가 적용 되었습니다.|  
|**originator**|**sysname**|트랜잭션을 시작한 게시자의 이름입니다.|  
|**originator_db**|**sysname**|트랜잭션이 시작된 데이터베이스의 이름입니다.|  
|**originator_publication**|**sysname**|트랜잭션이 시작된 게시의 이름입니다.|  
|**originator_publication_id**|**int**|트랜잭션이 시작된 게시에 대한 식별자입니다.|  
|**originator_db_version**|**int**|원래 데이터베이스의 버전 번호를 식별합니다.|  
|**originator_lsn**|**int**|원본 게시의 LSN을 식별합니다.|  
|**originator_version**|**int**|게시자의 버전 번호를 식별합니다.|  
|**originator_id**|**smallint**|충돌 감지를 위해 토폴로지의 각 노드를 식별합니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)을(를) 참조하세요.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
