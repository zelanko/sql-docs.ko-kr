---
title: sp_addtabletocontents (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addtabletocontents_TSQL
- sp_addtabletocontents
helpviewer_keywords:
- sp_addtabletocontents
ms.assetid: 2ea27001-74f4-463e-bf1b-b6b5a86b9219
author: stevestein
ms.author: sstein
ms.openlocfilehash: e9d5e0e22f5dcca3611923782786a83ada1672ca
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68117917"
---
# <a name="sp_addtabletocontents-transact-sql"></a>sp_addtabletocontents(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  원본 테이블을 검사하여 현재 추적 테이블에 없는 행이 있을 경우 병합 추적 테이블에 이 행에 대한 참조를 추가합니다. **Bcp**를 사용 하 여 대량의 데이터를 대량 로드 한 경우이 옵션을 사용 하 여 병합 추적 트리거를 실행 하지 않습니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addtabletocontents [ @table_name = ] 'table_name'  
    [ , [ @owner_name = ] 'owner_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @table_name = ] 'table_name'`테이블의 이름입니다. *table_name* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @owner_name = ] 'owner_name'`테이블 소유자의 이름입니다. *owner_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @filter_clause = ] 'filter_clause'`새로 로드 된 데이터의 행을 병합 추적 테이블에 추가 해야 하는 행을 제어 하는 필터 절을 지정 합니다. *filter_clause* 은 **nvarchar (4000)** 이며 기본값은 NULL입니다. *Filter_clause* **null**이면 대량 로드 된 모든 행이 추가 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addtabletocontents** 는 병합 복제 에서만 사용 됩니다.  
  
 *Table_name* 의 행은 **rowguidcol** 에 의해 참조 되며 병합 추적 테이블에 참조가 추가 됩니다. 병합 복제를 사용 하 여 게시 된 테이블로 데이터를 대량 복사 하 고 나면 **sp_addtabletocontents** 를 사용 해야 합니다. 저장 프로시저는 복사된 행의 추적을 시작하며 새 행이 다음 동기화에 포함될 것인지 확인합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addtabletocontents**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
