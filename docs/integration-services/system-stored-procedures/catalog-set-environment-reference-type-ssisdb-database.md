---
title: catalog.set_environment_reference_type(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b79e3a06-22c0-40e5-8933-1b3414db3329
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d50cef16424f5524429c6b4285af0ae8568391be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038701"
---
# <a name="catalogsetenvironmentreferencetype-ssisdb-database"></a>catalog.set_environment_reference_type(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 프로젝트에 대해 기존 환경 참조와 연결된 참조 유형 및 환경 이름을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.set_environment_reference_location [ @reference_id = reference_id  
    , [ @reference_type = ] reference_type  
 [  , [ @environment_folder_name = ] environment_folder_name ]  
```  
  
## <a name="arguments"></a>인수  
 [ @reference_id = ] *reference_id*  
 업데이트할 환경 참조의 고유 식별자입니다. *reference_id*는 **bigint**입니다.  
  
 [ @reference_type = ] *reference_type*  
 환경을 프로젝트와 같은 폴더(상대 참조)에서 찾을 수 있는지, 아니면 다른 폴더(절대 참조)에서 찾을 수 있는지를 나타냅니다. 상대 참조를 나타내려면 값 `R`을 사용하고, 절대 참조를 나타내려면 값 `A`를 사용합니다. *reference_type*은 **char(1)** 입니다.  
  
 [ @environment_folder_name = ] *environment_folder_name*  
 환경이 있는 폴더입니다. 이 값은 절대 참조에 필요합니다. *environment_folder_name*은 **nvarchar(128)** 입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 및 MODIFY 권한과 환경에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   폴더 이름, 환경 이름 또는 참조 ID가 잘못된 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
-   절대 참조는 *reference_location* 매개 변수에서 `A` 문자를 사용하여 지정했지만 폴더 이름이 *environment_folder_name* 매개 변수로 지정되지 않은 경우  
  
## <a name="remarks"></a>Remarks  
 프로젝트에는 상대 환경 참조 또는 절대 환경 참조가 있을 수 있습니다. 상대 참조는 환경을 이름으로 참조하며 환경이 프로젝트와 같은 폴더에 있어야 합니다. 절대 참조는 환경을 이름과 폴더로 참조하며 프로젝트와 다른 폴더에 있는 환경을 참조할 수도 있습니다. 하나의 프로젝트에서 여러 환경을 참조할 수 있습니다.  
  
> [!IMPORTANT]  
>  상대 참조를 지정하면 *environment_folder_name* 매개 변수 값이 사용되지 않고 환경 폴더 이름이 자동으로 **NULL**로 설정됩니다. 절대 참조를 지정한 경우에는 *environment_folder_name* 매개 변수에 환경 폴더 이름을 제공해야 합니다.  
  
  
