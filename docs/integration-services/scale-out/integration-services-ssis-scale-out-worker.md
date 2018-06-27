---
title: SSIS(SQL Server Integration Services) Scale Out 작업자 | Microsoft Docs
description: 이 문서에서는 SSIS Scale Out의 Scale Out 마스터 구성 요소 설명
ms.custom: performance
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: 2949f0aabaf4f59d6d2fc6635991f8eb0a921ca6
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35408125"
---
# <a name="integration-services-ssis-scale-out-worker"></a>Integration Services(SSIS) 규모 확장 작업자

Scale Out 작업자는 Scale Out 작업자 서비스를 실행하여 Scale Out 마스터에서 실행 작업을 끌어옵니다. 그런 다음 작업자가 `ISServerExec.exe`를 사용하여 로컬에서 패키지를 실행합니다.

## <a name="configure-the-scale-out-worker-service"></a>Scale Out 작업자 서비스 구성
Scale Out 작업자 서비스는 ` \<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config` 파일을 사용하여 구성합니다. 구성 파일을 업데이트한 후에는 서비스를 다시 시작해야 합니다.

Configuration  |설명  |기본값  
---------|---------|---------
DisplayName|규모 확장 작업자의 표시 이름입니다. **[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017에서는 사용되지 않습니다.**|컴퓨터 이름         
설명|규모 확장 작업자에 대한 설명입니다. **[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017에서는 사용되지 않습니다.**|비어 있음         
MasterEndpoint|규모 확장 마스터에 연결하는 끝점입니다.|규모 확장 작업자 설치 중에 설정된 끝점         
MasterHttpsCertThumbprint|규모 확장 마스터를 인증하는 데 사용되는 클라이언트 SSL 인증서의 지문입니다.|규모 확장 작업자 설치 중에 지정된 클라이언트 인증서의 지문          
WorkerHttpsCertThumbprint|규모 확장 작업자를 인증하는 데 사용되는 규모 확장 마스터에 대한 인증서의 지문입니다.|규모 확장 작업자 설치 중에 자동으로 생성되고 설치되는 인증서의 지문          
StoreLocation|작업자 인증서의 저장소 위치입니다.|LocalMachine       
StoreName|해당 작업자 인증서가 있는 저장소 이름입니다.|My         
AgentHeartbeatInterval|규모 확장 작업자 하트비트의 간격입니다.|00:01:00         
TaskHeartbeatInterval|규모 확장 작업자의 작업 상태 보고 간격입니다.|00:00:10         
HeartbeatErrorTollerance|마지막으로 성공한 작업 하트비트의 이 기간 이후 하트비트의 오류 응답이 수신되면 작업이 종료됩니다.|00:10:00      
TaskRequestMaxCPU|규모 확장 작업자가 작업을 요청할 수 있는 CPU의 상한입니다.|70.0         
TaskRequestMinMemory|규모 확장 작업자가 작업을 요청할 수 있는 메모리의 하한(MB)입니다.|100.0         
MaxTaskCount|규모 확장 작업자가 보유할 수 있는 최대 작업 수입니다.|10         
LeaseInternval|규모 확장 작업자가 보유하고 있는 작업의 임대 간격입니다.|00:01:00         
TasksRootFolder|작업 로그의 폴더입니다. 값이 비어 있는 경우 `\<drive\>:\Users\[account]\AppData\Local\SSIS\Cluster\Tasks` 폴더 경로가 사용됩니다. [account]는 규모 확장 작업자 서비스를 실행하는 계정입니다. 기본적으로 이 계정은 SSISScaleOutWorker140입니다.|비어 있음         
TaskLogLevel|규모 확장 작업자의 작업 로그 수준입니다. (자세한 정보 표시 0x01, 정보 0x02, 경고 0x04, 오류 0x08, 진행률 0x10, CriticalError 0x20, 감사 0x40)|126(정보, 경고, 오류, 진행률, CriticalError, 감사)     
TaskLogSegment|작업 로그 파일의 시간 범위입니다.|00:00:00         
TaskLogEnabled|작업 로그를 사용할 수 있는지 여부를 지정합니다.|true         
ExecutionLogCacheFolder|패키지 실행 로그 캐시에 사용되는 폴더입니다. 값이 비어 있는 경우 ` \<drive\>:\Users\[account]\AppData\Local\SSIS\Cluster\Agent\ELogCache` 폴더 경로가 사용됩니다. [account]는 규모 확장 작업자 서비스를 실행하는 계정입니다. 기본적으로 이 계정은 SSISScaleOutWorker140입니다.|비어 있음         
ExecutionLogMaxBufferLogCount|메모리에 있는 하나의 실행 로그 버퍼에서 캐시된 최대 실행 로그 수입니다.|10000        
ExecutionLogMaxInMemoryBufferCount|실행 로그에 대한 메모리의 최대 실행 로그 버퍼 수입니다.|10         
ExecutionLogRetryCount|실행 로깅이 실패할 경우 다시 시도 횟수입니다.|3
ExecutionLogRetryTimeout|실행 로깅이 실패할 경우 다시 시도 시간 제한입니다. i\ExecutionLogRetryTimeout에 도달하면 ExecutionLogRetryCount가 무시됩니다. |7.00:00:00(7일)        
AgentId|Scale Out 작업자의 작업자 에이전트 ID|자동으로 생성됨    
||||    

## <a name="view-the-scale-out-worker-log"></a>Scale Out 작업자 로그 보기
Scale Out 작업자 서비스의 로그 파일은 `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Agent` 폴더에 있습니다.

각 개별 작업의 로그 위치는 `TasksRootFolder`의 `WorkerSettings.config` 파일에 구성됩니다. 값을 지정하지 않으면 `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Tasks` 폴더에 로그가 있습니다. 

*[account]* 매개 변수는 Scale Out 작업자 서비스를 실행하는 계정입니다. 기본적으로 이 계정은 `SSISScaleOutWorker140`입니다.

## <a name="next-steps"></a>다음 단계
[Integration Services(SSIS) Scale Out 마스터](integration-services-ssis-scale-out-master.md)
