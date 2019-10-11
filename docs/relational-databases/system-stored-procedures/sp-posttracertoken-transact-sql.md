---
title: sp_posttracertoken (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- posttracerttoken
- posttracerttoken_TSQL
- sp_posttracertoken
- sp_posttracertoken_TSQL
helpviewer_keywords:
- sp_posttracertoken
ms.assetid: 24da5cd2-1c45-475e-93db-5bdf660f1c2c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7629c25264f0b45d68e29e947b1d5c40d02707e7
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041177"
---
# <a name="sp_posttracertoken-transact-sql"></a>sp_posttracertoken(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 프로시저는 추적 프로그램 토큰을 게시자의 트랜잭션 로그에 게시하고 대기 시간 통계 추적 프로세스를 시작합니다. 추적 프로그램 토큰이 트랜잭션 로그에 기록될 때, 기록된 토큰을 로그 판독기 에이전트에서 선택할 때, 선택된 토큰을 배포 에이전트에서 적용할 때 각각 정보가 기록됩니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다. 자세한 내용은 [트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_posttracertoken [ @publication = ] 'publication'   
    [ , [ @tracer_token_id = ] tracer_token_id OUTPUT  
    [ , [ @publisher = ] 'publisher'   
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`은 대기 시간이 측정 되는 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @tracer_token_id = ] _tracer_token_id OUTPUT`은 삽입 된 추적 프로그램 토큰의 ID입니다. *tracer_token_id* 은 **int** 이며 기본값은 NULL이 고 OUTPUT 매개 변수입니다. 이 값은 [ &#40;&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md) sp_helptracertokens [ &#40;&#41; ](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md) [transact-sql을 먼저 실행 하지 않고 sp_helptracertokenhistory transact-sql 또는 sp_deletetracertokenhistory transact-sql을 실행 하는 데 사용할 수 있습니다. &#40; &#41;](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md).  
  
`[ @publisher = ] 'publisher'`은 @no__t가 아닌 1 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정 합니다. *publisher* 는 **sysname**이며 기본값은 NULL이 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자에 대해서는 지정 하지 않아야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_posttracertoken** 은 트랜잭션 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-posttracertoken-trans_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만이 **sp_posttracertoken**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
