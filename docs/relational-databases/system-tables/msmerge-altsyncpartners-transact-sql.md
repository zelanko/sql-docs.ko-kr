---
title: MSmerge_altsyncpartners (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSmerge_altsyncpartners_TSQL
- MSmerge_altsyncpartners
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_altsyncpartners system table
ms.assetid: da51b0f8-5ad0-4aeb-96ed-2b3672a2a6e2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 014594e62b3313ea850139147e72528fb7d925c3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47652181"
---
# <a name="msmergealtsyncpartners-transact-sql"></a>MSmerge_altsyncpartners(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSmerge_altsyncpartners** 테이블의 현재 동기화 파트너는 게시자에 대 한 연결을 추적 합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|원래 게시자에 대한 식별자입니다.|  
|**alternate_subid**|**uniqueidentifier**|대체 동기화 파트너인 구독자에 대한 식별자입니다.|  
|**description**|**nvarchar(255)**|대체 동기화 파트너에 대한 설명입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
