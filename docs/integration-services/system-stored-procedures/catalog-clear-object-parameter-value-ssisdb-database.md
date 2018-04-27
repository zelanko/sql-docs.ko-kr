---
title: catalog.clear_object_parameter_value(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: dcbbb714-a051-4805-9e2b-2c2fb647c890
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: de237191883d20411bbe446acb4395e5982d35dc
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="catalogclearobjectparametervalue-ssisdb-database"></a>catalog.clear_object_parameter_value(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  서버에 저장된 기존 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트 또는 패키지에 대한 매개 변수 값을 지웁니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.clear_object_parameter [ @folder_name = ] folder_name   
    , [ @project_name = ] project_name   
    , [ @object_type = ] object_type   
    , [ @object_name = ] object_name   
    , [ @parameter_ name = ] parameter_name  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 프로젝트가 있는 폴더의 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [ @project_name = ] *project_name*  
 프로젝트의 이름입니다. *project_name*은 **nvarchar(128)** 입니다.  
  
 [ @object_type = ] *object_type*  
 개체의 유형입니다. 유효한 값은 프로젝트의 경우 `20`이고, 패키지의 경우 `30`입니다. *object_type*은 **smallInt**입니다.  
  
 [ @ object _name = ] *object _name*  
 패키지의 이름입니다. *object _name*은 **nvarchar(260)** 입니다.  
  
 [ @parameter_ name = ] *parameter_name*  
 매개 변수의 이름입니다. *parameter_ name*은 **nvarchar(128)** 입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 및 MODIFY 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 clear_object_parameter 저장 프로시저에서 오류가 발생하는 몇 가지 조건을 설명합니다.  
  
-   잘못된 개체 유형을 지정하거나 프로젝트에서 개체 이름을 찾을 수 없는 경우  
  
-   프로젝트가 없거나, 프로젝트에 액세스할 수 없거나, 프로젝트 이름이 잘못된 경우  
  
-   잘못된 매개 변수 이름을 지정한 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
  
