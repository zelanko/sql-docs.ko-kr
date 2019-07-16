---
title: sp_dbremove (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbremove
- sp_dbremove_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbremove
ms.assetid: a8513f4a-c025-49c8-99c3-4c83cb7f51ed
author: stevestein
ms.author: sstein
ms.openlocfilehash: ea264c48332f6e72a5f26b330e42cfb1e3d3ff8d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061248"
---
# <a name="spdbremove-transact-sql"></a>sp_dbremove(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 및 이에 연관된 모든 파일을 제거합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하는 것이 좋습니다 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dbremove [ @dbname = ] 'database' [ , [ @dropdev = ] 'dropdev' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @dbname = ] 'database'` 제거할 데이터베이스의 이름이입니다. *데이터베이스* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @dropdev = ] 'dropdev'` 이전 버전과 호환성을 위해서만 제공 하는 플래그 이며 현재는 무시 됩니다. *dropdev* 기본값이 **dropdev**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `sales`라는 데이터베이스 및 이와 연관된 모든 파일을 제거합니다.  
  
```  
EXEC sp_dbremove sales;  
```  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
 [sp_detach_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
  
