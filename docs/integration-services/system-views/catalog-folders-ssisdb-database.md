---
title: "catalog.folders (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 21a37c16-60aa-4b3f-8bca-ac90ad1697ac
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9622bd1a5f1415c9f506a00a63441081154b53ff
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogfolders-ssisdb-database"></a>catalog.folders(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 폴더를 표시합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|id|**bigint**|폴더의 고유 식별자입니다.|  
|name|**sysname(nvarchar(128)**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그 내에서 고유한 폴더의 이름입니다.|  
|description|**nvarchar (1024)**|폴더에 대한 설명입니다.|  
|created_by_sid|**varbinary(85)**|폴더를 만든 사용자의 보안 식별자(SID)입니다.|  
|created_by_name|**nvarchar (128)**|폴더를 만든 사용자의 이름입니다.|  
|created_time|**(7)**|폴더를 만든 날짜 및 시간입니다.|  
  
## <a name="remarks"></a>주의  
 이 뷰는 카탈로그에 있는 각 폴더에 대한 행을 표시합니다.  
  
## <a name="permissions"></a>Permissions  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   폴더에 대한 READ 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
> [!NOTE]  
>  서버에서 작업을 수행할 권한이 있으면 작업에 대한 정보를 볼 수 있는 권한도 있습니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  

