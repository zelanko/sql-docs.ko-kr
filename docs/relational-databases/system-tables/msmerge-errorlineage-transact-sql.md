---
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d6502c32f47668cbd2ce78ec91296ce61767a95f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889803"
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
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
