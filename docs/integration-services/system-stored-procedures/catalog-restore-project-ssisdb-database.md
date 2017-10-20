---
title: "catalog.restore_project (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 8adee525-579b-4d2f-b807-e2ecc07fb2e9
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 23074fc664591411666315036e3493e1b7b26134
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrestoreproject-ssisdb-database"></a>catalog.restore_project(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 프로젝트를 이전 버전으로 복원합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
restore_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project _name  
    , [ @object_version_lsn = ] object_version_lsn  
  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name =] *folder_name*  
 프로젝트가 있는 폴더의 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
 [ @project _name =] *project_name*  
 프로젝트의 이름입니다. *project_name* 은 **nvarchar (128)**합니다.  
  
 [ @object_version_lsn =] *object_version_lsn*  
 프로젝트의 버전입니다. *object_version_lsn* 은 **bigint**합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 프로젝트 세부 정보로 반환 되 **varbinary (max)** 경우 결과 집합의 일부로 *project_name* 를 찾을 수 있습니다.  
  
 **결과 집합 없음** 프로젝트 지정 된 폴더로 복원할 수 없는 경우 반환 됩니다.  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 및 MODIFY 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   프로젝트 버전이 없거나 프로젝트 이름과 일치하지 않는 경우  
  
-   프로젝트가 없는 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
## <a name="remarks"></a>주의  
 프로젝트가 복원되면 모든 매개 변수에 기본값이 할당되고 모든 환경 참조가 변경되지 않은 상태로 유지됩니다. 카탈로그에 유지 되는 프로젝트 버전의 최대 수는 카탈로그 속성에 따라 결정 됩니다 **MAX_VERSIONS_PER_PROJECT**에 나타난 것 처럼는 [catalog_property](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) 보기.  
  
> [!WARNING]  
>  프로젝트를 복원된 후 환경 참조가 더 이상 유효하지 않을 수도 있습니다.  
  
  
