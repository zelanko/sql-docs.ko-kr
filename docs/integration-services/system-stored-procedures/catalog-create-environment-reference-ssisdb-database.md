---
title: catalog.create_environment_reference(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 48069bea-31cb-4a0e-9849-a07edc94088f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d7b78f54633150fa507ca9df4a4c866cc4226e66
ms.sourcegitcommit: db1b6153f0bc2d221ba1ce15543ecc83e1045453
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82588219"
---
# <a name="catalogcreate_environment_reference-ssisdb-database"></a>catalog.create_environment_reference(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 프로젝트에 대한 환경 참조를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.create_environment_reference [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @environment_name = ] environment_name  
     , [ @reference_type = ] reference_type  
  [  , [ @environment_folder_name = ] environment_folder_name ]  
  [  , [ @reference_id = ] reference_id OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 환경을 참조하는 프로젝트의 폴더 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [ @project_name = ] *project_name*  
 환경을 참조하는 프로젝트의 이름입니다. *project_name*은 **nvarchar(128)** 입니다.  
  
 [ @environment_name = ] *environment_name*  
 참조되는 환경의 이름입니다. *environment_name*은 **nvarchar(128)** 입니다.  
  
 [ @reference_type = ] *reference_type*  
 환경을 프로젝트와 같은 폴더(상대 참조)에서 찾을 수 있는지, 아니면 다른 폴더(절대 참조)에서 찾을 수 있는지를 나타냅니다. 상대 참조를 나타내려면 값 `R`을 사용하고, 절대 참조를 나타내려면 값 `A`를 사용합니다. *reference_type*은 **char(1)** 입니다.  
  
 [ @environment_folder_name = ] *environment_folder_name*  
 참조되는 환경이 있는 폴더의 이름입니다. 이 값은 절대 참조에 필요합니다. *environment_folder_name*은 **nvarchar(128)** 입니다.  
  
 [ @reference_id = ] *reference_id*  
 새 참조에 대한 고유 식별자를 반환합니다. 이 매개 변수는 선택 사항입니다. *reference_id*는 **bigint**입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 및 MODIFY 권한과 환경에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   폴더 이름이 잘못된 경우  
  
-   프로젝트 이름이 잘못된 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
-   절대 참조는 *reference_location* 매개 변수에서 `A` 문자를 사용하여 지정했지만 폴더 이름이 *environment_folder_name* 매개 변수로 지정되지 않은 경우  
  
## <a name="remarks"></a>설명  
 프로젝트에는 상대 환경 참조 또는 절대 환경 참조가 있을 수 있습니다. 상대 참조는 환경을 이름으로 참조하며 환경이 프로젝트와 같은 폴더에 있어야 합니다. 절대 참조는 환경을 이름과 폴더로 참조하며 프로젝트와 다른 폴더에 있는 환경을 참조할 수도 있습니다. 하나의 프로젝트에서 여러 환경을 참조할 수 있습니다.  
  
  
