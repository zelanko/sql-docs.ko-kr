---
title: "SQL Server Integration Services (SSIS) 확장 마스터 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1672c015186998065b5d6dc95897147aa11d14ec
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out-master"></a>Integration Services(SSIS) 규모 확장 마스터
규모 확장 마스터는 SSISDB 카탈로그 및 규모 확장 마스터 서비스를 통해 규모 확장 시스템을 관리합니다. 

SSISDB 카탈로그는 규모 확장 작업자, 패키지 및 실행에 대한 모든 정보를 저장합니다. 이 카탈로그는 규모 확장 작업자를 사용하고 규모 확장에서 패키지를 실행할 수 있는 인터페이스를 제공합니다. 자세한 내용은 [연습: Integration Services 규모 확장 설치](walkthrough-set-up-integration-services-scale-out.md), [Integration Services에서 패키지 실행](run-packages-in-integration-services-ssis-scale-out.md)을 참조하세요.

규모 확장 마스터 서비스는 규모 확장 작업자와의 통신을 담당하는 Windows 서비스입니다. 이 서비스는 HTTPS 통해 규모 확장 작업자와 패키지 실행의 상태를 교환하며 SSISDB의 데이터에서 작동합니다. 

## <a name="scale-out-related-sql-views-and-stored-procedures-in-ssisdb"></a>스케일 아웃 관련 SQL 뷰 및 SSISDB에 저장 프로시저

#### <a name="views"></a>보기:
[[catalog].[master_properties]](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md), [[catalog].[worker_agents]](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md).

#### <a name="stored-procedures"></a>저장 프로시저:

- 규모 확장 작업자 관리:  
 [[catalog].[disable_worker_agent]](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md), [[catalog].[enable_worker_agent]](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md).
- 규모 확장에서 패키지 실행:   
[[catalog].[create_execution]](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [[catalog].[add_execution_worker]](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md), [[catalog].[start_execution]](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).   

## <a name="configure-sql-server-integration-services-scale-out-master-service"></a>SQL Server Integration Services 규모 확장 마스터 서비스 구성
규모 확장 마스터 서비스는 \<드라이버\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config 파일을 사용하여 구성할 수 있습니다. 구성 파일을 업데이트한 후 서비스를 다시 시작해야 합니다.


Configuration  |Description  |기본값  
---------|---------|---------
PortNumber|규모 확장 작업자와 통신하는 데 사용되는 네트워크 포트 번호입니다.|8391         
SSLCertThumbprint|규모 확장 작업자와의 통신을 보호하는 데 사용되는 SSL 인증서의 지문입니다.|규모 확장 마스터 설치 중에 지정된 SSL 인증서의 지문         
SqlServerName|이름에서 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] SSISDB 카탈로그를 포함 하 합니다. 예를 들어 ServerName\\\\InstanceName입니다.|스케일 아웃 마스터와 함께 설치 되는 SQL Server의 이름입니다.         
CleanupCompletedJobsIntervalInMs|완료된 실행 작업을 정리하는 간격(밀리초)입니다.|43200000         
DealWithExpiredTasksIntervalInMs|만료된 시행 작업을 처리하는 간격(밀리초)입니다.|300000
MasterHeartbeatIntervalInMs|규모 확장 마스터 하트비트의 간격(밀리초)입니다. 규모 확장 마스터가 SSISDB 카탈로그에서 온라인 상태를 업데이트하는 간격을 지정합니다.|30000
SqlConnectionTimeoutInSecs|SQL 연결 제한 시간 (초)에서 SSISDB에 연결할 때.|15        

## <a name="view-scale-out-master-service-log"></a>규모 확장 마스터 서비스 로그 보기
스케일 아웃 마스터 서비스 로그 파일에는 \<드라이버\>: \Users\\*[계정]*\AppData\Local\SSIS\ScaleOut\Master 폴더 경로입니다. 

*[계정]* 스케일 아웃 마스터 서비스 실행 계정을 참조 합니다. 기본적으로 이 계정은 SSISScaleOutMaster140입니다.

