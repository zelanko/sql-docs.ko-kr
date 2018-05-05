---
title: sp_helpsubscription (Transact SQL) | Microsoft Docs
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
f1_keywords:
- sp_helpsubscription_TSQL
- sp_helpsubscription
helpviewer_keywords:
- sp_helpsubscription
ms.assetid: ff96bcbf-e2b9-4da8-8515-d80d4ce86c16
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0634a1b6cd117b82d31324e58590d9217f402528
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpsubscription-transact-sql"></a>sp_helpsubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  특정 게시, 아티클, 구독자 또는 구독자 집합과 연관된 구독 정보를 나열합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpsubscription [ [ @publication = ] 'publication' ]   
    [ , [ @article = ] 'article' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @destination_db = ] 'destination_db' ]   
    [ , [ @found=] found OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication =** ] **'***게시***'**  
 연결된 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 **%**,이 서버에 대 한 모든 구독 정보를 반환 하는 합니다.  
  
 [  **@article=** ] **'***문서***'**  
 아티클의 이름입니다. *문서* 은 **sysname**, 기본값은 **%**, 선택한 게시 및 구독자에 대 한 모든 구독 정보를 반환 하는 합니다. 경우 **모든**, 게시에 전체 구독에 대해 하나의 항목이 반환 됩니다.  
  
 [  **@subscriber=** ] **'***구독자***'**  
 구독 정보를 가져올 구독자의 이름입니다. *구독자* 은 **sysname**, 기본값은 **%**, 선택한 게시 및 아티클에 대 한 모든 구독 정보를 반환 하는 합니다.  
  
 [  **@destination_db=** ] **'***destination_db***'**  
 대상 데이터베이스의 이름입니다. *destination_db* 은 **sysname**, 기본값은 **%** 합니다.  
  
 [  **@found=** ] **'***발견***'** 출력  
 행을 반환하는지 여부를 나타내는 플래그입니다. *찾을*은 **int** 및 출력 매개 변수, 기본값은 23456입니다.  
  
 **1** 은 게시를 찾았음을 나타냅니다.  
  
 **0** 게시를 찾지 못했음을 나타냅니다.  
  
 [ **@publisher**=] **'***게시자***'**  
 게시자의 이름입니다. *게시자* 은 **sysname**, 기본값은 현재 서버의 이름입니다.  
  
> [!NOTE]  
>  *게시자* 지정 하지 않아야, Oracle 게시자는 경우에만 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**subscriber**|**sysname**|구독자의 이름입니다.|  
|**게시**|**sysname**|게시의 이름입니다.|  
|**article**|**sysname**|아티클의 이름입니다.|  
|**대상 데이터베이스**|**sysname**|복제된 데이터가 있는 대상 데이터베이스의 이름입니다.|  
|**구독 상태**|**tinyint**|구독 상태입니다.<br /><br /> **0** = 비활성<br /><br /> **1** = 구독<br /><br /> **2** = 활성|  
|**동기화 유형**|**tinyint**|구독 동기화 유형입니다.<br /><br /> **1** = 자동<br /><br /> **2** = 없음|  
|**구독 유형**|**int**|구독 유형:<br /><br /> **0** = 밀어넣기<br /><br /> **1** = 끌어오기<br /><br /> **2** = 익명|  
|**전체 구독**|**bit**|구독이 게시 내의 모든 아티클에 관한 것인지 표시합니다.<br /><br /> **0** = 아니요<br /><br /> **1** = 예|  
|**구독 이름**|**nvarchar(255)**|구독의 이름입니다.|  
|**업데이트 모드**|**int**|**0** = 읽기 전용<br /><br /> **1** = 즉시 업데이트 구독|  
|**배포 작업 id**|**binary(16)**|배포 에이전트의 작업 ID입니다.|  
|**loopback_detection**|**bit**|루프백 검색은 배포 에이전트가 구독자에서 발생한 트랜잭션을 다시 구독자에게 보낼지 여부를 결정합니다.<br /><br /> **0** = 다시 보냅니다.<br /><br /> **1** = 다시 보내지 않았습니다.<br /><br /> 양방향 트랜잭션 복제에 사용됩니다. 자세한 내용은 [양방향 트랜잭션 복제](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md)를 참조하세요.|  
|**offload_enabled**|**bit**|복제 에이전트의 오프로드 실행이 구독자에서 실행되도록 설정되었는지 여부를 지정합니다.<br /><br /> 경우 **0**, 에이전트가 게시자에서 실행 됩니다.<br /><br /> 경우 **1**, 에이전트가 구독자에서 실행 됩니다.|  
|**offload_server**|**sysname**|원격 에이전트 활성화를 위해 사용할 수 있는 서버의 이름입니다. NULL 인 경우 다음 현재 offload_server에 나열 된 [MSdistribution_agents](../../relational-databases/system-tables/msdistribution-agents-transact-sql.md) 테이블을 사용 합니다.|  
|**dts_package_name**|**sysname**|DTS(데이터 변환 서비스) 패키지의 이름을 지정합니다.|  
|**dts_package_location**|**int**|구독에 할당된 경우 DTS 패키지의 위치입니다. 패키지가, 값이 있는 경우 **0** 패키지 위치를 지정 된 **배포자**합니다. 값이 **1** 지정는 **구독자**합니다.|  
|**subscriber_security_mode**|**smallint**|구독자의 보안 모드를 **1** 은 Windows 인증을 하 고 **0** 의미 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.|  
|**subscriber_login**|**sysname**|구독자의 로그인 이름입니다.|  
|**subscriber_password**||실제 구독자 암호는 반환되지 않습니다. 결과는 "**\*\*\*\*\*\***" 문자열입니다.|  
|**job_login**|**sysname**|배포 에이전트가 실행되는 Windows 계정의 이름입니다.|  
|**job_password**||실제 작업 암호는 반환되지 않습니다. 결과는 "**\*\*\*\*\*\***" 문자열입니다.|  
|**distrib_agent_name**|**nvarchar(100)**|구독을 동기화하는 에이전트 작업의 이름입니다.|  
|**subscriber_type**|**tinyint**|구독자의 유형으로 다음 중 하나일 수 있습니다.<br /><br /> **0** = SQL Server 구독자<br /><br /> **1** = ODBC 데이터 원본 서버<br /><br /> **2** = Microsoft JET 데이터베이스 (사용 되지 않음)<br /><br /> **3** = OLE DB 공급자|  
|**subscriber_provider**|**sysname**|SQL Server 이외 데이터 원본에 대한 OLE DB 공급자 등록에 사용되는 고유한 PROGID(프로그래밍 식별자)입니다.|  
|**subscriber_datasource**|**nvarchar(4000)**|OLE DB 공급자가 이해하는 데이터 원본의 이름입니다.|  
|**subscriber_providerstring**|**nvarchar(4000)**|데이터 원본을 식별하는 OLE DB 공급자별 연결 문자열입니다.|  
|**subscriber_location**|**nvarchar(4000)**|OLE DB 공급자가 이해하는 데이터베이스의 위치입니다.|  
|**subscriber_catalog**|**sysname**|OLE DB 공급자에 연결할 때 사용하는 카탈로그입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_helpsubscription** 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 실행 권한은 기본적으로 **public** 역할로 설정됩니다. 자신이 만든 구독에 대한 정보만 반환됩니다. 모든 구독에 대 한 정보는의 구성원에 게 반환 됩니다는 **sysadmin** 고정된 서버 역할의 멤버나 게시자는 **db_owner** 게시 데이터베이스의 고정된 데이터베이스 역할입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_addsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubstatus &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_dropsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
