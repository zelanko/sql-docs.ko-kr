---
description: catalog.projects(SSISDB 데이터베이스)
title: catalog.projects(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a6b595e1-5227-47ce-8ee2-a28c1e1d5645
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 874d4a89af11ab022ce2714334b9aefb506de1a6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421997"
---
# <a name="catalogprojects-ssisdb-database"></a>catalog.projects(SSISDB 데이터베이스)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **SSISDB** 카탈로그에 표시된 모든 프로젝트에 대한 자세한 정보를 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|project_id|**bigint**|프로젝트의 고유 식별자(ID)입니다.|  
|folder_id|**bigint**|프로젝트가 있는 폴더의 고유 ID입니다.|  
|name|**sysname**|프로젝트의 이름입니다.|  
|description|**nvarchar(1024)**|프로젝트에 대한 설명(옵션)입니다.|  
|project_format_version|**int**|프로젝트를 개발하는 데 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전입니다.|  
|deployed_by_sid|**varbinary(85)**|프로젝트를 설치한 사용자의 보안 식별자(SID)입니다.|  
|deployed_by_name|**nvarchar(128)**|프로젝트를 설치한 사용자의 이름입니다.|  
|last_deployed_time|**datetimeoffset(7)**|프로젝트를 마지막으로 배포하거나 다시 배포한 날짜 및 시간입니다.|  
|created_time|**datetimeoffset(7)**|프로젝트가 생성된 날짜 및 시간입니다.|  
|object_version_lsn|**bigint**|프로젝트의 버전입니다. 이 번호는 순차적이지 않을 수 있습니다.|  
|validation_status|**char(1)**|유효성 검사 상태입니다.|  
|last_validation_time|**datetimeoffset(7)**|마지막 유효성 검사 시간입니다.|  
  
## <a name="remarks"></a>설명  
 이 뷰는 카탈로그에 있는 각 프로젝트에 대한 행을 표시합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
> [!NOTE]  
>  프로젝트에 대한 READ 권한이 있으면 해당 프로젝트와 연결된 모든 패키지 및 환경 참조에 대해서도 READ 권한을 가집니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  
