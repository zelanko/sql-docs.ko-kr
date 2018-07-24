---
title: catalog.validate_package(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- validate_package stored procedure [Integration Services]
- catalog.validate_package stored procedure [Integration Services]
ms.assetid: 0dc03df1-b793-408f-af4c-c11188729abf
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 31326b03aa3f1321dcfc890020053b83e09e28a4
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38063821"
---
# <a name="catalogvalidatepackage-ssisdb-database"></a>catalog.validate_package(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 패키지의 유효성을 비동기적으로 검사합니다.  
  
## <a name="syntax"></a>구문  
  
```sql
catalog.validate_package [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @package_name = ] package_name  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @target_environment = ] target_environment ]  
 [  , [ @reference_id = ] reference_id ]  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 패키지가 있는 폴더의 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [ @project_name = ] *project_name*  
 패키지가 포함된 프로젝트의 이름입니다. *project_name*은 **nvarchar(128)** 입니다.  
  
 [ @package_name = ] *package_name*  
 패키지의 이름입니다. *package_name*은 **nvarchar(260)** 입니다.  
  
 [ @validation_id = ] *validation_id*  
 유효성 검사의 고유 식별자(ID)를 반환합니다. *validation_id*는 **bigint**입니다.  
  
 [ @use32bitruntime = ] *use32bitruntime*  
 64비트 운영 체제에서 32비트 런타임을 사용하여 패키지를 실행해야 하는지 여부를 나타냅니다. 64비트 운영 체제에서 실행할 때 32비트 런타임으로 패키지를 실행하려면 값 `1`을 사용합니다. 64비트 운영 체제에서 실행할 때 64비트 런타임으로 패키지를 실행하려면 값 `0`을 사용합니다. 이 매개 변수는 선택 사항입니다. *use32bitruntime*은 **bit**입니다.  
  
 [ @environment_scope = ] *environment_scope*  
 유효성 검사에서 고려되는 환경 참조를 나타냅니다. 값이 `A`이면 프로젝트와 연결된 모든 환경 참조가 유효성 검사에 포함되고, 값이 `S`이면 단일 환경 참조만 포함됩니다. 또한 값이 `D`이면 아무 환경 참조도 포함되지 않습니다. 이 경우 유효성 검사를 통과하려면 각 매개 변수 값이 리터럴 기본값이어야 합니다. 이 매개 변수는 선택 사항입니다. 문자 `D`가 기본적으로 사용됩니다. *environment_scope*은 **Char(1)** 입니다.  
  
 [ @reference_id = ] *reference_id*  
 환경 참조의 고유 ID입니다. 이 매개 변수는 단일 환경 참조가 유효성 검사에 포함되어 있는 경우, 즉 *environment_scope*이 `S`인 경우에만 필요합니다. *reference_id*는 **bigint**입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 권한과 해당되는 경우 참조된 환경에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   프로젝트 이름 또는 패키지 이름이 잘못된 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
-   유효성 검사에 포함된 하나 이상의 참조된 환경에 참조된 변수가 없는 경우  
  
-   패키지의 유효성 검사에 실패한 경우  
  
-   참조된 환경이 없는 경우  
  
-   유효성 검사에 포함된 참조된 환경에서 참조된 변수를 찾을 수 없는 경우  
  
-   변수가 패키지 매개 변수에서 참조되지만 유효성 검사에 참조된 환경이 포함되지 않은 경우  
  
## <a name="remarks"></a>Remarks  
 유효성 검사를 통해 패키지 실행을 방해할 수도 있는 문제를 확인할 수 있습니다. [catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md) 또는 [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 뷰를 사용하여 유효성 검사 상태를 모니터링할 수 있습니다.  
  
  
