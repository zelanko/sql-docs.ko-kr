---
title: sp_dbcmptlevel (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8c1d563e64769768a4c317bc0411eb40fb82b8d8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786199"
---
# <a name="sp_dbcmptlevel-transact-sql"></a>sp_dbcmptlevel(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  특정 데이터베이스 동작이 지정된 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 호환되도록 설정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]대신 [ALTER Database 호환성 수준을](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dbcmptlevel [ [ @dbname = ] name ]   
    [ , [ @new_cmptlevel = ] version ]  
```  
  
## <a name="arguments"></a>인수  
`[ @dbname = ] name`호환성 수준을 변경할 데이터베이스의 이름입니다. 데이터베이스 이름은 식별자에 대한 규칙을 따라야 합니다. *name* 은 **sysname**이며 기본값은 NULL입니다.  
  
`[ @new_cmptlevel = ] version`데이터베이스가 호환 되도록 설정할의 버전입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *version* 은 **tinyint**이며 기본값은 NULL입니다. 값은 다음 중 하나여야 합니다.  
  
 **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 매개 변수를 지정 하지 않거나 *name* 매개 변수를 지정 하지 않으면 **sp_dbcmptlevel** 에서 오류를 반환 합니다.  
  
 *Name* 이 *버전*없이 지정 된 경우는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 지정 된 데이터베이스의 현재 호환성 수준을 표시 하는 메시지를 반환 합니다.  
  
## <a name="remarks"></a>설명  
 호환성 수준에 대 한 설명은 [ALTER Database Compatibility Level &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)를 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스 소유자, **sysadmin** 고정 서버 역할의 멤버 및 고정 데이터베이스 역할 **db_owner** (현재 데이터베이스를 변경 하는 경우)에만이 프로시저를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [예약 키워드&#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
