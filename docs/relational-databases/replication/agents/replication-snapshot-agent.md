---
title: "복제 스냅숏 에이전트 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "스냅숏 에이전트, 실행 파일"
  - "에이전트 [SQL Server 복제], 스냅숏 에이전트"
  - "명령 프롬프트 [SQL Server 복제]"
  - "스냅숏 에이전트, 매개 변수 참조"
ms.assetid: 2028ba45-4436-47ed-bf79-7c957766ea04
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# 복제 스냅숏 에이전트
  복제 스냅숏 에이전트는 게시된 테이블과 데이터베이스 개체의 스키마 및 데이터를 포함하는 스냅숏 파일을 준비하여 스냅숏 폴더에 저장하고 배포 데이터베이스에 동기화 작업을 기록하는 실행 파일입니다.  
  
> [!NOTE]  
>  매개 변수는 지정되는 순서에 제한을 받지 않습니다.  
  
## 구문  
  
```  
  
snapshot [ -?]   
-Publisher server_name[\instance_name]   
-Publication publication_name   
[-70Subscribers]   
[-BcpBatchSize bcp_batch_size]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor server_name[\instance_name]]  
[-DistributorDeadlockPriority [-1|0|1] ]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1] ]  
[-DynamicFilterHostName dynamic_filter_host_name]  
[-DynamicFilterLogin dynamic_filter_login]  
[-DynamicSnapshotLocation dynamic_snapshot_location]   
[-EncryptionLevel [0|1|2]]  
[-FieldDelimiter field_delimiter]  
[-HistoryVerboseLevel [0|1|2|3] ]  
[-HRBcpBlocks number_of_blocks ]  
[-HRBcpBlockSize block_size ]  
[-HRBcpDynamicBlocks ]  
[-KeepAliveMessageInterval keep_alive_interval]  
[-LoginTimeOut login_time_out_seconds]  
[-MaxBcpThreads number_of_threads ]  
[-MaxNetworkOptimization [0|1]]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2] ]  
[-PacketSize packet_size]  
[-ProfileName profile_name]  
[-PublisherDB publisher_database]  
[-PublisherDeadlockPriority [-1|0|1] ]  
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-PublisherLogin publisher_login]  
[-PublisherPassword publisher_password]   
[-PublisherSecurityMode [0|1] ]  
[-QueryTimeOut query_time_out_seconds]  
[-ReplicationType [1|2] ]  
[-RowDelimiter row_delimiter]  
[-StartQueueTimeout start_queue_timeout_seconds]  
[-UsePerArticleContentsView use_per_article_contents_view]  
```  
  
