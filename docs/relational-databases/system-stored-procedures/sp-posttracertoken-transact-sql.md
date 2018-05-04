---
title: sp_posttracertoken (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedur+I741es
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- posttracerttoken
- posttracerttoken_TSQL
- sp_posttracertoken
- sp_posttracertoken_TSQL
helpviewer_keywords:
- sp_posttracertoken
ms.assetid: 24da5cd2-1c45-475e-93db-5bdf660f1c2c
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ce1d9fa3694d87941bfbf92ed4a5a48bd3f14de2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spposttracertoken-transact-sql"></a>sp_posttracertoken(Transact-SQL)
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
 [ **@publication**=] **'***게시***'**  
 대기 시간을 측정할 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@tracer_token_id=** ] *tracer_token_id * * * 출력**  
 삽입된 추적 프로그램 토큰의 ID입니다. *tracer_token_id* 은 **int** 가 출력 매개 변수 이며 기본값은 NULL입니다. 실행 하려면이 값을 사용할 수 있습니다 [sp_helptracertokenhistory &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md) 또는 [sp_deletetracertokenhistory &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md) 먼저 실행 하지 않고 [sp_helptracertokens &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md)합니다.  
  
 [  **@publisher=** ] **'***게시자***'**  
 지정 된 비-[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 은 **sysname**, 기본값은 NULL 지정 하지 않아야 하 고는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_posttracertoken** 트랜잭션 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-posttracertoken-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_posttracertoken**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
