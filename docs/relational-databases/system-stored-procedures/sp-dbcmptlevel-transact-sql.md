---
title: sp_dbcmptlevel (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbcmptlevel
- sp_dbcmptlevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbcmptlevel
ms.assetid: 508c686d-2bd4-41ba-8602-48ebca266659
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 96bd1aa87dba90963588db74935294c0dcdd8f0b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527431"
---
# <a name="spdbcmptlevel-transact-sql"></a>sp_dbcmptlevel(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  특정 데이터베이스 동작이 지정된 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 호환되도록 설정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 사용 하 여 [ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dbcmptlevel [ [ @dbname = ] name ]   
    [ , [ @new_cmptlevel = ] version ]  
```  
  
## <a name="arguments"></a>인수  
`[ @dbname = ] name` 호환성 수준이 변경 되는 데이터베이스의 이름이입니다. 데이터베이스 이름은 식별자에 대한 규칙을 따라야 합니다. *이름* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @new_cmptlevel = ] version` 버전이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하 여 데이터베이스가 호환 수 있습니다. *버전* 됩니다 **tinyint**, 기본값은 NULL입니다. 값은 다음 중 하나여야 합니다.  
  
 **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 매개 변수 없이 지정 된 경우 또는 경우는 *이름을* 매개 변수를 지정 하지 않으면 **sp_dbcmptlevel** 오류를 반환 합니다.  
  
 하는 경우 *이름을* 없이 지정 된 *버전*는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 지정한 데이터베이스의 현재 호환성 수준을 표시 하는 메시지를 반환 합니다.  
  
## <a name="remarks"></a>Remarks  
 호환성 수준에 대 한 참조 [ALTER DATABASE 호환성 수준 &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스 소유자의 멤버는 **sysadmin** 고정 서버 역할, 및 **db_owner** 고정된 데이터베이스 역할 (현재 데이터베이스를 변경 하려는) 하는 경우이 프로시저를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [예약 키워드&#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
