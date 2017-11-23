---
title: sp_changemergepublication (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_changemergepublication_TSQL
- sp_changemergepublication
helpviewer_keywords: sp_changemergepublication
ms.assetid: 81fe1994-7678-4852-980b-e02fedf1e796
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3f1798cd29ac1ee4afc0d7323866e37711291851
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spchangemergepublication-transact-sql"></a>sp_changemergepublication(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 게시의 속성을 변경합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changemergepublication [ @publication= ] 'publication'  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication=**] **'***게시***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@property=**] **'***속성***'**  
 지정된 게시에 대해 변경할 속성입니다. *속성* 은 **sysname**, 수 값 중 하나에 나열 될 다음 표에서 합니다.  
  
 [  **@value=**] **'***값***'**  
 지정한 속성의 새 값입니다. *값* 은 **nvarchar (255)**, 수 값 중 하나에 나열 될 다음 표에서 합니다.  
  
 이 표에서는 변경할 수 있는 게시의 속성 및 그 속성의 값에 대한 제한에 대해 설명합니다.  
  
|속성|값|Description|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|익명 구독을 허용합니다.|  
||**false**|익명 구독을 허용하지 않습니다.|  
|**allow_partition_realignment**|**true**|더 이상 구독자의 파티션에 속하지 않는 데이터를 제거하여 파티션 변경 결과를 반영할 수 있도록 구독자로 삭제 내용을 보냅니다. 이것이 기본 동작입니다.|  
||**false**|이전 파티션의 데이터가 구독자에 남습니다. 게시자에서 이 데이터에 대해 변경한 내용은 구독자로 복제되지 않습니다. 대신 구독자에서 변경한 내용이 게시자로 복제됩니다. 기록 목적으로 이전 파티션의 데이터에 액세스해야 하는 경우 구독에 해당 데이터를 보존하기 위해 사용합니다.|  
|**allow_pull**|**true**|지정된 게시에 대해 끌어오기 구독을 허용합니다.|  
||**false**|지정된 게시에 대해 끌어오기 구독을 허용하지 않습니다.|  
|**allow_push**|**true**|지정된 게시에 대해 밀어넣기 구독을 허용합니다.|  
||**false**|지정된 게시에 대해 밀어넣기 구독을 허용하지 않습니다.|  
|**allow_subscriber_initiated_snapshot**|**true**|구독자가 스냅숏 프로세스를 시작할 수 있습니다.|  
||**false**|구독자가 스냅숏 프로세스를 시작할 수 없습니다.|  
|**allow_subscription_copy**|**true**|이 게시를 구독하는 구독 데이터베이스를 복사할 수 있습니다.|  
||**false**|이 게시를 구독하는 구독 데이터베이스를 복사할 수 없습니다.|  
|**allow_synctoalternate**|**true**|이 게시자와 동기화할 수 있는 대체 동기화 파트너를 허용합니다.|  
||**false**|이 게시자와 동기화할 수 있는 대체 동기화 파트너를 허용하지 않습니다.|  
|**allow_web_synchronization**|**true**|HTTPS를 통해 구독을 동기화할 수 있습니다.|  
||**false**|HTTPS를 통해 구독을 동기화할 수 없습니다.|  
|**alt_snapshot_folder**||스냅숏의 대체 폴더 위치를 지정합니다.|  
|**automatic_reinitialization_policy**|**1**|구독을 다시 초기화하기 전에 구독자에서 변경 내용을 업로드합니다.|  
||**0**|변경 내용을 업로드하지 않고 구독을 다시 초기화합니다.|  
|**centralized_conflicts**|**true**|모든 충돌 레코드가 게시자에 저장됩니다. 이 속성을 변경할 경우 기존 구독자를 다시 초기화해야 합니다.|  
||**false**|충돌 레코드가 충돌 해결 중인 서버에 저장됩니다. 이 속성을 변경할 경우 기존 구독자를 다시 초기화해야 합니다.|  
|**compress_snapshot**|**true**|대체 스냅숏 폴더의 스냅숏을 CAB 형식으로 압축합니다. 기본 스냅숏 폴더의 스냅숏은 압축할 수 없습니다. 이 속성을 변경하려면 새 스냅숏이 필요합니다.|  
||**false**|기본적으로 스냅숏은 압축되지 않습니다. 이 속성을 변경하려면 새 스냅숏이 필요합니다.|  
|**conflict_logging**|**publisher**|충돌 레코드가 게시자에 저장됩니다.|  
||**subscriber**|충돌 레코드가 충돌을 발생시킨 구독자에 저장됩니다. 에 대 한 지원 되지 않습니다. [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자*합니다.*|  
||**both**|충돌 레코드가 게시자와 구독자 둘 다에 저장됩니다.|  
|**conflict_retention**||**int** 충돌을 보존할 일 단위로 보존 기간을 지정 하는 합니다. 설정 *conflict_retention* 를 **0** 의미 없는 충돌 정리가 필요 합니다.|  
|**설명**||게시에 대한 설명입니다.|  
|**dynamic_filters**|**true**|동적 절에 따라 게시를 필터링합니다.|  
||**false**|게시를 동적으로 필터링하지 않습니다.|  
|**enabled_for_internet**|**true**|인터넷에서 게시를 사용할 수 있습니다. FTP(파일 전송 프로토콜)를 사용하여 구독자로 스냅숏을 전송할 수 있습니다. _게시에 대한 동기화 파일은 C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\ftp 디렉터리에 저장됩니다.|  
||**false**|인터넷에서 게시를 사용할 수 없습니다.|  
|**ftp_address**||배포자용 FTP 서비스의 네트워크 주소입니다. 게시 스냅숏 파일이 저장될 위치를 지정합니다.|  
|**ftp_login**||FTP 서비스에 연결하는 데 사용되는 사용자 이름입니다.|  
|**ftp_password**||FTP 서비스에 연결하는 데 사용되는 사용자 암호입니다.|  
|**ftp_port**||배포자용 FTP 서비스의 포트 번호입니다. 게시 스냅숏 파일이 저장될 FTP 사이트의 TCP 포트 번호를 지정합니다.|  
|**ftp_subdirectory**||게시가 FTP를 사용하여 스냅숏 전파를 지원하는 경우 스냅숏 파일이 생성되는 위치를 지정합니다.|  
|**generation_leveling_threshold**|**int**|하나의 생성에 포함되는 변경 내용 수를 지정합니다. 생성은 게시자 또는 구독자에 배달되는 변경 내용 모음입니다.|  
|**keep_partition_changes**|**true**|동기화가 최적화됩니다. 변경된 파티션에 행이 있는 구독자만 영향을 받습니다. 이 속성을 변경하려면 새 스냅숏이 필요합니다.|  
||**false**|동기화가 최적화되지 않습니다. 구독자로 보낸 파티션은 파티션에서 데이터가 변경될 때 확인됩니다. 이 속성을 변경하려면 새 스냅숏이 필요합니다.|  
|**max_concurrent_merge**||이 한 **int** 은 게시에 대해 실행할 수 있는 동시 병합 프로세스의 최대 수를 나타내는입니다. 0이면 제한이 없습니다. 동시에 실행하도록 예약된 병합 프로세스 수가 이 값보다 클 경우 초과 작업은 currentlmerge 프로세스가 완료될 때까지 큐에서 기다립니다.|  
|**max_concurrent_dynamic_snapshots**||이 한 **int** 매개 변수가 있는 행 필터를 나타내는 필터링 된 데이터를 생성 하려면 스냅숏 세션의 최대 수 스냅숏 사용 하는 병합 게시에 대해 동시에 실행할 수 있는 있는지 합니다. 경우 **0**, 제한은 없습니다. 동시에 실행되도록 예약된 스냅숏 프로세스 수가 이 값보다 클 경우 초과 작업은 현재 병합 프로세스가 완료될 때까지 큐에서 기다립니다.|  
|**post_snapshot_script**||에 대 한 포인터를 지정 된 **.sql** 파일 위치입니다. 배포 에이전트 또는 병합 에이전트는 초기 동기화 동안 다른 복제된 개체 스크립트 및 데이터를 모두 적용한 후에 포스트 스냅숏 스크립트를 실행합니다. 이 속성을 변경하려면 새 스냅숏이 필요합니다.|  
|**pre_snapshot_script**||에 대 한 포인터를 지정 된 **.sql** 파일 위치입니다. 병합 에이전트는 구독자에서 스냅숏을 적용할 때 복제된 개체 스크립트를 실행하기 전에 프리 스냅숏 스크립트를 실행합니다. 이 속성을 변경하려면 새 스냅숏이 필요합니다.|  
|**publication_compatibility_level**|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
||**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**publish_to_activedirectory**|**true**|이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해서만 지원됩니다. 더 이상 Active Directory에 게시 정보를 추가할 수 없습니다.|  
||**false**|Active Directory에서 게시 정보를 제거합니다.|  
|**replicate_ddl**|**1**|게시자에서 실행되는 DDL(데이터 정의 언어) 문이 복제됩니다.|  
||**0**|DDL 문은 복제되지 않습니다.|  
|**보존**||이 한 **int** 의 수를 나타내는 *retention_period_unit* 지정된 된 게시에 대 한 변경 내용을 저장 하는 단위입니다. 보존 기간 내에 구독이 동기화되지 않고 구독이 받은 보류 중인 변경 내용이 배포자에서 정리 작업에 의해 제거되었으면 구독은 만료되며 다시 초기화해야 합니다. 허용되는 최대 보존 기간은 현재 날짜부터 9999년 12월 31일까지의 일 수입니다.<br /><br /> 참고: 병합 게시에 대 한 보존 기간에 서로 다른 시간대에 구독자를 수용 하기 위해 24 시간의 유예 기간에 있습니다.|  
|**retention_period_unit**|**일**|보존 기간(일)을 지정합니다.|  
||**주**|보존 기간(주)을 지정합니다.|  
||**월**|보존 기간(월)을 지정합니다.|  
||**연도**|보존 기간(년)을 지정합니다.|  
|**snapshot_in_defaultfolder**|**true**|스냅숏 파일이 기본 스냅숏 폴더에 저장됩니다.|  
||**false**|스냅숏 파일에 지정 된 대체 위치에 저장 됩니다 *alt_snapshot_folder*합니다. 이 조합은 스냅숏 파일이 기본 위치 및 대체 위치 양쪽 모두에 저장되도록 지정할 수 있습니다.|  
|**snapshot_ready**|**true**|게시에 대한 스냅숏을 사용할 수 있습니다.|  
||**false**|게시에 대한 스냅숏을 사용할 수 없습니다.|  
|**상태**|**활성**|게시가 활성 상태입니다.|  
||**비활성**|게시가 비활성 상태입니다.|  
|**sync_mode**|**네이티브** 또는<br /><br /> **네이티브 bcp**|초기 스냅숏에 모든 테이블의 기본 모드 대량 복사 프로그램 출력을 사용합니다.|  
||**문자**<br /><br /> 또는 **bcp 문자**|초기 스냅숏에 모든 테이블의 문자 모드 대량 복사 프로그램 출력을 사용합니다. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자의 경우에 필요합니다.|  
|**use_partition_groups**<br /><br /> 참고: 경우 partition_groups를 사용한 후 사용 하 여 되돌릴 **setupbelongs**, 설정 및 **use_partition_groups = false** 에 **changemergearticle**, 사용 하지 않을 스냅숏을 생성 한 후에 제대로 반영 합니다. 스냅숏이 생성하는 트리거는 파티션 그룹과 호환됩니다.<br /><br /> 이 시나리오를 해결 하는 상태를 비활성으로 설정, 수정 하는 **use_partition_groups**, 상태를 활성으로 설정 합니다.|**true**|게시에서 사전 계산 파티션을 사용합니다.|  
||**false**|게시에서 사전 계산 파티션을 사용하지 않습니다.|  
|**validate_subscriber_info**||구독자 정보를 검색하는 데 사용할 함수를 나열하고 구독자가 정보가 일관성 있게 분할되는지 확인하기 위해 사용하는 동적 필터링 조건의 유효성을 검사합니다.|  
|**web_synchronization_url**||웹 동기화에 사용되는 인터넷 URL의 기본값입니다.|  
|NULL(기본값)||에 대 한 지원 되는 값의 목록을 반환 *속성*합니다.|  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 이 저장 프로시저가 수행한 동작으로 인해 기존 스냅숏이 무효화될 수도 있습니다. *force_invalidate_snapshot* 는 **비트**, 기본값은 **0**합니다.  
  
 **0** 지정은 게시의 변경이 스냅숏을 무효화 하지 않습니다. 저장 프로시저가 새 스냅숏을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 지정는 게시를 변경 하면 스냅숏이 무효화 수 있습니다. 기존 구독에 새 스냅숏이 필요한 경우 이 값은 기존 스냅숏을 사용되지 않는 것으로 표시하고 새 스냅숏을 생성할 수 있는 권한을 부여합니다.  
  
 변경 시 새 스냅숏을 생성해야 하는 속성에 대해서는 주의 섹션을 참조하십시오.  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 이 저장 프로시저가 수행한 동작으로 인해 기존 구독을 다시 초기화해야 할 수도 있습니다. *force_reinit_subscription* 는 **비트** 기본값인 **0**합니다.  
  
 **0** 지정는 게시를 변경 하지 않아도 구독 다시 초기화 해야 합니다. 저장 프로시저가 기존 구독을 다시 초기화해야 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 게시 인해 기존 구독이 다시 초기화 해야를 변경 하 고 구독을 다시 초기화할 수 있는 권한이 부여를 지정 합니다.  
  
 변경 시 기존의 모든 구독을 다시 초기화해야 하는 속성에 대해서는 주의 섹션을 참조하십시오.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_changemergepublication** 병합 복제에 사용 됩니다.  
  
 다음 속성을 변경하려면 새 스냅숏을 생성해야 하며 값을 지정 해야 하면 **1** 에 대 한는 *force_invalidate_snapshot* 매개 변수입니다.  
  
-   **alt_snapshot_folder**  
  
-   **compress_snapshot**  
  
-   **dynamic_filters**  
  
-   **ftp_address**  
  
-   **ftp_login**  
  
-   **ftp_password**  
  
-   **ftp_port**  
  
-   **ftp_subdirectory**  
  
-   **post_snapshot_script**  
  
-   **publication_compatibility_level** (에 **80SP3** 만)  
  
-   **pre_snapshot_script**  
  
-   **snapshot_in_defaultfolder**  
  
-   **sync_mode**  
  
-   **use_partition_groups**  
  
 다음 속성을 변경하려면 기존 구독을 다시 초기화해야 하며 값을 지정 해야 **1** 에 대 한는 *force_reinit_subscription* 매개 변수입니다.  
  
-   **dynamic_filters**  
  
-   **validate_subscriber_info**  
  
 목록에 게시 개체를 Active Directory를 사용 하 여는 *publish_to_active_directory*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체는 Active Directory에 이미 만들어져 있어야 합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_changemergepublication](../../relational-databases/replication/codesnippet/tsql/sp-changemergepublicatio_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_changemergepublication**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergepublication &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_helpmergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
