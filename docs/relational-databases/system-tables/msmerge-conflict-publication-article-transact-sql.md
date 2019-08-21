---
title: MSmerge_conflict_&lt;게시&gt;_&lt;article(transact-sql)|&gt; Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflict_publication_article_TSQL
- MSmerge_conflict_publication_article
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflict_publication_article system table
ms.assetid: dc4490b4-02d8-4dfc-98f5-0cf8de8e11be
author: stevestein
ms.author: sstein
ms.openlocfilehash: 342b0f51fb4f68945f6ab8c4b511c5299acfba49
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893578"
---
# <a name="msmerge_conflict_ltpublicationgt_ltarticlegt-transact-sql"></a>하거나 msmerge\_충돌\_게시&lt;아티클(transact-sql&gt; )&gt;&lt;\_
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **하거나 msmerge\_충돌*게시*_아티클 테이블_ 에는 데이터 일치성을 얻기 위해 실행 취소 된 행 또는 충돌 하는 행에 대 한 정보가 포함 되어 있습니다.\_\_** 게시 안에 각 복제 테이블에 대한 충돌 테이블이 존재하는데 충돌 테이블 이름 끝에 게시 및 아티클 이름이 붙습니다. 이러한 아티클별 충돌 테이블은 충돌 기록을 위해 사용하는 데이터베이스에 존재하는데 대체로 게시 데이터베이스에 존재하지만 충돌을 분산하여 기록할 때는 구독 데이터베이스에 존재할 수도 있습니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**_아티클\_열\_이름_**|**variable**|복제된 테이블의 열을 나타냅니다. 이 시스템 테이블에는 테이블 아티클에 있는 각 열에 대한 열이 하나씩 있습니다.|  
|**rowguid**|**uniqueidentifier**|충돌 행의 행 식별자입니다.|  
|**ModifiedDate**|**datetime**|충돌이 발생한 시간입니다.|  
|**원본\_데이터\_원본 id**|**uniqueidentifier**|해당 행 변경이 취소되었거나 충돌 내용이 손실된 구독입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
