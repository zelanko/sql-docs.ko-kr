---
title: "catalog.set_object_parameter_value (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: fb887543-f92f-404d-9495-a1dd23a6716e
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 3a5dc70b1e955b3c702dc9e9dbe4776cc4ebd5ac
ms.contentlocale: ko-kr
ms.lasthandoff: 10/20/2017

---
# <a name="catalogsetobjectparametervalue-ssisdb-database"></a>catalog.set_object_parameter_value(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 매개 변수 값을 설정합니다. 환경 변수에 값을 연결 하거나 다른 값이 할당 될 때 기본적으로 사용 되는 리터럴 값을 할당 합니다.  
  
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
 매개 변수의 유형입니다. 프로젝트 매개 변수를 나타내려면 값 `20`을 사용하고, 패키지 매개 변수를 나타내려면 값 `30`을 사용합니다. *object_type* 은 **smallInt**합니다.  
  
 [@folder_name =] *folder_name*  
 매개 변수가 있는 폴더의 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
 [@project_name =] *project_name*  
 매개 변수가 포함된 프로젝트의 이름입니다. *project_name* 은 **nvarchar (128)**합니다.  
  
 [@parameter_name =] *p a r a*  
 매개 변수의 이름입니다. *p a r a* 은 **nvarchar (128)**합니다.  
  
 [@parameter_value =] *parameter_value*  
 매개 변수의 값입니다. *parameter_value* 은 **sql_variant**합니다.  
  
 [@object_name =] *object_name*  
 패키지의 이름입니다. 이 인수는 매개 변수가 패키지 매개 변수인 경우에 필요합니다. *object_name* 은 **nvarchar (260)**합니다.  
  
 [@value_type =] *value_type*  
 매개 변수 값의 유형입니다. 문자를 사용 하 여 `V` 임을 나타내는 *parameter_value* 실행 전에 할당 된 다른 값이 없는 경우 기본적으로 사용 되는 리터럴 값입니다. 문자를 사용 하 여 `R` 임을 나타내는 *parameter_value* 참조 된 값 이며 환경 변수의 이름으로 설정 합니다. 이 인수는 선택 사항이며, 기본적으로 `V` 문자가 사용됩니다. *value_type* 은 **char(1)**합니다.  
  
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
 다음 목록에서는 이 저장 프로시저에서 오류가 발생하는 몇 가지 조건을 설명합니다.  
  
-   매개 변수 유형이 잘못된 경우  
  
-   프로젝트 이름이 잘못된 경우  
  
-   패키지 매개 변수의 경우 패키지 이름이 잘못된 경우  
  
-   값 유형이 잘못된 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
## <a name="remarks"></a>주의  
  
-   없는 경우 *value_type* 지정 된 변수의 리터럴 값 *parameter_value* 기본적으로 사용 됩니다. 리터럴 값을 사용할 경우의 *value_set* 에 [object_parameters](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) 뷰가로 설정 되어 `1`합니다. NULL 매개 변수 값은 허용되지 않습니다.  
  
-   경우 *value_type* 에 문자 `R`, 참조 하는 값을 나타냄 *parameter_value* 환경 변수의 이름을 나타냅니다.  
  
-   값 `20` 에 사용할 수 있습니다. *object_type* 프로젝트 매개 변수를 나타냅니다. 이 경우 값에 대 한 *object_name* 아니므로 필요한 경우 모든 값에 대해 지정 된 *object_name* 는 무시 됩니다. 이 값은 사용자가 프로젝트 매개 변수를 설정하려는 경우에 사용됩니다.  
  
-   값 `30` 에 사용할 수 있습니다. *object_type* 패키지 매개 변수를 나타냅니다. 이 경우 값에 대 한 *object_name* 해당 패키지를 나타내는 데 사용 됩니다. 경우 *object_name* 를 지정 하지 않으면 저장된 프로시저는 오류를 반환 하 고 종료 합니다.  
  
  

