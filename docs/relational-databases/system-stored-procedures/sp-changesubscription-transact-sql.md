---
title: sp_changesubscription (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a293be4b745f30f4ee4a9bff6226e4e2ef80676f
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53209842"
---
# <a name="spchangesubscription-transact-sql"></a>sp_changesubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지연 업데이트 트랜잭션 복제와 관련된 스냅숏이나 트랜잭션 밀어넣기 구독 또는 끌어오기 구독의 속성을 변경합니다. 끌어오기 구독에 다른 모든 유형의 속성을 변경 하려면 사용 하 여 [sp_change_subscription_properties &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)합니다. **sp_changesubscription** 게시 데이터베이스의 게시자에서 실행 됩니다.  
  
> [!IMPORTANT]  
>  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@publication**=] **'**_게시_**'**  
 변경할 게시의 이름입니다. *게시*됩니다 **sysname**, 기본값은 없습니다  
  
 [ **@article** =] **'**_문서_**'**  
 변경할 아티클의 이름입니다. *문서* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@subscriber** =] **'**_구독자_**'**  
 구독자의 이름입니다. *구독자* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@destination_db** =] **'**_destination_db_**'**  
 구독 데이터베이스의 이름입니다. *destination_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@property=**] **'**_속성_**'**  
 지정된 구독에 대해 변경할 속성입니다. *속성* 됩니다 **nvarchar(30)**, 테이블의 값 중 하나일 수 있습니다.  
  
 [  **@value=**] **'**_값_**'**  
 지정 된 새 값입니다 *속성*합니다. *값* 됩니다 **nvarchar(4000)**, 테이블의 값 중 하나일 수 있습니다.  
  
|속성|값|Description|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정의 로그인입니다.|  
|**distrib_job_password**||에이전트가 실행되는 Windows 계정의 암호입니다.|  
|**subscriber_catalog**||OLE DB 공급자에 연결할 때 사용하는 카탈로그입니다. 이 속성에만 유효 이외[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다.|  
|**subscriber_datasource**||OLE DB 공급자가 이해하는 데이터 원본의 이름입니다. *이 속성에만 유효 이외* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *구독자입니다.*|  
|**subscriber_location**||OLE DB 공급자가 이해하는 데이터베이스의 위치입니다. *이 속성에만 유효 이외* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *구독자입니다.*|  
|**subscriber_login**||구독자에서의 로그인 이름입니다.|  
|**subscriber_password**||제공된 로그인에 대한 강력한 암호입니다.|  
|**subscriber_security_mode**|**1**|구독자에 연결할 때 Windows 인증을 사용합니다.|  
||**0**|구독자에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용합니다.|  
|**subscriber_provider**||[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 데이터 원본에 대한 OLE DB 공급자 등록에 사용되는 고유한 PROGID(프로그래밍 식별자)입니다. *이 속성에만 유효 이외* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *구독자입니다.*|  
|**subscriber_providerstring**||데이터 원본을 식별하는 OLE DB 공급자별 연결 문자열입니다. *이 속성에만 유효 이외* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *구독자입니다.*|  
|**subscriptionstreams**||_구독자에 변경 내용의 일괄 처리를 병렬로 적용하기 위해 배포 에이전트당 허용되는 연결의 수입니다. 값의 범위 **1** 하 **64** 대해서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. 이 속성은 이어야 **0** 에 대 한 비-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자, Oracle 게시자 또는 피어 투 피어 구독 합니다.|  
|**subscriber_type**|**1**|ODBC 데이터 원본 서버|  
||**3**|OLE DB 공급자|  
|**메모리 액세스에 최적화**|**bit**|구독 메모리 액세스에 최적화 된 테이블을 지원함을 나타냅니다. *memory_optimized* 됩니다 **비트**, 1 (구독 메모리 액세스에 최적화 된 테이블에서 지원) true와 같습니다.|  
  
 [  **@publisher =** ] **'**_게시자_**'**  
 지정 된 비- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 에 대해 지정할 수 없습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_changesubscription** 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
 **sp_changesubscription** 밀어넣기 구독의 속성을 수정 하 여 끌어오기 구독에 관련 된 지연 업데이트 트랜잭션 복제에만 사용할 수 있습니다. 끌어오기 구독에 다른 모든 유형의 속성을 변경 하려면 사용 하 여 [sp_change_subscription_properties &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)합니다.  
  
 에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_changesubscription**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_addsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
