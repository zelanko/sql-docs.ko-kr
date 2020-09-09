---
description: MSmerge_errorlineage(Transact-SQL)
title: MSmerge_errorlineage (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e6b7893c684db25c6a0dcfd4e7ae9cc2d6445065
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540317"
---
# <a name="msmerge_errorlineage-transact-sql"></a>MSmerge_errorlineage(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_errorlineage** 테이블은 구독자에서 삭제 되었지만 해당 삭제가 게시자에 전파 되지 않은 행을 포함 합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|병합 복제용으로 게시된 테이블에 할당된 정수 값입니다. **Sysmergearticles** 테이블의 애칭 필드에 해당 합니다.|  
|**rowguid**|**uniqueidentifier**|행 식별자입니다.|  
|**계보**|**varbinary (501)**|구독자와 게시자가 행을 업데이트한 내용의 기록 목록을 저장합니다. 충돌 상황을 발견하고 해결하기 위해 사용합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
