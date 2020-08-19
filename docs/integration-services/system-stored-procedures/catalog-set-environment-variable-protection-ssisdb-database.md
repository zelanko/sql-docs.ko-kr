---
description: catalog.set_environment_variable_protection(SSISDB 데이터베이스)
title: catalog.set_environment_variable_protection(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 005b6b2f-a5d9-4ea4-8d4e-beed6ab33c0d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5e5e93263d37acf72782f2b9a2fe3ef3f7c5d29d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422157"
---
# <a name="catalogset_environment_variable_protection-ssisdb-database"></a>catalog.set_environment_variable_protection(SSISDB 데이터베이스)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 환경 변수에 대한 민감도 비트를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.set_environment_variable_protection [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable_name  
    , [ @sensitive = ] sensitive  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 환경이 있는 폴더의 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [ @environment_name = ] *environment_name*  
 환경의 이름입니다. *environment_name*은 **nvarchar(128)** 입니다.  
  
 [ @variable_name = ] *variable_name*  
 환경 변수의 이름입니다. *variable_name*은 **nvarchar(128)** 입니다.  
  
 [ @sensitive = ] *sensitive*  
 변수에 중요한 값이 포함되었는지 여부를 나타냅니다. 환경 변수 값이 중요함을 나타내려면 값 `1`을 사용하고, 그렇지 않음을 나타내려면 값 `0`을 사용합니다. 중요한 값은 저장될 때 암호화되고, 중요하지 않은 값은 일반 텍스트로 저장됩니다. *중요한* 매개 변수는 **비트**입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   환경에 대한 READ 및 MODIFY 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   폴더 이름이 잘못된 경우  
  
-   환경 이름이 잘못된 경우  
  
-   환경 변수 이름이 잘못된 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
  
