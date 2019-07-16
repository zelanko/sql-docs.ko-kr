---
title: MSmerge_errorlineage (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_errorlineage_TSQL
- MSmerge_errorlineage
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_errorlineage system table
ms.assetid: 3bcbd328-c958-4cd4-a573-3c35539fa919
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1c3191191a9830a38a177ba3a3c353e5c34dedba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044763"
---
# <a name="msmergeerrorlineage-transact-sql"></a>MSmerge_errorlineage(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSmerge_errorlineage** 테이블에 행이 구독자에서 삭제 하지만 게시자에 있는 삭제 전파 되지 않습니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|병합 복제용으로 게시된 테이블에 할당된 정수 값입니다. nickname 필드에 해당 하는 **sysmergearticles** 테이블입니다.|  
|**rowguid**|**uniqueidentifier**|행 식별자입니다.|  
|**lineage**|**varbinary(501)**|구독자와 게시자가 행을 업데이트한 내용의 기록 목록을 저장합니다. 충돌 상황을 발견하고 해결하기 위해 사용합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
