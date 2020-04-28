---
title: sp_syscollector_stop_collection_set (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_stop_collection_set_TSQL
- sp_syscollector_stop_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_stop_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 4668cfb7-462f-40d0-948c-8f740a792a4d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3e09efe938dabb031e1c57020f051cd5ab03e55a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68010573"
---
# <a name="sp_syscollector_stop_collection_set-transact-sql"></a>sp_syscollector_stop_collection_set(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  컬렉션 집합을 중지합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_stop_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @stop_collection_job = ] stop_collection_job ]  
```  
  
## <a name="arguments"></a>인수  
 [ @collection_set_id = ] *collection_set_id*  
 컬렉션 집합의 고유한 로컬 식별자입니다. *collection_set_id* 은 **int** 이며 기본값은 NULL입니다. *name* 이 NULL 인 경우 *collection_set_id* 에 값이 있어야 합니다.  
  
 [ @name = ] '*이름*'  
 컬렉션 집합의 이름입니다. *name* 은 **sysname** 이며 기본값은 NULL입니다. *collection_set_id* 가 NULL 이면 *이름* 에 값이 있어야 합니다.  
  
 [ @stop_collection_job = ] *stop_collection_job*  
 컬렉션 집합의 컬렉션 작업이 실행 중인 경우 중단하도록 지정합니다. *stop_collection_job* 은 **bit** 이며 기본값은 1입니다.  
  
 *stop_collection_job* 는 컬렉션 모드가 cached로 설정 된 컬렉션 집합에만 적용 됩니다. 자세한 내용은 [sp_syscollector_create_collection_set &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)를 참조 하세요.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_syscollector_create_collection_set은 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행하려면 dc_operator(EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 해당 식별자를 사용하여 컬렉션 집합을 중지합니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_stop_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 수집](../../relational-databases/data-collection/data-collection.md)   
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
