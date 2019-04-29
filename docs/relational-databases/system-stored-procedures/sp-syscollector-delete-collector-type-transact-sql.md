---
title: sp_syscollector_delete_collector_type (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_delete_collector_type
- sp_syscollector_delete_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_delete_collector_type
ms.assetid: 3f32905e-0005-42cb-aef1-7bd04c51fbac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e7f36eb20b4a5f72ce980f8e35cb39580f4f5142
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004183"
---
# <a name="spsyscollectordeletecollectortype-transact-sql"></a>sp_syscollector_delete_collector_type(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  수집기 형식의 정의를 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_delete_collector_type [[ @collector_type_uid = ] 'collector_type_uid' ]  
          , [[ @name = ] 'name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @collector_type_uid = ] 'collector_type_uid'` 수집기 형식에 대 한 GUID입니다. *collector_type_uid* 됩니다 **uniqueidentifier** 경우 값이 있어야 하 고 *이름* NULL입니다.  
  
`[ @name = ] 'name'` 수집기 유형의 이름이입니다. *이름* 됩니다 **sysname** 하는 경우 값이 있어야 하 고 *collector_type_uid* NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 어느 *collector_type_uid* 또는 *이름* 해야 값, 둘 다 NULL 일 수 없습니다.  
  
 이 수집기 형식의 컬렉션 항목이 있으면 이 프로시저에서 오류가 발생됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **dc_admin** (EXECUTE 권한 있음)와이 프로시저를 실행 하려면 고정된 데이터베이스 역할.  
  
## <a name="example"></a>예제  
 이 예에서는 일반 T-SQL 쿼리 수집기 형식을 삭제합니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_delete_collector_type @collector_type_uid = '302E93D1-3424-4be7-AA8E-84813ECF2419';  
```  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)  
  
  
