---
title: "catalog.clear_object_parameter_value (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: dcbbb714-a051-4805-9e2b-2c2fb647c890
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5d0d89081a31341a8d813d9985940c0e3ce0160a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogclearobjectparametervalue-ssisdb-database"></a>catalog.clear_object_parameter_value(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
 [ @folder_name =] *folder_name*  
 프로젝트가 있는 폴더의 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
 [ @project_name =] *project_name*  
 프로젝트의 이름입니다. *project_name* 은 **nvarchar (128)**합니다.  
  
 [ @object_type =] *object_type*  
 개체의 유형입니다. 유효한 값은 프로젝트의 경우 `20`이고, 패키지의 경우 `30`입니다. *object_type* 은 **smallInt**합니다.  
  
 [개체 _name @ =] *_name 개체*  
 패키지의 이름입니다. *_name 개체* 은 **nvarchar (260)**합니다.  
  
 [ @parameter_ 이름 =] *p a r a*  
 매개 변수의 이름입니다. *parameter_ 이름* 은 **nvarchar (128)**합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 및 MODIFY 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 clear_object_parameter 저장 프로시저에서 오류가 발생 하는 몇 가지 조건을 설명 합니다.  
  
-   잘못된 개체 유형을 지정하거나 프로젝트에서 개체 이름을 찾을 수 없는 경우  
  
-   프로젝트가 없거나, 프로젝트에 액세스할 수 없거나, 프로젝트 이름이 잘못된 경우  
  
-   잘못된 매개 변수 이름을 지정한 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
  

