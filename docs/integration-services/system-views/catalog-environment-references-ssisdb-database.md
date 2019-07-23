---
title: catalog.environment_references(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: efec53ef-3e5a-4b76-b71d-a0cf9e11ac00
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c70439da5ba3f09cd39ea9cec78a14ea366d126d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038414"
---
# <a name="catalogenvironmentreferences-ssisdb-database"></a>catalog.environment_references(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **SSISDB** 카탈로그에 있는 모든 프로젝트의 환경 참조를 표시합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|reference_id|**bigint**|참조의 고유 식별자(ID)입니다.|  
|project_id|**bigint**|프로젝트의 고유 ID입니다.|  
|reference_type|**char(1)**|환경을 프로젝트와 같은 폴더(상대 참조)에서 찾을 수 있는지, 아니면 다른 폴더(절대 참조)에서 찾을 수 있는지를 나타냅니다. 값이 `R`이면 상대 참조를 사용하여 환경을 찾고, 값이 `A`이면 절대 참조를 사용하여 환경을 찾습니다.|  
|environment_folder_name|**sysname**|절대 참조를 사용하여 환경을 찾는 경우 폴더의 이름입니다.|  
|environment_name|**sysname**|프로젝에서 참조하는 환경의 이름입니다.|  
|validation_status|**char(1)**|유효성 검사의 상태입니다.|  
|last_validation_time|**datatimeoffset(7)**|마지막 유효성 검사 시간입니다.|  
  
## <a name="remarks"></a>Remarks  
 이 뷰는 카탈로그에 있는 각 환경 참조에 대한 행을 표시합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   해당 프로젝트에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
> [!NOTE]  
>  프로젝트에 대한 READ 권한이 있으면 해당 프로젝트와 연결된 모든 패키지 및 환경 참조에 대해서도 READ 권한을 가집니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
## <a name="remarks"></a>Remarks  
 프로젝트에는 상대 환경 참조 또는 절대 환경 참조가 있을 수 있습니다. 상대 참조는 환경을 이름으로 참조하며 환경이 프로젝트와 같은 폴더에 있어야 합니다. 절대 참조는 환경을 이름과 폴더로 참조하며 프로젝트와 다른 폴더에 있는 환경을 참조할 수도 있습니다. 하나의 프로젝트에서 여러 환경을 참조할 수 있습니다.  
  
  
