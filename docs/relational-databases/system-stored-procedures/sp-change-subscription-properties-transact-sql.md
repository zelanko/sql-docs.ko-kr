---
title: sp_change_subscription_properties (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_change_subscription_properties_TSQL
- sp_change_subscription_properties
helpviewer_keywords:
- sp_change_subscription_properties
ms.assetid: cf8137f9-f346-4aa1-ae35-91a2d3c16f17
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3fe61cfc2088b75e2ab1af2c457073ad723dd7f2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spchangesubscriptionproperties-transact-sql"></a>sp_change_subscription_properties(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  끌어오기 구독에 대한 정보를 업데이트합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_change_subscription_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publication_type = ] publication_type ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publisher=**] **'***게시자***'**  
 게시자의 이름입니다. *게시자* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 게시자 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@publication=**] **'***게시***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@property=**] **'***속성***'**  
 변경할 속성입니다. *속성* 은 **sysname**합니다.  
  
 [  **@value=**] **'***값***'**  
 속성의 새 값입니다. *값* 은 **nvarchar (1000)**, 기본값은 없습니다.  
  
 [  **@publication_type =** ] *publication_type*  
 게시의 복제 유형을 지정합니다. *publication_type* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|값|게시 유형|  
|-----------|----------------------|  
|**0**|트랜잭션|  
|**1**|스냅숏|  
|**2**|병합|  
|NULL(기본값)|복제가 게시 유형을 결정합니다. 저장 프로시저가 여러 테이블을 통해 검사하므로 이 옵션은 정확한 게시 유형을 제공하는 경우보다 느립니다.|  
  
 다음 표에서는 아티클의 속성 및 해당 속성의 값을 설명합니다.  
  
|속성|값|Description|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||스냅숏의 대체 폴더 위치를 지정합니다. NULL로 설정하면 게시자가 지정한 기본 위치에서 스냅숏 파일이 선택됩니다.|  
|**distrib_job_login**||에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정의 로그인입니다.|  
|**distrib_job_password**||에이전트가 실행되는 Windows 계정의 암호입니다.|  
|**distributor_login**||배포자 로그인입니다.|  
|**distributor_password**||배포자 암호입니다.|  
|**distributor_security_mode**|**1**|배포자에 연결할 때 Windows 인증을 사용합니다.|  
||**0**|배포자에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용합니다.|  
|**dts_package_name**||SQL Server 2000 DTS(데이터 변환 서비스) 패키지의 이름을 지정합니다. 이 값은 트랜잭션 또는 스냅숏 게시일 때만 지정할 수 있습니다.|  
|**dts_package_password**||패키지 암호를 지정합니다. *dts_package_password* 은 **sysname** 기본값은 NULL 이며 암호 속성이 남아 있을 것 이라는 것을 지정 하는 변경 되지 않습니다.<br /><br /> 참고: DTS 패키지에는 암호가 있어야 합니다.<br /><br /> 이 값은 트랜잭션 또는 스냅숏 게시일 때만 지정할 수 있습니다.|  
|**dts_package_location**||DTS 패키지가 저장된 위치입니다. 이 값은 트랜잭션 또는 스냅숏 게시일 때만 지정할 수 있습니다.|  
|**dynamic_snapshot_location**||스냅숏 파일을 저장한 폴더의 경로를 지정합니다. 이 값은 병합 게시일 때만 지정할 수 있습니다.|  
|**ftp_address**||이전 버전과의 호환성을 위해서만 지원됩니다.|  
|**ftp_login**||이전 버전과의 호환성을 위해서만 지원됩니다.|  
|**ftp_password**||이전 버전과의 호환성을 위해서만 지원됩니다.|  
|**ftp_port**||이전 버전과의 호환성을 위해서만 지원됩니다.|  
|**호스트 이름**||게시자에 연결할 때 사용하는 호스트 이름입니다.|  
|**internet_login**||기본 인증을 사용하여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 병합 에이전트가 사용하는 로그인입니다.|  
|**internet_password**||기본 인증을 사용하여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 병합 에이전트가 사용하는 암호입니다.|  
|**internet_security_mode**|**1**|웹 동기화에 Windows 통합 인증을 사용합니다. 웹 동기화에는 기본 인증을 사용하는 것이 좋습니다. 자세한 내용은 [웹 동기화 구성](../../relational-databases/replication/configure-web-synchronization.md)을 참조하세요.|  
||**0**|웹 동기화에 기본 인증을 사용합니다.<br /><br /> 참고: 웹 동기화 웹 서버에 SSL 연결이 필요합니다.|  
|**internet_timeout**||웹 동기화 요청이 만료되기 전까지의 시간(초)입니다.|  
|**internet_url**||웹 동기화를 위한 복제 수신기의 위치를 나타내는 URL입니다.|  
|**merge_job_login**||에이전트가 실행되는 Windows 계정의 로그인입니다.|  
|**merge_job_password**||에이전트가 실행되는 Windows 계정의 암호입니다.|  
|**publisher_login**||게시자 로그인입니다. 변경 *publisher_login* 구독을 병합 게시에 대해서만 지원 됩니다.|  
|**publisher_password**||게시자 암호입니다. 변경 *publisher_password* 구독을 병합 게시에 대해서만 지원 됩니다.|  
|**publisher_security_mode**|**1**|게시자에 연결할 때 Windows 인증을 사용합니다. 변경 *publisher_security_mode* 구독을 병합 게시에 대해서만 지원 됩니다.|  
||**0**|게시자에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용합니다.|  
|**use_ftp**|**true**|일반 프로토콜 대신 FTP를 사용하여 스냅숏을 검색합니다.|  
||**false**|일반 프로토콜을 사용하여 스냅숏을 검색합니다.|  
|**use_web_sync**|**true**|웹 동기화를 사용합니다.|  
||**false**|웹 동기화를 사용하지 않습니다.|  
|**working_directory**||FTP(파일 전송 프로토콜)를 사용하여 스냅숏 파일을 전송할 때 게시를 위해 데이터 및 스키마를 임시로 저장하는 데 사용하는 작업 디렉터리의 이름입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_change_subscription_properties** 모든 유형의 복제에 사용 됩니다.  
  
 **sp_change_subscription_properties** 끌어오기 구독에 사용 됩니다.  
  
 Oracle 게시자의 경우 값에 대 한 *publisher_db* 서버 인스턴스당 하나의 데이터베이스만 허용 하므로 무시 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_change_subscription_properties**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [끌어오기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [sp_addmergepullsubscription &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_addmergepullsubscription_agent&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_addpullsubscription &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_addpullsubscription_agent&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
