---
title: sp_MSchange_distribution_agent_properties (T-sql)
description: SQL Server 복제 토폴로지의 배포 에이전트 속성을 변경 하는 데 사용 되는 sp_MSchange_distribution_agent_properties 저장 프로시저에 대해 설명 합니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_distribution_agent_properties
- sp_MSchange_distribution_agent_properties_TSQL
helpviewer_keywords:
- sp_MSchange_distribution_agent_properties
ms.assetid: 7dac5e68-bf84-433a-a531-66921f35126f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1a2e2e3c0074c3fcc53298c2556c786c9b7057db
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75322279"
---
# <a name="sp_mschange_distribution_agent_properties-transact-sql"></a>sp_MSchange_distribution_agent_properties(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전의 배포자에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 실행 되는 배포 에이전트 작업의 속성을 변경 합니다. 이 저장 프로시저는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 인스턴스에서 게시자가 실행될 때 속성을 변경하는 데 사용됩니다. 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_MSchange_distribution_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber_db = ] 'subscriber_db'`구독 데이터베이스의 이름입니다. *subscriber_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @property = ] 'property'`변경할 게시 속성입니다. *속성* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @value = ] 'value'`새 속성 값입니다. *value* 는 **nvarchar (524)** 이며 기본값은 NULL입니다.  
  
 이 표에서는 변경할 수 있는 배포 에이전트 작업의 속성 및 그 속성 값의 제한에 대해 설명합니다.  
  
|속성|값|설명|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정의 로그인입니다.|  
|**distrib_job_password**||에이전트 작업 실행에 사용된 Windows 계정의 암호입니다.|  
|**subscriber_catalog**||OLE DB 공급자에 연결할 때 사용하는 카탈로그입니다. *이 속성은 이외* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자에만 유효 *합니다.*|  
|**subscriber_datasource**||OLE DB 공급자가 이해하는 데이터 원본의 이름입니다. *이 속성은 이외* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자에만 유효 *합니다.*|  
|**subscriber_location**||OLE DB 공급자가 이해하는 데이터베이스의 위치입니다. *이 속성은 이외* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자에만 유효 *합니다.*|  
|**subscriber_login**||구독을 동기화하기 위해 구독자에 연결할 때 사용하는 로그인입니다.|  
|**subscriber_password**||구독자 암호입니다.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_provider**||[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 데이터 원본에 대한 OLE DB 공급자 등록에 사용되는 고유한 PROGID(프로그래밍 식별자)입니다. *이 속성은 이외* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자에만 유효 *합니다.*|  
|**subscriber_providerstring**||데이터 원본을 식별하는 OLE DB 공급자별 연결 문자열입니다. *이 속성은 SQL Server 이외 구독자에만 유효합니다.*|  
|**subscriber_security_mode**|**1**|Windows 인증<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증입니다.|  
|**subscriber_type**|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]구독자|  
||**1**|ODBC 데이터 원본 서버|  
||**3**|OLE DB 공급자|  
|**subscriptionstreams**||변경 내용의 일괄 처리를 구독자에게 병렬로 적용하기 위해 배포 에이전트당 허용된 연결 수를 나타냅니다. *이외* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *구독자, Oracle 게시자 또는 피어 투 피어 구독* 에 대해서는 지원 되지 않습니다.|  
  
> [!NOTE]  
>  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_MSchange_distribution_agent_properties** 는 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 게시자가 이상 버전의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스에서 실행 되는 경우 [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) 를 사용 하 여 배포자에서 실행 되는 밀어넣기 구독을 동기화 하는 병합 에이전트 작업의 속성을 변경 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 배포자에서 **sysadmin** 고정 서버 역할의 멤버만 **sp_MSchange_distribution_agent_properties**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addpushsubscription_agent &#40;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [Transact-sql&#41;sp_addsubscription &#40;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)  
  
  
