---
title: sys. sp_rda_set_query_mode (Transact-sql) | Microsoft Docs
description: 현재 스트레치 사용 데이터베이스 및 해당 테이블에 대 한 쿼리가 로컬 및 원격 데이터 또는 로컬 데이터만 반환 하는지 여부를 지정 하려면 sp_rda_set_query_mode을 사용 합니다.
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 26b8a363de2faf9e39bc88e3dd1e0a26bd016e16
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540454"
---
# <a name="syssp_rda_set_query_mode-transact-sql"></a>sys. sp_rda_set_query_mode (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  현재 스트레치 사용 데이터베이스 및 해당 테이블에 대 한 쿼리가 로컬 및 원격 데이터 (기본값) 또는 로컬 데이터만 반환할지 여부를 지정 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>인수  
 [ @mode =] * \@ 모드*  
 는 다음 값 중 하나입니다.  
  
-   **사용 안 함** 스트레치 사용 테이블에 대 한 모든 쿼리가 실패 합니다.  
  
-   **LOCAL_ONLY** 스트레치 사용 테이블에 대 한 쿼리는 로컬 데이터만 반환 합니다.  
  
-   **LOCAL_AND_REMOTE** 스트레치 사용 테이블에 대 한 쿼리는 로컬 및 원격 데이터를 모두 반환 합니다. 기본 동작입니다.  
  
 [ @force =] * \@ force*  
 는 유효성 검사 없이 쿼리 모드를 변경 하려는 경우 1로 설정할 수 있는 선택적 비트 값입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0 (성공) 또는 >0 (실패)  
  
## <a name="permissions"></a>사용 권한  
 Db_owner 권한이 필요 합니다.  
  
## <a name="remarks"></a>설명  
 다음 확장 저장 프로시저는 스트레치 사용 데이터베이스에 대해서도 쿼리 모드를 설정 합니다.  
  
-   **sp_rda_deauthorize_db**  
  
     **Sp_rda_deauthorize_db** 를 실행 하면 스트레치 사용 데이터베이스 및 테이블에 대 한 모든 쿼리가 실패 합니다. 즉, 쿼리 모드는 사용 안 함으로 설정 됩니다. 이 모드를 종료 하려면 다음 작업 중 하나를 수행 합니다.  
  
    -   [Sp_rda_reauthorize_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 를 실행 하 여 원격 Azure 데이터베이스에 다시 연결 합니다. 이 작업은 자동으로 쿼리 모드를 LOCAL_AND_REMOTE으로 다시 설정 합니다 .이는 Stretch Database의 기본 동작입니다. 즉, 쿼리는 로컬 및 원격 데이터에서 결과를 반환 합니다.  
  
    -   LOCAL_ONLY 인수를 사용 하 여 [sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) 를 실행 하 여 쿼리가 로컬 데이터에 대해서만 계속 실행 되도록 합니다.  
  
-   **sp_rda_reauthorize_db**  
  
     [Sp_rda_reauthorize_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 를 실행 하 여 원격 Azure 데이터베이스에 다시 연결 하는 경우이 작업은 자동으로 쿼리 모드를 Stretch Database에 대 한 기본 동작인 LOCAL_AND_REMOTE으로 다시 설정 합니다. 즉, 쿼리는 로컬 및 원격 데이터에서 결과를 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [sp_rda_deauthorize_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
