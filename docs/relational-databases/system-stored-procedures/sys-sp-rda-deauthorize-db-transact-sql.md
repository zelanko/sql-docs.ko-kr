---
title: sys.sp_rda_deauthorize_db (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: stored-procedures
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_deauthorize_db
- sys.sp_rda_deauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_deauthorize_db stored procedure
ms.assetid: 2e362e15-2cd5-4856-9f0b-54df56b0866b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8ec00c03f479929b029b137919aef0e816e0be31
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979085"
---
# <a name="syssprdadeauthorizedb-transact-sql"></a>sys.sp_rda_deauthorize_db (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  로컬 스트레치 사용 데이터베이스와 원격 Azure 데이터베이스 간의 인증된 된 연결을 제거합니다. 실행할 **sp_rda_deauthorize_db** 원격 데이터베이스를 연결할 수 없거나 일관 되지 않은 상태의 및 데이터베이스의 모든 스트레치 사용 테이블에 대 한 쿼리 동작을 변경 하려는 경우.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_rda_deauthorize_db   
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 >0(실패)  
  
## <a name="permissions"></a>사용 권한  
 Db_owner 권한이 필요합니다.  
  
## <a name="remarks"></a>Remarks  
 실행 한 후 **sp_rda_deauthorize_db** , 스트레치 사용 데이터베이스 및 테이블에 대 한 모든 쿼리가 실패 합니다. 즉, 쿼리 모드를 사용 하지 않도록 설정 됩니다. 이 모드를 종료 하려면 다음 중 하나를 수행 합니다.  
  
-   실행할 [sys.sp_rda_reauthorize_db &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 원격 Azure 데이터베이스에 다시 연결 합니다. 이 작업이 자동으로 다시 설정 쿼리 모드를 LOCAL_AND_REMOTE를 Stretch Database 대 한 기본 동작 합니다. 즉, 쿼리는 로컬 및 원격 데이터에서 결과 반환합니다.  
  
-   실행 [sys.sp_rda_set_query_mode &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) 계속 해 서만 로컬 데이터에 대해 실행 하는 쿼리 수 있도록 LOCAL_ONLY 인수를 사용 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.sp_rda_set_query_mode &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)   
 [sys.sp_rda_reauthorize_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
