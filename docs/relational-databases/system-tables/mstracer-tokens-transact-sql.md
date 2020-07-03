---
title: MStracer_tokens (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MStracer_tokens_TSQL
- MStracer_tokens
dev_langs:
- TSQL
helpviewer_keywords:
- MStracer_tokens system table
ms.assetid: b273aa48-8188-4213-8e2c-311543c3236f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0822c2de02de9ef0a420f0066d058fad200b4a88
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881473"
---
# <a name="mstracer_tokens-transact-sql"></a>MStracer_tokens(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MStracer_tokens** 테이블은 게시에 삽입 된 추적 프로그램 토큰 레코드의 레코드를 유지 관리 합니다. 이 테이블은 배포 데이터베이스에 저장되며 성능 모니터링을 위해 복제에 사용됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|추적 프로그램 토큰 레코드를 식별합니다.|  
|**publication_id**|**int**|추적 프로그램 토큰 레코드가 삽입된 게시를 식별합니다.|  
|**publisher_commit**|**datetime**|추적 프로그램 토큰 레코드가 게시자에서 커밋된 날짜와 시간입니다.|  
|**distributor_commit**|**datetime**|추적 프로그램 토큰 레코드가 배포자에서 커밋된 날짜와 시간입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
