---
title: syspublications (시스템 뷰) (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- syspublications
- syspublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspublications view
ms.assetid: e5f57c32-efc0-4455-a74f-684dc2ae51f8
author: stevestein
ms.author: sstein
ms.openlocfilehash: f1724f86f9bfc34e505b9ba6ecddae4104270cd0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68094776"
---
# <a name="syspublications-system-view-transact-sql"></a>syspublications(시스템 뷰)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Syspublications** 뷰는 게시 정보를 노출 합니다. 이 뷰는 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**한**|**nvarchar(255)**|게시에 대한 설명 항목입니다.|  
|**name**|**sysname**|게시에 연결된 고유한 이름입니다.|  
|**pubid**|**int**|게시에 고유한 ID를 제공하는 ID 열입니다.|  
|**repl_freq**|**tinyint**|복제 빈도<br /><br /> **0** = 트랜잭션 기반 (트랜잭션).<br /><br /> **1** = 예약 된 테이블 새로 고침 (스냅숏)|  
|**status**|**tinyint**|게시 상태<br /><br /> **0** = 비활성<br /><br /> **1** = 활성|  
|**sync_method**|**tinyint**|동기화 메서드<br /><br /> **0** = 네이티브 BCP (대량 복사 프로그램 유틸리티)<br /><br /> **1** = 문자 BCP<br /><br /> **3** = 동시, 기본 BCP가 사용 되지만 스냅숏 중 테이블이 잠기지 않음을 의미 합니다.<br /><br /> **4** = Concurrent_c .이는 문자 BCP를 사용 하지만 스냅숏 동안 테이블이 잠기지 않음을 의미 합니다.|  
|**snapshot_jobid**|**binary(16)**|초기 스냅샷을 생성하기 위해 예약한 에이전트 작업을 식별합니다.|  
|**independent_agent**|**bit**|해당 게시에 독립 실행형 배포 에이전트가 있는지 여부를 지정합니다.<br /><br /> **0** = 게시에서 공유 배포 에이전트를 사용 하며 각 게시자 데이터베이스/구독자 데이터베이스 쌍에 단일 공유 에이전트가 있습니다.<br /><br /> **1** =이 게시에 대 한 독립 실행형 배포 에이전트 있습니다.|  
|**immediate_sync**|**bit**|스냅숏 에이전트 실행 될 때마다 동기화 파일을 만들지 아니면 다시 만들지를 나타냅니다. **1** 은 에이전트가 실행 될 때마다 생성 됨을 의미 합니다.|  
|**enabled_for_internet**|**bit**|게시에 대 한 동기화 파일이 FTP (파일 전송 프로토콜) 및 기타 서비스를 통해 인터넷에 노출 되는지 여부를 나타냅니다. 여기서 **1** 은 인터넷에서 액세스할 수 있음을 의미 합니다.|  
|**allow_push**|**bit**|게시에서 밀어넣기 구독이 허용 되는지 여부를 나타냅니다. **1** 은 해당 구독이 허용 됨을 의미 합니다.|  
|**allow_pull**|**bit**|게시에서 끌어오기 구독이 허용 되는지 여부를 나타냅니다. **1** 은 해당 구독이 허용 됨을 의미 합니다.|  
|**allow_anonymous**|**bit**|게시에서 익명 구독이 허용 되는지 여부를 나타냅니다. **1** 은 해당 구독이 허용 됨을 의미 합니다.|  
|**immediate_sync_ready**|**bit**|스냅샷 에이전트가 스냅샷을 생성하여 새 구독에서 사용하도록 준비하였는지 여부를 나타냅니다. 즉시 업데이트 게시에서만 의미가 있습니다. **1** 은 스냅숏이 준비 되었음을 나타냅니다.|  
|**allow_sync_tran**|**bit**|게시에서 즉시 업데이트 구독이 허용되는지 여부를 지정합니다. **1** 은 즉시 업데이트 구독이 허용 됨을 의미 합니다.|  
|**autogen_sync_procs**|**bit**|게시자에서 즉시 업데이트 구독에 대한 동기화 저장 프로시저가 생성되는지 여부를 지정합니다. **1** 은 게시자에서 생성 됨을 의미 합니다.|  
|**보존**|**int**|게시에 대한 변경 사항을 배포 데이터베이스에서 유지하는 시간(시간)을 나타냅니다.|  
|**allow_queued_tran**|**bit**|구독자의 변경 내용이 게시자에 적용될 수 있을 때까지 변경 지연이 설정되었는지 여부를 지정합니다. **1**인 경우 구독자의 변경 내용이 큐에 저장 됩니다.|  
|**snapshot_in_defaultfolder**|**bit**|스냅샷 파일을 기본 폴더에 저장할지 여부를 지정합니다. **0**인 경우 스냅숏 파일이 *alternate_snapshot_folder*에 지정 된 대체 위치에 저장 됩니다. 1인 경우 스냅샷 파일이 기본 폴더에 있습니다.|  
|**alt_snapshot_folder**|**nvarchar (510)**|스냅샷의 대체 폴더 위치를 지정합니다.|  
|**pre_snapshot_script**|**nvarchar (510)**|**.Sql** 파일 위치에 대 한 포인터를 지정 합니다. 배포 에이전트는 구독자에서 스냅샷을 적용할 때 복제된 개체 스크립트를 실행하기 전에 프리 스냅샷 스크립트를 실행합니다.|  
|**post_snapshot_script**|**nvarchar (510)**|**.Sql** 파일 위치에 대 한 포인터를 지정 합니다. 배포 에이전트는 초기 동기화 동안 기타 복제된 개체 스크립트 및 데이터를 적용한 후에 포스트 스냅샷 스크립트를 실행합니다.|  
|**compress_snapshot**|**bit**|*Alt_snapshot_folder* 위치에 기록 되는 스냅숏이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 형식으로 압축 되도록 지정 합니다. **1** 은 스냅숏이 압축 됨을 의미 합니다.|  
|**ftp_address**|**sysname**|배포자용 FTP 서비스의 네트워크 주소입니다. 배포 에이전트가 선택할 게시 스냅샷 파일의 위치를 지정합니다.|  
|**ftp_port**|**int**|배포자용 FTP 서비스의 포트 번호입니다. 배포 에이전트가 선택할 게시 스냅샷 파일의 위치를 지정합니다.|  
|**ftp_subdirectory**|**nvarchar (510)**|게시가 FTP를 사용한 스냅샷 전파를 지원할 경우 배포 에이전트가 선택할 수 있는 스냅샷 파일의 위치를 지정합니다.|  
|**ftp_login**|**nvarchar(256)**|FTP 서비스에 연결하는 데 사용되는 사용자 이름입니다.|  
|**ftp_password**|**nvarchar ( -1048)**|FTP 서비스에 연결하는 데 필요한 사용자 암호입니다.|  
|**allow_dts**|**bit**|게시에서 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] DTS(데이터 변환 서비스) 변환을 허용할지 여부를 지정합니다. **1** 은 DTS 변환을 허용 하도록 지정 합니다.|  
|**allow_subscription_copy**|**bit**|해당 게시를 구독하는 구독 데이터베이스를 복사하는 기능이 활성화되었는지 여부를 지정합니다. **1** 은 복사가 허용 됨을 의미 합니다.|  
|**centralized_conflicts**|**bit**|게시자에 충돌 레코드를 저장하는지 여부를 지정합니다.<br /><br /> **0** = 충돌을 일으킨 게시자와 구독자 모두에 충돌 레코드가 저장 됩니다.<br /><br /> **1** = 충돌 레코드가 게시자에 저장 됩니다.|  
|**conflict_retention**|**int**|충돌 레코드 보존 기간을 일 수로 지정합니다.|  
|**conflict_policy**|**int**|지연 업데이트 구독자 옵션을 사용할 때 수행하는 충돌 해결 정책을 지정합니다. 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **1** = 게시자가 충돌을 적용 합니다.<br /><br /> **2** = 구독자가 충돌을 적용 합니다.<br /><br /> **3** = 구독이 다시 초기화 됩니다.|  
|**queue_type**|**int**|사용할 큐의 유형을 지정합니다. 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **1** =. msmq. 메시지 큐 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 사용 하 여 트랜잭션을 저장 합니다.<br /><br /> **2** = .sql-를 사용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하 여 트랜잭션을 저장 합니다.<br /><br /> 참고: 메시지 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 큐 사용은 더 이상 사용 되지 않으며 더 이상 지원 되지 않습니다.|  
|**ad_guidname**|**sysname**|게시를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory에 게시할지 여부를 지정합니다. 유효한 GUID(전역 고유 식별자)가 게시를 Active Directory에 게시하는지 여부를 지정하며 GUID는 Active Directory 게시 개체인 objectGUID에 해당합니다. NULL인 경우 게시는 Active Directory에 게시되지 않습니다.<br /><br /> 참고: Active Directory에 게시는 더 이상 지원 되지 않습니다.|  
|**backward_comp_level**|**int**|데이터베이스 호환성 수준으로 다음 값 중 하나일 수 있습니다.<br /><br /> **90** = 90[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = 100[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|**allow_initialize_from_backup**|**bit**|구독자가 초기 스냅샷이 아닌 백업으로부터 이 게시에 대한 구독을 초기화할 수 있는지 여부를 지정합니다. **1** 은 백업에서 구독을 초기화할 수 있음을 의미 하 고 **0** 은 사용할 수 없음을 의미 합니다. 자세한 내용은 [스냅샷 없이 트랜잭션 구독 초기화](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)에서 수동으로 구독을 초기화하는 방법에 대해 설명합니다.|  
|**min_autonosync_lsn**|**binary (1)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|게시에 대해 스키마 복제가 지원될지 여부를 나타냅니다.<br /><br /> **1** = 게시자에서 실행 된 DDL 문이 복제 됩니다.<br /><br /> **0** = DDL 문이 복제 되지 않음을 나타냅니다. 자세한 내용은 [게시 데이터베이스의 스키마 변경](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)을 참조하세요.|  
|**options**|**int**|추가 게시 옵션을 지정하는 비트맵이며, 비트 옵션 값은 다음과 같습니다.<br /><br /> **0x1** -피어 투 피어 복제에 사용 됩니다.<br /><br /> **0x2** -피어 투 피어 복제에 대 한 로컬 변경 내용만 게시 합니다.<br /><br /> **0x4** -이외[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자에 사용할 수 있습니다.<br /><br /> **0x8** -피어 투 피어 충돌 검색을 사용 하도록 설정 합니다.|  
|**originator_id**|**smallint**|충돌 감지를 위해 피어 투 피어 복제 토폴로지의 각 노드를 식별합니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)을 참조하세요.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;를 &#40;하는 복제 저장 프로시저](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_addpublication &#40;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [Transact-sql&#41;sp_changepublication &#40;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)  
  
  
