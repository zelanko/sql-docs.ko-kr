---
title: catalog.restore_project(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 8adee525-579b-4d2f-b807-e2ecc07fb2e9
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4cab881c5be277251cbc4292f9a3c6e0c3cad45f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="catalogrestoreproject-ssisdb-database"></a>catalog.restore_project(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 프로젝트를 이전 버전으로 복원합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.restore_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project _name  
    , [ @object_version_lsn = ] object_version_lsn  
  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 프로젝트가 있는 폴더의 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [ @project _name = ] *project_name*  
 프로젝트의 이름입니다. *project_name*은 **nvarchar(128)** 입니다.  
  
 [ @object_version_lsn = ] *object_version_lsn*  
 프로젝트의 버전입니다. *object_version_lsn*은 **bigint**입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 *project_name*이 있는 경우 프로젝트 상세 정보가 **varbinary(MAX)** 로 결과 집합에 포함됩니다.  
  
 프로젝트를 지정된 폴더로 복원할 수 없는 경우 **NO RESULT SET**이 반환됩니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 및 MODIFY 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   프로젝트 버전이 없거나 프로젝트 이름과 일치하지 않는 경우  
  
-   프로젝트가 없는 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
## <a name="remarks"></a>Remarks  
 프로젝트가 복원되면 모든 매개 변수에 기본값이 할당되고 모든 환경 참조가 변경되지 않은 상태로 유지됩니다. 카탈로그에 유지되는 프로젝트 버전의 최대 수는 [catalog_property](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) 보기에 표시된 대로 **MAX_VERSIONS_PER_PROJECT** 카탈로그 속성에 따라 결정됩니다.  
  
> [!WARNING]  
>  프로젝트를 복원된 후 환경 참조가 더 이상 유효하지 않을 수도 있습니다.  
  
  
