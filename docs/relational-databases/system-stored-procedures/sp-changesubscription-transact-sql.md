---
description: sp_changesubscription(Transact-SQL)
title: sp_changesubscription (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- changesubscription
- sp_changesubscription
- changesubscription_TSQL
- sp_changesubscription_TSQL
helpviewer_keywords:
- sp_changesubscription
ms.assetid: f9d91fe3-47cf-4915-b6bf-14c9c3d8a029
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d1dd4a0fc40cf24896de912c1254b154a5538866
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543699"
---
# <a name="sp_changesubscription-transact-sql"></a>sp_changesubscription(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  지연 업데이트 트랜잭션 복제와 관련된 스냅샷이나 트랜잭션 밀어넣기 구독 또는 끌어오기 구독의 속성을 변경합니다. 다른 모든 끌어오기 구독 유형의 속성을 변경 하려면 [sp_change_subscription_properties &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)를 사용 합니다. **sp_changesubscription** 는 게시 데이터베이스의 게시자에서 실행 됩니다.  
  
> [!IMPORTANT]  
>  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changesubscription [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 변경할 게시의 이름입니다. *게시*는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'` 변경할 아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber = ] 'subscriber'` 구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @destination_db = ] 'destination_db'` 구독 데이터베이스의 이름입니다. *destination_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @property = ] 'property'` 지정 된 구독에 대해 변경할 속성입니다. *속성* 은 **nvarchar (30)** 이며 테이블의 값 중 하나일 수 있습니다.  
  
`[ @value = ] 'value'` 지정 된 *속성*의 새 값입니다. *value* 는 **nvarchar (4000)** 이며 테이블에 있는 값 중 하나일 수 있습니다.  
  
|속성|값|Description|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정의 로그인입니다.|  
|**distrib_job_password**||에이전트가 실행되는 Windows 계정의 암호입니다.|  
|**subscriber_catalog**||OLE DB 공급자에 연결할 때 사용하는 카탈로그입니다. 이 속성은 이외 구독자에만 유효 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.|  
|**subscriber_datasource**||OLE DB 공급자가 이해하는 데이터 원본의 이름입니다. *이 속성은 이외의 경우에만 유효 합니다* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *구독자.*|  
|**subscriber_location**||OLE DB 공급자가 이해하는 데이터베이스의 위치입니다. *이 속성은 이외의 경우에만 유효 합니다* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *구독자.*|  
|**subscriber_login**||구독자에서의 로그인 이름입니다.|  
|**subscriber_password**||제공된 로그인에 대한 강력한 암호입니다.|  
|**subscriber_security_mode**|**1**|구독자에 연결할 때 Windows 인증을 사용합니다.|  
||**0**|구독자에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용합니다.|  
|**subscriber_provider**||[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 데이터 원본에 대한 OLE DB 공급자 등록에 사용되는 고유한 PROGID(프로그래밍 식별자)입니다. *이 속성은 이외의 경우에만 유효 합니다* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *구독자.*|  
|**subscriber_providerstring**||데이터 원본을 식별하는 OLE DB 공급자별 연결 문자열입니다. *이 속성은 이외의 경우에만 유효 합니다* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *구독자.*|  
|**subscriptionstreams**||_구독자에 변경 내용의 일괄 처리를 병렬로 적용하기 위해 배포 에이전트당 허용되는 연결의 수입니다. 게시자에 대해 **1** 에서 **64** 사이의 값 범위가 지원 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이외 **0** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자, Oracle 게시자 또는 피어 투 피어 구독의 경우이 속성은 0 이어야 합니다.|  
|**subscriber_type**|**1**|ODBC 데이터 원본 서버|  
||**3**|OLE DB 공급자|  
|**memory_optimized**|**bit**|구독에서 메모리 액세스에 최적화 된 테이블을 지원함을 나타냅니다. *memory_optimized* 는 **bit**입니다. 여기서 1은 true (구독에서 메모리 액세스에 최적화 된 테이블을 지원함)입니다.|  
  
`[ @publisher = ] 'publisher'` 이외 게시자를 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  게시자에 대해 *게시자* 를 지정 하면 안 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changesubscription** 는 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
 **sp_changesubscription** 는 지연 업데이트 트랜잭션 복제와 관련 된 밀어넣기 구독 또는 끌어오기 구독의 속성을 수정 하는 데만 사용할 수 있습니다. 다른 모든 끌어오기 구독 유형의 속성을 변경 하려면 [sp_change_subscription_properties &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)를 사용 합니다.  
  
 에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_changesubscription**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addsubscription &#40;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_dropsubscription &#40;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
