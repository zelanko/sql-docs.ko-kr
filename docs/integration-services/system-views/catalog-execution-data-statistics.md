---
description: catalog.execution_data_statistics
title: catalog.execution_data_statistics | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 6f51407e-0e4e-4b44-af33-db14c9d40ded
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 24452ceffc1660e57b087395ded3923e47802314
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495226"
---
# <a name="catalogexecution_data_statistics"></a>catalog.execution_data_statistics 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 뷰는 지정된 패키지 실행에 대해 데이터 흐름 구성 요소가 다운스트림 구성 요소에 데이터를 전송할 때마다 행을 표시합니다. 이 뷰의 정보를 사용하여 구성 요소에 대한 데이터 처리량을 계산할 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|data_stats_id|**bigint**|데이터의 고유 ID(식별자)입니다.|  
|execution_id|**bigint**|실행 인스턴스의 고유 ID입니다.|  
|package_name|**nvarchar(260)**|실행 중에 시작된 첫 번째 패키지의 이름입니다.|  
|task_name|**nvarchar(4000)**|데이터 흐름 태스크의 이름입니다.|  
|dataflow_path_id_string|**nvarchar(4000)**|데이터 흐름 경로의 ID 문자열입니다.|  
|dataflow_path_name|**nvarchar(4000)**|데이터 흐름 경로의 이름입니다.|  
|source_component_name|**nvarchar(4000)**|데이터에 전송된 데이터 흐름 구성 요소의 이름입니다.|  
|destination_component_name|**nvarchar(4000)**|데이터를 수신한 데이터 흐름 구성 요소의 이름입니다.|  
|rows_sent|**bigint**|원본 구성 요소에서 전송된 행의 수입니다.|  
|created_time|**datatimeoffset(7)**|값을 가져온 시간입니다.|  
|execution_path|**nvarchar(max)**|구성 요소의 실행 경로입니다.|  
  
## <a name="remarks"></a>설명  
  
-   구성 요소의 출력이 여러 개인 경우 각 출력에 해당하는 행이 추가됩니다.  
  
-   기본적으로 실행이 시작되면 전송되는 행의 수에 대한 정보는 기록되지 않습니다.  
  
-   지정된 패키지 실행에 대해 이 데이터를 보려면 로깅 수준을 **Verbose**로 설정합니다. 자세한 내용은 [SSIS 서버에서 패키지 실행에 대한 로깅 설정](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
> [!NOTE]  
>  서버에서 작업을 수행할 권한이 있으면 작업에 대한 정보를 볼 수 있는 권한도 있습니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  
