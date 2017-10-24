---
title: "catalog.validate_package (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- validate_package stored procedure [Integration Services]
- catalog.validate_package stored procedure [Integration Services]
ms.assetid: 0dc03df1-b793-408f-af4c-c11188729abf
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 869b758e3ac922762c293eb8aa9a9537a4397bd6
ms.contentlocale: ko-kr
ms.lasthandoff: 10/20/2017

---
# <a name="catalogvalidatepackage-ssisdb-database"></a>catalog.validate_package(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
 [ @folder_name =] *folder_name*  
 패키지가 있는 폴더의 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
 [ @project_name =] *project_name*  
 패키지가 포함된 프로젝트의 이름입니다. *project_name* 은 **nvarchar (128)**합니다.  
  
 [ @package_name =] *package_name*  
 패키지의 이름입니다. *package_name* 은 **nvarchar (260)**합니다.  
  
 [ @validation_id =] *validation_id*  
 유효성 검사의 고유 식별자(ID)를 반환합니다. *validation_id* 은 **bigint**합니다.  
  
 [ @use32bitruntime =] *use32bitruntime*  
 64비트 운영 체제에서 32비트 런타임을 사용하여 패키지를 실행해야 하는지 여부를 나타냅니다. 값을 사용 하 여 `1` 64 비트 운영 체제에서 실행 하는 경우 32 비트 런타임 사용 하 여 패키지를 실행 합니다. 64비트 운영 체제에서 실행할 때 64비트 런타임으로 패키지를 실행하려면 값 `0`을 사용합니다. 이 매개 변수는 선택 사항입니다. *use32bitruntime* 은 **비트**합니다.  
  
 [ @environment_scope =] *environment_scope*  
 유효성 검사에서 고려되는 환경 참조를 나타냅니다. 값이 `A`이면 프로젝트와 연결된 모든 환경 참조가 유효성 검사에 포함되고, 값이 `S`이면 단일 환경 참조만 포함됩니다. 또한 값이 `D`이면 아무 환경 참조도 포함되지 않습니다. 이 경우 유효성 검사를 통과하려면 각 매개 변수 값이 리터럴 기본값이어야 합니다. 이 매개 변수는 선택 사항입니다. 문자 `D` 기본적으로 사용 됩니다. *environment_scope* 은 **Char(1)**합니다.  
  
 [ @reference_id =] *reference_id*  
 환경 참조의 고유 ID입니다. 이 매개 변수는 단일 환경 참조의 유효성 검사에 포함 되어 있는 경우에 필요 때 *environment_scope* 은 `S`합니다. *reference_id* 은 **bigint**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 권한과 해당되는 경우 참조된 환경에 대한 READ 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   프로젝트 이름 또는 패키지 이름이 잘못된 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
-   유효성 검사에 포함된 하나 이상의 참조된 환경에 참조된 변수가 없는 경우  
  
-   패키지의 유효성 검사에 실패한 경우  
  
-   참조된 환경이 없는 경우  
  
-   유효성 검사에 포함된 참조된 환경에서 참조된 변수를 찾을 수 없는 경우  
  
-   변수가 패키지 매개 변수에서 참조되지만 유효성 검사에 참조된 환경이 포함되지 않은 경우  
  
## <a name="remarks"></a>주의  
 유효성 검사는 패키지가 성공적으로 실행 하지 못하게 할 수 있는 문제를 식별 하는 데 도움이 됩니다. 사용 하 여는 [catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md) 또는 [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 뷰를 유효성 검사 상태를 모니터링 합니다.  
  
  
