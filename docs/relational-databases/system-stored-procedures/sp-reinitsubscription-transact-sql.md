---
title: sp_reinitsubscription (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitsubscription
- sp_reinitsubscription_TSQL
helpviewer_keywords:
- sp_reinitsubscription
ms.assetid: d56ae218-6128-4ff9-b06c-749914505c7b
author: stevestein
ms.author: sstein
ms.openlocfilehash: eaeeaa5009cb119b40dcde9b8f9baa170d8f7bef
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68762526"
---
# <a name="spreinitsubscription-transact-sql"></a>sp_reinitsubscription(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  구독을 다시 초기화하도록 표시합니다. 이 저장 프로시저는 밀어넣기 구독을 위해 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_reinitsubscription [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
        , [ @subscriber = ] 'subscriber'  
    [ , [ @destination_db = ] 'destination_db']  
    [ , [ @for_schema_change = ] 'for_schema_change']  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @ignore_distributor_failure = ] ignore_distributor_failure ]   
    [ , [ @invalidate_snapshot = ] invalidate_snapshot ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 all입니다.  
  
`[ @article = ] 'article'`아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 all입니다. 즉시 업데이트 게시의 경우 *아티클은* **모두**여야 합니다. 그렇지 않으면 저장 프로시저가 게시를 건너뛰고 오류를 보고 합니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @destination_db = ] 'destination_db'`대상 데이터베이스의 이름입니다. *destination_db* 는 **sysname**이며 기본값은 all입니다.  
  
`[ @for_schema_change = ] 'for_schema_change'`게시 데이터베이스에서 스키마가 변경 된 결과로 다시 초기화가 발생 하는지 여부를 나타냅니다. *for_schema_change* 는 **bit**이며 기본값은 0입니다. **0**인 경우 전체 게시가 아닌 전체 게시가 다시 초기화 되는 동안 즉시 업데이트를 허용 하는 게시에 대 한 활성 구독이 다시 활성화 됩니다. 이는 스키마가 변경되어 다시 초기화가 시작됨을 의미합니다. **1**인 경우 스냅숏 에이전트 실행 될 때까지 활성 구독이 다시 활성화 되지 않습니다.  
  
`[ @publisher = ] 'publisher'`이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정 합니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 에는 게시자를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하면 안 됩니다.  
  
`[ @ignore_distributor_failure = ] ignore_distributor_failure`배포자가 없거나 오프 라인 상태인 경우에도 다시 초기화할 수 있습니다. *ignore_distributor_failure* 는 **bit**이며 기본값은 0입니다. **0**인 경우 배포자가 없거나 오프 라인 상태 이면 다시 초기화가 실패 합니다.  
  
`[ @invalidate_snapshot = ] invalidate_snapshot`기존 게시 스냅숏을 무효화 합니다. *invalidate_snapshot* 는 **bit**이며 기본값은 0입니다. **1**인 경우 게시에 대해 새 스냅숏이 생성 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_reinitsubscription** 은 트랜잭션 복제에 사용 됩니다.  
  
 **sp_reinitsubscription** 는 피어 투 피어 트랜잭션 복제에 대해 지원 되지 않습니다.  
  
 초기 스냅샷이 자동으로 적용되고 게시가 업데이트할 수 있는 구독을 허용하지 않는 구독의 경우 이 저장 프로시저가 실행된 다음 스냅샷 에이전트가 실행되어야 스키마 및 대량 복사 프로그램 파일이 준비되어 배포 에이전트가 구독을 다시 동기화할 수 있게 됩니다.  
  
 초기 스냅샷이 자동으로 적용되고 게시가 업데이트할 수 있는 구독을 허용하는 구독의 경우 배포 에이전트는 가장 최신 스키마 및 스냅샷 에이전트가 이전에 만든 대량 복사 프로그램 파일을 사용하여 구독을 다시 동기화합니다. 배포 에이전트은 사용자가 사용 하지 않는 배포 에이전트 경우 **sp_reinitsubscription**를 실행 한 직후에 구독을 다시 동기화 합니다. 그렇지 않으면 메시지 간격 후에 동기화가 수행 될 수 있습니다 (배포 에이전트 명령 프롬프트 매개 변수를 통해 지정). **Messageinterval**).  
  
 **sp_reinitsubscription** 은 초기 스냅숏이 수동으로 적용 되는 구독에는 영향을 주지 않습니다.  
  
 게시에 대 한 익명 구독을 다시 동기화 하려면 **모든** 또는 NULL을 *구독자로*전달 합니다.  
  
 트랜잭션 복제는 아티클 수준에서 구독의 다시 초기화를 지원합니다. 아티클이 다시 초기화되도록 표시된 후 다음 동기화 동안 아티클의 스냅샷은 구독자에서 다시 적용됩니다. 그러나 동일한 구독자가 구독하는 종속 아티클이 있는 경우 게시에 있는 종속 아티클도 자동으로 다음과 같은 특정 상황에서 다시 초기화되지 않으면 아티클의 스냅샷을 다시 적용할 수 없습니다.  
  
-   아티클에 대해 미리 작성한 명령이 'drop'인 경우 아티클의 기준 개체에 관한 스키마 바운드 저장 프로시저 및 스키마 바운드 뷰의 해당 아티클도 다시 초기화되도록 표시됩니다.  
  
-   아티클의 스키마 옵션에 기본 키에 선언된 참조 무결성의 스크립팅을 포함하는 경우 다시 초기화된 아티클의 기본 테이블에 대해 외래 키 관계를 가진 기본 테이블이 있는 아티클도 다시 초기화되도록 표시됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_reinittranpushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitsubscription-tr_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버, **db_owner** 고정 데이터베이스 역할의 멤버 또는 구독의 작성자만 **sp_reinitsubscription**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
