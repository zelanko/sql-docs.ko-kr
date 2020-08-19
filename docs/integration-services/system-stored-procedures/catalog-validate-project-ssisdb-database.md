---
description: catalog.validate_project(SSISDB 데이터베이스)
title: catalog.validate_project(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 5270689a-46d4-4847-b41f-3bed1899e955
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c491a8914fb11da815d0887ae5b2248f1e2a7c19
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495357"
---
# <a name="catalogvalidate_project-ssisdb-database"></a>catalog.validate_project(SSISDB 데이터베이스)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 프로젝트의 유효성을 비동기적으로 검사합니다.  
  
## <a name="syntax"></a>구문  
  
```sql
catalog.validate_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @validate_type = ] validate_type  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @environment_scope = ] environment_scope ]  
 [  , [ @reference_id = ] reference_id ]  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 프로젝트가 있는 폴더의 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [ @project_name = ] *project_name*  
 프로젝트의 이름입니다. *project_name*은 **nvarchar(128)** 입니다.  
  
 [ @validate_type = ] *validate_type*  
 수행할 유효성 검사의 유형을 나타냅니다. 전체 유효성 검사를 수행하려면 `F` 문자를 사용합니다. 이 매개 변수는 선택 사항이며, 기본적으로 `F` 문자가 사용됩니다. *validate_type*은 **char(1)** 입니다.  
  
 [ @validation_id = ] *validation_id*  
 유효성 검사의 고유 식별자(ID)를 반환합니다. *validation_id*는 **bigint**입니다.  
  
 [ @use32bitruntime = ] *use32bitruntime*  
 64비트 운영 체제에서 32비트 런타임을 사용하여 패키지를 실행해야 하는지 여부를 나타냅니다. 64비트 운영 체제에서 실행할 때 32비트 런타임으로 패키지를 실행하려면 값 `1`을 사용합니다. 64비트 운영 체제에서 실행할 때 64비트 런타임으로 패키지를 실행하려면 값 `0`을 사용합니다. 이 매개 변수는 선택 사항입니다. *use32bitruntime*은 **bit**입니다.  
  
 [ @environment_scope = ] *environment_scope*  
 유효성 검사에서 고려되는 환경 참조를 나타냅니다. 값이 `A`이면 프로젝트와 연결된 모든 환경 참조가 유효성 검사에 포함되고, 값이 `S`이면 단일 환경 참조만 포함됩니다. 또한 값이 `D`이면 아무 환경 참조도 포함되지 않습니다. 이 경우 유효성 검사를 통과하려면 각 매개 변수 값이 리터럴 기본값이어야 합니다. 이 매개 변수는 선택 사항이며, 기본적으로 `D` 문자가 사용됩니다. *environment_scope*는 **char(1)** 입니다.  
  
 [ @reference_id = ] *reference_id*  
 환경 참조의 고유 ID입니다. 이 매개 변수는 단일 환경 참조가 유효성 검사에 포함되어 있는 경우, 즉 *environment_scope*이 `S`인 경우에만 필요합니다. *reference_id*는 **bigint**입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 유효성 검사 단계의 출력은 결과 집합의 다른 섹션으로 반환됩니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 권한과 해당되는 경우 참조된 환경에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 제공합니다.  
  
-   프로젝트에 있는 하나 이상의 패키지에 대한 유효성을 검사하지 못한 경우  
  
-   유효성 검사에 포함된 하나 이상의 참조된 환경에 참조된 변수가 없어 유효성을 검사하지 못한 경우  
  
-   지정된 유효성 검사 유형이 잘못된 경우  
  
-   프로젝트 이름 또는 환경 참조 ID가 잘못된 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
## <a name="remarks"></a>설명  
 유효성 검사를 통해 프로젝트에 있는 패키지 실행을 방해하는 문제를 확인할 수 있습니다. [catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md) 또는 [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 뷰를 사용하여 유효성 검사 상태를 모니터링할 수 있습니다.  
  
 사용자가 액세스할 수 있는 환경만 유효성 검사에 사용할 수 있습니다. 유효성 검사 출력은 결과 집합으로 클라이언트에 전송됩니다.  
  
 이 릴리스의 프로젝트 유효성 검사는 종속성 유효성 검사를 지원하지 않습니다.  
  
 전체 유효성 검사에서는 참조된 모든 환경 변수가 유효성 검사에 포함된 참조된 환경 내에 있는지를 확인합니다. 전체 유효성 검사 결과에는 유효하지 않은 환경 참조와 유효성 검사에 포함된 참조된 환경에서 찾을 수 없는 참조된 환경 변수가 나열됩니다.  
  
  
