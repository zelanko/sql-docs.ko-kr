---
title: "SQL Server Integration Services (SSIS) 확장 작업자 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 77cf90268938bada458aa159a5f18f885491b407
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out-worker"></a>Integration Services(SSIS) 규모 확장 작업자

스케일 아웃 작업자에서 실행 되는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 끌어오기 실행을 스케일 아웃 Worker 서비스 스케일 아웃 마스터에서 작업 하 고 패키지 ISServerExec.exe 사용 하 여 로컬로 실행 합니다.

## <a name="configure-sql-server-integration-services-scale-out-worker-service"></a>SQL Server Integration Services 규모 확장 작업자 서비스 구성
규모 확장 작업자 서비스는 \<드라이버\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config 파일을 사용하여 구성할 수 있습니다. 구성 파일을 업데이트한 후 서비스를 다시 시작해야 합니다.

Configuration  |Description  |기본값  
---------|---------|---------
DisplayName|규모 확장 작업자의 표시 이름입니다. **사용 중이 아닌 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 합니다.**|컴퓨터 이름         
Description|규모 확장 작업자에 대한 설명입니다. **사용 중이 아닌 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 합니다.**|비어 있음         
MasterEndpoint|규모 확장 마스터에 연결하는 끝점입니다.|규모 확장 작업자 설치 중에 설정된 끝점         
MasterHttpsCertThumbprint|규모 확장 마스터를 인증하는 데 사용되는 클라이언트 SSL 인증서의 지문입니다.|규모 확장 작업자 설치 중에 지정된 클라이언트 인증서의 지문          
WorkerHttpsCertThumbprint|규모 확장 작업자를 인증하는 데 사용되는 규모 확장 마스터에 대한 인증서의 지문입니다.|규모 확장 작업자 설치 중에 자동으로 생성되고 설치되는 인증서의 지문          
StoreLocation|작업자 인증서의 저장소 위치입니다.|LocalMachine       
StoreName|해당 작업자 인증서가 있는 저장소 이름입니다.|My         
AgentHeartbeatInterval|규모 확장 작업자 하트비트의 간격입니다.|00:01:00         
TaskHeartbeatInterval|규모 확장 작업자의 작업 상태 보고 간격입니다.|00:00:10         
HeartbeatErrorTollerance|마지막으로 성공한 작업 하트비트의 이 기간 이후 하트비트의 오류 응답이 수신되면 작업이 종료됩니다.|00:10:00      
TaskRequestMaxCPU|규모 확장 작업자가 작업을 요청할 수 있는 CPU의 상한입니다. **사용 중이 아닌 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 합니다.**|70.0         
TaskRequestMinMemory|규모 확장 작업자가 작업을 요청할 수 있는 메모리의 하한(MB)입니다. **사용 중이 아닌 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 합니다.**|100.0         
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
ExecutionLogRetryTimeout|실행 로깅에 실패 하면 재시도 제한 합니다. ExecutionLogRetryCount은 ExecutionLogRetryTimeout에 도달 하는 경우 무시 됩니다.|7.00:00:00 (7 일)        
AgentId|확장 규모 작업자의 작업자 에이전트 ID입니다.|자동으로 생성됨        

## <a name="view-scale-out-worker-log"></a>규모 확장 작업자 로그 보기
스케일 아웃 Worker 서비스의 로그 파일을는 \<드라이버\>: \Users\\*[계정]*\AppData\Local\SSIS\ScaleOut\Agent 폴더 경로입니다.

각 개별 작업의 로그 위치는 TasksRootFolder에 따라 WorkerSettings.config 파일에서 구성 됩니다. 로그는 지정 되지 않은 경우에 \<드라이버\>: \Users\\*[계정]*\AppData\Local\SSIS\ScaleOut\Tasks 폴더 경로입니다. 

*[계정]* 스케일 아웃 작업자 서비스를 실행 하는 계정입니다. 기본적으로 이 계정은 SSISScaleOutWorker140입니다.

