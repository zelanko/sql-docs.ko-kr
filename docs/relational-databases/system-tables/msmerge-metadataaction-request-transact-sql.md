---
title: MSmerge_metadataaction_request (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_metadataaction_request
- MSmerge_metadataaction_request_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_metadataaction_request system table
ms.assetid: cd31a114-900a-4218-ab58-d959e547c647
author: stevestein
ms.author: sstein
ms.openlocfilehash: 09f3fa61a1f79e98b8cd3330a03361b1b6a5c507
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106375"
---
# <a name="msmergemetadataactionrequest-transact-sql"></a>MSmerge_metadataaction_request(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSmerge_metadataaction_request** 테이블은 필요한 각 보정 동작에 대 한 하나의 행을 저장 합니다. 오류가 발생 하 고 동기화를 다시 시도해 야 하는 경우에 웹 동기화를 사용 하 여에 항목이 생성 됩니다 **MSmerge_metadataaction_request**합니다. 다음 병합의 업로드 단계 동안 동기화 중인 게시에 속한 모든 아티클에 대한 요청은 이 테이블에서 검색되어 업로드됩니다. 동기화를 성공적으로 완료 되 면, 해당 행을 **MSmerge_metadataaction_request** 테이블이 삭제 됩니다. 이 테이블은 게시 데이터베이스의 게시자와 구독 데이터베이스의 구독자에 저장됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|게시된 테이블의 애칭입니다.|  
|**rowguid**|**uniqueidentifier**|지정된 행의 행 식별자입니다.|  
|**action**|**tinyint**|필요한 보정 동작을 식별합니다.|  
|**generation**|**bigint**|보정 동작이 필요한 생성의 값입니다.|  
|**changed**|**int**|내부적으로만 사용됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [병합 복제에 대한 웹 동기화](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
