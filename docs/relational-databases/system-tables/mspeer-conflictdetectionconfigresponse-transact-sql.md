---
title: MSpeer_conflictdetectionconfigresponse (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSpeer_conflictdetectionconfigresponse
- MSpeer_conflictdetectionconfigresponse_TSQL
dev_langs: TSQL
helpviewer_keywords: MSpeer_conflictdetectionconfigureresponse
ms.assetid: 2685fb66-731d-40f7-af4b-596b9222c5d4
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb96eb44f44e3a7a0d1e1e4bcd0b1ce8dc00cf5e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mspeerconflictdetectionconfigresponse-transact-sql"></a>MSpeer_conflictdetectionconfigresponse(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  피어 투 피어 복제에서 토폴로지 차원 구성 요청에 대한 각 노드의 응답을 저장하기 위해 사용됩니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|request_id|**int**|충돌 구성 요청 항목을 식별 하는 [MSpeer_conflictdetectionconfigrequest](../../relational-databases/system-tables/mspeer-conflictdetectionconfigrequest-transact-sql.md) 테이블입니다.|  
|peer_node|**sysname**|응답을 생성한 서버 인스턴스의 이름입니다.|  
|peer_db|**sysname**|응답을 생성한 피어에 있는 구독 데이터베이스입니다.|  
|peer_version|**sysname**|게시자의 버전 번호를 식별합니다.|  
|peer_db_version|**sysname**|피어 데이터베이스의 버전 번호를 식별합니다.|  
|is_peer|**bit**|노드가 읽기 전용 구독자인지 여부를 나타냅니다. 값이 **0** 읽기 전용 구독자를 표시 합니다.|  
|conflict_detection_enabled|**bit**|토폴로지에 대해 충돌 검색을 사용할지 여부를 지정합니다.|  
|originator_id|**varbinary (16)**|충돌 감지를 위해 토폴로지의 각 노드를 식별합니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)을(를) 참조하세요.|  
|peer_conflict_retention|**int**|메타데이터가 충돌 테이블에 저장된 기간(일 수)입니다.|  
|peer_subscriptions|**XML**|요청에 응답한 노드에 대한 정보입니다.|  
|progress_phase|**nvarchar (32)**|다음 값 중 하나를 사용하여 현재 처리 단계를 식별합니다.<br /><br /> 시작됨<br /><br /> Peer version collected<br /><br /> Status collected|  
|modified_date|**datetime**|단계가 완료된 날짜와 시간입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
