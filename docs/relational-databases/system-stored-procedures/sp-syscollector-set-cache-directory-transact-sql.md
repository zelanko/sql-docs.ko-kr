---
description: sp_syscollector_set_cache_directory(Transact-SQL)
title: sp_syscollector_set_cache_directory (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ea0f5784b29ac235984e098f3b40d9ceafb2b12c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545928"
---
# <a name="sp_syscollector_set_cache_directory-transact-sql"></a>sp_syscollector_set_cache_directory(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  수집된 데이터를 관리 데이터 웨어하우스에 업로드하기 전에 저장할 디렉터리를 지정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_set_cache_directory [ @cache_directory = ] 'cache_directory'  
```  
  
## <a name="arguments"></a>인수  
`[ @cache_directory = ] 'cache_directory'` 수집 된 데이터가 임시로 저장 되는 파일 시스템의 디렉터리입니다. *cache_directory* 은 **nvarchar (255)** 이며 기본값은 NULL입니다. 값을 지정하지 않으면 기본 임시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리가 사용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 캐시 디렉터리 구성을 변경하려면 먼저 데이터 수집기를 사용하지 않도록 설정해야 합니다. 데이터 수집기를 사용하면 이 저장 프로시저가 실패합니다. 자세한 내용은 [데이터 컬렉션 활성화 또는 비활성화](../../relational-databases/data-collection/enable-or-disable-data-collection.md)및 [데이터 컬렉션 관리](../../relational-databases/data-collection/manage-data-collection.md)를 참조 하세요.  
  
 Sp_syscollector_set_cache_directory 실행 될 때 지정 된 디렉터리가 존재 하지 않아도 됩니다. 그러나 디렉터리를 만들 때까지 데이터를 성공적으로 캐시 하 고 업로드할 수 없습니다. 따라서 이 저장 프로시저를 실행하기 전에 지정된 디렉터리를 만드는 것이 좋습니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행하려면 dc_admin(EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 데이터 수집기를 사용 하지 않도록 설정 하 고 데이터 수집기의 캐시 디렉터리를로 설정한 `D:\tempdata` 다음 데이터 수집기를 사용 하도록 설정 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_window&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
