---
title: sys. sp_rda_deauthorize_db (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_deauthorize_db
- sys.sp_rda_deauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_deauthorize_db stored procedure
ms.assetid: 2e362e15-2cd5-4856-9f0b-54df56b0866b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bc01f07e3a07200970066e6ed505b29b3ccb9c09
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053406"
---
# <a name="syssp_rda_deauthorize_db-transact-sql"></a>sys. sp_rda_deauthorize_db (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  로컬 스트레치 사용 데이터베이스와 원격 Azure 데이터베이스 간의 인증 된 연결을 제거 합니다. 원격 데이터베이스에 연결할 수 없거나 일관 되지 않은 상태에 있을 때 데이터베이스의 모든 스트레치 사용 테이블에 대 한 쿼리 동작을 변경 하려는 경우 **sp_rda_deauthorize_db** 를 실행 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_rda_deauthorize_db   
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0 (성공) 또는 >0 (실패)  
  
## <a name="permissions"></a>사용 권한  
 Db_owner 권한이 필요 합니다.  
  
## <a name="remarks"></a>설명  
 **Sp_rda_deauthorize_db** 를 실행 하면 스트레치 사용 데이터베이스 및 테이블에 대 한 모든 쿼리가 실패 합니다. 즉, 쿼리 모드는 사용 안 함으로 설정 됩니다. 이 모드를 종료 하려면 다음 작업 중 하나를 수행 합니다.  
  
-   [Sp_rda_reauthorize_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 를 실행 하 여 원격 Azure 데이터베이스에 다시 연결 합니다. 이 작업은 자동으로 쿼리 모드를 LOCAL_AND_REMOTE으로 다시 설정 합니다 .이는 Stretch Database의 기본 동작입니다. 즉, 쿼리는 로컬 및 원격 데이터에서 결과를 반환 합니다.  
  
-   LOCAL_ONLY 인수를 사용 하 여 [transact-sql&#41;&#40;sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) 실행 하 여 쿼리가 로컬 데이터에 대해서만 계속 실행 되도록 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [sp_rda_set_query_mode &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)   
 [sp_rda_reauthorize_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
