---
title: "catalog.execution_parameter_values (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: ec93e67b-04ce-4aae-ab96-3ad20e9793ad
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 60907a82f3d0bb9f273355fd6bfbd7378ce72c9f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutionparametervalues-ssisdb-database"></a>catalog.execution_parameter_values(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  실행 인스턴스 중에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 사용한 실제 매개 변수 값을 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|execution_parameter_id|**bigint**|실행 매개 변수의 고유 식별자(ID)입니다.|  
|execution_id|**bigint**|실행 인스턴스의 고유 ID입니다.|  
|object_type|**smallint**|값이 `20`이면 이 매개 변수는 프로젝트 매개 변수입니다. 값이 `30`이면 이 매개 변수는 패키지 매개 변수입니다. 값이 `50`, 매개 변수는 다음 중 하나:<br /><br /> **LOGGING_LEVEL**<br /><br /> **DUMP_ON_ERROR**<br /><br /> **DUMP_ON_EVENT**<br /><br /> **DUMP_EVENT_CODE**<br /><br /> **CALLER_INFO**<br /><br /> **동기화**|  
|parameter_data_type|**nvarchar (128)**|매개 변수의 데이터 형식입니다.|  
|parameter_name|**sysname**|매개 변수의 이름입니다.|  
|parameter_value|**sql_variant**|매개 변수의 값입니다. 중요 한 경우는 `0`, 일반 텍스트 값이 표시 됩니다. 중요 한 경우는 `1`, **NULL** 값이 표시 됩니다.|  
|sensitive|**bit**|값이 `1`이면 매개 변수 값이 중요하고, 값이 `0`이면 매개 변수 값이 중요하지 않습니다.|  
|required|**bit**|값이 `1`이면 실행을 시작하는 데 매개 변수 값이 필요하고, 값이 `0`이면 실행을 시작하는 데 매개 변수 값이 필요하지 않습니다.|  
|value_set|**bit**|값이 `1`이면 매개 변수 값이 할당되었고, 값이 `0`이면 매개 변수 값이 할당되지 않았습니다.|  
|runtime_override|**bit**|값이 `1`이면 실행이 시작되기 전에 매개 변수 값이 원래 값에서 변경된 것이고, 값이 `0`이면 매개 변수 값이 원래 설정된 값입니다.|  
  
## <a name="remarks"></a>주의  
 이 뷰는 카탈로그의 각 실행 매개 변수에 대한 행을 표시합니다. 실행 매개 변수 값은 단일 실행 인스턴스 중에 프로젝트 매개 변수 또는 패키지 매개 변수에 할당되는 값입니다.  
  
## <a name="permissions"></a>Permissions  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
> [!NOTE]  
>  서버에서 작업을 수행할 권한이 있으면 작업에 대한 정보를 볼 수 있는 권한도 있습니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  
