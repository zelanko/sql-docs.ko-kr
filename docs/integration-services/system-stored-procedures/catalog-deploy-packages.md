---
title: catalog.deploy_packages | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 8e861df6-d103-4d84-8438-e822533f6849
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1839430dd7fb83ab16c4de46011819e3ce28e835
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeploypackages"></a>catalog.deploy_packages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  하나 이상의 패키지에 있는 폴더에 배포는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그 또는 이전에 배포 된 기존 패키지를 업데이트 합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
[catalog].[deploy_packages]     [ @folder_name = ] folder_name,    [ @project_name = ] project_name,    [ @packages_table = ] packages_table,     [ @operation_id OUTPUT ] operation_id OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name =] *folder_name*  
 폴더 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
 [ @project_name =] *project_name*  
 폴더에 프로젝트의 이름입니다. *project_name* 은 **nvarchar (128)**합니다.  
  
 [ @packages_table =] *packages_table*  
 이진 내용을 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 (.dtsx) 파일입니다. *packages_table* 은 **[catalog]. [ Package_Table_Type]**  
  
 [ @operation_id =] *operation_id*  
 배포 작업에 대한 고유 식별자를 반환합니다. *operation_id* 은 **bigint**합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트 또는 패키지를 업데이트 하려면 패키지에 대 한 수정 권한을에 대 한 CREATE_OBJECTS 권한.  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 이 저장 프로시저에서 오류가 발생하는 몇 가지 조건을 설명합니다.  
  
-   매개 변수가 참조 하는 개체가 존재 하지 않는, 매개 변수를 이미 존재 하는 개체를 생성 하려고 합니다. 또는 매개 변수를 다른 방법으로 올바르지 않습니다.  
  
-   사용자에게 적절한 권한이 없는 경우  
  
  

