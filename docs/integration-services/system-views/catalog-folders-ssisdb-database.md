---
title: catalog.folders(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 21a37c16-60aa-4b3f-8bca-ac90ad1697ac
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 98238937164a1b09a9389d22717541f25393d000
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65714804"
---
# <a name="catalogfolders-ssisdb-database"></a>catalog.folders(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 폴더를 표시합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|id|**bigint**|폴더의 고유 식별자입니다.|  
|NAME|**sysname(nvarchar(128))**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그 내에서 고유한 폴더의 이름입니다.|  
|description|**nvarchar(1024)**|폴더에 대한 설명입니다.|  
|created_by_sid|**varbinary(85)**|폴더를 만든 사용자의 보안 식별자(SID)입니다.|  
|created_by_name|**nvarchar(128)**|폴더를 만든 사용자의 이름입니다.|  
|created_time|**datetimeoffset(7)**|폴더를 만든 날짜 및 시간입니다.|  
  
## <a name="remarks"></a>Remarks  
 이 뷰는 카탈로그에 있는 각 폴더에 대한 행을 표시합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   폴더에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
> [!NOTE]  
>  서버에서 작업을 수행할 권한이 있으면 작업에 대한 정보를 볼 수 있는 권한도 있습니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  
