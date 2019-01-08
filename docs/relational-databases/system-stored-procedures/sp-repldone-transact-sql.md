---
title: sp_repldone (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: aaeebd1aa2d6fe4ea443c7ed18ac157135ae4d64
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747753"
---
# <a name="sprepldone-transact-sql"></a>sp_repldone(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버에서 마지막으로 배포된 트랜잭션을 식별하는 레코드를 업데이트합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!CAUTION]  
>  실행 하는 경우 **sp_repldone** 수동으로 순서 및 배달 된 트랜잭션 일관성을 해칠 수 있습니다. **sp_repldone** 는 숙련 된 복제 지원 전문가 지시에 따라 복제 문제 해결에 사용 해야 합니다.  
  
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
 [  **@xactid=**] *xactid*  
 서버의 마지막 분산 트랜잭션의 첫 번째 레코드는 LSN (로그 시퀀스 번호)을입니다. *xactid* 됩니다 **binary(10)로 표현**, 기본값은 없습니다.  
  
 [  **@xact_seqno=**] *xact_seqno*  
 서버의 마지막 분산 트랜잭션의 마지막 레코드의 LSN입니다. *xact_seqno* 됩니다 **binary(10)로 표현**, 기본값은 없습니다.  
  
 [  **@numtrans=**] *numtrans*  
 분산 트랜잭션의 수가입니다. *numtrans* 됩니다 **int**, 기본값은 없습니다.  
  
 [  **@time=**] *시간*  
 트랜잭션의 마지막 일괄 처리를 배포하는 데 필요한 시간(밀리초)입니다. *시간* 됩니다 **int**, 기본값은 없습니다.  
  
 [  **@reset=**] *다시 설정*  
 다시 설정 상태입니다. *다시 설정* 됩니다 **int**, 기본값은 없습니다. 하는 경우 **1**모든 복제 된 트랜잭션 로그에 표시 된으로 분산 합니다. 하는 경우 **0**트랜잭션 로그가 첫 번째 복제 된 트랜잭션으로 다시 설정 되 고 복제 된 트랜잭션이 없습니다 표시 된으로 분산 합니다. *다시 설정* 유효한 경우에 둘 다 *xactid* 하 고 *xact_seqno* null입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_repldone** 트랜잭션 복제에 사용 됩니다.  
  
 **sp_repldone** 로그 판독기 프로세스에 의해 어떤 트랜잭션이 배포 되었는지 추적 하는 데 사용 됩니다.  
  
 사용 하 여 **sp_repldone**, 수동으로 트랜잭션 (배포자에 게 전송 됨) 복제 된 서버 알릴 수 있습니다. 또한 트랜잭션을 복제를 대기하고 있는 다음 트랜잭션으로 표시하도록 변경할 수 있습니다. 복제된 트랜잭션 목록에서 앞뒤로 이동할 수 있습니다(해당 트랜잭션 이하의 모든 트랜잭션이 배포됨 표시됩니다).  
  
 필수 매개 변수 *xactid* 하 고 *xact_seqno* 사용 하 여 얻을 수 있습니다 **sp_repltrans** 하거나 **sp_replcmds**합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_repldone**합니다.  
  
## <a name="examples"></a>예  
 때 *xactid* 가 null 인 경우 *xact_seqno* 가 null 인 경우 및 *재설정* 은 **1**, 복제 된 모든 로그에 트랜잭션이 표시 됩니다으로 분산 합니다. 이러한 방법은 더 이상 유효하지 않은 트랜잭션 로그에 복제된 트랜잭션이 있는 상태에서 로그를 자를 때 유용합니다. 예를 들어 다음과 같습니다.  
  
```  
EXEC sp_repldone @xactid = NULL, @xact_segno = NULL, @numtrans = 0,     @time = 0, @reset = 1  
```  
  
> [!CAUTION]  
>  이 프로시저는 트랜잭션 보류 중인 복제가 있을 때 트랜잭션 로그를 자를 수 있도록 하며 비상 시에 사용합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_replcmds&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replflush &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
