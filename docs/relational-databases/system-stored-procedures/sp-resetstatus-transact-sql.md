---
title: sp_resetstatus (TRANSACT-SQL) | Microsoft Docs
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
- sp_resetstatus
- sp_resetstatus_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_resetstatus
ms.assetid: b892727f-ea3b-4b94-88d9-f2386ad4962c
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5bb03b3447698fe8e72168b86373c518418bc0db
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025309"
---
# <a name="spresetstatus-transact-sql"></a>sp_resetstatus(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  주의 대상 데이터베이스의 상태를 다시 설정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_resetstatus [ @dbname = ] 'database'  
```  
  
## <a name="arguments"></a>인수  
 [ @dbname=] '*데이터베이스*'  
 재설정할 데이터베이스의 이름입니다. *데이터베이스* 됩니다 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 sp_resetstatus는 데이터베이스에서 주의 대상 플래그를 해제합니다. 이 프로시저는 sys.databases에서 명명된 데이터베이스의 모드 및 상태 열을 업데이트합니다. 이 프로시저를 실행하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 대해 문의하여 모든 문제점을 해결해야 합니다. sp_resetstatus를 실행한 후에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스를 중지한 후 다시 시작합니다.  
  
 데이터베이스는 여러 가지 이유로 주의 대상이 됩니다. 운영 시스템에 의해 데이터베이스 리소스에 대한 액세스가 거부되거나 하나 이상의 데이터베이스 파일이 사용 불가능하거나 손상되어 주의 대상이 될 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 sysadmin 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks2012` 데이터베이스의 상태를 다시 설정합니다.  
  
```  
EXEC sp_resetstatus 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
