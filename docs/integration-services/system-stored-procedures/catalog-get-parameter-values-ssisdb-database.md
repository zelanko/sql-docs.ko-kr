---
title: catalog.get_parameter_values(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 5b1aeaf7-c938-4aef-bafc-e4d7a82eb578
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 391a47edc45145bac21ce351e36c613f2a76addd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65716104"
---
# <a name="cataloggetparametervalues-ssisdb-database"></a>catalog.get_parameter_values(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 프로젝트 및 해당 패키지에서 기본 매개 변수 값을 검색 및 확인합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.get_parameter_values [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @package_name = ] package_name  
  [  , [ @reference_id = ] reference_id  ]  
  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 프로젝트가 있는 폴더의 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [ @project_name = ] *project_name*  
 매개 변수가 있는 프로젝트의 이름입니다. *project_name*은 **nvarchar(128)** 입니다.  
  
 [ @package_name = ] *package_name*  
 패키지의 이름입니다. 패키지 이름을 지정하면 모든 프로젝트 매개 변수와 특정 패키지의 매개 변수를 검색할 수 있습니다. 모든 프로젝트 매개 변수와 모든 패키지의 매개 변수를 검색하려면 NULL을 사용합니다. *package_name*은 **nvarchar(260)** 입니다.  
  
 [ @reference_id = ] *reference_id*  
 환경 참조의 고유 식별자입니다. 이 매개 변수는 선택 사항입니다. *reference_id*는 **bigint**입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 다음 형식의 테이블을 반환합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|매개 변수의 유형입니다. 값은 프로젝트 매개 변수의 경우 `20`이고, 패키지 매개 변수의 경우 `30`입니다.|  
|parameter_data_type|**nvarchar(128)**|매개 변수의 데이터 형식입니다.|  
|parameter_name|**sysname**|매개 변수의 이름입니다.|  
|parameter_value|**sql_variant**|매개 변수의 값입니다.|  
|sensitive|**bit**|값이 `1`이면 매개 변수 값이 중요하고, 값이 `0`이면 매개 변수 값이 중요하지 않습니다.|  
|required|**bit**|값이 `1`이면 실행을 시작하는 데 매개 변수 값이 필요하고, 값이 `0`이면 실행을 시작하는 데 매개 변수 값이 필요하지 않습니다.|  
|value_set|**bit**|값이 `1`이면 매개 변수 값이 할당되었고, 값이 `0`이면 매개 변수 값이 할당되지 않았습니다.|  
  
> [!NOTE]  
>  리터럴 값은 일반 텍스트로 표시됩니다. **NULL**은 중요한 값 대신 표시됩니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 권한과 해당되는 경우 참조된 환경에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   지정된 폴더 또는 프로젝트에서 패키지를 찾을 수 없는 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
-   지정된 환경 참조가 없는 경우  
  
  
