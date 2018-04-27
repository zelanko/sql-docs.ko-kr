---
title: catalog.set_object_parameter_value(SSISDB 데이터베이스) | Microsoft Docs
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
ms.assetid: fb887543-f92f-404d-9495-a1dd23a6716e
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: de4f863322b805d8a2dfc0e6f21cae8378095e93
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="catalogsetobjectparametervalue-ssisdb-database"></a>catalog.set_object_parameter_value(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 매개 변수 값을 설정합니다. 이 값을 환경 변수에 연결하거나, 할당된 다른 값이 없는 경우 기본적으로 사용되는 리터럴 값을 할당합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.set_object_parameter_value [@object_type =] object_type   
    , [@folder_name =] folder_name   
    , [@project_name =] project_name   
    , [@parameter_name =] parameter _name   
    , [@parameter_value =] parameter_value   
 [  , [@object_name =] object_name ]  
 [  , [@value_type =] value_type ]  
```  
  
## <a name="arguments"></a>인수  
 [@object_type =] *object_type*  
 매개 변수의 유형입니다. 프로젝트 매개 변수를 나타내려면 값 `20`을 사용하고, 패키지 매개 변수를 나타내려면 값 `30`을 사용합니다. *object_type*은 **smallInt**입니다.  
  
 [@folder_name =] *folder_name*  
 매개 변수가 있는 폴더의 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [@project_name =] *project_name*  
 매개 변수가 포함된 프로젝트의 이름입니다. *project_name*은 **nvarchar(128)** 입니다.  
  
 [@parameter_name =] *parameter_name*  
 매개 변수의 이름입니다. *parameter_name*은 **nvarchar(128)** 입니다.  
  
 [@parameter_value =] *parameter_value*  
 매개 변수의 값입니다. *parameter_value*는 **sql_variant**입니다.  
  
 [@object_name =] *object_name*  
 패키지의 이름입니다. 이 인수는 매개 변수가 패키지 매개 변수인 경우에 필요합니다. *object_name*은 **nvarchar(260)** 입니다.  
  
 [@value_type =] *value_type*  
 매개 변수 값의 유형입니다. *parameter_value*가 실행 전에 할당된 다른 값이 없어 기본적으로 사용되는 리터럴 값임을 나타내려면 `V` 문자를 사용하고, *parameter_value*가 환경 변수 이름으로 설정된 참조 값임을 나타내려면 `R` 문자를 사용합니다. 이 인수는 선택 사항이며, 기본적으로 `V` 문자가 사용됩니다. *value_type*은 **char(1)** 입니다.  
  
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
 다음 목록에서는 이 저장 프로시저에서 오류가 발생하는 몇 가지 조건을 설명합니다.  
  
-   매개 변수 유형이 잘못된 경우  
  
-   프로젝트 이름이 잘못된 경우  
  
-   패키지 매개 변수의 경우 패키지 이름이 잘못된 경우  
  
-   값 유형이 잘못된 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
## <a name="remarks"></a>Remarks  
  
-   *value_type*이 지정되지 않으면 *parameter_value*에 대한 리터럴 값이 기본적으로 사용됩니다. 리터럴 값이 사용되는 경우 [object_parameters](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) 뷰의 *value_set*가 `1`로 설정됩니다. NULL 매개 변수 값은 허용되지 않습니다.  
  
-   *value_type*에 참조된 값임을 나타내는 `R` 문자가 포함된 경우 *parameter_value*는 환경 변수 이름을 참조합니다.  
  
-   값 `20`은 *object_type*이 프로젝트 매개 변수임을 나타내는 데 사용될 수 있습니다. 이 경우 *object_name* 값은 필요하지 않으므로 *object_name*에 대해 지정된 모든 값을 무시합니다. 이 값은 사용자가 프로젝트 매개 변수를 설정하려는 경우에 사용됩니다.  
  
-   값 `30`은 *object_type*이 패키지 매개 변수임을 나타내는 데 사용될 수 있습니다. 이 경우 *object_name* 값은 해당 패키지를 나타내는 데 사용됩니다. *object_name*을 지정하지 않으면 저장 프로시저가 오류를 반환하고 종료됩니다.  
  
  
