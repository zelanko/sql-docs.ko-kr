---
title: "Integration Services(SSIS) 규모 확장 작업자 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 480a3f3d-9a79-4a02-81e5-7d27afd756c4
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Integration Services(SSIS) 규모 확장 작업자
규모 확장 작업자는 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] 규모 확장 작업자 서비스를 실행하여 규모 확장 마스터에서 실행 작업을 끌어오고 ISServerExec.exe를 사용하여 로컬에서 패키지를 실행합니다.

## <a name="configure-sql-server-integration-services-scale-out-worker-service"></a>SQL Server Integration Services 규모 확장 작업자 서비스 구성
규모 확장 작업자 서비스는 \<드라이버\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config 파일을 사용하여 구성할 수 있습니다. 구성 파일을 업데이트한 후 서비스를 다시 시작해야 합니다.
    


Configuration  |Description  |기본값  
---------|---------|---------
DisplayName|규모 확장 작업자의 표시 이름입니다. **[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1에서는 사용되지 않습니다.**|컴퓨터 이름         
Description|규모 확장 작업자에 대한 설명입니다. **[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1에서는 사용되지 않습니다.**|비어 있음         
MasterEndpoint|규모 확장 마스터에 연결하는 끝점입니다.|규모 확장 작업자 설치 중에 설정된 끝점         
MasterHttpsCertThumbprint|규모 확장 마스터를 인증하는 데 사용되는 클라이언트 SSL 인증서의 지문입니다.|규모 확장 작업자 설치 중에 지정된 클라이언트 인증서의 지문          
WorkerHttpsCertThumbprint|규모 확장 작업자를 인증하는 데 사용되는 규모 확장 마스터에 대한 인증서의 지문입니다.|규모 확장 작업자 설치 중에 자동으로 생성되고 설치되는 인증서의 지문          
StoreLocation|작업자 인증서의 저장소 위치입니다.|LocalMachine       
StoreName|해당 작업자 인증서가 있는 저장소 이름입니다.|My         
AgentHeartbeatInterval|규모 확장 작업자 하트비트의 간격입니다.|00:01:00         
TaskHeartbeatInterval|규모 확장 작업자의 작업 상태 보고 간격입니다.|00:00:10         
HeartbeatErrorTollerance|마지막으로 성공한 작업 하트비트의 이 기간 이후 하트비트의 오류 응답이 수신되면 작업이 종료됩니다.|00:10:00      
TaskRequestMaxCPU|규모 확장 작업자가 작업을 요청할 수 있는 CPU의 상한입니다. **[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1에서는 사용되지 않습니다.**|70.0         
TaskRequestMinMemory|규모 확장 작업자가 작업을 요청할 수 있는 메모리의 하한(MB)입니다. **[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1에서는 사용되지 않습니다.**|100.0         
MaxTaskCount|규모 확장 작업자가 보유할 수 있는 최대 작업 수입니다.|10         
LeaseInternval|규모 확장 작업자가 보유하고 있는 작업의 임대 간격입니다.|00:01:00         
TasksRootFolder|작업 로그의 폴더입니다. 값이 비어 있는 경우 \<드라이버\>:\Users\\*[account]*\AppData\Local\SSIS\Cluster\Tasks 폴더 경로가 사용됩니다. [account]는 규모 확장 작업자 서비스를 실행하는 계정입니다. 기본적으로 이 계정은 SSISScaleOutWorker140입니다.|비어 있음         
TaskLogLevel|규모 확장 작업자의 작업 로그 수준입니다. (자세한 정보 표시 0x01, 정보 0x02, 경고 0x04, 오류 0x08, 진행률 0x10, CriticalError 0x20, 감사 0x40)|126(정보,경고,오류,진행률,CriticalError,감사)     
TaskLogSegment|작업 로그 파일의 시간 범위입니다.|00:00:00         
TaskLogEnabled|작업 로그를 사용할 수 있는지 여부를 지정합니다.|true         
ExecutionLogCacheFolder|패키지 실행 로그 캐시에 사용되는 폴더입니다. 값이 비어 있는 경우 \<드라이버\>:\Users\\*[account]*\AppData\Local\SSIS\Cluster\Agent\ELogCache 폴더 경로가 사용됩니다. [account]는 규모 확장 작업자 서비스를 실행하는 계정입니다. 기본적으로 이 계정은 SSISScaleOutWorker140입니다.|비어 있음         
ExecutionLogMaxBufferLogCount|메모리에 있는 하나의 실행 로그 버퍼에서 캐시된 최대 실행 로그 수입니다.|10000        
ExecutionLogMaxInMemoryBufferCount|실행 로그에 대한 메모리의 최대 실행 로그 버퍼 수입니다.|10         
ExecutionLogRetryCount|실행 로깅이 실패할 경우 다시 시도 횟수입니다.|3         
AgentId|확장 규모 작업자의 작업자 에이전트 ID입니다.|자동으로 생성됨        



## <a name="view-scale-out-worker-log"></a>규모 확장 작업자 로그 보기
규모 확장 작업자 서비스의 로그 파일은 \<드라이버\>:\Users\\*[account]*\AppData\Local\SSIS\Cluster\Agent 폴더 경로에 있습니다.

각 개별 작업의 로그 위치는 TasksRootFolder에 따라 WorkerSettings.config 파일에서 구성 됩니다. 지정하지 않을 경우 로그는 \<드라이버\>:\Users\\*[account]*\AppData\Local\SSIS\Cluster\Tasks 폴더 경로에 있습니다. 

*[account]* 폴더는 규모 확장 작업자 서비스를 실행하는 계정입니다. 기본적으로 이 계정은 SSISScaleOutWorker140입니다.
    