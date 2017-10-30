---
title: "catalog.deny_permission (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: de310bac-2ddc-4ef9-8783-43dcb02a94f1
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 689a59e92286881fa3be7ee3754a786ccb54ae6c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdenypermission-ssisdb-database"></a>catalog.deny_permission(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 보안 개체에 대한 사용 권한을 거부합니다.  
  
## <a name="syntax"></a>구문  
  
```sql
catalog.deny_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>인수  
 [ @object_type =] *object_type*  
 보안 개체의 유형입니다. 보안 개체 유형에 폴더 (`1`), 프로젝트 (`2`), 환경 (`3`), 및 작업 (`4`). *object_type* 은 **smallint***합니다.*  
  
 [ @object_id =] *object_id*  
 보안 개체의 고유 식별자(ID) 또는 기본 키입니다. *object_id* 은 **bigint**합니다.  
  
 [ @principal_id =] *principal_id*  
 거부할 보안 주체의 ID입니다. *principal_id* 은 **int**합니다.  
  
 [ @permission_type =] *permission_type*  
 거부할 사용 권한의 유형입니다. *permission_type* 은 **smallint**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공)  
  
 1 (object_class 잘못 되었습니다.)  
  
 2 (object_id 존재 하지 않음)  
  
 3 (보안 주체가 존재 하지 않음)  
  
 4 (권한이 잘못 되었습니다.)  
  
 5(기타 오류)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   개체에 대한 MANAGE_PERMISSIONS 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="remarks"></a>주의  
 이 저장 프로시저를 통해 다음 표에 설명된 사용 권한 유형을 거부할 수 있습니다.  
  
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
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   Permission_type를 지정 하는 경우 프로시저는 명시적으로 지정된 된 개체에 대 한 지정된 된 보안 주체에 할당 된 지정된 된 사용을 거부 합니다. 해당 인스턴스가 없는 경우에도 프로시저에서 성공 코드 값(`0`)을 반환합니다.  
  
-   Permission_type를 생략 하면 프로시저는 지정된 된 개체에 지정된 된 보안 주체에 대 한 모든 권한을 거부 합니다.  
  
  

