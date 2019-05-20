---
title: SSIS(SQL Server Integration Services) Scale Out 마스터 | Microsoft Docs
description: 이 문서에서는 SSIS Scale Out의 Scale Out 마스터 구성 요소 설명
ms.custom: performance
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: 51c2efbde3a87c85722022b9114354e8f57d8c9d
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65718549"
---
# <a name="integration-services-ssis-scale-out-master"></a>Integration Services(SSIS) 규모 확장 마스터

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Scale Out 마스터는 SSISDB 카탈로그 및 Scale Out 마스터 서비스를 통해 Scale Out 시스템을 관리합니다. 

SSISDB 카탈로그는 Scale Out 작업자, 패키지 및 실행에 대한 모든 정보를 저장합니다. 이 카탈로그는 규모 확장 작업자를 사용하고 규모 확장에서 패키지를 실행할 수 있는 인터페이스를 제공합니다. 자세한 내용은 [연습: Integration Services Scale Out 설치](walkthrough-set-up-integration-services-scale-out.md) 및 [Integration Services에서 패키지 실행](run-packages-in-integration-services-ssis-scale-out.md)을 참조하세요.

Scale Out 마스터 서비스는 Scale Out 작업자와의 통신을 담당하는 Windows 서비스입니다. HTTPS 통해 Scale Out 작업자의 패키지 실행 상태를 반환하며 SSISDB의 데이터에서 작동합니다. 

## <a name="scale-out-views-and-stored-procedures-in-ssisdb"></a>SSISDB의 Scale Out 보기 및 저장 프로시저

### <a name="views"></a>뷰

- [[catalog].[master_properties]](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)
- [[catalog].[worker_agents]](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)

### <a name="stored-procedures"></a>저장 프로시저

- Scale Out 작업자 관리:
    - [[catalog].[disable_worker_agent]](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)
    - [[catalog].[enable_worker_agent]](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)

- Scale Out에서 패키지 실행:
    - [[catalog].[create_execution]](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)
    - [[catalog].[add_execution_worker]](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)
    - [[catalog].[start_execution]](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)

## <a name="configure-the-scale-out-master-service"></a>Scale Out 마스터 서비스 구성

Scale Out 마스터 서비스는 `<drive>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config` 파일을 사용하여 구성합니다. 구성 파일을 업데이트한 후에는 서비스를 다시 시작해야 합니다.


|Configuration  |설명  |기본값  |
|---------|---------|---------|
|PortNumber|규모 확장 작업자와 통신하는 데 사용되는 네트워크 포트 번호입니다.|8391|
|SSLCertThumbprint|규모 확장 작업자와의 통신을 보호하는 데 사용되는 SSL 인증서의 지문입니다.|규모 확장 마스터 설치 중에 지정된 SSL 인증서의 지문|
|SqlServerName|SSISDB 카탈로그를 포함하는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]의 이름입니다. 예: ServerName\\InstanceName.|Scale Out 마스터와 함께 설치되는 SQL Server의 이름입니다.|
|CleanupCompletedJobsIntervalInMs|완료된 실행 작업을 정리하는 간격(밀리초)입니다.|43200000|
|DealWithExpiredTasksIntervalInMs|만료된 시행 작업을 처리하는 간격(밀리초)입니다.|300000|
|MasterHeartbeatIntervalInMs|규모 확장 마스터 하트비트의 간격(밀리초)입니다. 이 속성은 Scale Out 마스터가 SSISDB 카탈로그에서 온라인 상태를 업데이트하는 간격을 지정합니다.|30000|
|SqlConnectionTimeoutInSecs|SSISDB에 연결할 때 SQL 연결 시간 제한(초 단위)입니다.|15|
||||    

## <a name="view-the-scale-out-master-service-log"></a>Scale Out 마스터 서비스 로그 보기

Scale Out 마스터 서비스 로그 파일은 `<drive>:\Users\[account]\AppData\Local\SSIS\ScaleOut\Master` 폴더에 있습니다. 

*[account]* 매개 변수는 Scale Out 마스터 서비스를 실행하는 계정을 나타냅니다. 기본적으로 이 계정은 `SSISScaleOutMaster140`입니다.

## <a name="next-steps"></a>다음 단계

[Integration Services(SSIS) Scale Out 작업자](integration-services-ssis-scale-out-worker.md)
