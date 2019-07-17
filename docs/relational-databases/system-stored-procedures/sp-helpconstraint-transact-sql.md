---
title: sp_helpconstraint (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpconstraint
- sp_helpconstraint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpconstraint
ms.assetid: 29d6cd36-535d-4765-bca8-62f9d9886ff5
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bd443a8e03663eb3fb46e75e09d852c797f6d427
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101378"
---
# <a name="sphelpconstraint-transact-sql"></a>sp_helpconstraint(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  모든 제약 조건의 유형, 제약 조건의 사용자 정의 또는 시스템 제공 이름, 제약 조건 유형을 정의한 열 및 제약 조건을 정의한 식(DEFAULT 및 CHECK 제약 조건만)의 목록을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpconstraint [ @objname = ] 'table'   
     [ , [ @nomsg = ] 'no_message' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @objname = ] 'table'` 제약 조건 정보를 반환할 테이블이입니다. 지정된 테이블은 반드시 현재 데이터베이스에 대해 로컬이어야 합니다. *테이블* 됩니다 **nvarchar(776)** , 기본값은 없습니다.  
  
`[ @nomsg = ] 'no_message'` 테이블 이름을 출력 하는 선택적 매개 변수가입니다. *no_message* 됩니다 **varchar(5)** , 기본값은 **msg**합니다. **nomsg** 인쇄를 표시 하지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 **sp_helpconstraint** 기본 키에 참여 하는 경우 내림차순으로 인덱싱된 열이 표시 됩니다. 내림차순으로 인덱싱된 열은 이름 다음에 빼기 기호(-)를 포함한 상태로 결과 집합에 나열됩니다. 기본값에 따라 오름차순으로 인덱싱된 열은 이름만 나열됩니다.  
  
## <a name="remarks"></a>설명  
 실행 **sp_help**_테이블_ 지정된 된 테이블에 대 한 모든 정보를 보고 합니다. 제약 조건 정보만 보려면 **sp_helpconstraint**합니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Product` 테이블에 대한 모든 제약 조건을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helpconstraint 'Production.Product';  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.key_constraints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys.check_constraints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.default_constraints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md)  
  
  
