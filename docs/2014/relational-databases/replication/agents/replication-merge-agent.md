---
title: 복제 병합 에이전트 | Microsoft 문서
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Merge Agent, executables
- Merge Agent, parameter reference
- agents [SQL Server replication], Merge Agent
- command prompt [SQL Server replication]
ms.assetid: fe1e7f60-b0c8-45e9-a5e8-4fedfa73d7ea
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec21ff98d49cff26bde48452a30fd347c23782fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63216006"
---
# <a name="replication-merge-agent"></a>Replication Merge Agent
  복제 병합 에이전트는 데이터베이스 테이블에 저장된 초기 스냅샷 파일을 구독자에 적용하는 유틸리티 실행 파일입니다. 또한 이 에이전트는 초기 스냅샷이 만들어진 후 게시자에서 발생한 증분 데이터 변경 내용을 병합하고, 사용자가 구성한 규칙에 따라 또는 사용자가 만든 사용자 지정 해결 프로그램을 사용하여 충돌을 조정합니다.  
  
> [!NOTE]  
>  매개 변수는 지정되는 순서에 제한을 받지 않습니다. 선택적 매개 변수가 지정되지 않은 경우 로컬 컴퓨터의 미리 정의된 레지스트리 설정 값이 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
      replmerg [-?]   
