---
title: MSmerge_metadataaction_request (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSmerge_metadataaction_request
- MSmerge_metadataaction_request_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_metadataaction_request system table
ms.assetid: cd31a114-900a-4218-ab58-d959e547c647
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bd34379e4bdf4a9567d1bc3e9bb1e3aff2f8a401
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="msmergemetadataactionrequest-transact-sql"></a>MSmerge_metadataaction_request(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_metadataaction_request** 테이블에는 필요한 각 보정 동작에 대해 한 행을 저장 합니다. 오류가 발생 하 고 동기화 다시 시도해 야 하는 경우 웹 동기화를 사용 하 여에 항목이 하나 생성 됩니다 **MSmerge_metadataaction_request**합니다. 다음 병합의 업로드 단계 동안 동기화 중인 게시에 속한 모든 아티클에 대한 요청은 이 테이블에서 검색되어 업로드됩니다. 동기화 성공적으로 완료 되 면, 해당 행에는 **MSmerge_metadataaction_request** 테이블이 삭제 됩니다. 이 테이블은 게시 데이터베이스의 게시자와 구독 데이터베이스의 구독자에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|게시된 테이블의 애칭입니다.|  
|**rowguid**|**uniqueidentifier**|지정된 행의 행 식별자입니다.|  
|**action**|**tinyint**|필요한 보정 동작을 식별합니다.|  
|**generation**|**bigint**|보정 동작이 필요한 생성의 값입니다.|  
|**변경**|**int**|내부적으로만 사용됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [병합 복제에 대한 웹 동기화](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
