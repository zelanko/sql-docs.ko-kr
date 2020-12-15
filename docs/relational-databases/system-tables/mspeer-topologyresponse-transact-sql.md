---
description: MSpeer_topologyresponse(Transact-SQL)
title: MSpeer_topologyresponse (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_topologyresponse
- MSpeer_topologyresponse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_topologyresponse
ms.assetid: 1bc5c0c6-c432-405c-89fd-e953d173a247
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 82f44d74f896ee1d7b394d7e5dc8102aa7726856
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464574"
---
# <a name="mspeer_topologyresponse-transact-sql"></a>MSpeer_topologyresponse(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  피어 투 피어 복제에서 토폴로지 상태 요청에 대한 각 노드의 응답을 저장하기 위해 사용됩니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|request_id|**int**|[MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md) 테이블에서 토폴로지 상태 요청 항목을 식별 합니다.|  
|peer|**sysname**|응답을 생성한 서버 인스턴스의 이름입니다.|  
|peer_version|**int**|게시자의 버전 번호를 식별합니다.|  
|peer_db|**sysname**|응답을 생성한 피어에 있는 구독 데이터베이스입니다.|  
|originator_id|**int**|충돌 감지를 위해 토폴로지의 각 노드를 식별합니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)을 참조하세요.|  
|peer_conflict_retention|**int**|메타데이터가 충돌 테이블에 저장된 기간(일 수)입니다.|  
|received_date|**datetime**|토폴로지 요청이 수신된 시간입니다.|  
|connection_info|**xml**|요청에 응답한 노드에 대한 정보입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
