---
title: sp_addqreader_agent (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addqreader_agent_TSQL
- sp_addqreader_agent
helpviewer_keywords:
- sp_addqreader_agent
ms.assetid: dc9f591a-e67e-4ba8-bf47-defd5eda0822
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d89800f8eeaa7c960b636f93555009cbc87c028f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32990668"
---
# <a name="spaddqreaderagent-transact-sql"></a>sp_addqreader_agent(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 배포자에 대한 큐 판독기 에이전트를 추가합니다. 이 저장 프로시저는 배포 데이터베이스의 배포자 또는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addqreader_agent [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
    [ , [ @job_name = ] 'job_name'  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>인수  
 [ **@job_login**=] **'***job_login***'**  
 에이전트 실행에 사용되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정의 로그인입니다. *job_login* 은 **nvarchar (257)**, 기본값은 없습니다. 이 Windows 계정은 에이전트가 배포자에 연결할 때 항상 사용됩니다.  
  
 [ **@job_password**=] **'***job_password***'**  
 에이전트 실행에 사용되는 Windows 계정의 암호입니다. *job_password* 은 **sysname**, 기본값은 없습니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 최상의 보안을 위해 런타임에 로그인 이름과 암호를 제공해야 합니다.  
  
 [ **@job_name**=] **'***job_name***'**  
 기존 에이전트 작업의 이름입니다. *job_name* 은 **sysname**, 기본값은 NULL입니다. 이 매개 변수는 새로 만든 작업(기본값) 대신 기존 작업을 사용하여 에이전트가 만들어지는 경우에만 지정됩니다.  
  
 [  **@frompublisher=** ] *frompublisher*  
 프로시저가 게시자에서 실행되는지 여부를 지정합니다. *frompublisher* 는 bit 이며 기본값은 **0**합니다. 값이 **1** 프로시저가 게시 데이터베이스의 게시자에서 실행 되 고 있음을 의미 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 **sp_addqreader_agent** 트랜잭션 복제에 사용 됩니다.  
  
 **sp_addqreader_agent** 지연 업데이트 한 후 원하는 배포자에서 한 번 이상 실행 해야 [sp_adddistributiondb](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) 하기 전에 [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)합니다.  
  
 실행할 때 큐 판독기 에이전트 작업이 제거 되 [sp_dropdistributiondb](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_addqreader_agent**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [복제 스크립트 업그레이드&#40;복제 Transact-SQL 프로그래밍&#41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_changeqreader_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md)   
 [sp_helpqreader_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md)  
  
  
