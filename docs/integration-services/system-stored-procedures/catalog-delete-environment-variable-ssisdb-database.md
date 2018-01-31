---
title: "catalog.delete_environment_variable(SSISDB 데이터베이스) | Microsoft Docs"
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
ms.assetid: 894b3bdb-aa34-463e-aba4-1b68ad96a0ef
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f40a1f005aca284624b78e3ac48a92c909dc7e32
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="catalogdeleteenvironmentvariable-ssisdb-database"></a>catalog.delete_environment_variable(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 환경에서 환경 변수를 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
delete_environment_variable [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable_name  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 환경이 있는 폴더의 이름입니다. *folder_name*은 **nvarchar(128)**입니다.  
  
 [ @environment_name = ] *environment_name*  
 변수가 있는 환경의 이름입니다. *environment_name*은 **nvarchar(128)**입니다.  
  
 [ @variable_name = ] *variable_name*  
 삭제할 변수의 이름입니다. *variable_name*은 **nvarchar(128)**입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   환경에 대한 READ 및 MODIFY 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   환경 이름이 잘못된 경우  
  
-   환경 변수가 없는 경우  
  
  
