---
title: sp_syscollector_set_cache_directory (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_directory_TSQL
- sp_syscollector_set_cache_directory
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_set_cache_directory stored procedure
ms.assetid: df56d5a5-8961-494f-a745-d752ca63805a
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2fec21ffdac0ee58f6927935942fedadda563f0f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260889"
---
# <a name="spsyscollectorsetcachedirectory-transact-sql"></a>sp_syscollector_set_cache_directory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  수집된 데이터를 관리 데이터 웨어하우스에 업로드하기 전에 저장할 디렉터리를 지정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_set_cache_directory [ @cache_directory = ] 'cache_directory'  
```  
  
## <a name="arguments"></a>인수  
 [ **@cache_directory =** ] **'***cache_directory***'**  
 수집된 데이터가 임시로 저장되는 파일 시스템의 디렉터리입니다. *cache_directory* 은 **nvarchar (255)**, 기본값은 NULL입니다. 값을 지정하지 않으면 기본 임시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리가 사용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 캐시 디렉터리 구성을 변경하려면 먼저 데이터 수집기를 사용하지 않도록 설정해야 합니다. 데이터 수집기를 사용하면 이 저장 프로시저가 실패합니다. 자세한 내용은 참조 [사용 또는 사용 데이터 컬렉션 사용 안 함](../../relational-databases/data-collection/enable-or-disable-data-collection.md), 및 [데이터 컬렉션 관리](../../relational-databases/data-collection/manage-data-collection.md)합니다.  
  
 sp_syscollector_set_cache_directory가 실행될 때는 지정된 디렉터리가 없어도 되지만 데이터를 성공적으로 캐시하고 업데이트하려면 이 디렉터리를 만들어야 합니다. 따라서 이 저장 프로시저를 실행하기 전에 지정된 디렉터리를 만드는 것이 좋습니다.  
  
## <a name="permissions"></a>Permissions  
 이 프로시저를 실행하려면 dc_admin(EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터 수집기를 사용 하지 않도록 설정, 데이터 수집기에 대 한 캐시 디렉터리를 설정 `D:\tempdata`를 설정한 다음 데이터 수집기를 활성화 하 고 있습니다.  
  
```sql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXEC dbo.sp_syscollector_set_cache_directory N'D:\tempdata';  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_window&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
