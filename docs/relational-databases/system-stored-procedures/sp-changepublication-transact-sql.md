---
title: sp_changepublication (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changepublication
- sp_changepublication_TSQL
helpviewer_keywords:
- sp_changepublication
ms.assetid: c36e5865-25d5-42b7-b045-dc5036225081
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1e5b128a38fc32b16cca9d0a8e59f09aef88676c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68762421"
---
# <a name="sp_changepublication-transact-sql"></a>sp_changepublication(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  게시의 속성을 변경합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_changepublication [ [ @publication = ] 'publication' ]  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @property = ] 'property'`변경할 게시 속성입니다. *속성* 은 **nvarchar (255)** 입니다.  
  
`[ @value = ] 'value'`새 속성 값입니다. *value* 는 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
 이 표에서는 변경할 수 있는 게시의 속성 및 그 속성의 값에 대한 제한에 대해 설명합니다.  
  
|속성|값|Description|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|지정 된 게시에 대해 익명 구독을 만들 수 있으며 *immediate_sync* 도 **true**여야 합니다. 피어 투 피어 게시의 경우 변경할 수 없습니다.|  
||**false**|지정된 게시에 대해 익명 구독을 만들 수 없습니다. 피어 투 피어 게시의 경우 변경할 수 없습니다.|  
|**allow_initialize_from_backup**|**true**|구독자는 초기 스냅샷이 아닌 백업으로부터 이 게시에 대한 구독을 초기화할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
||**false**|구독자는 초기 스냅샷을 사용해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
|**allow_partition_switch**|**true**|ALTER TABLE ... SWITCH 문은 게시 된 데이터베이스에 대해 실행할 수 있습니다. 자세한 내용은 [분할 테이블 및 인덱스 복제](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)를 참조하세요.|  
||**false**|ALTER TABLE ... 게시 된 데이터베이스에 대해 SWITCH 문을 실행할 수 없습니다.|  
|**allow_pull**|**true**|지정된 게시에 대해 끌어오기 구독을 허용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
||**false**|지정된 게시에 대해 끌어오기 구독을 허용하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
|**allow_push**|**true**|지정된 게시에 대해 밀어넣기 구독을 허용합니다.|  
||**false**|지정된 게시에 대해 밀어넣기 구독을 허용하지 않습니다.|  
|**allow_subscription_copy**|**true**|이 게시를 구독하는 데이터베이스를 복사하는 기능을 설정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
||**false**|이 게시를 구독하는 데이터베이스를 복사하는 기능을 해제합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
|**alt_snapshot_folder**||스냅샷에 대한 대체 폴더의 위치입니다.|  
|**centralized_conflicts**|**true**|충돌 레코드가 게시자에 저장됩니다. 활성 구독이 없을 때만 변경할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
||**false**|충돌 기록을 충돌을 일으킨 게시자 및 구독자에 모두 저장합니다. 활성 구독이 없을 때만 변경할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
|**compress_snapshot**|**true**|대체 스냅샷 폴더의 스냅샷은 .cab 파일 형식으로 압축됩니다. 기본 스냅샷 폴더의 스냅샷은 압축할 수 없습니다.|  
||**false**|스냅샷은 압축되지 않으며 이는 복제의 기본 동작입니다.|  
|**conflict_policy**|**pub wins**|충돌 시 게시자 내용이 적용되는 구독자를 업데이트하기 위한 충돌 해결 정책입니다. 이 속성은 활성 구독이 없을 경우에만 변경될 수 있습니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
||**sub reinit**|구독자를 업데이트할 때 충돌이 발생하면 구독은 다시 초기화됩니다. 이 속성은 활성 구독이 없을 경우에만 변경될 수 있습니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
||**sub wins**|충돌 시 구독자 내용이 적용되는 구독자를 업데이트하기 위한 충돌 해결 정책입니다. 이 속성은 활성 구독이 없을 경우에만 변경될 수 있습니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
|**conflict_retention**||충돌 보존 기간 (일)을 지정 하는 **int** 입니다. 기본 보존 기간은 14일입니다. **0** 은 충돌 정리가 필요 하지 않음을 의미 합니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
|**한**||게시에 관해 설명하는 선택적인 항목입니다.|  
|**enabled_for_het_sub**|**true**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자를 지원하도록 게시를 설정합니다. 게시에 대 한 구독이 있는 경우에는 **enabled_for_het_sub** 를 변경할 수 없습니다. **Enabled_for_het_sub** 을 true로 설정 하기 전에 다음 요구 사항을 준수 하기 위해 [복제 저장 프로시저 (transact-sql)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) 를 실행 해야 할 수 있습니다.<br /> - **allow_queued_tran** 은 **false**여야 합니다.<br /> - **allow_sync_tran** 은 **false**여야 합니다.<br /> **Enabled_for_het_sub** 를 **true** 로 변경 하면 기존 게시 설정이 변경 될 수 있습니다. 자세한 내용은 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)을(를) 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
||**false**|게시는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자를 지원하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
|**enabled_for_internet**|**true**|인터넷에서 게시를 사용할 수 있으며 FTP(파일 전송 프로토콜)를 사용하여 구독자로 스냅샷 파일을 전송할 수 있습니다. 게시에 대 한 동기화 파일은 C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\ftp. 디렉터리에 저장 됩니다. *ftp_address* 는 NULL 일 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
||**false**|인터넷에서 게시를 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
|**enabled_for_p2p**|**true**|게시는 피어 투 피어 복제를 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.<br /> **Enabled_for_p2p** 를 **true**로 설정 하려면 다음 제한 사항이 적용 됩니다.<br /> - **allow_anonymous** 은 **false** 여야 합니다.<br /> - **allow_dts** 은 **false**여야 합니다.<br /> - **allow_initialize_from_backup** **true** 여야 합니다.<br /> - **allow_queued_tran** 은 **false**여야 합니다.<br /> - **allow_sync_tran** 은 **false**여야 합니다.<br /> - **enabled_for_het_sub** 은 **false**여야 합니다.<br /> - **independent_agent** 은 **true**여야 합니다.<br /> - **repl_freq** 는 **연속**이어야 합니다.<br /> - **replicate_ddl** **1**이어야 합니다.|  
||**false**|게시는 피어 투 피어 복제를 지원하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
|**ftp_address**||FTP로 액세스 가능한 게시 스냅샷 파일의 위치입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
|**ftp_login**||사용자 이름은 FTP 서비스에 연결하는 데 사용되며 ANONYMOUS 값을 허용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
|**ftp_password**||FTP 서비스에 연결하는 데 사용한 사용자 이름에 대한 암호입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
|**ftp_port**||배포자용 FTP 서비스의 포트 번호입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
|**ftp_subdirectory**||게시가 FTP를 사용하여 스냅샷 전파를 지원하는 경우 스냅샷 파일이 생성되는 위치를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
|**immediate_sync**|**true**|스냅샷 에이전트가 실행될 때마다 게시에 대한 동기화 파일이 생성되거나 다시 생성됩니다. 구독 전에 스냅샷 에이전트가 완료된 경우 구독자는 구독 후에 바로 동기화 파일을 받을 수 있습니다. 새 구독은 스냅샷 에이전트를 가장 최근에 실행하여 생성된 최신 동기화 파일을 가져옵니다. *independent_agent* 도 **true**여야 합니다. **Immediate_sync**에 대 한 자세한 내용은 아래 설명 부분을 참조 하세요.|  
||**false**|새 구독이 있는 경우에만 동기화 파일이 만들어집니다. 구독자는 스냅샷 에이전트가 시작되어 완료될 때까지는 구독 이후의 동기화 파일을 받을 수 없습니다.|  
|**independent_agent**|**true**|게시에는 전용 배포 에이전트가 있습니다.|  
||**false**|게시는 공유 배포 에이전트를 사용하며 게시/구독 데이터베이스 쌍마다 공유 에이전트가 있습니다.|  
|**p2p_continue_onconflict**|**true**|충돌이 감지되면 배포 에이전트에서 변경 내용을 계속 처리합니다.<br /> **주의:** 의 `FALSE`기본값을 사용 하는 것이 좋습니다. 이 옵션을로 `TRUE`설정 하면 배포 에이전트는 송신자 ID가 가장 높은 노드에서 충돌 하는 행을 적용 하 여 토폴로지의 데이터를 수렴 하려고 시도 합니다. 이 방법으로 데이터가 일치하게 되지 않는 경우도 있습니다. 충돌이 검색된 후 토폴로지의 일관성을 확인해야 합니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)의 "충돌 처리"를 참조하십시오.|  
||**false**|충돌이 감지되면 배포 에이전트에서 변경 내용 처리를 중지합니다.|  
|**post_snapshot_script**||초기 동기화 동안 다른 모든 복제된 개체 스크립트 및 데이터를 적용한 후에 배포 에이전트가 실행하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일의 위치를 지정합니다.|  
|**pre_snapshot_script**||초기 동기화 동안 다른 모든 복제된 개체 스크립트 및 데이터를 적용하기 전에 배포 에이전트가 실행하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일의 위치를 지정합니다.|  
|**publish_to_ActiveDirectory**|**true**|이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해서만 지원됩니다. 더 이상 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory에 게시 정보를 추가할 수 없습니다.|  
||**false**|Active Directory에서 게시 정보를 제거합니다.|  
|**queue_type**|**sql**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하여 트랜잭션을 저장합니다. 이 속성은 활성 구독이 없을 경우에만 변경될 수 있습니다.<br /><br /> 참고: 메시지 큐 사용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에 대 한 지원이 중단 되었습니다. *Value* 에 **msmq** 값을 지정 하면 오류가 발생 합니다.|  
|**repl_freq**|**주기가**|모든 로그 기반의 트랜잭션에 대한 출력을 게시합니다.|  
||**스냅숏에**|예약된 동기화 이벤트만 게시합니다.|  
|**replicate_ddl**|**1**|게시자에서 실행된 DDL(데이터 정의 언어) 문이 복제됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다.|  
||**0**|DDL 문은 복제되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시의 경우에는 이 속성을 변경할 수 없습니다. 피어 투 피어 복제를 사용할 때는 스키마 변경 내용의 복제를 해제할 수 없습니다.|  
|**replicate_partition_switch**|**true**|ALTER TABLE ... 게시 된 데이터베이스에 대해 실행 되는 SWITCH 문을 구독자에 복제 해야 합니다. 이 옵션은 *allow_partition_switch* 이 TRUE로 설정 된 경우에만 유효 합니다. 자세한 내용은 [분할 테이블 및 인덱스 복제](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)를 참조하세요.|  
||**false**|ALTER TABLE ... SWITCH 문은 구독자에 복제 되지 않아야 합니다.|  
|**보존**||구독 작업에 대 한 보존 기간 (시간)을 나타내는 **int** 입니다. 구독이 보존 기간 동안 활성화되지 않으면 제거됩니다.|  
|**snapshot_in_defaultfolder**|**true**|스냅샷 파일이 기본 스냅샷 폴더에 저장됩니다. *Alt_snapshot_folder*도 지정한 경우에는 스냅숏 파일이 기본 위치 및 대체 위치 모두에 저장 됩니다.|  
||**false**|스냅숏 파일은 *alt_snapshot_folder*에 지정 된 대체 위치에 저장 됩니다.|  
|**status**|**활성**|구독자는 게시가 생성되는 즉시 게시 데이터를 사용할 수 있습니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
||**라**|게시가 생성되면 구독자가 게시 데이터를 사용할 수 없습니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
|**sync_method**|**native**|구독을 동기화할 때 모든 테이블의 기본 모드 대량 복사 출력을 사용합니다.|  
||**자의**|구독을 동기화할 때 모든 테이블의 문자 모드 대량 복사 출력을 사용합니다.|  
||**노드당**|모든 테이블의 기본 모드 대량 복사 프로그램 출력을 사용하지만 스냅샷을 생성하는 동안에는 테이블을 잠그지 않습니다. 스냅샷 복제에는 적합하지 않습니다.|  
||**concurrent_c**|모든 테이블의 문자 모드 대량 복사 프로그램 출력을 사용하지만 스냅샷을 생성하는 동안에는 테이블을 잠그지 않습니다. 스냅샷 복제에는 적합하지 않습니다.|  
|**taskid**||이 속성은 더 이상 사용되지 않으며 지원되지 않습니다.|  
|**allow_drop**|**true**|트랜잭션 `DROP TABLE` 복제의 일부인 아티클에 대해 DLL 지원을 사용 하도록 설정 합니다. 지원 되는 최소 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 버전: 서비스 팩 2 이상 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 및 서비스 팩 1 이상. 추가 참조: [KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1)|
||**false**|트랜잭션 `DROP TABLE` 복제의 일부인 아티클에 대해 DLL 지원을 사용 하지 않도록 설정 합니다. 이 값은이 속성의 **기본값** 입니다.|
|**NULL** (기본값)||*속성*에 대해 지원 되는 값 목록을 반환 합니다.|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`이 저장 프로시저가 수행한 동작으로 인해 기존 스냅숏이 무효화 될 수 있음을 승인 합니다. *force_invalidate_snapshot* 은 **bit**이며 기본값은 **0**입니다.  
  - **0** 은 아티클에 대 한 변경으로 인해 스냅숏이 무효화 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅샷을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  - **1** 은 아티클에 대 한 변경으로 인해 스냅숏이 무효화 될 수 있음을 지정 합니다. 기존 구독에 새 스냅샷이 필요한 경우 이 값은 기존 스냅샷을 사용되지 않는 것으로 표시하고 새 스냅샷을 생성할 수 있는 권한을 부여합니다.   
변경 시 새 스냅샷의 생성을 필요로 하는 속성에 대해서는 주의 섹션을 참조하십시오.  
  
[**@force_reinit_subscription =** ] *force_reinit_subscription*  
 이 저장 프로시저가 수행한 동작으로 인해 기존 구독을 다시 초기화해야 할 수도 있습니다. *force_reinit_subscription* 은 **bit** 이며 기본값은 **0**입니다.  
  - **0** 은 아티클에 대 한 변경으로 인해 구독이 다시 초기화 되지 않도록 지정 합니다. 저장 프로시저가 기존 구독을 다시 초기화해야 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  - **1** 은 아티클에 대 한 변경으로 인해 기존 구독이 다시 초기화 되도록 지정 하며 구독을 다시 초기화할 수 있는 권한을 부여 합니다.  
  
`[ @publisher = ] 'publisher'`이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정 합니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
  > [!NOTE]  
  >  *publisher* 게시자에 대 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 한 아티클 속성을 변경할 때는 게시자를 사용 하면 안 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changepublication** 는 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 다음 속성을 변경한 후에는 새 스냅숏을 생성 해야 하며 *force_invalidate_snapshot* 매개 변수에 **1** 값을 지정 해야 합니다.  
-   **alt_snapshot_folder**  
-   **compress_snapshot**  
-   **enabled_for_het_sub**  
-   **ftp_address**  
-   **ftp_login**  
-   **ftp_password**  
-   **ftp_port**  
-   **ftp_subdirectory**  
-   **post_snapshot_script**  
-   **pre_snapshot_script**  
-   **snapshot_in_defaultfolder**  
-   **sync_mode**  
  
**Publish_to_active_directory** 매개 변수를 사용 하 여 Active Directory에서 게시 개체를 나열 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하려면 Active Directory에서 개체가 이미 만들어져 있어야 합니다.  
  
## <a name="impact-of-immediate-sync"></a>즉시 동기화의 영향  
 즉시 동기화가 설정되어 있으면 구독이 없어도 초기 스냅숏이 생성된 후에 로그의 모든 변경 내용이 즉시 추적됩니다. 기록 된 변경 내용은 고객이 백업을 사용 하 여 새 피어 노드를 추가할 때 사용 됩니다. 백업이 복원 된 후에는 백업이 수행 된 후에 발생 하는 다른 변경 내용과 피어가 동기화 됩니다. 배포 데이터베이스에서 명령이 추적 되므로 동기화 논리는 마지막으로 백업 된 LSN을 확인 하 고이를 시작 지점으로 사용 하 여 최대 보존 기간 내에 백업이 수행 된 경우에는 명령을 사용할 수 있습니다. 최소 보존 기간의 기본값은 0 시간이 고 최대 보존 기간은 24 시간입니다.  
  
 즉시 동기화를 해제하면 변경 내용이 최소 보존 기간으로 유지되고 이미 복제된 모든 트랜잭션은 즉시 정리됩니다. 즉시 동기화가 해제되고 기본 보존 기간으로 구성된 경우 백업 수행 후 필요한 변경 내용이 정리되어 새 피어 노드가 제대로 초기화되지 않을 수 있습니다. 왼쪽의 유일한 옵션은 토폴로지를 정지하는 것입니다. 즉시 동기화를 설정하면 보다 큰 유연성을 제공하며 P2P 복제에 권장되는 설정입니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_changepublication](../../relational-databases/replication/codesnippet/tsql/sp-changepublication-tra_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_changepublication**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Transact-sql&#41;sp_addpublication &#40;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [Transact-sql&#41;sp_droppublication &#40;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [Transact-sql&#41;sp_helppublication &#40;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
