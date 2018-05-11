---
title: catalog.deploy_packages | Microsoft Docs
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
ms.assetid: 8e861df6-d103-4d84-8438-e822533f6849
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f79688853f2c165364c1057a77d03dc01ad5fbd9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="catalogdeploypackages"></a>catalog.deploy_packages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 폴더에 하나 이상의 패키지를 배포하거나 이전에 배포된 기존 패키지를 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
[catalog].[deploy_packages]     [ @folder_name = ] folder_name,    [ @project_name = ] project_name,    [ @packages_table = ] packages_table,     [ @operation_id OUTPUT ] operation_id OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 폴더 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [ @project_name = ] *project_name*  
 폴더에 있는 프로젝트의 이름입니다. *project_name*은 **nvarchar(128)** 입니다.  
  
 [ @packages_table = ] *packages_table*  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지(.dtsx) 파일의 이진 콘텐츠입니다. *packages_table*은 **[catalog].[Package_Table_Type]** 입니다.  
  
 [ @operation_id = ] *operation_id*  
 배포 작업에 대한 고유 식별자를 반환합니다. *operation_id*는 **bigint**입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 CREATE_OBJECTS 권한 또는 업데이트할 패키지에 대한 MODIFY 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 이 저장 프로시저에서 오류가 발생하는 몇 가지 조건을 설명합니다.  
  
-   매개 변수가 존재하지 않는 개체를 참조하거나, 이미 있는 개체를 만들려고 하거나, 기타 다른 방식으로 잘못된 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
  
