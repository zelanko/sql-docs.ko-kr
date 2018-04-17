---
title: MSpeer_topologyresponse (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
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
- MSpeer_topologyresponse
- MSpeer_topologyresponse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_topologyresponse
ms.assetid: 1bc5c0c6-c432-405c-89fd-e953d173a247
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8e89ab3a49d899b4cf17a5b0037272ea3a3faaf4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="mspeertopologyresponse-transact-sql"></a>MSpeer_topologyresponse(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  피어 투 피어 복제에서 토폴로지 상태 요청에 대한 각 노드의 응답을 저장하기 위해 사용됩니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|request_id|**int**|토폴로지 상태 요청 항목을 식별 하는 [MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md) 테이블입니다.|  
|peer|**sysname**|응답을 생성한 서버 인스턴스의 이름입니다.|  
|peer_version|**int**|게시자의 버전 번호를 식별합니다.|  
|peer_db|**sysname**|응답을 생성한 피어에 있는 구독 데이터베이스입니다.|  
|originator_id|**int**|충돌 감지를 위해 토폴로지의 각 노드를 식별합니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)을(를) 참조하세요.|  
|peer_conflict_retention|**int**|메타데이터가 충돌 테이블에 저장된 기간(일 수)입니다.|  
|received_date|**datetime**|토폴로지 요청이 수신된 시간입니다.|  
|connection_info|**xml**|요청에 응답한 노드에 대한 정보입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