-Publisherserver_name[\instance_name]  
-PublisherDBpublisher_database-Publicationpublication-Subscriberserver_name[\instance_name]  
-SubscriberDBsubscriber_database  
[-AltSnapshotFolderalt_snapshot_folder_path]  
[-Continuous]  
[-DefinitionFiledef_path_and_file_name]  
[-DestThreadsnumber_of_destination_threads]  
[-Distributorserver_name[\instance_name]]  
[-DistributorLogindistributor_login]  
[-DistributorPassworddistributor_password]  
[-DistributorSecurityMode [0|1]]  
[-DownloadGenerationsPerBatchdownload_generations_per_batch]  
[-DownloadReadChangesPerBatchdownload_read_changes_per_batch]  
[-DownloadWriteChangesPerBatchdownload_write_changes_per_batch]  
[-DynamicSnapshotLocationdynamic_snapshot_location]  
[-EncryptionLevel [0|1|2]]  
[-ExchangeType [1|2|3]]  
[-FastRowCount [0|1]]  
[-FileTransferType [0|1]]  
[-ForceConvergenceLevel [0|1|2 (Publisher|Subscriber|Both)]]  
[-FtpAddressftp_address]  
[-FtpPasswordftp_password]  
[-FtpPortftp_port]  
[-FtpUserNameftp_user_name]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-Hostnamehost_name]  
[-InteractiveResolution [0|1]]  
[-InternetLogininternet_login]  
[-InternetPasswordinternet_password]  
[-InternetProxyLogininternet_proxy_login]  
[-InternetProxyPasswordinternet_proxy_password]  
[-InternetProxyServerinternet_proxy_server]  
[-InternetSecurityMode [0|1]]  
[-InternetTimeoutinternet_timeout]  
[-InternetURL internet_url]  
[-KeepAliveMessageIntervalkeep_alive_message_interval_seconds]  
[-LoginTimeOutlogin_time_out_seconds]  
[-MakeGenerationIntervalmake_generation_interval_seconds]  
[-MaxBcpThreadsnumber_of_threads]  
[-MaxDownloadChangesnumber_of_download_changes]  
[-MaxUploadChangesnumber_of_upload_changes]  
[-MetadataRetentionCleanup [0|1]]  
[-Output]  
[-OutputVerboseLevel [0|1|2]]  
[-ParallelUploadDownload [0|1]]  
[-PacketSizepacket_size]   
[-PollingIntervalpolling_interval]  
[-ProfileNameprofile_name]  
[-PublisherFailoverPartnerserver_name[\instance_name] ]  
[-PublisherLoginpublisher_login]  
[-PublisherPassword publisher_password]  
[-PublisherSecurityMode [0|1]]  
[-QueryTimeOutquery_time_out_seconds]  
[-SrcThreadsnumber_of_source_threads]  
[-StartQueueTimeoutstart_queue_timeout_seconds]  
[-SubscriberConflictClean [0|1]]  
[-SubscriberDatabasePathsubscriber_path]  
[-SubscriberDBAddOption [0|1|2|3]]  
[-SubscriberLoginsubscriber_login]  
[-SubscriberPasswordsubscriber_password   
[-SubscriberSecurityMode [0|1]]  
[-SubscriberType [0|1|2|3|4|5|6|7|8|9]]  
[-SubscriptionType [0|1|2]]  
[-SyncToAlternate [0|1]  
[-UploadGenerationsPerBatchupload_generations_per_batch]  
[-UploadReadChangesPerBatchupload_read_changes_per_batch]  
[-UploadWriteChangesPerBatchupload_write_changes_per_batch]  
[-UseInprocLoader]  
[-Validate [0|1|2|3]]  
[-ValidateIntervalvalidate_interval]  
```  
  
## <a name="arguments"></a>인수  
 **-?**  
 사용 가능한 모든 매개 변수를 출력합니다.  
  
 **-Publisher** _server_name_[ **\\** _instance_name_]  
 게시자의 이름입니다. 해당 서버에 있는 기본 *server_name* 인스턴스에 대해 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 지정합니다. 해당 서버에 있는 명명된 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대해 server_name을 지정하고,  
  
 **-PublisherDB** _publisher_database_  
 게시자 데이터베이스의 이름입니다.  
  
 **-Publication** _publication_  
 게시의 이름입니다. 이 매개 변수는 게시가 새 구독이나 다시 초기화된 구독에 대해 항상 스냅샷을 사용할 수 있도록 설정된 경우에만 유효합니다.  
  
 **-Subscriber** _server_name_[ **\\** _instance_name_]  
 구독자의 이름입니다. 해당 서버에 있는 기본 *server_name* 인스턴스에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 지정합니다. 해당 서버에 있는 명명된 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대해 server_name을 지정하고,  
  
 **-SubscriberDB** _subscriber_database_  
 구독자 데이터베이스의 이름입니다.  
  
 **-AltSnapshotFolder** _alt_snapshot_folder_path_  
 구독에 대한 초기 스냅샷이 들어 있는 폴더의 경로입니다.  
  
 **-Continuous**  
 에이전트에서 복제된 트랜잭션의 폴링을 계속 시도할지 여부를 지정합니다. 이 인수가 지정된 경우 에이전트는 보류 중인 트랜잭션이 없는 경우에도 원본의 복제된 트랜잭션을 폴링 간격에 따라 폴링합니다.  
  
 **-DestThreads** _number_of_destination_threads_  
 병합 에이전트에서 대상에 변경 내용을 적용하는 데 사용하는 대상 스레드의 개수를 지정합니다. 업로드 중에는 게시자가 대상이 되고 다운로드 중에는 구독자가 대상이 됩니다. 기본값은 4입니다.  
  
 **-DefinitionFile** _def_path_and_file_name_  
 에이전트 정의 파일의 경로입니다. 에이전트 정의 파일에는 에이전트의 명령 프롬프트 인수가 들어 있습니다. 파일 내용은 실행 파일로 구문 분석됩니다. 임의 문자가 있는 인수 값을 지정하려면 큰따옴표(")를 사용합니다.  
  
 **-Distributor** _server_name_[ **\\** _instance_name_]  
 배포자 이름입니다. 해당 서버에 있는 기본 *인스턴스에 대해* server_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 지정하고, 해당 서버에 있는 명명된 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대해 server_name을 지정하고, 배포자(밀어넣기) 배포의 경우에는 로컬 컴퓨터에 있는 기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름이 기본 이름이 됩니다.  
  
 **-DistributorLogin** _distributor_login_  
 배포자의 로그인 이름입니다.  
  
 **-DistributorPassword** _distributor_password_  
 배포자 암호입니다.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 배포자의 보안 모드를 지정합니다. 값 **0** 은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 모드(기본값)를 나타내며 값 **1** 은 Windows 인증 모드를 나타냅니다.  
  
 **-DownloadGenerationsPerBatch** _download_generations_per_batch_  
 게시자의 변경 내용을 구독자로 다운로드하는 동안 한 번의 일괄 처리에서 처리할 세대 수입니다. 세대는 아티클 단위의 논리적 변경 내용 그룹으로 정의됩니다. 안정적인 통신 연결의 기본값은 100이고, 안정적이지 않은 통신 연결의 기본값은 10입니다.  
  
 **-DownloadReadChangesPerBatch** _download_read_changes_per_batch_  
 게시자의 변경 내용을 구독자로 다운로드하는 동안 한 번의 일괄 처리에서 읽을 변경 내용 수입니다. 기본값은 100입니다.  
  
 **-DownloadWriteChangesPerBatch** _download_write_changes_per_batch_  
 게시자의 변경 내용을 구독자로 다운로드하는 동안 한 번의 일괄 처리에서 적용할 변경 내용 수입니다. 기본값은 100입니다.  
  
 **-DynamicSnapshotLocation** _dynamic_snapshot_location_  
 게시에서 매개 변수가 있는 행 필터를 사용할 경우 필터링된 데이터 스냅샷 파일의 위치입니다.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 연결을 만들 때 병합 에이전트에서 사용하는 SSL(Secure Sockets Layer) 암호화의 수준입니다.  
  
|EncryptionLevel 값|Description|  
|---------------------------|-----------------|  
|**0**|SSL이 사용되지 않음을 지정합니다.|  
|**1**|SSL이 사용되지만 에이전트에서 SSL 서버 인증서가 트러스트된 발급자에 의해 서명된 것인지 확인하지 않음을 지정합니다.|  
|**2**|SSL이 사용되고 인증서가 확인됨을 지정합니다.|  

 > [!NOTE]  
 >  유효한 SSL 인증서는 SQL Server의 정규화된 도메인 이름으로 정의됩니다. -EncryptionLevel을 2로 설정할 때 에이전트가 성공적으로 연결되도록 하려면 로컬 SQL Server에서 별칭을 만듭니다. '별칭 이름' 매개 변수는 서버 이름이어야 하며 '서버' 매개 변수는 SQL Server의 정규화된 이름으로 설정되어야 합니다.
  
 자세한 내용은 [SQL Server 복제 보안](../security/view-and-modify-replication-security-settings.md)합니다.  
  
 **-ExchangeType** [ **1**| **2**| **3**]  
 > [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] 업로드를 제한하려면 `@subscriber_upload_options`의 `sp_addmergearticle`를 대신 사용하십시오.  
  
 동기화를 수행할 때의 데이터 교환 유형을 지정하며 값은 다음 중 하나일 수 있습니다.  
  
|ExchangeType 값|Description|  
|------------------------|-----------------|  
|**1**|에이전트에서 구독자의 데이터 변경 내용을 게시자로 업로드합니다.|  
|**2**|에이전트에서 게시자의 데이터 변경 내용을 구독자로 다운로드합니다.|  
|**3** (기본값)|에이전트에서는 먼저 구독자의 데이터 변경 내용을 게시자로 업로드한 다음 게시자의 데이터 변경 내용을 구독자로 다운로드합니다. 웹 동기화의 경우 이 옵션을 사용해야 합니다.|  
  
 다운로드 전용 아티클을 사용하면 게시에 있는 개별 아티클의 동기화 동작을 제어할 수 있으며 성능도 향상됩니다. 자세한 내용은 [다운로드 전용 아티클로 병합 복제 성능 최적화](../merge/optimize-merge-replication-performance-with-download-only-articles.md)를 참조하세요.  
  
 `ExchangeType`을 사용하여 병합 복제의 업로드 및 다운로드 단계를 별도의 세션으로 분리하는 경우 `ExchangeType`을 먼저 1로 설정한 상태로 병합 에이전트를 실행한 후 값을 2로 설정하여 병합 에이전트를 다시 실행해야 합니다. 두 매개 변수를 사용하여 병합 에이전트를 실행하는 데 실패하면 메타데이터가 삭제되고 구독을 다시 초기화해야 합니다(업로드 제외).  
  
 **-FastRowCount** [**0**|**1**]  
 행 개수 유효성 검사에 사용할 행 개수 계산 방법의 유형을 지정합니다. 값 **1** (기본값)은 빠른 행 개수 계산 방법을 나타냅니다. 값 **0** 은 전체 행 개수 계산 방법을 나타냅니다.  
  
 **-FileTransferType** [**0**|**1**]  
 파일 전송 유형을 지정합니다. 값 **0** 은 UNC(Universal Naming Convention)를 나타내고, 값 **1** 은 FTP(File Transfer Protocol)를 나타냅니다.  
  
 **-ForceConvergenceLevel** [**0**|**1**|**2** ( **Publisher**| **Subscriber**| **Both**)]  
 병합 에이전트에서 사용할 일치성 수준을 지정하며 값은 다음 중 하나가 될 수 있습니다.  
  
|ForceConvergenceLevel 값|Description|  
|---------------------------------|-----------------|  
|**0** (기본값)|기본. 추가 일치 작업 없이 표준 병합을 수행합니다.|  
|**1**|모든 세대에 대해 일치 작업을 수행합니다.|  
|**2**|모든 세대에 대해 일치 작업을 수행하고 손상된 계보를 수정합니다. 이 값을 지정할 경우 계보를 수정할 위치를 게시자, 구독자 또는 게시자와 구독자 모두로 지정합니다.|  
  
 **-FtpAddress** _ftp_address_  
 배포자용 FTP 서비스의 네트워크 주소입니다. 지정되지 않은 경우, **Distributor** 가 사용됩니다.  
  
 **-FtpPassword** _ftp_password_  
 FTP 서비스에 연결할 때 사용되는 사용자 암호입니다.  
  
 **-FtpPort** _ftp_port_  
 배포자용 FTP 서비스의 포트 번호입니다. 지정되지 않은 경우, FTP 서비스용 기본 포트 번호(21)가 사용됩니다.  
  
 **-FtpUserName** _ftp_user_name_  
 FTP 서비스에 연결할 때 사용할 사용자 이름입니다. 지정되지 않은 경우, anonymous가 사용됩니다.  
  
 **-HistoryVerboseLevel** [**1**|**2**|**3**]  
 병합 작업을 수행하는 동안 기록에 추가되는 양을 지정합니다. **1**을 선택하여 성능에서 기록 로깅의 영향을 최소화할 수 있습니다.  
  
|HistoryVerboseLevel 값|Description|  
|-------------------------------|-----------------|  
|**0**|최종 에이전트 상태 메시지, 최종 세션 정보 및 기타 오류를 기록합니다.|  
|**1**|각 세션 상태의 증분 세션 정보를 기록합니다. 여기에는 최종 에이전트 상태 메시지, 최종 세션 정보 및 오류뿐 아니라 완료율도 포함됩니다.|  
|**2**|기본. 각 세션 상태의 증분 세션 정보와 아티클 수준 세션 정보를 기록합니다. 여기에는 최종 에이전트 상태 메시지, 최종 세션 정보 및 오류뿐 아니라 완료율도 포함됩니다. 에이전트 상태 메시지도 기록됩니다.|  
|**3**|기록되는 에이전트 진행 메시지가 더 많다는 점만 제외하고 **-HistoryVerboseLevel** = **2**와 동일합니다.|  
  
 **-Hostname** _host_name_  
 로컬 컴퓨터의 네트워크 이름입니다. 기본값은 로컬 컴퓨터 이름입니다.  
  
 **-InteractiveResolution** [**0**|**1**]  
 동기화를 수행하는 동안 충돌이 발생할 경우 대화형 충돌 해결을 사용할지 여부를 지정합니다. 기본값은 **0**으로, 대화형 충돌 해결을 사용하지 않음을 나타냅니다.  
  
 **-InternetLogin** _internet_login_  
 인증이 필요한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 수신기 ISAPI DLL에 연결할 때 사용되는 로그인 이름을 지정합니다.  
  
 **-InternetPassword** _internet_password_  
 인증이 필요한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 수신기 ISAPI DLL에 연결할 때 사용되는 암호를 지정합니다.  
  
 **-InternetProxyLogin**  *internet_proxy_login*  
 인증이 필요한 프록시 서버( *internet_proxy_server*에 정의됨)에 연결할 때 사용되는 로그인 이름을 지정합니다.  
  
 **-InternetProxyPassword**  *internet_proxy_password*  
 인증이 필요한 프록시 서버( *internet_proxy_server*에 정의됨)에 연결할 때 사용되는 암호를 지정합니다.  
  
 **-InternetProxyServer**  *internet_proxy_server*  
 *internet_url*에 지정된 HTTP 리소스에 액세스할 때 사용할 프록시 서버를 지정합니다.  
  
 **-InternetSecurityMode** [**0**|**1**]  
 웹 동기화를 수행하는 동안 웹 서버에 연결할 때 사용할 IIS 보안 모드를 지정합니다. 값 **0** 은 기본 인증을 나타내고, 값 **1** 은 Windows 통합 인증(기본값)을 나타냅니다.  
  
 **-InternetTimeout** _internet_timeout_  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 수신기 ISAPI DLL에 대한 연결 제한 시간이 초과되기까지의 시간(초)을 지정합니다.  
  
 **-InternetURL** _internet_url_  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 수신기 ISAPI DLL에 연결하는 데 사용되는 URL을 지정합니다. 이 속성은 반드시 지정해야 합니다.  
  
 **-KeepAliveMessageInterval** _keep_alive_message_interval_seconds_  
 기록 스레드가 기존 연결에서 서버의 응답을 기다리고 있는지 확인할 때까지 걸리는 시간(초)입니다. 이 값을 줄이면 장기 실행 일괄 처리를 실행할 때 점검 에이전트에서 병합 에이전트를 주의 대상으로 표시하지 않도록 할 수 있습니다. 기본값은 **300** 초입니다.  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 로그인 시간이 초과될 때까지 걸리는 시간(초)입니다. 기본값은 **15** 초입니다.  
  
 **-MakeGenerationInterval** _make_generation_interval_seconds_  
 생성 만들기 또는 클라이언트에 다운로드할 변경 내용의 일괄 처리 간에 대기하는 시간(초)입니다. 기본값은 **1** 초입니다.  
  
 makegeneration은 게시자 변경 내용을 구독자로 다운로드하기 위해 준비하는 프로세스로, 다운로드하는 동안 성능 병목 상태를 일으킬 수 있습니다. makegeneration 프로세스는 **-MakeGenerationInterval**에 지정된 간격 내에서 이미 실행된 경우 현재 동기화 세션에서 생략됩니다. 이는 동기화 동시성에 도움이 되며, 구독자가 변경 내용을 다운로드하지 않으려는 경우 특히 유용합니다.  
  
 **-MaxBcpThreads** _number_of_threads_  
 병렬로 수행할 수 있는 대량 복사 작업 수를 지정합니다. 동시에 존재하는 스레드 및 ODBC 연결의 최대 개수는 **MaxBcpThreads** 와 게시 데이터베이스의 시스템 테이블 **sysmergeschemachange** 에 나타나는 대량 복사 요청 수 중 더 작은 값입니다. **MaxBcpThreads** 값은 0보다 크고 하드 코딩된 상한값이 없어야 합니다. 기본값은 **1**입니다.  
  
 **-MaxDownloadChanges** _number_of_download_changes_  
 게시자에서 구독자로 다운로드할 변경된 행의 최대 개수를 지정합니다. 다운로드되는 행 수가 지정된 최대값보다 클 수도 있습니다. 전체 세대가 처리되는 경우나, 병렬 대상 스레드가 실행될 수 있고 각 스레드가 첫 번째 전달에서 100개 이상의 변경 내용을 처리하는 경우가 이러한 경우에 해당됩니다. 기본적으로 다운로드할 수 있는 모든 변경 내용이 보내집니다.  
  
 **-MaxUploadChanges** _number_of_upload_changes_  
 구독자에서 게시자로 업로드할 변경된 행의 최대 개수를 지정합니다. 업로드되는 행 수가 지정된 최대값보다 클 수도 있습니다. 전체 세대가 처리되는 경우나, 병렬 대상 스레드가 실행될 수 있고 각 스레드가 첫 번째 전달에서 100개 이상의 변경 내용을 처리하는 경우가 이러한 경우에 해당됩니다. 기본적으로 업로드할 수 있는 모든 변경 내용이 보내집니다.  
  
 **-MetadataRetentionCleanup** [**0**|**1**]  
 게시 보존 기간에 따라 [MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql), [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql), [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql), [MSmerge_past_partition_mappings](/sql/relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql)및 [MSmerge_current_partition_mappings](/sql/relational-databases/system-tables/msmerge-current-partition-mappings) 에서 메타데이터를 제거할지 여부를 지정합니다. 기본값은 **1**로서, 정리를 수행함을 나타냅니다. 값 **0** 은 정리를 자동으로 수행하지 않음을 나타냅니다.  
  
 **-Output** _output_path_and_file_name_  
 에이전트 출력 파일의 경로입니다. 파일 이름을 지정하지 않으면 출력이 콘솔로 전달됩니다. 지정된 파일 이름이 존재하면 출력이 파일에 추가됩니다.  
  
 **-OutputVerboseLevel** [**0**|**1**|**2**]  
 출력이 자세해야 하는지 여부를 지정합니다. 정보 표시 수준이 **0**이면 오류 메시지만 출력됩니다. 정보 표시 수준이 **1**이면 모든 진행률 보고 메시지가 출력됩니다. 정보 표시 수준이 **2** (기본값)이면 디버깅에 유용한 오류 메시지와 진행률 보고 메시지가 모두 출력됩니다.  
  
 **-ParallelUploadDownload** [**0**|**1**]  
 병합 에이전트에서 게시자에 업로드되는 변경 내용과 구독자에 다운로드되는 변경 내용을 병렬로 처리할지 여부를 지정합니다. 병렬 처리는 네트워크 대역폭이 높은 대규모 환경에서 유용합니다. **ParallelUploadDownload** 가 **1**이면 병렬 처리가 사용됩니다.  
  
 **-PacketSize**  
 패킷 크기(바이트)입니다. 기본값은 4096바이트입니다.  
  
 **-PollingInterval** _polling_interval_  
 게시자 또는 구독자에서 데이터 변경 내용을 쿼리하는 빈도(초)입니다. 기본값은 60초입니다.  
  
 **-ProfileName** _profile_name_  
 에이전트 매개 변수에 사용할 에이전트 프로필을 지정합니다. **ProfileName** 이 NULL이면 에이전트 프로필이 사용되지 않습니다. **ProfileName** 이 지정되지 않으면 에이전트 유형에 대한 기본 프로필이 사용됩니다. 자세한 내용은 [복제 에이전트 프로필](replication-agent-profiles.md)을 참조하세요.  
  
 **-PublisherFailoverPartner** _server_name_[ **\\** _instance_name_]  
 게시 데이터베이스와 함께 데이터베이스 미러링 세션에 참여하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 장애 조치 파트너 인스턴스를 지정합니다. 자세한 내용은 [데이터베이스 미러링 및 복제&#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)을 참조하세요.  
  
 **-PublisherLogin** _publisher_login_  
 게시자 로그인 이름입니다. **PublisherSecurityMode** 가 **0** ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증의 경우)이면 이 매개 변수를 지정해야 합니다.  
  
 **-PublisherPassword** _publisher_password_  
 게시자 암호입니다. **PublisherSecurityMode** 가 **0** ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증의 경우)이면 이 매개 변수를 지정해야 합니다.  
  
 **-PublisherSecurityMode** [**0**|**1**]  
 게시자의 보안 모드를 지정합니다. 값 **0** 은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증(기본값)을 나타내며 값 **1** 은 Windows 인증 모드를 나타냅니다.  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 쿼리 시간이 초과될 때까지 걸리는 시간(초)입니다. 기본값은 300초입니다. `QueryTimeout` 값이 1800보다 클 경우 병합 에이전트에서는 이 값을 사용하여 분할된 스냅숏이 생성되기를 기다릴 시간을 결정하기도 합니다.  
  
 **-SrcThreads** _number_of_source_threads_  
 병합 에이전트에서 원본의 변경 내용을 열거하는 데 사용하는 원본 스레드의 개수를 지정합니다. 업로드 중에는 구독자가 원본이 되고 다운로드 중에는 게시자가 원본이 됩니다. 기본값은 **3**입니다.  
  
 **-StartQueueTimeout** _start_queue_timeout_seconds_  
 동시에 실행 중인 병합 프로세스의 수가 **@max_concurrent_merge** 의 **@max_concurrent_merge**을 참조하세요. 최대 시간(초)에 도달한 경우 병합 에이전트가 계속 대기 중이면 해당 병합 에이전트가 종료됩니다. 값 0은 에이전트가 취소될 경우에도 무기한 대기함을 의미합니다.  
  
 **-SubscriberDatabasePath** _subscriber_database_path_  
 **SubscriberType** 이 **2** 로서, ODBC DSN(데이터 원본 이름)이 없는 Jet 데이터베이스에 대한 연결이 허용되는 경우 Jet 데이터베이스(.mdb 파일)의 경로입니다.  
  
 **-SubscriberDBAddOption** [**0**| **1**| **2**| **3**]  
 기존 구독자 데이터베이스가 있는지 여부를 지정합니다.  
  
|SubscriberDBAddOption 값|Description|  
|---------------------------------|-----------------|  
|**0**|기존 데이터베이스를 사용합니다(기본값).|  
|**1**|비어 있는 새 구독자 데이터베이스를 만듭니다.|  
|**2**|새 데이터베이스를 만들어 지정된 파일에 연결합니다.|  
|**3**|새 데이터베이스를 만들어 연결하고 해당 파일에 있을 수 있는 모든 구독을 사용하도록 설정합니다.|  
  
> [!NOTE]  
>  값 **2** 와 **3**을 사용할 경우에는 **SubscriberDatabasePath** 옵션에서 구독자의 데이터베이스 경로를 지정해야 합니다.  
  
 **-SubscriberLogin** _subscriber_login_  
 구독자의 로그인 이름입니다. **SubscriberSecurityMode** 가 **0** ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증의 경우)이면 이 매개 변수를 지정해야 합니다.  
  
 **-SubscriberPassword** _subscriber_password_  
 구독자 암호입니다. **SubscriberSecurityMode** 가 **0** ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증의 경우)이면 이 매개 변수를 지정해야 합니다.  
  
 **-SubscriberSecurityMode** [ **0**| **1**]  
 구독자의 보안 모드를 지정합니다. 값 **0** 은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증(기본값)을 나타내며 값 **1** 은 Windows 인증 모드를 나타냅니다.  
  
 **-SubscriberConflictClean** [ **0**| **1**]  
 동기화 프로세스를 수행하는 동안 구독자에서 충돌 테이블을 정리할지 여부를 나타냅니다. 값 **1** 은 구독자의 충돌 테이블이 정리됨을 나타냅니다. 이 매개 변수는 분산 충돌 로깅을 사용하는 게시자에 대한 구독에만 사용됩니다.  
  
 **-SubscriberType** [ **0**| **1**| **3**| **4**| **5**| **6**| **7**| **8**]  
 병합 에이전트에서 사용하는 구독자 연결 유형을 지정합니다. 이 매개 변수에는 기본값 **0** 만 지원됩니다.  
  
 **-SubscriptionType**[ **0**| **1**| **2**]  
 배포의 구독 유형을 지정합니다. 값 **0** 은 밀어넣기 구독(기본값)을, 값 **1** 은 끌어오기 구독을, 값 **2** 는 익명 구독을 나타냅니다.  
  
 **-SyncToAlternate** [ **0|1**]  
 병합 에이전트에서 구독자와 대체 게시자 간의 동기화를 수행하는지 여부를 지정합니다. 값 **1** 은 동기화 대상이 대체 게시자임을 나타냅니다. 기본값은 **0**입니다.  
  
 **-UploadGenerationsPerBatch** _upload_generations_per_batch_  
 구독자의 변경 내용을 게시자로 업로드하는 동안 한 번의 일괄 처리에서 처리할 세대 수입니다. 세대는 아티클 단위의 논리적 변경 내용 그룹으로 정의됩니다. 안정적인 통신 연결의 기본값은 **100**이고, 안정적이지 않은 통신 연결의 기본값은 **1**입니다.  
  
 **-UploadReadChangesPerBatch** _upload_read_changes_per_batch_  
 구독자의 변경 내용을 게시자로 업로드하는 동안 한 번의 일괄 처리에서 읽을 변경 내용 수입니다. 기본값은 **100**입니다.  
  
 **-UploadWriteChangesPerBatch** _upload_write_changes_per_batch_  
 구독자의 변경 내용을 게시자로 업로드하는 동안 한 번의 일괄 처리에서 적용할 변경 내용 수입니다. 기본값은 **100**입니다.  
  
 **-UseInprocLoader**  
 병합 에이전트에서 구독자에 스냅샷 파일을 적용할 때 BULK INSERT 명령을 사용하도록 지정하여 초기 스냅샷의 성능을 향상시킵니다. 이 매개 변수는 XML 데이터 형식과 호환되지 않으므로 이후에는 지원되지 않습니다. XML 데이터를 복제하지 않을 계획이라면 이 매개 변수를 사용할 수 있습니다. 이 매개 변수는 문자 모드 스냅샷과 함께 사용할 수 없습니다. 이 매개 변수를 사용하려면 구독자의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정에 스냅샷 .bcp 데이터 파일이 있는 디렉터리에 대한 읽기 권한이 있어야 합니다. 이 매개 변수를 사용하지 않으면 에이전트에서 로드한 ODBC 드라이버가 파일 내용을 읽으므로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정의 보안 컨텍스트가 사용되지 않습니다.  
  
 **-Validate** [**0**|**1**|**2**|**3**]  
 병합 세션이 종료될 때 유효성 검사를 수행할지 여부와 수행할 유효성 검사 유형을 지정합니다. 값 **3** 이 권장 값입니다.  
  
|값 유효성 검사|Description|  
|--------------------|-----------------|  
|**0** (기본값)|유효성 검사를 수행하지 않습니다.|  
|**1**|행 개수의 유효성만 검사합니다.|  
|**2**|행 개수 및 체크섬의 유효성을 검사합니다.|  
|**3**|행 개수 및 이진 체크섬의 유효성을 검사합니다.|  
  
> [!NOTE]  
>  구독자에서의 데이터 형식과 게시자에서의 데이터 형식이 다른 경우 이진 체크섬 또는 체크섬 유효성 검사가 올바르지 않을 수 있습니다. 자세한 내용은 [복제된 데이터의 유효성 검사](../validate-data-at-the-subscriber.md)의 "데이터 유효성 검사에 대한 고려 사항" 섹션을 참조하세요.  
  
 **-ValidateInterval** _validate_interval_  
 연속 모드에서 구독 유효성 검사가 수행되는 빈도(분)입니다. 기본값은 **60** 분입니다.  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  도메인 사용자 계정(기본값)이 아닌 로컬 시스템 계정에서 실행되도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트를 설치한 경우 해당 서비스에서는 로컬 컴퓨터에만 액세스할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트에서 실행되는 병합 에이전트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 로그인할 때 Windows 인증 모드를 사용하도록 구성된 경우 해당 병합 에이전트가 실패합니다. 기본 설정은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증입니다.  
  
 병합 에이전트를 시작하려면 명령 프롬프트에서 **replmerg.exe** 를 실행합니다. 자세한 내용은 [복제 에이전트 실행 파일](../concepts/replication-agent-executables-concepts.md)을 참조하십시오.  
  
 연속 모드에서 실행하는 동안 현재 세션에 대한 병합 에이전트 기록은 제거되지 않습니다. 장기 실행 에이전트로 인해 성능에 영향을 미칠 수 있는 병합 기록 테이블에 다수의 항목이 발생할 수 있습니다. 이 문제를 해결하려면 예약 모드로 전환하거나, 계속해서 연속 모드를 사용하지만 정기적으로 병합 에이전트를 다시 시작하는 전용 작업을 만들거나, 기록 수준의 자세한 정도를 줄여 행 수를 줄임으로써 성능에 미치는 영향을 줄이십시오.  
  
## <a name="see-also"></a>관련 항목  
 [복제 에이전트 관리](replication-agent-administration.md)  
  
  
