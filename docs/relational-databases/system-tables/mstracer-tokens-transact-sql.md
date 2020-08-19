---
description: MStracer_tokens(Transact-SQL)
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
ms.openlocfilehash: 4e3604e25213740d58a1d01b686d3d698bcc44a3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427635"
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
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
