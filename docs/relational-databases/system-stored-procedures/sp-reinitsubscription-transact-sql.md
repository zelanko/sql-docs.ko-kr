---
title: sp_reinitsubscription (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: b9d03099ae48bf463df82d1392e97d4729ec518a
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528785"
---
# <a name="spreinitsubscription-transact-sql"></a>sp_reinitsubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'` 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 all을 사용 하 여 합니다.  
  
`[ @article = ] 'article'` 아티클의 이름이입니다. *문서* 됩니다 **sysname**, 기본값은 all을 사용 하 여 합니다. 즉시 업데이트 게시의 경우 *문서* 있어야 **모든**고, 그렇지 않으면 저장된 프로시저가 게시를 건너뛰고 오류를 보고 합니다.  
  
`[ @subscriber = ] 'subscriber'` 구독자의 이름이입니다. *구독자* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @destination_db = ] 'destination_db'` 대상 데이터베이스의 이름이입니다. *destination_db* 됩니다 **sysname**, 기본값은 all을 사용 하 여 합니다.  
  
`[ @for_schema_change = ] 'for_schema_change'` 게시 데이터베이스에서 스키마 변경의 결과로 다시 초기화가 발생 하는지 여부를 나타냅니다. *for_schema_change* 됩니다 **비트**, 기본값은 0입니다. 하는 경우 **0**,으로 하 고의 아티클 일부가 아닌 전체 게시가 다시 초기화 하는 즉시 업데이트를 허용 하는 게시에 대 한 활성 구독이 다시 활성화 됩니다. 이는 스키마가 변경되어 다시 초기화가 시작됨을 의미합니다. 하는 경우 **1**, 스냅숏 에이전트가 실행 될 때까지 활성 구독이 다시 활성화 되지 않습니다.  
  
`[ @publisher = ] 'publisher'` 지정 된 비- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 에 대해 사용할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
`[ @ignore_distributor_failure = ] ignore_distributor_failure` 배포자가 없거나 오프 라인 상태인 경우에 다시 초기화할 수 있도록 합니다. *ignore_distributor_failure* 됩니다 **비트**, 기본값은 0입니다. 하는 경우 **0**, 배포자가 없거나 오프 라인 상태인 경우 다시 초기화가 실패 합니다.  
  
`[ @invalidate_snapshot = ] invalidate_snapshot` 기존 게시 스냅숏을 무효화합니다. *invalidate_snapshot* 됩니다 **비트**, 기본값은 0입니다. 하는 경우 **1**, 게시에 대 한 새 스냅숏이 생성 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_reinitsubscription** 트랜잭션 복제에 사용 됩니다.  
  
 **sp_reinitsubscription** 피어 투 피어 트랜잭션 복제에 지원 되지 않습니다.  
  
 초기 스냅숏이 자동으로 적용되고 게시가 업데이트할 수 있는 구독을 허용하지 않는 구독의 경우 이 저장 프로시저가 실행된 다음 스냅숏 에이전트가 실행되어야 스키마 및 대량 복사 프로그램 파일이 준비되어 배포 에이전트가 구독을 다시 동기화할 수 있게 됩니다.  
  
 초기 스냅숏이 자동으로 적용되고 게시가 업데이트할 수 있는 구독을 허용하는 구독의 경우 배포 에이전트는 가장 최신 스키마 및 스냅숏 에이전트가 이전에 만든 대량 복사 프로그램 파일을 사용하여 구독을 다시 동기화합니다. 배포 에이전트를 실행 한 후에 즉시 구독을 다시 동기화 **sp_reinitsubscription**배포 에이전트가 없는 경우이 고, 그렇지 않으면 동기화 메시지 간격 (후 발생할 수 있습니다, 배포 에이전트 명령 프롬프트 매개 변수에서 지정 합니다. **MessageInterval**).  
  
 **sp_reinitsubscription** 초기 스냅숏이 수동으로 적용은 구독에 영향을 주지 합니다.  
  
 게시에 대 한 익명 구독을 동기화 하려면 다음을 전달 **모든** 또는 NULL *구독자*합니다.  
  
 트랜잭션 복제는 아티클 수준에서 구독의 다시 초기화를 지원합니다. 아티클이 다시 초기화되도록 표시된 후 다음 동기화 동안 아티클의 스냅숏은 구독자에서 다시 적용됩니다. 그러나 동일한 구독자가 구독하는 종속 아티클이 있는 경우 게시에 있는 종속 아티클도 자동으로 다음과 같은 특정 상황에서 다시 초기화되지 않으면 아티클의 스냅숏을 다시 적용할 수 없습니다.  
  
-   아티클에 대해 미리 작성한 명령이 'drop'인 경우 아티클의 기준 개체에 관한 스키마 바운드 저장 프로시저 및 스키마 바운드 뷰의 해당 아티클도 다시 초기화되도록 표시됩니다.  
  
-   아티클의 스키마 옵션에 기본 키에 선언된 참조 무결성의 스크립팅을 포함하는 경우 다시 초기화된 아티클의 기본 테이블에 대해 외래 키 관계를 가진 기본 테이블이 있는 아티클도 다시 초기화되도록 표시됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_reinittranpushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitsubscription-tr_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할의 멤버, 합니다 **db_owner** 고정된 데이터베이스 역할 또는 구독의 작성자 실행할 수 있습니다 **sp_reinitsubscription** .  
  
## <a name="see-also"></a>관련 항목  
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
