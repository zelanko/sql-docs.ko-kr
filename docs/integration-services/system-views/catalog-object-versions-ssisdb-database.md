---
title: catalog.object_versions(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 2fd8c020-1c77-4702-8e6b-efa6a348daab
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7dac194c0ceb54eeb716b9cf5ec676e7fe120d8f
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296512"
---
# <a name="catalogobject_versions-ssisdb-database"></a>catalog.object_versions(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 개체의 버전을 표시합니다. 이 릴리스에서는 프로젝트 버전만 이 뷰에서 지원됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|object_version_lsn|**bigint**|개체 버전의 고유 식별자(ID)입니다. 이 번호는 순차적이지 않을 수 있습니다.|  
|object_id|**bigint**|개체의 고유 ID입니다.|  
|object_type|**smallint**|개체의 유형입니다. 프로젝트의 경우 값 `20`이 표시됩니다.|  
|object_name|**sysname(nvarchar(128))**|개체 이름입니다.|  
|description|**nvarchar(1024)**|프로젝트에 대한 설명입니다.|  
|created_by|**nvarchar(128)**|카탈로그에 개체를 추가한 사용자의 이름입니다.|  
|created_time|**datetimeoffset**|개체가 카탈로그에 추가된 날짜 및 시간입니다.|  
|restored_by|**nvarchar(128)**|개체를 복원한 사용자의 이름입니다.|  
|last_restored_time|**datetimeoffset**|개체가 마지막으로 복원된 날짜 및 시간입니다.|  
  
## <a name="remarks"></a>Remarks  
 이 뷰는 카탈로그에 있는 개체의 각 버전에 대한 행을 표시합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 뷰의 행을 보려면 다음 권한 중 하나가 있어야 합니다.  
  
-   개체에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할의 멤버 자격  
  
> [!NOTE]  
>  행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  
