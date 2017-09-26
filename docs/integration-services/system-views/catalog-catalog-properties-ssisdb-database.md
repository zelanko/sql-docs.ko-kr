---
title: "catalog.catalog_properties (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: e604a382-95c8-4764-b268-742eb5c6d4cf
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ca3d5da05126d5b71bf6d714f9e8449f9f5c8335
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcatalogproperties-ssisdb-database"></a>catalog.catalog_properties(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 속성을 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|카탈로그 속성의 이름입니다.|  
|property_value|**nvarchar(256)**|카탈로그 속성 값입니다.|  
  
## <a name="remarks"></a>주의  
 이 뷰는 각 카탈로그 속성에 대한 행을 표시합니다. 이 뷰에 표시되는 속성은 다음과 같습니다.  
  
|속성 이름|Description|  
|-------------------|-----------------|  
|**ENCRYPTION_ALGORITHM**|중요한 데이터를 암호화하는 데 사용되는 암호화 알고리즘의 유형입니다. 지원 되는 값: `DES`, `TRIPLE_DES`, `TRIPLE_DES_3KEY`, `DESX`, `AES_128`, `AES_192`, 및 `AES_256`합니다. 참고:이 속성을 변경 하려면 단일 사용자 모드에서 카탈로그 데이터베이스 여야 합니다.|  
|**MAX_PROJECT_VERSIONS**|단일 프로젝트에 대해 유지할 새 프로젝트 버전 수입니다. 버전 정리가 설정된 경우 이 개수를 초과하는 이전 버전은 모두 삭제됩니다.|  
|**OPERATION_CLEANUP_ENABLED**|값이 `TRUE`, 작업 정보와 작업 메시지가 보다 오래 된 **RETENTION_WINDOW** (일)는 카탈로그에서 삭제 됩니다. 값이 `FALSE`이면 모든 작업 정보 및 작업 메시지가 카탈로그에 저장됩니다. 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업은 작업 정리를 수행합니다.|  
|**RETENTION_WINDOW**|작업 정보 및 작업 메시지가 카탈로그에 저장되는 일 수 입니다. 값이 `-1`이면 보관 기간이 무한합니다. 참고: 정리 작업을 사용할 경우 설정 **OPERATION_CLEANUP_ENABLED** 를 **FALSE**합니다.|  
|**VALIDATION_TIMEOUT**|이 속성에 지정된 시간(초) 내에 완료되지 않은 유효성 검사는 중지됩니다.|  
|**VERSION_CLEANUP_ENABLED**|값이 `TRUE`만 **MAX_PROJECT_VERSIONS** 개수의 프로젝트 버전만 카탈로그에 저장 되 고 다른 모든 프로젝트 버전이 삭제 됩니다. 값이 **FALSE**, 모든 프로젝트 버전이 카탈로그에 저장 됩니다. 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업은 작업 정리를 수행합니다.|  
|**SERVER_LOGGING_LEVEL**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 대한 기본 로깅 수준입니다.|  
  
## <a name="permissions"></a>Permissions  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
  
