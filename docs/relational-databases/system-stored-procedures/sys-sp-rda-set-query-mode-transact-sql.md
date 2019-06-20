---
title: sys.sp_rda_set_query_mode (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_query_mode
- sys.sp_rda_set_query_mode_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_query_mode stored procedure
ms.assetid: 65a0b390-cf87-4db7-972a-1fdf13456c88
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: aa168f3bbac37e34730d5ee0ab348f5fd7d1743d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65982879"
---
# <a name="syssprdasetquerymode-transact-sql"></a>sys.sp_rda_set_query_mode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  로컬 및 원격 데이터 (기본값) 또는 로컬 데이터에만 현재 스트레치 사용 데이터베이스 및 해당 테이블에 대 한 쿼리를 반환 하는지 여부를 지정 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>인수  
 [ @mode = ] *@mode*  
 다음 값 중 하나입니다.  
  
-   **사용 안 함** 스트레치 사용 테이블에 대 한 모든 쿼리가 실패 합니다.  
  
-   **LOCAL_ONLY** 스트레치 사용 테이블에 대 한 쿼리 로컬 데이터만 반환 합니다.  
  
-   **LOCAL_AND_REMOTE** 스트레치 사용 테이블에 대 한 쿼리 로컬 및 원격 데이터를 반환 합니다. 이것이 기본 동작입니다.  
  
 [ @force = ]  *@force*  
 유효성 검사 없이 쿼리 모드를 변경 하려는 경우 1로 설정할 수 있는 선택적 비트 값이입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0 (성공) 또는 > 0 (실패)  
  
## <a name="permissions"></a>사용 권한  
 Db_owner 권한이 필요합니다.  
  
## <a name="remarks"></a>Remarks  
 다음 확장된 저장된 프로시저를 스트레치 사용 데이터베이스에 대 한 쿼리 모드를 설정할 수도 있습니다.  
  
-   **sp_rda_deauthorize_db**  
  
     실행 한 후 **sp_rda_deauthorize_db** , 스트레치 사용 데이터베이스 및 테이블에 대 한 모든 쿼리가 실패 합니다. 즉, 쿼리 모드를 사용 하지 않도록 설정 됩니다. 이 모드를 종료 하려면 다음 중 하나를 수행 합니다.  
  
    -   실행할 [sys.sp_rda_reauthorize_db &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 원격 Azure 데이터베이스에 다시 연결 합니다. 이 작업이 자동으로 다시 설정 쿼리 모드를 LOCAL_AND_REMOTE를 Stretch Database 대 한 기본 동작 합니다. 즉, 쿼리는 로컬 및 원격 데이터에서 결과 반환합니다.  
  
    -   실행할 [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) 계속 해 서만 로컬 데이터에 대해 실행 하는 쿼리 수 있도록 LOCAL_ONLY 인수를 사용 합니다.  
  
-   **sp_rda_reauthorize_db**  
  
     실행할 때 [sys.sp_rda_reauthorize_db &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 원격 Azure 데이터베이스에 다시 연결 하려면이 작업이 자동으로 다시 설정 쿼리 모드를 LOCAL_AND_REMOTE 기본 동작에 대 한 Stretch Database. 즉, 쿼리는 로컬 및 원격 데이터에서 결과 반환합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.sp_rda_deauthorize_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
