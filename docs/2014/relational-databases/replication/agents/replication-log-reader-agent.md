---
title: 복제 로그 판독기 에이전트 | Microsoft 문서
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Log Reader Agent, executables
- Log Reader Agent, parameter reference
- agents [SQL Server replication], Log Reader Agent
- command prompt [SQL Server replication]
ms.assetid: 5487b645-d99b-454c-8bd2-aff470709a0e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e2dbe201e2690a013902ad6891b7f93f68fe0e04
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63127012"
---
# <a name="replication-log-reader-agent"></a>복제 로그 판독기 에이전트
  복제 로그 판독기 에이전트는 트랜잭션 복제를 위해 구성한 각 데이터베이스의 트랜잭션 로그를 모니터링하고 트랜잭션 로그에서 복제 대상으로 표시된 트랜잭션을 배포 데이터베이스에 복사하는 실행 파일입니다.  
  
> [!NOTE]  
>  매개 변수는 지정되는 순서에 제한을 받지 않습니다. 선택적 매개 변수가 지정되지 않은 경우 기본 에이전트 프로필을 기반으로 하여 미리 정의된 값이 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
      logread [-?]   
-Publisherserver_name[\instance_name]   
-PublisherDBpublisher_database   
[-Continuous]  
[-DefinitionFiledef_path_and_file_name]  
[-Distributorserver_name[\instance_name]]  
[-DistributorLogindistributor_login]  
[-DistributorPassworddistributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-ExtendedEventConfigFileconfiguration_path_and_file_name]  
[-HistoryVerboseLevel [0|1|2]]  
[-KeepAliveMessageIntervalkeep_alive_message_interval_seconds]  
[-LoginTimeOutlogin_time_out_seconds]  
[-LogScanThresholdscan_threshold]  
[-MaxCmdsInTrannumber_of_commands]  
[-MessageIntervalmessage_interval]  
[-Outputoutput_path_and_file_name]  
[-OutputVerboseLevel [0|1|2|3|4]]  
[-PacketSizepacket_size]  
[-PollingIntervalpolling_interval]  
[-ProfileNameprofile_name]   
[-PublisherFailoverPartnerserver_name[\instance_name] ]  
[-PublisherSecurityMode [0|1]]  
[-PublisherLoginpublisher_login]  
[-PublisherPasswordpublisher_password]   
[-QueryTimeOutquery_time_out_seconds]  
[-ReadBatchSizenumber_of_transactions]   
[-ReadBatchThresholdread_batch_threshold]  
[-RecoverFromDataErrors]  
```  
  
## <a name="arguments"></a>인수  
 **-?**  
 사용 정보를 표시합니다.  
  
 **-Publisher** _server_name_[ **\\** _instance_name_]  
 게시자의 이름입니다. 해당 서버에 있는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 기본 인스턴스에 대해 *server_name*을 지정합니다. 해당 서버에 있는 명명된 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대해 server_name을 지정하고,  
  
 **-PublisherDB** _publisher_database_  
 게시자 데이터베이스의 이름입니다.  
  
 **-Continuous**  
 에이전트에서 복제된 트랜잭션의 폴링을 계속 시도할지 여부를 지정합니다. 이 인수가 지정된 경우 에이전트는 보류 중인 트랜잭션이 없는 경우에도 원본의 복제된 트랜잭션을 폴링 간격에 따라 폴링합니다.  
  
 **-DefinitionFile** _def_path_and_file_name_  
 에이전트 정의 파일의 경로입니다. 에이전트 정의 파일에는 에이전트의 명령줄 인수가 들어 있습니다. 파일 내용은 실행 파일로 구문 분석됩니다. 임의 문자가 있는 인수 값을 지정하려면 큰따옴표(")를 사용합니다.  
  
 **-Distributor** _server_name_[ **\\** _instance_name_]  
 배포자 이름입니다. 해당 서버에 있는 기본 *server_name* 인스턴스에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 지정합니다. 해당 서버에 있는 명명된 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대해 server_name을 지정하고,  
  
 **-DistributorLogin** _distributor_login_  
 배포자의 로그인 이름입니다.  
  
 **-DistributorPassword** _distributor_password_  
 배포자 암호입니다.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 배포자의 보안 모드를 지정합니다. 값 **0** 은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 모드(기본값)를 나타내며 값 **1** 은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 인증 모드를 나타냅니다.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 연결을 만들 때 로그 판독기 에이전트에서 사용하는 SSL(Secure Sockets Layer) 암호화의 수준입니다.  
  
|EncryptionLevel 값|Description|  
|---------------------------|-----------------|  
|**0**|SSL이 사용되지 않음을 지정합니다.|  
|**1**|SSL이 사용되지만 에이전트에서 SSL 서버 인증서가 트러스트된 발급자에 의해 서명된 것인지 확인하지 않음을 지정합니다.|  
|**2**|SSL이 사용되고 인증서가 확인됨을 지정합니다.|  

 > [!NOTE]  
 >  유효한 SSL 인증서는 SQL Server의 정규화된 도메인 이름으로 정의됩니다. -EncryptionLevel을 2로 설정할 때 에이전트가 성공적으로 연결되도록 하려면 로컬 SQL Server에서 별칭을 만듭니다. '별칭 이름' 매개 변수는 서버 이름이어야 하며 '서버' 매개 변수는 SQL Server의 정규화된 이름으로 설정되어야 합니다.
 
 자세한 내용은 [SQL Server 복제 보안](../security/view-and-modify-replication-security-settings.md)을 참조 하세요.  
  
 **-ExtendedEventConfigFile** _configuration_path_and_file_name_  
 확장 이벤트 XML 구성 파일의 경로 및 파일 이름을 지정합니다. 확장 이벤트 구성 파일에서는 세션을 구성하고 추적 이벤트를 사용하도록 설정할 수 있습니다.  
  
 **-HistoryVerboseLevel** [ **0**| **1**| **2**]  
 로그 판독기 작업을 수행하는 동안 기록에 추가되는 양을 지정합니다. **1**을 선택하여 기록 로깅이 성능에 주는 영향을 최소화할 수 있습니다.  
  
|HistoryVerboseLevel 값|Description|  
|-------------------------------|-----------------|  
|**0**||  
|**1**|기본값 시작, 진행, 성공 등과 같이 상태가 동일한 이전 기록 메시지를 항상 업데이트합니다. 상태가 같은 이전 레코드가 없으면 새 레코드를 삽입합니다.|  
|**2**|유휴 메시지나 장기 실행 작업 메시지에 대한 레코드가 없으면 새 기록 레코드를 삽입합니다. 이 경우 이전 레코드를 업데이트합니다.|  
  
 **-KeepAliveMessageInterval** _keep_alive_message_interval_seconds_  
 기록 스레드가 기존 연결에서 서버의 응답을 기다리고 있는지 확인할 때까지 걸리는 시간(초)입니다. 이 값을 줄이면 장기 실행 일괄 처리를 실행할 때 점검 에이전트에서 로그 판독기 에이전트를 주의 대상으로 표시하지 않도록 할 수 있습니다. 기본값은 300초입니다.  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 로그인 시간이 초과될 때까지 걸리는 시간(초)입니다. 기본값은 15초입니다.  
  
 **-LogScanThreshold** _scan_threshold_  
 내부적으로만 사용됩니다.  
  
 **-MaxCmdsInTran** _number_of_commands_  
 로그 판독기가 배포 데이터베이스에 명령을 쓸 때 하나의 트랜잭션으로 그룹화되는 문의 최대 개수를 지정합니다. 이 매개 변수를 사용하면 로그 판독기 에이전트와 배포 에이전트가 게시자에서 여러 명령으로 구성된 큰 트랜잭션을 구독자에 적용할 때 여러 개의 작은 트랜잭션으로 나눌 수 있습니다. 이 매개 변수를 지정하면 배포자에서 경합을 줄일 수 있고 게시자와 구독자 간 대기 시간을 줄일 수 있습니다. 원래 트랜잭션이 작은 단위로 적용되므로 구독자는 엄격한 트랜잭션 원자성을 깨고 원래 트랜잭션이 끝나기 전에 큰 논리적 게시자 트랜잭션의 행에 액세스할 수 있습니다. 기본값은 **0**으로 게시자의 트랜잭션 경계를 유지합니다.  
  
> [!NOTE]  
>  이 매개 변수는[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외의 게시에 대해서는 무시됩니다. 자세한 내용은 [Performance Tuning for Oracle Publishers](../non-sql/performance-tuning-for-oracle-publishers.md)의 "트랜잭션 세트 작업 구성" 섹션을 참조하십시오.  
  
 **-MessageInterval** _message_interval_  
 기록 로깅에 사용되는 시간 간격입니다. 기록 이벤트는 마지막 기록 이벤트가 기록된 후 **MessageInterval** 값에 도달할 때 기록됩니다.  
  
 원본에 사용할 수 있는 복제된 트랜잭션이 없는 경우 에이전트에서는 배포자에 트랜잭션 없음 메시지를 보고합니다. 이 옵션은 다른 트랜잭션 없음 메시지를 보고하기 전에 에이전트에서 기다리는 시간을 지정합니다. 에이전트에서는 이전에 복제된 트랜잭션을 처리한 후 원본에 사용할 수 있는 트랜잭션이 없는지 감지할 때 항상 트랜잭션 없음 메시지를 보고합니다. 기본값은 60초입니다.  
  
 **-Output** _output_path_and_file_name_  
 에이전트 출력 파일의 경로입니다. 파일 이름을 지정하지 않으면 출력이 콘솔로 전달됩니다. 지정된 파일 이름이 존재하면 출력이 파일에 추가됩니다.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2** | **3** | **4** ]  
 출력이 자세해야 하는지 여부를 지정합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|오류 메시지만 출력됩니다.|  
|**1**|모든 에이전트 진행률 보고 메시지가 출력됩니다.|  
|**2** (기본값)|모든 오류 메시지와 에이전트 진행률 보고 메시지가 출력됩니다.|  
|**3**|복제된 각 명령의 처음 100바이트가 출력됩니다.|  
|**4**|복제된 모든 명령이 출력됩니다.|  
  
 값 2-4는 디버깅할 때 유용합니다.  
  
 **-PacketSize** _packet_size_  
 패킷 크기(바이트)입니다. 기본값은 4096바이트입니다.  
  
 **-PollingInterval** _polling_interval_  
 로그에서 복제된 트랜잭션을 쿼리하는 빈도(초)입니다. 기본값은 5초입니다.  
  
 **-ProfileName** _profile_name_  
 에이전트 매개 변수에 사용할 에이전트 프로필을 지정합니다. **ProfileName** 이 NULL이면 에이전트 프로필이 사용되지 않습니다. **ProfileName** 이 지정되지 않으면 에이전트 유형에 대한 기본 프로필이 사용됩니다. 자세한 내용은 [복제 에이전트 프로필](replication-agent-profiles.md)을 참조하세요.  
  
 **-PublisherFailoverPartner** _server_name_[ **\\** _instance_name_]  
 게시 데이터베이스와 함께 데이터베이스 미러링 세션에 참여하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 장애 조치 파트너 인스턴스를 지정합니다. 자세한 내용은 [데이터베이스 미러링 및 복제&#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)을 참조하세요.  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 게시자의 보안 모드를 지정합니다. 값 **0** 은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증(기본값)을 나타내며 값 **1** 은 Windows 인증 모드를 나타냅니다.  
  
 **-PublisherLogin** _publisher_login_  
 게시자 로그인 이름입니다.  
  
 **-PublisherPassword** _publisher_password_  
 게시자 암호입니다.  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 쿼리 시간이 초과될 때까지 걸리는 시간(초)입니다. 기본값은 1800초입니다.  
  
 **-ReadBatchSize** _number_of_transactions_  
 게시 데이터베이스의 트랜잭션 로그에서 읽은 처리 사이클당 최대 트랜잭션 수로서, 기본값은 500입니다. 에이전트에서는 로그의 모든 트랜잭션을 읽을 때까지 일괄 처리로 트랜잭션을 계속 읽습니다. 이 매개 변수는 Oracle 게시자에 대해서는 지원되지 않습니다.  
  
 **-ReadBatchThreshold** _number_of_commands_  
 배포 에이전트에서 구독자에 대해 실행하기 전에 트랜잭션 로그에서 읽을 복제 명령의 수입니다. 기본값은 0입니다. 이 매개 변수가 지정되어 있지 않으면 로그 판독기 에이전트에서는 로그의 끝까지 또는 **-ReadBatchSize** (트랜잭션 수)에 지정된 개수까지 읽습니다.  
  
 **-RecoverFromDataErrors**  
 SQL Server 이외의 게시자에서 게시된 열 데이터에 오류가 발생할 경우에도 로그 판독기 에이전트가 계속 실행되도록 지정합니다. 기본적으로는 이러한 오류가 발생하면 로그 판독기 에이전트가 실패합니다. **-RecoverFromDataErrors**를 사용하면 잘못된 열 데이터가 NULL 또는 null이 아닌 적절한 값으로 복제되며 [MSlogreader_history](/sql/relational-databases/system-tables/mslogreader-history-transact-sql) 테이블에 경고 메시지가 기록됩니다. 이 매개 변수는 Oracle 게시자에 대해서만 지원됩니다.  
  
## <a name="remarks"></a>설명  
  
> [!IMPORTANT]  
>  도메인 사용자 계정(기본값) 대신 로컬 시스템 계정에서 실행되도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트를 설치한 경우 해당 서비스에서는 로컬 컴퓨터에만 액세스할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트에서 실행되는 로그 판독기 에이전트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 로그인할 때 Windows 인증 모드를 사용하도록 구성된 경우 해당 로그 판독기 에이전트가 실패합니다. 기본 설정은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증입니다. 보안 계정을 변경하는 방법에 대한 자세한 내용은 [View and Modify Replication Security Settings](../security/view-and-modify-replication-security-settings.md)을 참조하십시오.  
  
 로그 판독기 에이전트를 시작하려면 명령 프롬프트에서 **logread.exe** 를 실행합니다. 자세한 내용은 [복제 에이전트 실행 파일 개념](../concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|**-ExtendedEventConfigFile** 매개 변수를 추가했습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [복제 에이전트 관리](replication-agent-administration.md)  
  
  
