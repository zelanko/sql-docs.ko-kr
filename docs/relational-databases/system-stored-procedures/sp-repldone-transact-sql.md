---
title: sp_repldone (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldone
- sp_repldone_TSQL
helpviewer_keywords:
- sp_repldone
ms.assetid: 045d3cd1-712b-44b7-a56a-c9438d4077b9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 35cd38269fabba59d257e41141141764b6d4919d
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771110"
---
# <a name="sprepldone-transact-sql"></a>sp_repldone(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  서버에서 마지막으로 배포된 트랜잭션을 식별하는 레코드를 업데이트합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!CAUTION]  
>  **Sp_repldone** 을 수동으로 실행 하는 경우 전달 된 트랜잭션의 순서와 일관성을 무효화할 수 있습니다. **sp_repldone** 은 숙련 된 복제 지원 전문가의 지시에 따라 복제 문제를 해결 하는 데만 사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_repldone [ @xactid= ] xactid   
        , [ @xact_seqno= ] xact_seqno   
    [ , [ @numtrans= ] numtrans ]   
    [ , [ @time= ] time   
    [ , [ @reset= ] reset ]  
```  
  
## <a name="arguments"></a>인수  
`[ @xactid = ] xactid`서버의 마지막 분산 트랜잭션에 대 한 첫 번째 레코드의 LSN (로그 시퀀스 번호)입니다. *xactid* 는 **binary (10)** 이며 기본값은 없습니다.  
  
`[ @xact_seqno = ] xact_seqno`서버의 마지막 분산 트랜잭션에 대 한 마지막 레코드의 LSN입니다. *xact_seqno* 는 **binary (10)** 이며 기본값은 없습니다.  
  
`[ @numtrans = ] numtrans`분산 된 트랜잭션의 수입니다. *numtrans* 은 **int**이며 기본값은 없습니다.  
  
`[ @time = ] time`트랜잭션의 마지막 일괄 처리를 배포 하는 데 필요한 시간 (밀리초)입니다 (제공 된 경우). *시간은* **int**이며 기본값은 없습니다.  
  
`[ @reset = ] reset`다시 설정 상태입니다. *reset* 은 **int**이며 기본값은 없습니다. **1**인 경우 로그의 모든 복제 된 트랜잭션이 분산 된 것으로 표시 됩니다. **0**인 경우 트랜잭션 로그는 첫 번째 복제 된 트랜잭션으로 다시 설정 되 고 복제 된 트랜잭션은 분산 된 것으로 표시 되지 않습니다. *reset* 은 *xactid* 및 *xact_seqno* 가 모두 NULL 인 경우에만 유효 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_repldone** 은 트랜잭션 복제에 사용 됩니다.  
  
 **sp_repldone** 은 배포 된 트랜잭션을 추적 하기 위해 로그 판독기 프로세스에서 사용 됩니다.  
  
 **Sp_repldone**을 사용 하면 트랜잭션이 복제 (배포자에 전송 됨) 되도록 서버에 수동으로 지시할 수 있습니다. 또한 트랜잭션을 복제를 대기하고 있는 다음 트랜잭션으로 표시하도록 변경할 수 있습니다. 복제된 트랜잭션 목록에서 앞뒤로 이동할 수 있습니다(해당 트랜잭션 이하의 모든 트랜잭션이 배포됨 표시됩니다).  
  
 *Xactid* 및 *xact_seqno* 필수 매개 변수는 **sp_repltrans** 또는 **sp_replcmds**를 사용 하 여 가져올 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버는 **sp_repldone**을 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 *Xactid* 가 null 이면 *xact_seqno* 가 null이 고 *reset* 이 **1**이면 로그의 모든 복제 된 트랜잭션이 분산 된 것으로 표시 됩니다. 이러한 방법은 더 이상 유효하지 않은 트랜잭션 로그에 복제된 트랜잭션이 있는 상태에서 로그를 자를 때 유용합니다. 예를 들어 다음과 같습니다.  
  
```  
EXEC sp_repldone @xactid = NULL, @xact_segno = NULL, @numtrans = 0,     @time = 0, @reset = 1  
```  
  
> [!CAUTION]  
>  이 프로시저는 트랜잭션 보류 중인 복제가 있을 때 트랜잭션 로그를 자를 수 있도록 하며 비상 시에 사용합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_replcmds&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replflush &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
