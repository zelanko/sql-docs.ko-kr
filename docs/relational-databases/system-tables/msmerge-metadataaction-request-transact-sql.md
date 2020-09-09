---
description: MSmerge_metadataaction_request(Transact-SQL)
title: MSmerge_metadataaction_request (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7e616cea34c3c2b440decaec14ac20be3a6bcc30
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547073"
---
# <a name="msmerge_metadataaction_request-transact-sql"></a>MSmerge_metadataaction_request(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_metadataaction_request** 테이블은 필요한 각 보정 작업에 대해 하나의 행을 저장 합니다. 웹 동기화를 사용 하 여 오류가 발생 하 고 동기화를 다시 시도해 야 하는 경우에는 **MSmerge_metadataaction_request**로 항목이 생성 됩니다. 다음 병합의 업로드 단계 동안 동기화 중인 게시에 속한 모든 아티클에 대한 요청은 이 테이블에서 검색되어 업로드됩니다. 동기화가 성공적으로 완료 되 면 **MSmerge_metadataaction_request** 테이블의 해당 행이 삭제 됩니다. 이 테이블은 게시 데이터베이스의 게시자와 구독 데이터베이스의 구독자에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|게시된 테이블의 애칭입니다.|  
|**rowguid**|**uniqueidentifier**|지정된 행의 행 식별자입니다.|  
|**action**|**tinyint**|필요한 보정 동작을 식별합니다.|  
|**작성**|**bigint**|보정 동작이 필요한 생성의 값입니다.|  
|**변경**|**int**|내부적으로만 사용됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰 ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [병합 복제에 대한 웹 동기화](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
