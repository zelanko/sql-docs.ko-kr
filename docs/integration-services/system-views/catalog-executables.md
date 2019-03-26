---
title: catalog.executables | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: bae22d0c-e190-426f-a074-c1d1170e8dd8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a2f83708d8a384e6b010c816556bf3da187a5f86
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58281047"
---
# <a name="catalogexecutables"></a>catalog.executables
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 뷰는 지정된 실행 작업에서 각 실행에 대한 행을 표시합니다.  
  
 실행 개체는 사용자가 패키지의 제어 흐름에 추가하는 태스크 또는 컨테이너입니다.  
  
|열 이름|**Data type**|설명|  
|-----------------|-------------------|-----------------|  
|executable_id|**bigint**|해당 실행에 대한 고유 식별자입니다.|  
|execution_id|**bigint**|실행 인스턴스의 고유 식별자입니다.|  
|executable_name|**nvarchar(4000)**|실행의 이름입니다.|  
|executable_guid|**nvarchar(38)**|실행의 GUID입니다.|  
|package_name|**nvarchar(260)**|패키지의 이름입니다.|  
|package_path|**nvarchar(max)**|패키지의 경로입니다.|  
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
> [!NOTE]  
>  서버에서 작업을 수행할 권한이 있으면 작업에 대한 정보를 볼 수 있는 권한도 있습니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
## <a name="remarks"></a>Remarks  
  
