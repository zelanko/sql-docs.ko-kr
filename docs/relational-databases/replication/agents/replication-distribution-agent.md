---
title: 복제 배포 에이전트 | Microsoft 문서
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distribution Agent, executables
- agents [SQL Server replication], Distribution Agent
- Distribution Agent, parameter reference
- command prompt [SQL Server replication]
ms.assetid: 7b4fd480-9eaf-40dd-9a07-77301e44e2ac
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 7524d1c984d1e12b744c57b97cfeb586dff3f7ce
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68770753"
---
# <a name="replication-distribution-agent"></a>복제 배포 에이전트
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  복제 배포 에이전트는 스냅샷(스냅샷 복제 및 트랜잭션 복제의 경우) 및 배포 데이터베이스 테이블에 저장된 트랜잭션(트랜잭션 배포의 경우)을 구독자의 대상 테이블로 이동하는 실행 파일입니다.  
  
> [!NOTE]  
>  매개 변수는 지정되는 순서에 제한을 받지 않습니다. 선택적 매개 변수가 지정되지 않은 경우 로컬 컴퓨터의 미리 정의된 레지스트리 설정 값이 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
distrib [-?]  
-Publisher server_name[\instance_name]  
-PublisherDB publisher_database  
-Subscriber server_name[\instance_name]  
-SubscriberDB subscriber_database   
[-AltSnapshotFolder alt_snapshot_folder_path]   
[-BcpBatchSize bcp_batch_size]  
[-CommitBatchSize commit_batch_size]  
[-CommitBatchThreshold commit_batch_threshold]  
[-Continuous]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor distributor]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-ErrorFile error_path_and_file_name]  
[-ExtendedEventConfigFile configuration_path_and_file_name]  
[-FileTransferType [0|1]]  
[-FtpAddress ftp_address]  
[-FtpPassword ftp_password]   
[-FtpPort ftp_port]  
[-FtpUserName ftp_user_name]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-Hostname host_name]  
[-KeepAliveMessageInterval keep_alive_message_interval_seconds]  
[-LoginTimeOut login_time_out_seconds]  
[-MaxBcpThreads]  
[-MaxDeliveredTransactions number_of_transactions]  
[-MessageInterval message_interval]  
[-OledbStreamThreshold oledb_stream_threshold]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2]]  
[-PacketSize packet_size]  
[-PollingInterval polling_interval]  
[-ProfileName profile_name]  
[-Publication publication]  
[-QueryTimeOut query_time_out_seconds]  
[-QuotedIdentifier quoted_identifier]  
[-SkipErrors native_error_id [:...n]]  
[-SubscriberDatabasePath subscriber_path]  
[-SubscriberLogin subscriber_login]  
[-SubscriberPassword subscriber_password]  
[-SubscriberSecurityMode [0|1]]  
[-SubscriberType [0|1|3]]  
[-SubscriptionStreams [1|2|...64]]  
[-SubscriptionTableName subscription_table]  
[-SubscriptionType [0|1|2]]  
[-TransactionsPerHistory [0|1|...10000]]  
[-UseDTS]  
[-UseInprocLoader]  
[-UseOledbStreaming]  
```  
  
## <a name="arguments"></a>인수  
 **-?**  
 사용 가능한 모든 매개 변수를 출력합니다.  
  
 **-Publisher** _server_name_[ **\\** _instance_name_]  
 게시자의 이름입니다. 해당 서버에 있는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 기본 인스턴스에 대해 *server_name*을 지정합니다. 해당 서버에 있는 명명된 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대해 server_name을 지정하고,  
  
 **-PublisherDB** _publisher_database_  
 게시자 데이터베이스의 이름입니다.  
  
 **-Subscriber** _server_name_[ **\\** _instance_name_]  
 구독자의 이름입니다. 해당 서버에 있는 기본 *server_name* 인스턴스에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 지정합니다. 해당 서버에 있는 명명된 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대해 server_name을 지정하고,  
  
 **-SubscriberDB** _subscriber_database_  
 구독자 데이터베이스의 이름입니다.  
  
 **-AltSnapshotFolder** _alt_snapshot_folder_path_  
 구독에 대한 초기 스냅샷이 들어 있는 폴더의 경로입니다.  
  
 **-BcpBatchSize** _bcp_batch_size_  
 대량 복사 작업에서 보낼 행 수입니다. **bcp in** 작업을 수행하는 경우 일괄 처리 크기는 한 번의 트랜잭션으로 서버에 보낼 행 수이며 배포 에이전트가 **bcp** 진행 메시지를 기록하기 전에 보내야 하는 행 수이기도 합니다. **bcp out** 작업을 수행하는 경우 고정 일괄 처리 크기로 **1000** 이 사용됩니다.  
  
 **-CommitBatchSize** _commit_batch_size_  
 COMMIT 문을 실행하기 전에 구독자에 대해 실행할 트랜잭션의 개수입니다. 기본값은 100이고 최대 값은 10000입니다.
  
 **-CommitBatchThreshold**  _commit_batch_threshold_  
 COMMIT 문을 실행하기 전에 구독자에 대해 실행할 복제 명령의 개수입니다. 기본값은 1000이고 최대 값은 10000입니다. 
  
 **-Continuous**  
 에이전트에서 복제된 트랜잭션의 폴링을 계속 시도할지 여부를 지정합니다. 이 인수가 지정된 경우 에이전트는 보류 중인 트랜잭션이 없는 경우에도 원본의 복제된 트랜잭션을 폴링 간격에 따라 폴링합니다.  
  
 **-DefinitionFile** _def_path_and_file_name_  
 에이전트 정의 파일의 경로입니다. 에이전트 정의 파일에는 에이전트의 명령 프롬프트 인수가 들어 있습니다. 파일 내용은 실행 파일로 구문 분석됩니다. 임의 문자가 있는 인수 값을 지정하려면 큰따옴표(")를 사용합니다.  
  
 **-Distributor** _distributor_  
 배포자 이름입니다. 배포자(밀어넣기) 배포의 경우에는 로컬 배포자의 이름이 기본 이름이 됩니다.  
  
 **-DistributorLogin** _distributor_login_  
 배포자의 로그인 이름입니다.  
  
 **-DistributorPassword** _distributor_password_  
 배포자 암호입니다.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 배포자의 보안 모드를 지정합니다. 값 0은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 모드를 나타내고 값 1은 Windows 인증 모드(기본값)를 나타냅니다.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 연결을 만들 때 배포 에이전트에서 사용하는 SSL(Secure Sockets Layer) 암호화의 수준입니다.  
  
|EncryptionLevel 값|Description|  
|---------------------------|-----------------|  
|**0**|SSL이 사용되지 않음을 지정합니다.|  
|**1**|SSL이 사용되지만 에이전트에서 SSL 서버 인증서가 트러스트된 발급자에 의해 서명된 것인지 확인하지 않음을 지정합니다.|  
|**2**|SSL이 사용되고 인증서가 확인됨을 지정합니다.|  
 
 > [!NOTE]  
 >  유효한 SSL 인증서는 SQL Server의 정규화된 도메인 이름으로 정의됩니다. -EncryptionLevel을 2로 설정할 때 에이전트가 성공적으로 연결되도록 하려면 로컬 SQL Server에서 별칭을 만듭니다. '별칭 이름' 매개 변수는 서버 이름이어야 하며 '서버' 매개 변수는 SQL Server의 정규화된 이름으로 설정되어야 합니다.

 자세한 내용은 [복제 보안 설정 보기 및 수정](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)을 참조하세요.  
  
 **-ErrorFile** _error_path_and_file_name_  
 배포 에이전트에서 생성한 오류 파일의 경로 및 파일 이름입니다. 이 파일은 구독자에서 복제 트랜잭션을 적용하는 동안 오류가 발생할 때마다 생성되며 게시자나 배포자에서 발생한 오류는 이 파일에 기록되지 않습니다. 이 파일에는 실패한 복제 트랜잭션 및 관련 오류 메시지가 들어 있습니다. 지정하지 않으면 오류 파일이 배포 에이전트의 현재 디렉터리에 생성됩니다. 오류 파일 이름은 배포 에이전트의 이름에 .err 확장명을 붙인 것입니다. 지정된 파일 이름이 존재하면 오류 메시지가 파일에 추가됩니다. 이 매개 변수는 최대 256개의 유니코드 문자일 수 있습니다.  
  
 **-ExtendedEventConfigFile** _configuration_path_and_file_name_  
 확장 이벤트 XML 구성 파일의 경로 및 파일 이름을 지정합니다. 확장 이벤트 구성 파일에서는 세션을 구성하고 추적 이벤트를 사용하도록 설정할 수 있습니다.  
  
 **-FileTransferType** [ **0**| **1**]  
 파일 전송 유형을 지정합니다. 값 **0** 은 UNC(Universal Naming Convention)를 나타내고, 값 **1** 은 FTP(File Transfer Protocol)를 나타냅니다.  
  
 **-FtpAddress** _ftp_address_  
 배포자용 FTP 서비스의 네트워크 주소입니다. 지정되지 않은 경우, **DistributorAddress** 가 사용됩니다. **DistributorAddress** 가 지정되지 않은 경우 **Distributor** 가 사용됩니다.  
  
 **-FtpPassword** _ftp_password_  
 FTP 서비스에 연결할 때 사용되는 사용자 암호입니다.  
  
 **-FtpPort** _ftp_port_  
 배포자용 FTP 서비스의 포트 번호입니다. 지정되지 않은 경우, FTP 서비스용 기본 포트 번호(21)가 사용됩니다.  
  
 **-FtpUserName**  _ftp_user_name_  
 FTP 서비스에 연결할 때 사용할 사용자 이름입니다. 지정되지 않은 경우, **anonymous** 가 사용됩니다.  
  
 **-HistoryVerboseLevel** [ **0** | **1** | **2** | **3** ]  
 배포 작업을 수행하는 동안 기록에 추가되는 양을 지정합니다. **1**을 선택하여 기록 로깅이 성능에 주는 영향을 최소화할 수 있습니다.  
  
|HistoryVerboseLevel 값|Description|  
|-------------------------------|-----------------|  
|**0**|진행 메시지를 콘솔이나 출력 파일에 씁니다. 기록 레코드는 배포 데이터베이스에 기록되지 않습니다.|  
|**1**|기본값 시작, 진행, 성공 등과 같이 상태가 동일한 이전 기록 메시지를 항상 업데이트합니다. 상태가 같은 이전 레코드가 없으면 새 레코드를 삽입합니다.|  
|**2**|유휴 메시지나 장기 실행 작업 메시지에 대한 레코드가 없으면 새 기록 레코드를 삽입합니다. 이 경우 이전 레코드를 업데이트합니다.|  
|**3**|유휴 메시지에 대한 레코드가 없으면 항상 새 레코드를 삽입합니다.|  
  
 **-Hostname** _host_name_  
 게시자에 연결할 때 사용하는 호스트 이름입니다. 이 매개 변수는 최대 128개의 유니코드 문자일 수 있습니다.  
  
 **-KeepAliveMessageInterval** _keep_alive_message_interval_seconds_  
 기록 스레드가 기존 연결에서 서버의 응답을 기다리고 있는지 확인할 때까지 걸리는 시간(초)입니다. 이 값을 줄이면 장기 실행 일괄 처리를 실행할 때 점검 에이전트에서 배포 에이전트를 주의 대상으로 표시하지 않도록 할 수 있습니다. 기본값은 **300** 초입니다.  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 로그인 시간이 초과될 때까지 걸리는 시간(초)입니다. 기본값은 **15** 초입니다.  
  
 **-MaxBcpThreads** _number_of_threads_  
 병렬로 수행할 수 있는 대량 복사 작업 수를 지정합니다. 동시에 존재하는 스레드 및 ODBC 연결의 최대 개수는 **MaxBcpThreads** 와 배포 데이터베이스의 동기화 트랜잭션에 나타나는 대량 복사 요청 수 중 더 작은 값입니다. **MaxBcpThreads** 값은 **0** 보다 크고 하드 코딩된 상한값이 없어야 합니다. 기본값은 최대값이 **8** 인 프로세서 수의 **2**배입니다. 게시자에서 동시 스냅샷 옵션을 사용하여 생성된 스냅샷을 적용할 경우 **MaxBcpThreads**에 지정한 숫자에 관계없이 하나의 스레드가 사용됩니다.  
  
 **-MaxDeliveredTransactions** _number_of_transactions_  
 한 번의 동기화에서 구독자에 적용되는 밀어넣기 또는 끌어오기 트랜잭션의 최대 개수입니다. 값 **0** 은 최대값이 무한개의 트랜잭션임을 나타냅니다. 다른 값은 구독자가 게시자에서 끌어오는 동기화의 기간을 줄이는 데 사용할 수 있습니다.  
  
> [!NOTE]  
>  -MaxDeliveredTransactions와 -Continuous를 둘 다 지정한 경우 배포 에이전트는 -Continuous가 지정되었음에도 불구하고 지정된 개수의 트랜잭션을 제공한 다음 중지합니다. 작업이 완료되면 배포 에이전트를 다시 시작해야 합니다.  
  
 **-MessageInterval**  _message_interval_  
 기록 로깅에 사용되는 시간 간격입니다. 기록 이벤트는 다음과 같은 경우에 기록됩니다.  
  
-   마지막 기록 이벤트가 기록된 후 **TransactionsPerHistory** 값에 도달한 경우  
  
-   마지막 기록 이벤트가 기록된 후 **MessageInterval** 값에 도달한 경우  
  
 원본에 사용할 수 있는 복제된 트랜잭션이 없는 경우 에이전트에서는 배포자에 트랜잭션 없음 메시지를 보고합니다. 이 옵션은 다른 트랜잭션 없음 메시지를 보고하기 전에 에이전트에서 기다리는 시간을 지정합니다. 에이전트에서는 이전에 복제된 트랜잭션을 처리한 후 원본에 사용할 수 있는 트랜잭션이 없는지 감지할 때 항상 트랜잭션 없음 메시지를 보고합니다. 기본값은 60초입니다.  
  
 **-OledbStreamThreshold** _oledb_stream_threshold_  
 BLOB(Binary Large Object)의 최소 크기(바이트)를 지정합니다. 이 크기를 넘으면 데이터가 스트림으로 바인딩됩니다. 이 매개 변수를 사용하려면 **–UseOledbStreaming**을 지정해야 합니다. 값은 400바이트에서 1048576바이트 사이일 수 있으며 기본값은 16384바이트입니다.  
  
 **-Output** _output_path_and_file_name_  
 에이전트 출력 파일의 경로입니다. 파일 이름을 지정하지 않으면 출력이 콘솔로 전달됩니다. 지정된 파일 이름이 존재하면 출력이 파일에 추가됩니다.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 출력이 자세해야 하는지 여부를 지정합니다. 정보 표시 수준이 **0**이면 오류 메시지만 출력됩니다. 정보 표시 수준이 **1**이면 모든 진행률 보고 메시지가 출력됩니다. 정보 표시 수준이 **2** (기본값)이면 디버깅에 유용한 오류 메시지와 진행률 보고 메시지가 모두 출력됩니다.  
  
 **-PacketSize** _packet_size_  
 패킷 크기(바이트)입니다. 기본값은 4096바이트입니다.  
  
 **-PollingInterval** _polling_interval__  
 배포 데이터베이스에서 복제된 트랜잭션을 쿼리하는 빈도(초)입니다. 기본값은 5초입니다.  
  
 **-ProfileName** _profile_name_  
 에이전트 매개 변수에 사용할 에이전트 프로필을 지정합니다. **ProfileName** 이 NULL이면 에이전트 프로필이 사용되지 않습니다. **ProfileName** 이 지정되지 않으면 에이전트 유형에 대한 기본 프로필이 사용됩니다. 자세한 내용은 [복제 에이전트 프로필](../../../relational-databases/replication/agents/replication-agent-profiles.md)을 참조하세요.  
  
 **-Publication**  _publication_  
 게시의 이름입니다. 이 매개 변수는 게시가 새 구독이나 다시 초기화된 구독에 대해 항상 스냅샷을 사용할 수 있도록 설정된 경우에만 유효합니다.  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 쿼리 시간이 초과될 때까지 걸리는 시간(초)입니다. 기본값은 1800초입니다.  
  
 **-QuotedIdentifier** _quoted_identifier_  
 사용할 따옴표 붙은 식별자 문자를 지정합니다. 값의 첫 번째 문자는 배포 에이전트에서 사용하는 값을 나타냅니다. 값을 지정하지 않고 **QuotedIdentifier** 를 사용하면 배포 에이전트에서는 공백을 사용합니다. **QuotedIdentifier** 를 사용하지 않는 경우 배포 에이전트에서는 구독자가 지원하는 따옴표 붙은 식별자를 사용합니다.  
  
 **-SkipErrors** _native_error_id_ [ **:** _...n_]  
 이 에이전트에서 건너뛸 오류 번호를 지정하는 콜론으로 구분된 목록입니다.  
  
 **-SubscriberDatabasePath** _subscriber_database_path_  
 **SubscriberType** 이 **2** 로서, ODBC DSN(데이터 원본 이름)이 없는 Jet 데이터베이스에 대한 연결이 허용되는 경우 Jet 데이터베이스(.mdb 파일)의 경로입니다.  
  
 **-SubscriberLogin** _subscriber_login_  
 구독자의 로그인 이름입니다. **SubscriberSecurityMode** 가 **0** ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증의 경우)이면 이 매개 변수를 지정해야 합니다.  
  
 **-SubscriberPassword** _subscriber_password_  
 구독자 암호입니다. **SubscriberSecurityMode** 가 **0** ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증의 경우)이면 이 매개 변수를 지정해야 합니다.  
  
 **-SubscriberSecurityMode** [ **0**| **1**]  
 구독자의 보안 모드를 지정합니다. 값 **0** 은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 나타내고 값 **1** 은 Windows 인증 모드(기본값)를 나타냅니다.  
  
 **-SubscriberType** [ **0**| **1**| **3**]  
 배포 에이전트에서 사용하는 구독자 연결 유형을 지정합니다.  
  
|SubscriberType 값|Description|  
|--------------------------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|**1**|ODBC 데이터 원본|  
|**3**|OLE DB 데이터 원본|  
  
 **-SubscriptionStreams** [**0**|**1**|**2**|...**64**]  
 단일 스레드를 사용할 때 나타나는 여러 가지 트랜잭션 특징을 유지하면서 변경 내용의 일괄 처리를 구독자에 대해 병렬로 적용하기 위해 배포 에이전트당 허용된 연결 수입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 게시자의 경우 1에서 64 사이의 값 범위가 지원됩니다. 이 매개 변수는 게시자 및 배포자가 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 실행 중인 경우에만 지원됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자 또는 피어 투 피어 구독의 경우 이 매개 변수가 지원되지 않거나 0이어야 합니다.  
  
> [!NOTE]  
>  여러 연결 중 하나가 실행 또는 커밋되지 않으면 모든 연결에서 현재 일괄 처리를 중지하고 에이전트가 단일 스트림을 사용하여 실패한 일괄 처리를 다시 시도합니다. 이러한 재시도 단계가 완료되기 전에는 구독자에 임시 트랜잭션 불일치가 발생할 수 있으며 실패한 일괄 처리가 성공적으로 커밋되면 구독자의 트랜잭션 일관성이 다시 유지됩니다.  
  
> [!IMPORTANT]  
>  **-SubscriptionStreams**의 값으로 2 이상을 지정할 경우 구독자에서 트랜잭션을 받는 순서가 게시자에서 트랜잭션을 만든 순서와 다를 수 있습니다. 이 동작으로 인해 동기화 중 제약 조건 위반이 발생할 경우에는 동기화할 때 NOT FOR REPLICATION 옵션을 사용하여 제약 조건이 적용되지 않도록 해야 합니다. 자세한 내용은 [동기화하는 동안 트리거 및 제약 조건 동작 제어&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)를 참조하세요.  
  
> [!NOTE]  
>  Subscriptionstreams는 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 제공하도록 구성된 아티클에 대해서는 작동하지 않습니다. subscriptionstreams를 사용하려면 대신 저장 프로시저 호출을 제공하도록 아티클을 구성하십시오.  
  
 **-SubscriptionTableName** _subscription_table_  
 지정된 구독자에서 생성되거나 사용된 구독 테이블의 이름입니다. 지정되지 않은 경우 [MSreplication_subscriptions&#40;Transact-SQL&#41;](../../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) 테이블이 사용됩니다. 긴 파일 이름을 지원하지 않는 DBMS(데이터베이스 관리 시스템)의 경우에 이 옵션을 사용합니다.  
  
 **-SubscriptionType** [ **0**| **1**| **2**]  
 배포의 구독 유형을 지정합니다. 값 **0** 은 밀어넣기 구독을, 값 **1** 은 끌어오기 구독을, 값 **2** 는 익명 구독을 나타냅니다.  
  
 **-TransactionsPerHistory** [ **0**| **1**|... **10000**]  
 기록 로깅의 트랜잭션 간격을 지정합니다. 기록 로깅의 마지막 인스턴스 후 커밋된 트랜잭션의 수가 이 옵션보다 클 경우 기록 메시지가 기록됩니다. 기본값은 100입니다. 값이 **0** 이면 **TransactionsPerHistory**에는 제한이 없습니다. See the preceding **–MessageInterval**parameter.  
  
 **-UseDTS**  
 데이터 변환을 허용하는 게시의 매개 변수로 지정해야 합니다.  
  
 **-UseInprocLoader**  
 배포 에이전트에서 구독자에 스냅샷 파일을 적용할 때 BULK INSERT 명령을 사용하도록 지정하여 초기 스냅샷의 성능을 향상시킵니다. 이 매개 변수는 XML 데이터 형식과 호환되지 않으므로 이후에는 지원되지 않습니다. XML 데이터를 복제하지 않을 계획이라면 이 매개 변수를 사용할 수 있습니다. 이 매개 변수는 문자 모드 스냅샷 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자와 함께 사용할 수 없습니다. 이 매개 변수를 사용하려면 구독자의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정에 스냅샷 .bcp 데이터 파일이 있는 디렉터리에 대한 읽기 권한이 있어야 합니다. 이 매개 변수를 사용하지 않으면 에이전트([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자의 경우) 또는 에이전트에서 로드한 ODBC 드라이버([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구독자의 경우)가 파일 내용을 읽으므로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정의 보안 컨텍스트가 사용되지 않습니다.  
  
 **-UseOledbStreaming**  
 이 인수를 지정하면 BLOB(Binary Large Object) 데이터를 스트림으로 바인딩할 수 있습니다. 크기(바이트)가 얼마 이상일 때 스트림을 사용할지를 지정하려면 **-OledbStreamThreshold** 를 사용합니다. **UseOledbStreaming** 은 기본적으로 사용하도록 설정됩니다. **UseOledbStreaming**은 **C:\Program Files\Microsoft SQL Server\\<version\>\COM** 폴더에 데이터를 씁니다.  
  
## <a name="remarks"></a>설명  
  
> [!IMPORTANT]  
>  도메인 사용자 계정(기본값)이 아닌 로컬 시스템 계정에서 실행되도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트를 설치한 경우 해당 서비스에서는 로컬 컴퓨터에만 액세스할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트에서 실행되는 배포 에이전트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 인스턴스에 로그인할 때 Windows 인증 모드를 사용하도록 구성된 경우 해당 배포 에이전트가 실패합니다. 기본 설정은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증입니다. 보안 계정을 변경하는 방법에 대한 자세한 내용은 [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)을 참조하십시오.  
  
 배포 에이전트를 시작하려면 명령 프롬프트에서 **distrib.exe** 를 실행합니다. 자세한 내용은 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|**-ExtendedEventConfigFile** 매개 변수를 추가했습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [복제 에이전트 관리](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
