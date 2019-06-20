---
title: MSsubscription_properties (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_properties
- MSsubscription_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_properties system table
ms.assetid: f96fc1ae-b798-4b05-82a7-564ae6ef23b8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bc3e113ab9ace64cac0d41cb34bdec1c44355e48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63032988"
---
# <a name="mssubscriptionproperties-transact-sql"></a>MSsubscription_properties(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSsubscription_properties** 테이블이 구독자에 복제 에이전트를 실행 하는 데 필요한 매개 변수 정보에 대 한 행을 포함 합니다. 이 테이블은 끌어오기 구독의 경우 구독자의 구독 데이터베이스에 저장되고 밀어넣기 구독의 경우 배포자의 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|게시자의 이름입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**publication**|**sysname**|게시의 이름입니다.|  
|**publication_type**|**int**|게시의 유형입니다.<br /><br /> **0** = 트랜잭션.<br /><br /> **2** = 병합 합니다.|  
|**publisher_login**|**sysname**|게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 사용하는 로그인 ID입니다.|  
|**publisher_password**|**nvarchar(524)**|게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 사용하는 암호화된 암호입니다.|  
|**publisher_security_mode**|**int**|게시자에서 구현된 보안 모드입니다.<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server 인증 합니다.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증입니다.<br /><br /> **2** = 동기화 트리거를 사용 하는 정적 **sysservers** 원격 프로시저 호출 (RPC), 작업을 수행 하는 항목 및 *게시자* 정의 해야 합니다는 **sysservers**테이블에서 원격 서버 또는 연결 된 서버입니다.|  
|**distributor**|**sysname**|배포자 이름입니다.|  
|**distributor_login**|**sysname**|배포자에서 SQL Server 인증에 사용 되는 로그인 ID입니다.|  
|**distributor_password**|**nvarchar(524)**|배포자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 사용되는 암호화된 암호입니다.|  
|**distributor_security_mode**|**int**|배포자에서 구현된 보안 모드입니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.<br /><br /> **1** = Windows 인증입니다.|  
|**ftp_address**|**sysname**|배포자용 FTP(파일 전송 프로토콜) 서비스의 네트워크 주소입니다.|  
|**ftp_port**|**int**|배포자용 FTP 서비스의 포트 번호입니다.|  
|**ftp_login**|**sysname**|FTP 서비스에 연결하는 데 사용되는 사용자 이름입니다.|  
|**ftp_password**|**nvarchar(524)**|FTP 서비스에 연결하는 데 사용되는 사용자 암호입니다.|  
|**alt_snapshot_folder**|**nvarchar(255)**|스냅숏의 대체 폴더 위치를 지정합니다.|  
|**working_directory**|**nvarchar(255)**|데이터 및 스키마 파일을 저장하는 데 사용되는 작업 디렉터리의 이름입니다.|  
|**use_ftp**|**bit**|일반 프로토콜 대신 FTP를 사용하여 스냅숏을 검색하도록 지정합니다. 하는 경우 **1**, FTP를 사용 합니다.|  
|**dts_package_name**|**sysname**|DTS(데이터 변환 서비스) 패키지의 이름을 지정합니다.|  
|**dts_package_password**|**nvarchar(524)**|패키지 암호를 지정합니다.|  
|**dts_package_location**|**int**|DTS 패키지가 저장된 위치입니다.|  
|**enabled_for_syncmgr**|**bit**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 동기화 관리자를 통해 구독을 동기화할 수 있는지 여부를 지정합니다.<br /><br /> **0** = 구독이 동기화 관리자에 등록 되지 않았습니다.<br /><br /> **1** = 구독이 동기화 관리자를 사용 하 여 등록 되며 및 시작 하지 않고 동기화 할 수 있습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.|  
|**offload_agent**|**bit**|에이전트를 원격으로 활성화할 수 있는지 여부를 지정합니다. 하는 경우 **0**, 에이전트를 원격으로 활성화할 수 없습니다.|  
|**offload_server**|**sysname**|원격 활성화에 사용하는 서버의 네트워크 이름을 지정합니다.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|스냅숏 파일을 저장한 폴더의 경로를 지정합니다.|  
|**use_web_sync**|**bit**|HTTP를 통해 구독을 동기화할 수 있는지 여부를 지정합니다. 값이 **1** 이 기능을 사용 하는 것을 의미 합니다.|  
|**internet_url**|**nvarchar(260)**|웹 동기화에 대한 복제 수신기의 위치를 나타내는 URL입니다.|  
|**internet_login**|**sysname**|병합 에이전트가 사용 하 여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 사용 하는 로그인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.|  
|**internet_password**|**nvarchar(524)**|병합 에이전트가 사용 하 여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 사용 하는 로그인 암호를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.|  
|**internet_security_mode**|**int**|여기서 값에는 웹 동기화를 호스팅하는 웹 서버에 연결할 때 사용 되는 인증 모드 **1** Windows 인증 및 값 의미 **0** 의미 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.|  
|**internet_timeout**|**int**|웹 동기화 요청이 만료되기 전까지의 시간(초)입니다.|  
|**hostname**|**sysname**|에 대 한 값을 지정 **HOST_NAME** 에서이 함수는 사용 하는 경우를 **여기서** 조인 필터 또는 논리적 레코드 관계 절.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
