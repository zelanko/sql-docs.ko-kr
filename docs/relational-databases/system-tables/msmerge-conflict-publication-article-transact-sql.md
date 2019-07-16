---
title: MSmerge_conflict_&lt;발행물&gt;_&lt;문서&gt; (TRANSACT-SQL) | Microsoft Docs
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
ms.openlocfilehash: dfae18a55ddb8b1c95aad25e27f006b28fde79af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895108"
---
# <a name="msmergeconflictltpublicationgtltarticlegt-transact-sql"></a>MSmerge_conflict_&lt;발행물&gt;_&lt;문서&gt; (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSmerge_conflict_*게시*_ * 문서*** 테이블을 데이터 일치성을 얻기 위해 취소 된 행 변경 내용 또는 충돌 하는 행에 정보를 포함 합니다. 게시 안에 각 복제 테이블에 대한 충돌 테이블이 존재하는데 충돌 테이블 이름 끝에 게시 및 아티클 이름이 붙습니다. 이러한 아티클별 충돌 테이블은 충돌 기록을 위해 사용하는 데이터베이스에 존재하는데 대체로 게시 데이터베이스에 존재하지만 충돌을 분산하여 기록할 때는 구독 데이터베이스에 존재할 수도 있습니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|***article_column_name***|**variable**|복제된 테이블의 열을 나타냅니다. 이 시스템 테이블에는 테이블 아티클에 있는 각 열에 대한 열이 하나씩 있습니다.|  
|**rowguid**|**uniqueidentifier**|충돌 행의 행 식별자입니다.|  
|**ModifiedDate**|**datetime**|충돌이 발생한 시간입니다.|  
|**origin_datasource_id**|**uniqueidentifier**|해당 행 변경이 취소되었거나 충돌 내용이 손실된 구독입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
