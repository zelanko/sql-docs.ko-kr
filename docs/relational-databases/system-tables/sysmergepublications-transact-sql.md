---
description: sysmergepublications(Transact-SQL)
title: sysmergepublications (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 51a23c71b99ff57cb9dda76dd65cfc25fcf4a097
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473215"
---
# <a name="sysmergepublications-transact-sql"></a>sysmergepublications(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  데이터베이스에 정의된 각 병합 게시당 한 개의 행을 포함합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**발행자**|**sysname**|기본 서버의 이름입니다.|  
|**publisher_db**|**sysname**|기본 게시자 데이터베이스의 이름입니다.|  
|**name**|**sysname**|게시의 이름입니다.|  
|**description**|**nvarchar(255)**|게시에 대한 간단한 설명입니다.|  
|**보존**|**int**|전체 게시 집합의 보존 기간으로, 단위는 **retention_period_unit** 열의 값으로 표시 됩니다.|  
|**publication_type**|**tinyint**|게시가 필터링되었음을 나타냅니다.<br /><br /> **0** = 필터링 되지 않습니다.<br /><br /> **1** = 필터링 됨|  
|**pubid**|**uniqueidentifier**|이 게시의 고유한 ID입니다. 게시를 추가할 때 생성됩니다.|  
|**designmasterid**|**uniqueidentifier**|나중에 사용하기 위해 예약되어 있습니다.|  
|**parentid**|**uniqueidentifier**|현재의 피어 또는 하위 집합 게시가 작성된 부모 게시입니다. 계층 구조적 게시 토폴로지에 사용됩니다.|  
|**sync_mode**|**tinyint**|해당 게시의 동기화 모드입니다.<br /><br /> **0** = 네이티브<br /><br /> **1** = 문자|  
|**allow_push**|**int**|게시에서 밀어내기 구독이 허용되는지 여부를 나타냅니다.<br /><br /> **0** = 밀어넣기 구독이 허용 되지 않습니다.<br /><br /> **1** = 밀어넣기 구독이 허용 됩니다.|  
|**allow_pull**|**int**|게시에서 끌어오기 구독이 허용되는지 여부를 나타냅니다.<br /><br /> **0** = 끌어오기 구독이 허용 되지 않습니다.<br /><br /> **1** = 끌어오기 구독이 허용 됩니다.|  
|**allow_anonymous**|**int**|게시에서 익명 구독이 허용되는지 여부를 나타냅니다.<br /><br /> **0** = 익명 구독이 허용 되지 않습니다.<br /><br /> **1** = 익명 구독이 허용 됩니다.|  
|**centralized_conflicts**|**int**|충돌 레코드가 게시자에 저장되는지 여부를 나타냅니다.<br /><br /> **0** = 충돌 레코드가 게시자에 저장 되지 않습니다.<br /><br /> **1** = 충돌 레코드가 게시자에 저장 됩니다.|  
|**status**|**tinyint**|나중에 사용하기 위해 예약되어 있습니다.|  
|**snapshot_ready**|**tinyint**|게시의 스냅샷 상태를 나타냅니다.<br /><br /> **0** = 스냅숏을 사용할 준비가 되지 않았습니다.<br /><br /> **1** = 스냅숏을 사용할 준비가 되었습니다.<br /><br /> **2** =이 게시에 대 한 새 스냅숏을 만들어야 합니다.|  
|**enabled_for_internet**|**bit**|게시에 대한 동기화 파일이 FTP 및 다른 서비스를 통해 인터넷에 제공되는지 여부를 나타냅니다.<br /><br /> **0** = 인터넷에서 동기화 파일에 액세스할 수 있습니다.<br /><br /> **1** = 인터넷에서 동기화 파일에 액세스할 수 없습니다.|  
|**dynamic_filters**|**bit**|매개 변수가 있는 행 필터를 사용하여 게시를 필터링하는지 여부를 표시합니다.<br /><br /> **0** = 게시가 행 필터링 되지 않습니다.<br /><br /> **1** = 게시가 행 필터링 됩니다.|  
|**snapshot_in_defaultfolder**|**bit**|스냅샷 파일을 기본 폴더에 저장하는지 여부를 지정합니다.<br /><br /> **0** = 스냅숏 파일이 기본 폴더에 있습니다.<br /><br /> **1** = 스냅숏 파일이 **alt_snapshot_folder**에 지정 된 위치에 저장 됩니다.|  
|**alt_snapshot_folder**|**nvarchar(255)**|스냅샷에 대한 대체 폴더의 위치입니다.|  
|**pre_snapshot_script**|**nvarchar(255)**|에 대 한 포인터입니다. 구독자에서 스냅숏을 적용할 때 병합 에이전트 복제 개체 스크립트 보다 먼저 실행 되는 **sql** 파일입니다.|  
|**post_snapshot_script**|**nvarchar(255)**|에 대 한 포인터입니다. 초기 동기화 중에 다른 모든 복제 개체 스크립트 및 데이터를 적용 한 후 병합 에이전트 실행 되는 **sql** 파일입니다.|  
|**compress_snapshot**|**bit**|**Alt_snapshot_folder** 위치에 작성 된 스냅숏이 CAB 형식으로 압축 되는지 여부를 지정 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] . **0** 은 파일이 압축 되지 않도록 지정 합니다.|  
|**ftp_address**|**sysname**|배포자용 FTP(파일 전송 프로토콜) 서비스의 네트워크 주소입니다. FTP를 사용하는 경우 병합 에이전트가 선택할 수 있도록 게시 스냅샷 파일을 둘 장소를 지정합니다.|  
|**ftp_port**|**int**|배포자용 FTP 서비스의 포트 번호입니다.|  
|**ftp_subdirectory**|**nvarchar(255)**|병합 에이전트가 스냅샷 파일을 선택할 수 있는 하위 디렉터리입니다.|  
|**ftp_login**|**sysname**|FTP 서비스에 연결하는 데 사용되는 사용자 이름입니다.|  
|**ftp_password**|**nvarchar (524)**|FTP 서비스에 연결하는 데 필요한 사용자 암호입니다.|  
|**conflict_retention**|**int**|충돌을 보존할 보존 기간을 일 수로 지정합니다. 이 기간이 지나면 충돌 행은 충돌 테이블에서 제거됩니다.|  
|**keep_before_values**|**int**|해당 게시에 대해 동기화가 최적화되는지 여부를 지정합니다.<br /><br /> **0** = 동기화가 최적화 되지 않으며 파티션에서 데이터가 변경 될 때 모든 구독자에 게 전송 되는 파티션이 확인 됩니다.<br /><br /> **1** = 동기화가 최적화 되었으며 변경 된 파티션에 행이 있는 구독자만 영향을 받습니다.|  
|**allow_subscription_copy**|**bit**|구독 데이터베이스 복사 기능의 사용 여부를 지정합니다. **0** 은 복사가 허용 되지 않음을 의미 합니다.|  
|**allow_synctoalternate**|**bit**|대체 동기화 파트너가 해당 게시자와 동기화될 수 있는지 여부를 지정합니다. **0** 은 동기화 파트너가 허용 되지 않음을 의미 합니다.|  
|**validate_subscriber_info**|**nvarchar (500)**|구독자 정보를 검색하고 구독자에서 매개 변수가 있는 행 필터링 조건의 유효성을 검사하는 데 사용하는 함수를 나열합니다.|  
|**ad_guidname**|**sysname**|게시를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory에 게시할지 여부를 지정합니다. 유효한 GUID는 게시가 Active Directory 게시 되도록 지정 하 고 GUID는 해당 Active Directory 게시 개체 **objectGUID**입니다. NULL인 경우 게시는 Active Directory에 게시되지 않습니다.|  
|**backward_comp_level**|**int**|데이터베이스 호환성 수준이며 다음 값 중 하나일 수 있습니다.<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .<br /><br /> **100**  =  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] .|  
|**max_concurrent_merge**|**int**|최대 동시 병합 프로세스 수입니다. 이 속성 값이 **0** 이면 지정 된 시간에 실행 중인 동시 병합 프로세스 수에 제한이 없음을 의미 합니다. 이 속성은 병합 게시에 대해 한 번에 실행할 수 있는 동시 병합 프로세스의 수를 제한합니다. 실행하도록 허용된 값보다 많은 스냅샷 프로세스를 동시에 실행하도록 예약할 경우 초과 작업은 큐에 두고 현재 실행 중인 병합 프로세스가 완료될 때까지 기다립니다.|  
|**max_concurrent_dynamic_snapshots**|**int**|병합 게시에 대해 동시에 실행할 수 있는 필터링된 동시 데이터 스냅샷 세션의 최대 수입니다. **0**인 경우 지정 된 시간에 게시에 대해 동시에 실행할 수 있는 필터링 된 동시 데이터 스냅숏 세션의 최대 수에 제한이 없습니다. 이 속성은 병합 게시에 대해 한 번에 실행할 수 있는 동시 스냅샷 프로세스의 수를 제한합니다. 실행하도록 허용된 값보다 많은 스냅샷 프로세스를 동시에 실행하도록 예약할 경우 초과 작업은 큐에 두고 현재 실행 중인 병합 프로세스가 완료될 때까지 기다립니다.|  
|**use_partition_groups**|**smallint**|게시에서 사전 계산 파티션을 사용하는지 여부를 지정합니다.|  
|**dynamic_filters_function_list**|**nvarchar (500)**|게시의 매개 변수가 있는 행 필터에 사용되는 함수의 목록으로서 세미콜론으로 구분됩니다.|  
|**partition_id_eval_proc**|**sysname**|할당된 파티션 ID를 확인하기 위해 구독자의 병합 에이전트가 실행하는 프로시저의 이름을 지정합니다.|  
|**publication_number**|**smallint**|**Pubid**에 2 바이트 매핑을 제공 하는 id 열을 지정 합니다. **pubid** 는 게시에 대 한 전역적으로 고유한 식별자 이지만 게시 번호는 지정 된 데이터베이스 에서만 고유 합니다.|  
|**replicate_ddl**|**int**|게시에 대해 스키마 복제가 지원될지 여부를 나타냅니다.<br /><br /> **0** = DDL 문이 복제 되지 않습니다.<br /><br /> **1** = 게시자에서 실행 된 DDL 문이 복제 됩니다.<br /><br /> 자세한 내용은 [게시 데이터베이스의 스키마 변경](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)을 참조하세요.|  
|**allow_subscriber_initiated_snapshot**|**bit**|구독자가 매개 변수가 있는 필터를 사용하여 게시에 대한 스냅샷을 생성하는 프로세스를 시작할 수 있음을 나타냅니다. **1** 은 구독자가 스냅숏 프로세스를 시작할 수 있음을 나타냅니다.|  
|**dynamic_snapshot_queue_timeout**|**int**|매개 변수가 있는 필터를 사용할 때 스냅샷 생성 프로세스가 시작될 때까지 구독자가 큐에서 대기하는 시간(분)을 지정합니다.|  
|**dynamic_snapshot_ready_timeout**|**int**|매개 변수가 있는 필터를 사용할 때 스냅샷 생성 프로세스가 완료될 때까지 구독자가 대기하는 시간(분)을 지정합니다.|  
|**총판**|**sysname**|게시 배포자의 이름입니다.|  
|**snapshot_jobid**|**binary(16)**|구독자가 스냅샷 생성 프로세스를 시작할 수 있을 때 스냅샷을 생성하는 에이전트 작업을 식별합니다.|  
|**allow_web_synchronization**|**bit**|게시가 웹 동기화를 사용 하도록 설정 되었는지 여부를 지정 합니다. **1** 은 게시에 대해 웹 동기화가 사용 하도록 설정 되어 있음을 의미 합니다.|  
|**web_synchronization_url**|**nvarchar (500)**|웹 동기화에 사용되는 인터넷 URL의 기본값을 지정합니다.|  
|**allow_partition_realignment**|**bit**|게시자의 행 수정으로 인해 파티션이 변경된 경우 구독자에게 삭제 내용을 보낼지 여부를 나타냅니다.<br /><br /> **0** = 이전 파티션의 데이터가 구독자에 남게 됩니다. 게시자에서이 데이터에 대 한 변경 내용이이 구독자에 복제 되지 않지만 구독자에서 변경한 내용은 게시자에 복제 됩니다.<br /><br /> **1** = 더 이상 구독자의 파티션에 속하지 않는 데이터를 제거 하 여 파티션 변경 결과를 반영 하기 위해 구독자에 삭제 합니다.<br /><br /> 자세한 내용은 [sp_addmergepublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)를 참조 하세요.<br /><br /> 참고:이 값이 **0** 인 경우 구독자에 남아 있는 데이터는 읽기 전용인 것 처럼 처리 되어야 합니다. 그러나이는 복제 시스템에서 엄격 하 게 적용 되지 않습니다.|  
|**retention_period_unit**|**tinyint**|*보존 기간*을 정의할 때 사용 되는 단위를 정의 합니다 .이 값은 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 일<br /><br /> **1** = 주<br /><br /> **2** = 월<br /><br /> **3** = 년|  
|**decentralized_conflicts**|**int**|충돌을 발생시킨 구독자에 충돌 레코드가 저장되는지 여부를 지정합니다.<br /><br /> **0** = 충돌 레코드가 구독자에 저장 되지 않습니다.<br /><br /> **1** = 충돌 레코드가 구독자에 저장 됩니다.|  
|**generation_leveling_threshold**|**int**|하나의 생성에 포함되는 변경 내용 수를 지정합니다. 생성은 게시자 또는 구독자에 배달되는 변경 내용 모음입니다.|  
|**automatic_reinitialization_policy**|**bit**|자동 다시 초기화가 발생하기 전에 구독자에서 변경 사항을 업로드할지 여부를 나타냅니다.<br /><br /> **1** = 자동 다시 초기화가 수행 되기 전에 구독자에서 변경 내용이 업로드 됩니다.<br /><br /> **0** = 자동 다시 초기화 전에 변경 내용이 업로드 되지 않습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰 ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Transact-sql&#41;sp_addmergepublication &#40;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [Transact-sql&#41;sp_changemergepublication &#40;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)  
  
  
