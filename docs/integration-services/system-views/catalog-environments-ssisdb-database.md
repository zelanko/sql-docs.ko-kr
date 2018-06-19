---
title: catalog.environments(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 7014c0e3-65dc-4a46-842e-4decf3737748
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 55122a93fe990445285ace9f7c73eac2109bdc9e
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35329887"
---
# <a name="catalogenvironments-ssisdb-database"></a>catalog.environments(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 모든 환경에 대한 자세한 정보를 표시합니다. 환경에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트에서 참조할 수 있는 변수가 포함됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|environment_id|**bigint**|환경의 고유 식별자(ID)입니다.|  
|NAME|**sysname**|환경의 이름입니다.|  
|folder_id|**bigint**|환경이 있는 폴더의 고유 ID입니다.|  
|description|**nvarchar(1024)**|환경에 대한 설명입니다. 이 값은 선택 사항입니다.|  
|created_by_sid|**varbinary(85)**|환경을 만든 사용자의 보안 식별자(SID)입니다.|  
|created_by_name|**nvarchar(128)**|환경을 만든 사용자의 이름입니다.|  
|created_time|**datetimeoffset**|환경을 만든 날짜 및 시간입니다.|  
  
## <a name="remarks"></a>Remarks  
 이 뷰는 카탈로그에 있는 각 환경에 대한 행을 표시합니다. 환경 이름은 해당 환경이 있는 폴더와 관련하여 고유해야 합니다. 예를 들어 `E1`이라는 환경은 카탈로그의 여러 폴더에 존재할 수 있지만 각 폴더에는 `E1`이라는 환경이 하나만 있어야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   환경에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
> [!NOTE]  
>  행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  
