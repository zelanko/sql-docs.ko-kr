---
title: sysmergepublications (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergepublications
- sysmergepublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepublications system table
ms.assetid: 7f82c6c3-22d1-47c0-a92b-4d64b98cc455
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d807b4b62eed46e99fdeaf0225fadb59b26042a8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62817039"
---
# <a name="sysmergepublications-transact-sql"></a>sysmergepublications(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스에 정의된 각 병합 게시당 한 개의 행을 포함합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|기본 서버의 이름입니다.|  
|**publisher_db**|**sysname**|기본 게시자 데이터베이스의 이름입니다.|  
|**name**|**sysname**|게시의 이름입니다.|  
|**description**|**nvarchar(255)**|게시에 대한 간단한 설명입니다.|  
|**retention**|**int**|단위 값으로 표시 됩니다는 여기서 전체 게시 집합의 보존 기간을 **retention_period_unit** 열입니다.|  
|**publication_type**|**tinyint**|게시가 필터링되었음을 나타냅니다.<br /><br /> **0** = 필터링 안 됩니다.<br /><br /> **1** = 필터링 합니다.|  
|**pubid**|**uniqueidentifier**|이 게시의 고유한 ID입니다. 게시를 추가할 때 생성됩니다.|  
|**designmasterid**|**uniqueidentifier**|나중에 사용하도록 예약되어 있습니다.|  
|**parentid**|**uniqueidentifier**|현재의 피어 또는 하위 집합 게시가 작성된 부모 게시입니다. 계층 구조적 게시 토폴로지에 사용됩니다.|  
|**sync_mode**|**tinyint**|해당 게시의 동기화 모드입니다.<br /><br /> **0** = 기본입니다.<br /><br /> **1** = 문자입니다.|  
|**allow_push**|**int**|게시에서 밀어내기 구독이 허용되는지 여부를 나타냅니다.<br /><br /> **0** = 밀어내기 구독이 허용 되지 않습니다.<br /><br /> **1** = 밀어내기 구독이 허용 됩니다.|  
|**allow_pull**|**int**|게시에서 끌어오기 구독이 허용되는지 여부를 나타냅니다.<br /><br /> **0** = 끌어오기 구독이 허용 되지 않습니다.<br /><br /> **1** = 끌어오기 구독이 허용 됩니다.|  
|**allow_anonymous**|**int**|게시에서 익명 구독이 허용되는지 여부를 나타냅니다.<br /><br /> **0** = 익명 구독이 허용 되지 않습니다.<br /><br /> **1** = 익명 구독이 허용 됩니다.|  
|**centralized_conflicts**|**int**|충돌 레코드가 게시자에 저장되는지 여부를 나타냅니다.<br /><br /> **0** = 충돌 레코드가 게시자에서 저장 되지 않습니다.<br /><br /> **1** = 충돌 레코드가 게시자에 저장 됩니다.|  
|**상태**|**tinyint**|나중에 사용하도록 예약되어 있습니다.|  
|**snapshot_ready**|**tinyint**|게시의 스냅숏 상태를 나타냅니다.<br /><br /> **0** = 스냅숏 사용에 대 한 준비 되지 않았습니다.<br /><br /> **1** = 스냅숏을 사용할 준비가 되었습니다.<br /><br /> **2** 새 스냅숏으로 =이 게시를 만들어야 합니다.|  
|**enabled_for_internet**|**bit**|게시에 대한 동기화 파일이 FTP 및 다른 서비스를 통해 인터넷에 제공되는지 여부를 나타냅니다.<br /><br /> **0** = 동기화 파일은 인터넷에서 액세스할 수 있습니다.<br /><br /> **1** = 동기화 파일을 인터넷에서 액세스할 수 없습니다.|  
|**dynamic_filters**|**bit**|매개 변수가 있는 행 필터를 사용하여 게시를 필터링하는지 여부를 표시합니다.<br /><br /> **0** = 게시가 행 필터링 되지 않습니다.<br /><br /> **1** = 게시가 행 필터링 됩니다.|  
|**snapshot_in_defaultfolder**|**bit**|스냅숏 파일을 기본 폴더에 저장하는지 여부를 지정합니다.<br /><br /> **0** = 스냅숏 파일이 기본 폴더에 있습니다.<br /><br /> **1** = 스냅숏 파일에서 지정 된 위치에 저장 됩니다 **alt_snapshot_folder**합니다.|  
|**alt_snapshot_folder**|**nvarchar(255)**|스냅숏에 대한 대체 폴더의 위치입니다.|  
|**pre_snapshot_script**|**nvarchar(255)**|에 대 한 포인터를 합니다. **sql** 전에 모든 복제 개체의 병합 에이전트가 실행 되는 파일을 구독자에서 스냅숏을 적용할 때 스크립트입니다.|  
|**post_snapshot_script**|**nvarchar(255)**|에 대 한 포인터를 합니다. **sql** 는 병합 에이전트를 실행 한 후 모든 다른 복제 개체 스크립트 및 데이터는 초기 동기화 동안 적용 된 파일입니다.|  
|**compress_snapshot**|**bit**|지정 여부를에 작성 한 스냅숏을 합니다 **alt_snapshot_folder** 위치에 압축는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 형식으로 합니다. **0** 파일 압축 되지 않도록 지정 합니다.|  
|**ftp_address**|**sysname**|배포자용 FTP(파일 전송 프로토콜) 서비스의 네트워크 주소입니다. FTP를 사용하는 경우 병합 에이전트가 선택할 수 있도록 게시 스냅숏 파일을 둘 장소를 지정합니다.|  
|**ftp_port**|**int**|배포자용 FTP 서비스의 포트 번호입니다.|  
|**ftp_subdirectory**|**nvarchar(255)**|병합 에이전트가 스냅숏 파일을 선택할 수 있는 하위 디렉터리입니다.|  
|**ftp_login**|**sysname**|FTP 서비스에 연결하는 데 사용되는 사용자 이름입니다.|  
|**ftp_password**|**nvarchar(524)**|FTP 서비스에 연결하는 데 필요한 사용자 암호입니다.|  
|**conflict_retention**|**int**|충돌을 보존할 보존 기간을 일 수로 지정합니다. 이 기간이 지나면 충돌 행은 충돌 테이블에서 제거됩니다.|  
|**keep_before_values**|**int**|해당 게시에 대해 동기화가 최적화되는지 여부를 지정합니다.<br /><br /> **0** = 동기화가 최적화 되지 않습니다 및 모든 구독자에 게 보낸 파티션은 파티션에서 데이터가 변경 될 때 확인 됩니다.<br /><br /> **1** = 동기화가 최적화 및 변경된 된 파티션에 행을 가진 구독자만 영향을 받습니다.|  
|**allow_subscription_copy**|**bit**|구독 데이터베이스 복사 기능의 사용 여부를 지정합니다. **0** 복사 허용 되지 않음을 의미 합니다.|  
|**allow_synctoalternate**|**bit**|대체 동기화 파트너가 해당 게시자와 동기화될 수 있는지 여부를 지정합니다. **0** 동기화 파트너가 허용 되지 않음을 의미 합니다.|  
|**validate_subscriber_info**|**nvarchar(500)**|구독자 정보를 검색하고 구독자에서 매개 변수가 있는 행 필터링 조건의 유효성을 검사하는 데 사용하는 함수를 나열합니다.|  
|**ad_guidname**|**sysname**|게시를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory에 게시할지 여부를 지정합니다. 올바른 GUID 지정 Active Directory에 게시 하 고 GUID는 해당 Active Directory 게시 개체인 **objectGUID**합니다. NULL인 경우 게시는 Active Directory에 게시되지 않습니다.|  
|**backward_comp_level**|**int**|데이터베이스 호환성 수준이며 다음 값 중 하나입니다.<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|**max_concurrent_merge**|**int**|최대 동시 병합 프로세스 수입니다. 값이 **0** 에이 속성의 지정된 된 시간에 실행 중인 동시 병합 프로세스 수 제한이 있다는 것을 의미 합니다. 이 속성은 병합 게시에 대해 한 번에 실행할 수 있는 동시 병합 프로세스의 수를 제한합니다. 실행하도록 허용된 값보다 많은 스냅숏 프로세스를 동시에 실행하도록 예약할 경우 초과 작업은 큐에 두고 현재 실행 중인 병합 프로세스가 완료될 때까지 기다립니다.|  
|**max_concurrent_dynamic_snapshots**|**int**|병합 게시에 대해 동시에 실행할 수 있는 필터링된 동시 데이터 스냅숏 세션의 최대 수입니다. 하는 경우 **0**, 언제 든 지 게시에 대해 동시에 실행할 수 있는 필터링 된 동시 데이터 스냅숏 세션의 최대 수에 대 한 제한은 없습니다. 이 속성은 병합 게시에 대해 한 번에 실행할 수 있는 동시 스냅숏 프로세스의 수를 제한합니다. 실행하도록 허용된 값보다 많은 스냅숏 프로세스를 동시에 실행하도록 예약할 경우 초과 작업은 큐에 두고 현재 실행 중인 병합 프로세스가 완료될 때까지 기다립니다.|  
|**use_partition_groups**|**smallint**|게시에서 사전 계산 파티션을 사용하는지 여부를 지정합니다.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|게시의 매개 변수가 있는 행 필터에 사용되는 함수의 목록으로서 세미콜론으로 구분됩니다.|  
|**partition_id_eval_proc**|**sysname**|할당된 파티션 ID를 확인하기 위해 구독자의 병합 에이전트가 실행하는 프로시저의 이름을 지정합니다.|  
|**publication_number**|**smallint**|에 대 한 2 바이트 매핑을 제공 하는 id 열을 지정 **pubid**합니다. **pubid** 이지만 게시 번호는 고유 specififed 데이터베이스에만 게시에 대 한 전역적으로 고유 식별자입니다.|  
|**replicate_ddl**|**int**|게시에 대해 스키마 복제가 지원될지 여부를 나타냅니다.<br /><br /> **0** = DDL 문이 복제 되지 않습니다.<br /><br /> **1** DDL = 게시자에서 실행 하는 문이 복제 됩니다.<br /><br /> 자세한 내용은 [게시 데이터베이스의 스키마 변경](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)을 참조하세요.|  
|**allow_subscriber_initiated_snapshot**|**bit**|구독자가 매개 변수가 있는 필터를 사용하여 게시에 대한 스냅숏을 생성하는 프로세스를 시작할 수 있음을 나타냅니다. **1** 구독자가 스냅숏 프로세스를 시작할 수 있음을 나타냅니다.|  
|**dynamic_snapshot_queue_timeout**|**int**|매개 변수가 있는 필터를 사용할 때 스냅숏 생성 프로세스가 시작될 때까지 구독자가 큐에서 대기하는 시간(분)을 지정합니다.|  
|**dynamic_snapshot_ready_timeout**|**int**|매개 변수가 있는 필터를 사용할 때 스냅숏 생성 프로세스가 완료될 때까지 구독자가 대기하는 시간(분)을 지정합니다.|  
|**distributor**|**sysname**|게시 배포자의 이름입니다.|  
|**snapshot_jobid**|**binary(16)**|구독자가 스냅숏 생성 프로세스를 시작할 수 있을 때 스냅숏을 생성하는 에이전트 작업을 식별합니다.|  
|**allow_web_synchronization**|**bit**|게시 웹 동기화에 사용 되는지 여부를 지정 합니다. 여기서 **1** 웹 동기화는 게시에 대해 사용할 수 있음을 의미 합니다.|  
|**web_synchronization_url**|**nvarchar(500)**|웹 동기화에 사용되는 인터넷 URL의 기본값을 지정합니다.|  
|**allow_partition_realignment**|**bit**|게시자의 행 수정으로 인해 파티션이 변경된 경우 구독자에게 삭제 내용을 보낼지 여부를 나타냅니다.<br /><br /> **0** 이전에서 = 데이터 파티션 여기서 게시자에서이 데이터 변경 내용이 구독자로 복제 되지 것입니다 하지만 구독자에서 변경 내용을 게시자로 복제는 구독자에 남게 됩니다.<br /><br /> **1** = 구독자의 파티션에 더 포함 되지 않은 데이터를 제거 하 여 파티션 변경 결과 반영 하도록 구독자에 게 삭제 합니다.<br /><br /> 자세한 내용은 [sp_addmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)합니다.<br /><br /> 참고: 그러나이 값이 구독자에 남은 데이터는 **0** 엄격 하 게 적용 되지 복제 시스템에 의해; 읽기 전용인 것 처럼 처리 해야 합니다.|  
|**retention_period_unit**|**tinyint**|정의할 때 사용할 단위를 정의 *보존*에 다음이 값 중 하나일 수 있습니다.<br /><br /> **0** = 일입니다.<br /><br /> **1** = 주입니다.<br /><br /> **2** = 월.<br /><br /> **3** 연도입니다.|  
|**decentralized_conflicts**|**int**|충돌을 발생시킨 구독자에 충돌 레코드가 저장되는지 여부를 지정합니다.<br /><br /> **0** = 충돌 레코드가 구독자에 저장 되지 않습니다.<br /><br /> **1** = 충돌 레코드가 구독자에 저장 됩니다.|  
|**generation_leveling_threshold**|**int**|하나의 생성에 포함되는 변경 내용 수를 지정합니다. 생성은 게시자 또는 구독자에 배달되는 변경 내용 모음입니다.|  
|**automatic_reinitialization_policy**|**bit**|자동 다시 초기화가 발생하기 전에 구독자에서 변경 사항을 업로드할지 여부를 나타냅니다.<br /><br /> **1** = 자동 다시 초기화가 발생 하기 전에 구독자에서 변경 내용이 업로드 됩니다.<br /><br /> **0** = 자동 다시 초기화 하기 전에 변경 내용이 업로드 되지 않습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)  
  
  
