---
title: sp_deletetracertokenhistory (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletetracertokenhistory
- sp_deletetracertokenhistory_TSQL
helpviewer_keywords:
- sp_deletetracertokenhistory
ms.assetid: 9ae1be14-0d2f-40b1-9d6e-22d79726abf4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f84cd1cbb9a49f0c13a93fdff721f430983088ca
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955974"
---
# <a name="spdeletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

추적 프로그램 토큰 레코드를 제거 합니다 [MStracer_tokens &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) 하 고 [MStracer_history &#40;Transact SQL&#41; ](../../relational-databases/system-tables/mstracer-history-transact-sql.md) 시스템 테이블입니다. 이 저장 프로시저는 게시 데이터베이스의 게시자 또는 배포 데이터베이스의 배포자에서 실행됩니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```
sp_deletetracertokenhistory [ @publication = ] 'publication'
    [ , [ @tracer_id = ] tracer_id ]
    [ , [ @cutoff_date = ] cutoff_date ]
    [ , [ @publisher = ] 'publisher' ]
    [ , [ @publisher_db = ] 'publisher_db' ]
```

## <a name="arguments"></a>인수

`@publication= 'publication'`  
추적 프로그램 토큰이 삽입된 게시의 이름입니다. 데이터 형식이 **sysname**합니다. 이 매개 변수는 필수적 요소입니다.

`[ @tracer_id= ] tracer_id`  
삭제할 추적 프로그램 토큰의 ID입니다. 데이터 형식이 **int**합니다. 기본값은 *null*합니다. 하는 경우 *null*, 게시에 속한 모든 추적 프로그램 토큰이 삭제 됩니다.

`[ @cutoff_date= ] cutoff_date`  
이 날짜를 삭제 하기 전에 게시에 삽입 하는 추적 프로그램 토큰입니다. 데이터 형식이 **날짜/시간**합니다. 기본값은 *null*합니다.

`[ @publisher= ] 'publisher'`  
게시자의 이름입니다. 데이터 형식이 **sysname**합니다. 기본값은 *null*합니다.

> [!NOTE]
> 에 대 한에이 매개 변수를 지정 해야 이외 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자 또는 배포자에서 저장된 프로시저를 실행 하는 경우.

`[ @publisher_db= ] 'publisher_db'`  
게시 데이터베이스의 이름입니다. 데이터 형식이 **sysname**합니다. 기본값은 NULL입니다. 이 매개 변수는 게시자에서 저장 프로시저가 실행될 경우 무시됩니다.

> [!NOTE]
> 배포자에서 저장된 프로시저를 실행할 때이 매개 변수를 지정 해야 합니다.

## <a name="return-code-values"></a>반환 코드 값

**0** (성공) 또는 **1** (실패)

## <a name="remarks"></a>Remarks

**sp_deletetracertokenhistory** 트랜잭션 복제에 사용 됩니다.  

두 매개 변수를 지정 하는 경우 오류가 발생 *tracer_id* 하 고 *cutoff_date*합니다.

실행할 수 없는 경우 **sp_deletetracertokenhistory** 추적 프로그램 토큰 메타 데이터를 삭제 하려면 정보를 삭제할 정기적으로 예약 된 기록 정리가 발생 합니다.

실행 하 여 추적 프로그램 토큰 Id를 확인할 수 있습니다 [sp_helptracertokens &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) 쿼리 해 합니다 [MStracer_tokens &#40;Transact SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) 시스템 테이블.

## <a name="permissions"></a>사용 권한

다음 담당자 실행 수 있는 권한이 **sp_deletetracertokenhistory**:

- 멤버는 **replmonitor** 배포 데이터베이스의 역할
- 멤버는 **sysadmin** 고정된 서버 역할입니다.
- 멤버는 **db_owner** 게시 데이터베이스의 고정된 데이터베이스 역할을 합니다.
- 합니다 **db_owner** 고정된 데이터베이스입니다.

## <a name="see-also"></a>관련 항목

[트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

[sp_helptracertokenhistory &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)
