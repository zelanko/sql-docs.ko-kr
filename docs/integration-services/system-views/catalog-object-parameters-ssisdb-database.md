---
title: "catalog.object_parameters (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: d7b04903-2d61-4159-9456-475942d1f732
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9d538e5b55ef4e8880afb2d008b11c17d9a03189
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogobjectparameters-ssisdb-database"></a>catalog.object_parameters(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 모든 패키지 및 프로젝트의 매개 변수를 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|parameter_id|**bigint**|매개 변수의 고유 식별자(ID)입니다.|  
|project_id|**bigint**|프로젝트의 고유 ID입니다.|  
|object_type|**smallint**|매개 변수의 유형입니다. 값은 프로젝트 매개 변수의 경우 `20`이고, 패키지 매개 변수의 경우 `30`입니다.|  
|object_name|**sysname**|해당 프로젝트 또는 패키지의 이름입니다.|  
|parameter_name|**sysname(nvarchar(128))**|매개 변수의 이름입니다.|  
|data_type|**nvarchar (128)**|매개 변수의 데이터 형식입니다.|  
|required|**bit**|값이 `1`이면 실행을 시작하는 데 매개 변수 값이 필요하고, 값이 `0`이면 실행을 시작하는 데 매개 변수 값이 필요하지 않습니다.|  
|sensitive|**bit**|값이 `1`이면 매개 변수 값이 중요하고, 값이 `0`이면 매개 변수 값이 중요하지 않습니다.|  
|description|**nvarchar (1024)**|패키지에 대한 설명(옵션)입니다.|  
|design_default_value|**sql_variant**|프로젝트 또는 패키지 디자인 중에 할당된 매개 변수의 기본값입니다.|  
|default_value|**sql_variant**|서버에서 현재 사용되는 기본값입니다.|  
|value_type|**char(1)**|매개 변수 값의 유형을 나타냅니다. 이 필드는 표시 `V` parameter_value 리터럴 값인 경우 및 `R` 때 값이 환경 변수를 참조 하 여 할당 됩니다.|  
|value_set|**bit**|값이 `1`이면 매개 변수 값이 할당되었고, 값이 `0`이면 매개 변수 값이 할당되지 않았습니다.|  
|referenced_variable_name|**nvarchar (128)**|매개 변수 값에 할당된 환경 변수의 이름입니다. 기본값은 **NULL**합니다.|  
|validation_status|**char(1)**|정보를 제공하기 위해서만 확인됩니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 사용되지 않습니다.|  
|last_validation_time|**(7)**|정보를 제공하기 위해서만 확인됩니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 사용되지 않습니다.|  
  
## <a name="permissions"></a>Permissions  
 이 뷰의 행을 보려면 다음 권한 중 하나가 있어야 합니다.  
  
-   프로젝트에 대한 READ 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격이 **sysadmin** 서버 역할입니다.  
  
 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  

