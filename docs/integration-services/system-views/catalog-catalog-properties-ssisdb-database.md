---
title: catalog.catalog_properties(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 12/11/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: e604a382-95c8-4764-b268-742eb5c6d4cf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9b5f7628f0284cb4662f0cf88bff1fd80cb2014e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295226"
---
# <a name="catalogcatalog_properties-ssisdb-database"></a>catalog.catalog_properties(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 속성을 표시합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|카탈로그 속성의 이름입니다.|  
|property_value|**nvarchar(256)**|카탈로그 속성 값입니다.|  
  
## <a name="remarks"></a>Remarks  
 이 뷰는 각 카탈로그 속성에 대한 행을 표시합니다.
  
|속성 이름|설명|  
|-------------------|-----------------|  
|**DEFAULT_EXECUTION_MODE**|패키지에 대한 서버 차원의 기본 실행 모드 – `Server`(0) 또는 `Scale Out`(1). |
|**ENCRYPTION_ALGORITHM**|중요한 데이터를 암호화하는 데 사용되는 암호화 알고리즘의 유형입니다. 지원되는 값은 `DES`, `TRIPLE_DES`, `TRIPLE_DES_3KEY`, `DESX`, `AES_128`, `AES_192` 및 `AES_256`입니다. 참고: 이 속성을 변경하려면 단일 사용자 모드에서 카탈로그 데이터베이스를 실행해야 합니다.|
|**IS_SCALEOUT_ENABLED**|값이 `True`이면 SSIS Scale Out 기능을 사용하도록 설정됩니다. Scale Out을 사용하도록 설정하지 않은 경우 이 속성은 보기에 나타나지 않을 수 있습니다.|
|**MAX_PROJECT_VERSIONS**|단일 프로젝트에 대해 유지되는 새 프로젝트 버전 수입니다. 버전 정리가 설정된 경우 이 개수를 초과하는 이전 버전은 모두 삭제됩니다.|  
|**OPERATION_CLEANUP_ENABLED**|값이 `TRUE`이면 **RETENTION_WINDOW**(일)보다 오래된 작업 정보 및 작업 메시지가 카탈로그에서 삭제되고, 값이 `FALSE`이면 모든 작업 정보 및 작업 메시지가 카탈로그에 저장됩니다. 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업은 작업 정리를 수행합니다.|  
|**RETENTION_WINDOW**|작업 정보 및 작업 메시지가 카탈로그에 저장되는 일 수 입니다. 값이 `-1`이면 보관 기간이 무한합니다. 참고: 정리를 실행하지 않으려면 **OPERATION_CLEANUP_ENABLED**를 **FALSE**로 설정합니다.|
|**SCHEMA_BUILD**|SSISDB 카탈로그 데이터베이스 스키마의 빌드 번호입니다. 이 숫자는 SSISDB 카탈로그를 만들거나 업그레이드할 때마다 변경됩니다.|
|**SCHEMA_VERSION**|SSISDB 카탈로그 데이터베이스 스키마의 주 버전 번호입니다. 이 숫자는 SSISDB 카탈로그를 만들거나 주 버전을 업그레이드 할 때마다 변경됩니다.|
|**VALIDATION_TIMEOUT**|이 속성에 지정된 시간(초) 내에 완료되지 않은 유효성 검사는 중지됩니다.|  
|**SERVER_CUSTOMIZED_LOGGING_LEVEL**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 대한 기본 사용자 지정된 로깅 수준입니다. 사용자 지정된 로깅 수준을 만들지 않은 경우 이 속성은 보기에 나타나지 않을 수 있습니다.|
|**SERVER_LOGGING_LEVEL**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 대한 기본 로깅 수준입니다.|
|**SERVER_OPERATION_ENCRYPTION_LEVEL**|값이 1(`PER_EXECUTION`)인 경우, 중요한 실행 매개 변수 및 실행 로그를 보호하는 데 사용되는 인증서 및 대칭 키가 각 *실행*에 대해 만들어집니다. 값이 2(`PER_PROJECT`)이 경우, 각 *프로젝트*에 대해 인증서 및 대칭 키가 한 번 만들어집니다. 이 속성에 대한 자세한 내용은 SSIS 저장 프로시저 [catalog.cleanup_server_log](../system-stored-procedures/catalog-cleanup-server-log.md#remarks)에 대한 주의를 참조하세요.|
|**VERSION_CLEANUP_ENABLED**|값이 `TRUE`이면 **MAX_PROJECT_VERSIONS**에 해당하는 개수의 프로젝트 버전만 카탈로그에 저장되고 다른 모든 프로젝트 버전은 삭제됩니다. 값이 **FALSE**이면 모든 프로젝트 버전이 카탈로그에 저장됩니다. 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업은 작업 정리를 수행합니다.|
|||
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
  
