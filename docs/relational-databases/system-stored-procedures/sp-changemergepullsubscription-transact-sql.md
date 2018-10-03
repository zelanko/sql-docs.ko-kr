---
title: sp_changemergepullsubscription (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_changemergepullsubscription
- sp_changemergepullsubscription_TSQL
helpviewer_keywords:
- sp_changemergepullsubscription
ms.assetid: 5e0d04f2-6175-44a2-ad96-a8e2986ce4c9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43397c243985fac65e14be8af3acadf129fd8114
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47714941"
---
# <a name="spchangemergepullsubscription-transact-sql"></a>sp_changemergepullsubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 끌어오기 구독의 속성을 변경합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changemergepullsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @publisher= ] 'publisher' ]  
    [ , [ @publisher_db= ] 'publisher_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication=**] **'***publication***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 %입니다.  
  
 [ **@publisher=**] **'***publisher***'**  
 게시자의 이름입니다. *게시자*됩니다 **sysname**, 기본값은 %입니다.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 게시자 데이터베이스의 이름입니다. *publisher_db*됩니다 **sysname**, 기본값은 %입니다.  
  
 [  **@property=**] **'***속성***'**  
 변경할 속성의 이름입니다. *속성* 됩니다 **sysname**, 테이블의 값 중 하나일 수 있습니다.  
  
 [  **@value=**] **'***값***'**  
 지정한 속성의 새 값입니다. *값*됩니다 **nvarchar(255)**, 테이블의 값 중 하나일 수 있습니다.  
  
|속성|값|Description|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||기본 위치가 아니거나 기본 위치에 추가된 위치일 경우 스냅숏 폴더가 저장되는 위치입니다.|  
|**description**||해당 병합 끌어오기 구독에 관한 설명입니다.|  
|**배포자**||배포자의 이름입니다.|  
|**distributor_login**||배포자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 사용되는 로그인 ID입니다.|  
|**distributor_password**||배포자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 사용되는 암호입니다.|  
|**distributor_security_mode**|**1**|배포자에 연결할 때 Windows 인증을 사용합니다.|  
||**0**|배포자에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용합니다.|  
|**dynamic_snapshot_location**||스냅숏 파일을 저장한 폴더의 경로입니다.|  
|**ftp_address**||이전 버전과의 호환성을 위해서만 사용 가능합니다. 배포자용 FTP(파일 전송 프로토콜) 서비스의 네트워크 주소입니다.|  
|**ftp_login**||이전 버전과의 호환성을 위해서만 사용 가능합니다. FTP 서비스 연결에 사용되는 사용자 이름입니다.|  
|**ftp_password**||이전 버전과의 호환성을 위해서만 사용 가능합니다. FTP 서비스에 연결할 때 사용되는 사용자 암호입니다.|  
|**ftp_port**||이전 버전과의 호환성을 위해서만 사용 가능합니다. 배포자용 FTP 서비스의 포트 번호입니다.|  
|**호스트 이름**||조인 필터 또는 논리적 레코드 관계의 WHERE 절에서 HOST_NAME() 함수를 사용할 때 함수에 필요한 값을 지정합니다.|  
|**internet_login**||기본 인증을 사용하여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 병합 에이전트가 사용하는 로그인입니다.|  
|**internet_password**||기본 인증을 사용하여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 병합 에이전트가 사용하는 로그인 암호입니다.|  
|**internet_security_mode**|**1**|웹 동기화를 호스팅하는 웹 서버에 연결할 때 Windows 인증을 사용합니다.|  
||**0**|웹 동기화를 호스팅하는 웹 서버에 연결할 때 기본 인증을 사용합니다.|  
|**internet_timeout**||웹 동기화 요청이 만료되기 전까지의 시간(초)입니다.|  
|**internet_url**||웹 동기화를 위한 복제 수신기의 위치를 나타내는 URL입니다.|  
|**merge_job_login**||에이전트가 실행되는 Windows 계정의 로그인입니다.|  
|**merge_job_password**||에이전트가 실행되는 Windows 계정의 암호입니다.|  
|**priority**||이전 버전과 호환성을 위해서만;에서 사용 가능 실행 [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md) 게시자 대신 구독의 우선 순위를 수정 합니다.|  
|**publisher_login**||게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 사용되는 로그인 ID입니다.|  
|**publisher_password**||게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 사용되는 암호입니다.|  
|**publisher_security_mode**|**0**|게시자에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용합니다.|  
||**1**|게시자에 연결할 때 Windows 인증을 사용합니다.|  
||**2**|동기화 트리거는 정적을 사용 **sysservers** 원격 프로시저 호출 (RPC), 및 게시자 작업을 수행 하는 항목에 정의 되어 있어야 합니다 **sysservers** 테이블에서 원격 서버 또는 연결 된 서버입니다.|  
|**sync_type**|**자동 번역**|게시된 테이블의 스키마 및 초기 데이터가 구독자에게 먼저 전송됩니다.|  
||**없음**|구독자에 게시된 테이블에 대한 스키마 및 초기 데이터가 이미 있습니다. 시스템 테이블과 데이터는 항상 전송됩니다.|  
|**use_ftp**|**true**|스냅숏을 검색하는 일반적인 프로토콜 대신 FTP를 사용합니다.|  
||**false**|스냅숏을 검색하는 일반적인 프로토콜을 사용합니다.|  
|**use_web_sync**|**true**|HTTP를 통해 구독을 동기화할 수 있습니다.|  
||**false**|HTTP를 통해 구독을 동기화할 수 없습니다.|  
|**use_interactive_resolver**|**true**|조정 과정에 대화형 해결 프로그램을 사용합니다.|  
||**false**|대화형 해결 프로그램을 사용하지 않습니다.|  
|**working_directory**||해당 옵션이 지정된 경우 FTP를 사용하여 스냅숏 파일이 전송될 디렉터리의 정규화된 경로입니다.|  
|NULL(기본값)||에 대 한 지원 되는 값의 목록을 반환 *속성*합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_changemergepullsubscription** 병합 복제에 사용 됩니다.  
  
 현재 서버 및 현재 데이터베이스는 각각 구독자 및 구독자 데이터베이스로 간주됩니다.  
  
 에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_changemergepullsubscription**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [끌어오기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [sp_addmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
