---
title: catalog.execution_property_override_values | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 83cbdd6f-ddde-47bf-abde-36bd24272621
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 922d55e335c8310cec3cf4db8967cadc2affd1f3
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65714875"
---
# <a name="catalogexecutionpropertyoverridevalues"></a>catalog.execution_property_override_values 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  패키지 실행 중 설정된 속성 재정의 값을 표시합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|property_id|**bigint**|속성 재정의 값에 대한 고유 ID입니다.|  
|execution_id|**bigint**|실행 인스턴스의 고유 ID입니다.|  
|property_path|**nvarchar(4000)**|패키지의 속성에 대한 경로입니다.|  
|property_value|**nvarchar(max)**|속성의 재정의 값입니다.|  
|sensitive|**bit**|값이 1이면 속성이 중요하며 저장될 때 암호화됩니다. 값이 0이면 속성이 중요하지 않으며 값이 일반 텍스트로 저장됩니다.|  
  
## <a name="remarks"></a>Remarks  
 이 보기는 **패키지 실행** 대화 상자의 **고급** 탭에 있는 **속성 재정의** 섹션을 사용하여 속성 값이 재정의된 각 실행에 대한 행을 표시합니다. 속성에 대한 경로는 패키지 테스트의 **패키지 경로** 속성에서 파생됩니다.  
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
> [!NOTE]  
>  서버에서 작업을 수행할 권한이 있으면 작업에 대한 정보를 볼 수 있는 권한도 있습니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  
