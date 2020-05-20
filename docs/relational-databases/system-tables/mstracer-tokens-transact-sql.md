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
ms.openlocfilehash: 6978f0b1c5a18d63fb73d5f06280eed972d1d546
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829198"
---
# <a name="mstracer_tokens-transact-sql"></a>MStracer_tokens(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
  
