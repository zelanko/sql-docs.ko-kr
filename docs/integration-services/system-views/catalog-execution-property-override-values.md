---
title: catalog.execution_property_override_values | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
ms.assetid: 83cbdd6f-ddde-47bf-abde-36bd24272621
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ed9ae4ea7a7165efe53a551832d8e4a0eb7a2114
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutionpropertyoverridevalues"></a>catalog.execution_property_override_values
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  패키지 실행 중 설정된 속성 재정의 값을 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|property_id|**bigint**|속성 재정의 값에 대한 고유 ID입니다.|  
|execution_id|**bigint**|실행 인스턴스의 고유 ID입니다.|  
|property_path|**nvarchar(4000)**|패키지의 속성에 대한 경로입니다.|  
|property_value|**nvarchar(max)**|속성의 재정의 값입니다.|  
|sensitive|**bit**|값이 1이면 속성이 중요하며 저장될 때 암호화됩니다. 값이 0이면 속성이 중요하지 않으며 값이 일반 텍스트로 저장됩니다.|  
  
## <a name="remarks"></a>주의  
 속성의 값이 재정의 된를 사용 하 여 각 실행에 대해 한 행을 표시 하는이 보기는 **속성 재정의** 섹션는 **고급** 탭은 **패키지 실행** 대화 상자입니다. 속성에 대 한 경로에서 파생 되는 **패키지 경로** 패키지 태스크의 속성입니다.  
  
## <a name="permissions"></a>Permissions  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
> [!NOTE]  
>  서버에서 작업을 수행할 권한이 있으면 작업에 대한 정보를 볼 수 있는 권한도 있습니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  