## 인수  
 **-?**  
 사용 가능한 모든 매개 변수를 출력합니다.  
  
 **-게시자**  *server_name*[**\\***instance_name*]    
 게시자의 이름입니다. 기본 인스턴스에 대해 server_name을 지정 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 해당 서버에 있습니다. 지정 *server_name***\\***instance_name* 의 명명 된 인스턴스에 대 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 해당 서버에 있습니다.  
  
 **-게시** *게시*  
 게시의 이름입니다. 이 매개 변수는 게시가 새 구독이나 다시 초기화된 구독에 대해 항상 스냅숏을 사용할 수 있도록 설정된 경우에만 유효합니다.  
  
 **-70Subscribers**  
 구독자에서 실행 중인 경우에 사용 해야 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전 7.0입니다.  
  
 **-BcpBatchSize** *bcp*_ *일괄 처리*\_ *크기*  
 대량 복사 작업에서 보낼 행 수입니다. **bcp in** 작업을 수행하는 경우 일괄 처리 크기는 한 번의 트랜잭션으로 서버에 보낼 행 수이며 배포 에이전트가 **bcp** 진행 메시지를 기록하기 전에 보내야 하는 행 수이기도 합니다. **bcp out** 작업을 수행하는 경우 고정 일괄 처리 크기로 1000이 사용됩니다. 값 0은 메시지 로깅을 사용하지 않음을 나타냅니다.  
  
 **-DefinitionFile** *def_path_and_file_name*  
 에이전트 정의 파일의 경로입니다. 에이전트 정의 파일에는 에이전트의 명령줄 인수가 들어 있습니다. 파일 내용은 실행 파일로 구문 분석됩니다. 임의 문자가 있는 인수 값을 지정하려면 큰따옴표(")를 사용합니다.  
  
 **-배포자** *server_name*[**\\***instance_name*]  
 배포자 이름입니다. 지정 *server_name* 의 기본 인스턴스에 대 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 해당 서버에 있습니다. 지정 *server_name***\\***instance_name* 의 명명 된 인스턴스에 대 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 해당 서버에 있습니다.  
  
 **-DistributorDeadlockPriority** [**-1**|**0**|**1**]  
 교착 상태가 발생할 경우 배포자에 대한 스냅숏 에이전트 연결의 우선 순위입니다. 이 매개 변수는 스냅숏을 생성하는 동안 스냅숏 에이전트와 사용자 응용 프로그램 사이에서 발생할 수 있는 교착 상태를 해결하기 위해 지정됩니다.  
  
|DistributorDeadlockPriority 값|설명|  
|---------------------------------------|-----------------|  
|**-1**|배포자에서 교착 상태가 발생할 경우 스냅숏 에이전트 이외의 응용 프로그램이 우선 순위를 갖습니다.|  
|**0** (기본값)|우선 순위가 할당되지 않습니다.|  
|**1**|배포자에서 교착 상태가 발생할 경우 스냅숏 에이전트가 우선 순위를 갖습니다.|  
  
 **-DistributorLogin** *distributor_login*  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하여 배포자에 연결할 때 사용되는 로그인입니다.  
  
 **-DistributorPassword** *distributor_password*  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하여 배포자에 연결할 때 사용되는 암호입니다. .  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 배포자의 보안 모드를 지정합니다. 값이 **0** 나타냅니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 모드 (기본값), 및의 값 **1** Windows 인증 모드를 나타냅니다.  
  
 **-DynamicFilterHostName** *dynamic_filter_host_name*  
 에 대 한 값을 설정 하는 데 사용 됩니다 [HOST_NAME (& a) #40; TRANSACT-SQL & #41;](../../../t-sql/functions/host-name-transact-sql.md) 동적 스냅숏을 때 필터링에서 생성 됩니다. 예를 들어 하위 집합 필터 절 `rep_id = HOST_NAME()` 아티클에 대해 지정 된 설정의 **DynamicFilterHostName** 병합 에이전트를 호출 하기 전에 속성 "fbjones"가 "을"fbjones "가" 있는 행만 **rep_id** 열은 복제 됩니다.  
  
 **-DynamicFilterLogin** *의 dynamic_filter_login*  
 에 대 한 값을 설정 하는 데 사용 됩니다 [SUSER_SNAME (& a) #40; TRANSACT-SQL & #41;](../../../t-sql/functions/suser-sname-transact-sql.md)동적 스냅숏을 때 필터링에서 생성 됩니다. 예를 들어 하위 집합 필터 절 `user_id = SUSER_SNAME()` 아티클에 대해 지정 된 설정의 **DynamicFilterLogin** 속성을 호출 하기 전에 "rsmith"는 **실행** 의 메서드는 **SQLSnapshot** 개체에 "rsmith"가 "를 포함 하는 행만는 **user_id** 열 스냅숏에 포함 됩니다.  
  
 **-DynamicSnapshotLocation** *dynamic_snapshot_location*  
 동적 스냅숏을 생성할 위치입니다.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 연결을 만들 때 스냅숏 에이전트에서 사용하는 SSL(Secure Sockets Layer) 암호화의 수준입니다.  
  
|EncryptionLevel 값|설명|  
|---------------------------|-----------------|  
|**0**|SSL이 사용되지 않음을 지정합니다.|  
|**1**|SSL이 사용되지만 에이전트에서 SSL 서버 인증서가 트러스트된 발급자에 의해 서명된 것인지 확인하지 않음을 지정합니다.|  
|**2**|SSL이 사용되고 인증서가 확인됨을 지정합니다.|  
  
 자세한 내용은 참조 [보안 개요 & #40; 복제 및 #41;](../../../relational-databases/replication/security/security-overview-replication.md)합니다.  
  
 **-FieldDelimiter** *field_delimiter*  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 대량 복사 데이터 파일에서 필드 끝을 표시하는 문자 또는 문자 시퀀스입니다. 기본값은 \n\<x$3>\n입니다.  
  
 **-HistoryVerboseLevel** [ **1**| **2**| **3**]  
 스냅숏 작업을 수행하는 동안 기록에 추가되는 양을 지정합니다. **1**을 선택하여 성능에서 기록 로깅의 영향을 최소화할 수 있습니다.  
  
|HistoryVerboseLevel 값|설명|  
|-------------------------------|-----------------|  
|**0**|진행 메시지를 콘솔이나 출력 파일에 씁니다. 기록 레코드는 배포 데이터베이스에 기록되지 않습니다.|  
|**1**|시작, 진행, 성공 등과 같이 상태가 동일한 이전 기록 메시지를 항상 업데이트합니다. 상태가 같은 이전 레코드가 없으면 새 레코드를 삽입합니다.|  
|**2** (기본값)|유휴 메시지나 장기 실행 작업 메시지에 대한 레코드가 없으면 새 기록 레코드를 삽입합니다. 이 경우 이전 레코드를 업데이트합니다.|  
|**3**|유휴 메시지에 대한 레코드가 없으면 항상 새 레코드를 삽입합니다.|  
  
 **-HRBcpBlocks** *number_of_blocks*  
 수 **bcp** 기록기 스레드와 판독기 스레드 사이 대기 하는 데이터 블록입니다. 기본값은 50입니다. **HRBcpBlocks** 는 Oracle 게시에만 사용됩니다.  
  
> [!NOTE]  
>  성능 튜닝에이 매개 변수는 **bcp** Oracle 게시자에서 성능입니다.  
  
 -**HRBcpBlockSize***block_size*  
 각각의 크기를 킬로바이트 (KB) 단위로 **bcp** 데이터 블록입니다. 기본값은 64KB입니다. **HRBcpBlocks** 는 Oracle 게시에만 사용됩니다.  
  
> [!NOTE]  
>  성능 튜닝에이 매개 변수는 **bcp** Oracle 게시자에서 성능입니다.  
  
 **-HRBcpDynamicBlocks**  
 여부의 크기는 **bcp** 데이터 블록을 동적으로 증가할 수 있습니다. **HRBcpBlocks** 는 Oracle 게시에만 사용됩니다.  
  
> [!NOTE]  
>  성능 튜닝에이 매개 변수는 **bcp** Oracle 게시자에서 성능입니다.  
  
 **-KeepAliveMessageInterval** *keep_alive_interval*  
 "Waiting for backend message" 기록 하기 전에 스냅숏 에이전트가 대기 하는 초 단위로 시간을가 [MSsnapshot_history](../../../relational-databases/system-tables/mssnapshot-history-transact-sql.md) 테이블입니다. 기본값은 300초입니다.  
  
 **-LoginTimeOut** *login_time_out_seconds*  
 로그인 시간이 초과될 때까지 걸리는 시간(초)입니다. 기본값은 **15** 초입니다.  
  
 **-MaxBcpThreads** *number_of_threads*  
 병렬로 수행할 수 있는 대량 복사 작업 수를 지정합니다. 동시에 존재하는 스레드 및 ODBC 연결의 최대 개수는 **MaxBcpThreads** 와 배포 데이터베이스의 동기화 트랜잭션에 나타나는 대량 복사 요청 수 중 더 작은 값입니다. **MaxBcpThreads** 보다 큰 값이 있어야 **0** 없습니다 하드 코딩 된 상한값이 있습니다. 기본값은 **1**입니다.  
  
 \- **MaxNetworkOptimization** [ **0**| **1**]  
 관련이 없는 삭제 작업을 구독자에 보낼지 여부를 나타냅니다. 관련이 없는 삭제 작업은 구독자의 파티션에 속하지 않는 행에 대해 구독자에게 보내지는 DELETE 명령입니다. 관련이 없는 삭제 작업은 데이터 무결성 또는 일치성에 영향을 주지 않지만 불필요한 네트워크 트래픽을 초래할 수 있습니다. **MaxNetworkOptimization** 의 기본값은 **0**입니다. **MaxNetworkOptimization** 을 **1** 로 설정하면 관련이 없는 삭제 작업이 최소화되므로 네트워크 트래픽이 줄어들고 네트워크 성능은 최대화됩니다. 이 매개 변수를 **1** 로 설정하면 메타데이터 저장소 공간이 늘어나며 여러 수준의 조인 필터와 복잡한 하위 집합 필터가 있는 경우 성능이 저하됩니다. 복제 토폴로지를 신중하게 평가한 후 관련이 없는 삭제 작업으로 인해 네트워크 트래픽이 허용 불가능한 수준으로 높아지는 경우에만 **MaxNetworkOptimization** 을 **1** 로 설정해야 합니다.  
  
> [!NOTE]  
>  이 매개 변수를 설정 **1** 는 병합 게시의 동기화 최적화 옵션이로 설정 된 경우에 유용 **true** (의 **@keep_partition_changes** 의 매개 변수 [sp_addmergepublication (& a) #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)).  
  
 **-출력** *output_path_and_file_name*  
 에이전트 출력 파일의 경로입니다. 파일 이름을 지정하지 않으면 출력이 콘솔로 전달됩니다. 지정된 파일 이름이 존재하면 출력이 파일에 추가됩니다.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 출력이 자세해야 하는지 여부를 지정합니다.  
  
|OutputVerboseLevel 값|설명|  
|------------------------------|-----------------|  
|**0**|오류 메시지만 출력됩니다.|  
|**1** (기본값)|모든 진행률 보고 메시지가 출력됩니다(기본값).|  
|**2**|모든 오류 메시지 및 진행률 보고 메시지가 출력되며, 디버깅에 유용합니다.|  
  
 **-PacketSize** *packet_size*  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 때 스냅숏 에이전트에서 사용하는 패킷 크기(바이트)입니다. 기본값은 8192바이트입니다.  
  
> [!NOTE]  
>  성능이 향상될 것이라는 확신이 없으면 패킷 크기를 변경하지 마세요. 대부분의 응용 프로그램에는 기본 패킷 크기가 제일 좋습니다.  
  
 **-ProfileName** *profile_name*  
 에이전트 매개 변수에 사용할 에이전트 프로필을 지정합니다. **ProfileName** 이 NULL이면 에이전트 프로필이 사용되지 않습니다. **ProfileName** 이 지정되지 않으면 에이전트 유형에 대한 기본 프로필이 사용됩니다. 내용은 [복제 에이전트 프로필](../../../relational-databases/replication/agents/replication-agent-profiles.md)합니다.  
  
 **-PublisherDB** *publisher_database*  
 게시 데이터베이스의 이름입니다. 이 매개 변수는 Oracle 게시자에 대해서는 지원되지 않습니다.  
  
 **-PublisherDeadlockPriority** [**-1**|**0**|**1**]  
 교착 상태가 발생할 경우 게시자에 대한 스냅숏 에이전트 연결의 우선 순위입니다. 이 매개 변수는 스냅숏을 생성하는 동안 스냅숏 에이전트와 사용자 응용 프로그램 사이에서 발생할 수 있는 교착 상태를 해결하기 위해 지정됩니다.  
  
|PublisherDeadlockPriority 값|설명|  
|-------------------------------------|-----------------|  
|**-1**|게시자에서 교착 상태가 발생할 경우 스냅숏 에이전트 이외의 응용 프로그램이 우선 순위를 갖습니다.|  
|**0** (기본값)|우선 순위가 할당되지 않습니다.|  
|**1**|게시자에서 교착 상태가 발생할 경우 스냅숏 에이전트가 우선 순위를 갖습니다.|  
  
 **-PublisherFailoverPartner** *server_name*[**\\***instance_name*]  
 게시 데이터베이스와 함께 데이터베이스 미러링 세션에 참여하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 장애 조치 파트너 인스턴스를 지정합니다. 자세한 내용은 참조 [데이터베이스 미러링 및 복제 & #40; SQL Server 및 #41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)합니다.  
  
 **-PublisherLogin** *publisher_login*  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하여 게시자에 연결할 때 사용되는 로그인입니다.  
  
 **-PublisherPassword**  *publisher_password*  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하여 게시자에 연결할 때 사용되는 암호입니다. .  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 게시자의 보안 모드를 지정합니다. 값이 **0** 나타냅니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 (기본값), 및의 값 **1** Windows 인증 모드를 나타냅니다.  
  
 **-QueryTimeOut** *query_time_out_seconds*  
 쿼리 시간이 초과될 때까지 걸리는 시간(초)입니다. 기본값은 1800초입니다.  
  
 **-ReplicationType** [ **1**| **2**]  
 복제 유형을 지정합니다. 값 **1** 은 트랜잭션 복제를 나타내며 값 **2** 는 병합 복제를 나타냅니다.  
  
 **-RowDelimiter** *row_delimiter*  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 대량 복사 데이터 파일에서 행 끝을 표시하는 문자 또는 문자 시퀀스입니다. 기본값은 \n\<,@g>\n입니다.  
  
 **-StartQueueTimeout** *start_queue_timeout_seconds*  
 스냅숏 에이전트가 실행 되는 동시 동적 스냅숏 프로세스 수가으로 설정 된 제한 때까지 대기 하는 시간 (초)의 최대 수는 **@max_concurrent_dynamic_snapshots** 속성 [sp_addmergepublication (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)합니다. 최대 시간(초)에 도달한 경우 스냅숏 에이전트가 계속 대기 중이면 해당 스냅숏 에이전트가 종료됩니다. 값 0은 에이전트가 취소될 경우에도 무기한 대기함을 의미합니다.  
  
 \- **UsePerArticleContentsView** *use_per_article_contents_view*  
 이 매개 변수는 더 이상 사용되지 않으며 이전 버전과의 호환성을 위해서만 지원됩니다.  
  
## 주의  
  
> [!IMPORTANT]  
>  도메인 사용자 계정(기본값)이 아닌 로컬 시스템 계정에서 실행되도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트를 설치한 경우 해당 서비스에서는 로컬 컴퓨터에만 액세스할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트에서 실행되는 스냅숏 에이전트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 로그인할 때 Windows 인증 모드를 사용하도록 구성된 경우 해당 스냅숏 에이전트가 실패합니다. 기본 설정은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증입니다.  
  
 스냅숏 에이전트를 시작하려면 명령 프롬프트에서 **snapshot.exe** 를 실행합니다. 자세한 내용은 [복제 에이전트 실행 파일](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)을 참조하십시오.  
  
## 참고 항목  
 [복제 에이전트 관리](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  