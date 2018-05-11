---
title: catalog.revoke_permission(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- revoke_permission stored procedure [Integration Services]
- catalog.revoke_permission stored procedure [Integration Services]
ms.assetid: 850b9c26-5c7c-47b9-a61c-5cf9bb5948cf
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4a9f75b9f3fa96590410754a536d05d702b1832e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="catalogrevokepermission-ssisdb-database"></a>catalog.revoke_permission(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 보안 개체에 대한 사용 권한을 취소합니다.  
  
## <a name="syntax"></a>구문  
  
```sql
catalog.revoke_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>인수  
 [ @object_type = ] *object_type*  
 보안 개체의 유형입니다. 보안 개체 유형에는 폴더(`1`), 프로젝트(`2`), 환경(`3`) 및 작업(`4`)이 있습니다. *object_type*은 **smallint**** 입니다.  
  
 [ @object_id = ] *object_id*  
 보안 개체의 고유 식별자(ID)입니다. *object_id*는 **bigint**입니다.  
  
 [ @principal_id = ] *principal_id*  
 사용 권한을 취소할 보안 주체의 ID입니다. *principal_id*는 **int**입니다.  
  
 [ @permission_type = ] *permission_type*  
 사용 권한의 유형입니다. *permission_type*은 **smallint**입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공)  
  
 1(object_class가 유효하지 않습니다.)  
  
 2(object_id가 없습니다.)  
  
 3(보안 주체가 없습니다.)  
  
 4(권한이 잘못되었습니다.)  
  
 5(기타 오류)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>Remarks  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   개체에 대한 ASSIGN_PERMISSIONS 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="remarks"></a>Remarks  
 permission_type을 지정한 경우 저장 프로시저는 개체의 보안 주체에 명시적으로 할당된 사용 권한을 제거합니다. 해당 인스턴스가 없는 경우에도 프로시저에서 성공 코드 값(`0`)을 반환합니다. permission_type을 생략한 경우에는 저장 프로시저에서 개체의 보안 주체에 대한 모든 사용 권한을 제거합니다.  
  
> [!NOTE]  
>  보안 주체가 지정된 사용 권한이 있는 역할의 멤버인 경우에는 개체에 대한 지정된 사용 권한을 계속 유지할 수도 있습니다.  
  
 이 저장 프로시저를 통해 다음 표에 설명된 사용 권한 유형을 취소할 수 있습니다.  
  
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
  
  
