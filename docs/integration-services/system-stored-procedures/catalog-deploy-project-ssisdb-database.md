---
title: catalog.deploy_project(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 2e3439b4-7226-4b61-a993-7a1d161eac7e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f85e27484378d1074564a320aea7f8ed1766e1ce
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72251329"
---
# <a name="catalogdeploy_project-ssisdb-database"></a>catalog.deploy_project(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 폴더에 프로젝트를 배포하거나 이전에 배포된 기존 프로젝트를 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.deploy_project [@folder_name =] folder_name   
      , [@project_name =] project_name   
      , [@project_stream =] projectstream   
    [ , [@operation_id ] = operation_id OUTPUT ]   
```  
  
## <a name="arguments"></a>인수  
 [@folder_name =] *folder_name*  
 프로젝트가 배포되는 폴더의 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [@project_name =] *project_name*  
 폴더에 있는 새 프로젝트 또는 업데이트된 프로젝트의 이름입니다. *project_name*은 **nvarchar(128)** 입니다.  
  
 [@projectstream =] *projectstream*  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트 배포 파일(.ispac 확장명)의 이진 내용입니다.  
  
 SELECT 문을 OPENROWSET 함수 및 BULK 행 집합 공급자와 함께 사용하여 파일의 이진 내용을 검색할 수 있습니다. 예제는 [Integration Services(SSIS) 프로젝트 및 패키지 배포](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)를 참조하세요. OPENROWSET에 대한 자세한 내용은 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)을 참조하세요.  
  
 *projectstream*은 **varbinary(MAX)** 입니다.  
  
 [@operation_id =] *operation_id*  
 배포 작업에 대한 고유 식별자를 반환합니다. *operation_id*는 **bigint**입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   새 프로젝트를 배포할 폴더에 대한 CREATE_OBJECTS 권한 또는 업데이트할 프로젝트에 대한 MODIFY 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 이 저장 프로시저에서 오류가 발생하는 몇 가지 조건을 설명합니다.  
  
-   매개 변수가 존재하지 않는 개체를 참조하거나, 이미 있는 개체를 만들려고 하거나, 기타 다른 방식으로 잘못된 경우  
  
-   *\@project_name* 매개 변수 값이 배포 파일에 있는 프로젝트의 이름과 일치하지 않는 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
## <a name="remarks"></a>설명  
 이 저장 프로시저는 프로젝트를 배포하거나 업데이트하는 동안 프로젝트의 개별 패키지에 대한 보호 수준을 확인하지 않습니다.  
  
  
