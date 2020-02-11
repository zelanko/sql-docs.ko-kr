---
title: sp_syscollector_enable_collector (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_enable_collector
- sp_syscollector_enable_collector_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_enable_collector
- data collector [SQL Server], stored procedures
ms.assetid: 53ff2b0d-b7da-4e3d-8f3d-35e857bc3720
author: stevestein
ms.author: sstein
ms.openlocfilehash: ab6087b68fba057e6acd91f43804b0e324992e1d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68000811"
---
# <a name="sp_syscollector_enable_collector-transact-sql"></a>sp_syscollector_enable_collector(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터 수집기를 사용하도록 설정합니다. 데이터 수집기는 서버마다 하나뿐이므로 매개 변수가 필요하지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
dbo.sp_syscollector_enable_collector   
```  
  
## <a name="arguments"></a>인수  
 None  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 기본값은 서버의 데이터 수집기입니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행하려면 **dc_admin** 또는 **dc_operator** (EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터 수집기를 사용하도록 설정합니다.  
  
```sql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_enable_collector;  
```  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 수집](../../relational-databases/data-collection/data-collection.md)  
  
  
