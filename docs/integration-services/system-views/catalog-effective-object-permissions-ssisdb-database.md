---
title: catalog.effective_object_permissions(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- catalog.effective_object_permissions views [Integration Services]
- effective_object_permissions view [Integration Services]
ms.assetid: e70c4ce9-79f5-44df-ac75-6c29b6e38776
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7e3cca42b69d32b324c0ddb749a5fb4ef8550c13
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58272317"
---
# <a name="catalogeffectiveobjectpermissions-ssisdb-database"></a>catalog.effective_object_permissions(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 모든 개체의 현재 보안 주체에 대한 유효 사용 권한을 표시합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|보안 개체의 유형입니다. 보안 개체 유형에는 폴더(`1`), 프로젝트(`2`), 환경(`3`) 및 작업(`4`)이 있습니다.|  
|object_id|**bigint**|개체의 고유 식별자(ID) 또는 기본 키입니다.|  
|permission_type|**smallint**|사용 권한의 유형입니다.|  
  
## <a name="remarks"></a>Remarks  
 이 뷰는 다음 표에 나열된 사용 권한 유형을 표시합니다.  
  
|permission_type 값|사용 권한 이름|사용 권한 설명|적용할 수 있는 개체 유형|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|보안 주체가 개체의 일부로 간주되는 정보(예: 속성)를 읽을 수 있습니다. 개체 내에 포함된 다른 개체의 내용을 열거하거나 읽을 수는 없습니다.|폴더, 프로젝트, 환경, 작업|  
|`2`|MODIFY|보안 주체가 개체의 일부로 간주되는 정보(예: 속성)를 수정할 수 있습니다. 개체 내에 포함된 다른 개체를 수정할 수는 없습니다.|폴더, 프로젝트, 환경, 작업|  
|`3`|CREATE 문을 실행하기 전에|보안 주체가 프로젝트의 모든 패키지를 실행할 수 있습니다.|프로젝트|  
|`4`|MANAGE_PERMISSIONS|보안 주체가 개체에 사용 권한을 할당할 수 있습니다.|폴더, 프로젝트, 환경, 작업|  
|`100`|CREATE_OBJECTS|보안 주체가 폴더에 개체를 만들 수 있습니다.|Folder|  
|`101`|READ_OBJECTS|보안 주체가 폴더의 모든 개체를 읽을 수 있습니다.|Folder|  
|`102`|MODIFY_OBJECTS|보안 주체가 폴더의 모든 개체를 수정할 수 있습니다.|Folder|  
|`103`|EXECUTE_OBJECTS|보안 주체가 폴더의 모든 프로젝트에 있는 모든 패키지를 실행할 수 있습니다.|Folder|  
|`104`|MANAGE_OBJECT_PERMISSIONS|보안 주체가 폴더의 모든 개체에 대한 사용 권한을 관리할 수 있습니다.|Folder|  
  
 호출자가 사용 권한을 가진 개체만 평가됩니다. 사용 권한은 다음을 기준으로 계산됩니다.  
  
-   명시적 사용 권한  
  
-   상속된 사용 권한  
  
-   역할에 속한 보안 주체의 멤버 자격  
  
-   그룹에 속한 보안 주체의 멤버 자격  
  
## <a name="permissions"></a>사용 권한  
 사용자는 자신이 속한 역할 및 자신에 대한 유효 사용 권한만 볼 수 있습니다.  
  
  
