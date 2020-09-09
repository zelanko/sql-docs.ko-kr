---
description: sp_deletetracertokenhistory(Transact-SQL)
title: sp_deletetracertokenhistory (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c08b5373109ab3ea6174aac190ed8fb7b04b2e0e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543541"
---
# <a name="sp_deletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory(Transact-SQL)

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

[MStracer_tokens &#40;transact-sql&#41;](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) 에서 추적 프로그램 토큰 레코드를 제거 하 고 [&#40;transact-sql&#41;](../../relational-databases/system-tables/mstracer-history-transact-sql.md) 시스템 테이블을 MStracer_history 합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자 또는 배포 데이터베이스의 배포자에서 실행됩니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

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
추적 프로그램 토큰이 삽입된 게시의 이름입니다. 데이터 형식은 **sysname**입니다. 이 매개 변수는 필수입니다.

`[ @tracer_id= ] tracer_id`  
삭제할 추적 프로그램 토큰의 ID입니다. 데이터 형식이 **int**입니다. 기본값은 *null*입니다. *Null*인 경우 게시에 속한 모든 추적 프로그램 토큰이 삭제 됩니다.

`[ @cutoff_date= ] cutoff_date`  
이 날짜 이전에 게시에 삽입 된 추적 프로그램 토큰입니다. 데이터 형식이 **datetime**입니다. 기본값은 *null*입니다.

`[ @publisher= ] 'publisher'`  
게시자의 이름입니다. 데이터 형식은 **sysname**입니다. 기본값은 *null*입니다.

> [!NOTE]
> 이 매개 변수는 이외 게시자에 대해서만 지정 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 배포자에서 저장 프로시저를 실행 하는 경우에만 지정 해야 합니다.

`[ @publisher_db= ] 'publisher_db'`  
게시 데이터베이스의 이름입니다. 데이터 형식은 **sysname**입니다. 기본값은 NULL입니다. 이 매개 변수는 게시자에서 저장 프로시저가 실행될 경우 무시됩니다.

> [!NOTE]
> 이 매개 변수는 배포자에서 저장 프로시저를 실행할 때 지정 해야 합니다.

## <a name="return-code-values"></a>반환 코드 값

**0** (성공) 또는 **1** (실패)

## <a name="remarks"></a>설명

**sp_deletetracertokenhistory** 은 트랜잭션 복제에 사용 됩니다.  

*Tracer_id* 와 *cutoff_date*매개 변수를 모두 지정 하면 오류가 발생 합니다.

**Sp_deletetracertokenhistory** 를 실행 하 여 추적 프로그램 토큰 메타 데이터를 삭제 하는 경우 정기적으로 예약 된 기록 정리가 수행 될 때 정보가 삭제 됩니다.

추적 프로그램 토큰 Id는 [transact-sql&#41;&#40;sp_helptracertokens ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) 실행 [MStracer_tokens 하거나 transact-sql &#40;](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) 시스템 테이블을&#41;하 여 확인할 수 있습니다.

## <a name="permissions"></a>사용 권한

다음 직원만 **sp_deletetracertokenhistory**를 실행할 수 있습니다.

- 배포 데이터베이스에서 **replmonitor** 역할의 멤버
- **Sysadmin** 고정 서버 역할의 멤버입니다.
- 게시 데이터베이스에 있는 **db_owner** 고정 데이터베이스 역할의 멤버입니다.
- 고정 데이터베이스의 **db_owner** 입니다.

## <a name="see-also"></a>참고 항목

[트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

[Transact-sql&#41;sp_helptracertokenhistory &#40;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)
