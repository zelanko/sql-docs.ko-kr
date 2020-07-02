---
title: sp_syscollector_delete_collector_type (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f3b9a8dd128bab509c4cfd760e097bc33ae2508e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725563"
---
# <a name="sp_syscollector_delete_collector_type-transact-sql"></a>sp_syscollector_delete_collector_type(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  수집기 형식의 정의를 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_delete_collector_type [[ @collector_type_uid = ] 'collector_type_uid' ]  
          , [[ @name = ] 'name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @collector_type_uid = ] 'collector_type_uid'`수집기 유형의 GUID입니다. *collector_type_uid* 은 **UNIQUEIDENTIFIER** 이며 *이름이* NULL 인 경우 값이 있어야 합니다.  
  
`[ @name = ] 'name'`수집기 유형의 이름입니다. *name* 은 **SYSNAME** 이며 *collector_type_uid* NULL 인 경우 값이 있어야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 *Collector_type_uid* 또는 *이름* 에는 값이 있어야 하며 둘 다 NULL 일 수 없습니다.  
  
 이 수집기 형식의 컬렉션 항목이 있으면 이 프로시저에서 오류가 발생됩니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행 하려면 **dc_admin** (실행 권한 포함) 고정 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="example"></a>예제  
 이 예에서는 일반 T-SQL 쿼리 수집기 형식을 삭제합니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_delete_collector_type @collector_type_uid = '302E93D1-3424-4be7-AA8E-84813ECF2419';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 수집](../../relational-databases/data-collection/data-collection.md)  
  
  
