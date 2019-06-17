---
title: sp_syscollector_set_cache_window (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_window
- sp_syscollector_set_cache_window_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_set_cache_window stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 660f2749-392f-46bf-89f3-27764d848507
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fd261178b852e8e890dd654893ce8fc167a15915
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63004301"
---
# <a name="spsyscollectorsetcachewindow-transact-sql"></a>sp_syscollector_set_cache_window(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  실패한 데이터 업로드의 시도 횟수를 설정합니다. 오류가 발생 시 업로드를 다시 시도하면 수집된 데이터의 손실 위험을 완화할 수 있습니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_set_cache_window [ @cache_window = ] cache_window   
```  
  
## <a name="arguments"></a>인수  
 [ @cache_window = ] *cache_window*  
 데이터 손실이 없는 오류 발생 시에 관리 데이터 웨어하우스에 대한 데이터 업로드를 다시 시도하는 횟수입니다. *cache_window* 됩니다 **int** 1의 기본값입니다. *cache_window* 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|-1|실패한 이전 업로드의 업로드 데이터를 모두 캐시합니다.|  
|0|실패한 업로드의 데이터를 캐시하지 않습니다.|  
|*n*|N 실패 한 이전 업로드의에서 데이터를 캐시 합니다. 여기서 *n* > = 1입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 캐시 시간대 구성을 변경하려면 먼저 데이터 수집기를 사용하지 않도록 설정해야 합니다. 데이터 수집기를 사용하면 이 저장 프로시저가 실패합니다. 자세한 내용은 [사용 또는 사용 데이터 컬렉션 사용 안 함](../../relational-databases/data-collection/enable-or-disable-data-collection.md), 및 [데이터 컬렉션 관리](../../relational-databases/data-collection/manage-data-collection.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행하려면 dc_admin(EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터 수집기를 사용하지 않도록 설정하고 3회까지 실패한 업로드의 데이터를 보존하는 캐시 시간대를 구성한 다음 데이터 수집기를 다시 사용하도록 설정합니다.  
  
```sql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXECUTE dbo.sp_syscollector_set_cache_window 3;  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
```  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_directory&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)  
  
  
