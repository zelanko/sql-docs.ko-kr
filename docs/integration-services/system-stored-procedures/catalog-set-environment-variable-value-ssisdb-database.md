---
title: catalog.set_environment_variable_value(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 1d493dad-9d9c-4f0a-87e2-20a2d4a35f99
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bc7e6d934c8256ebb0bed35afd1c538580eac431
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758153"
---
# <a name="catalogset_environment_variable_value-ssisdb-database"></a>catalog.set_environment_variable_value(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 환경 변수 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.set_environment_variable_value [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable _name  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 환경이 있는 폴더의 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [ @environment_name = ] *environment_name*  
 환경의 이름입니다. *environment_name*은 **nvarchar(128)** 입니다.  
  
 [ @variable _name = ] *variable _name*  
 환경 변수의 이름입니다. *variable_name*은 **nvarchar(128)** 입니다.  
  
 [ @value = ] *value*  
 환경 변수의 값입니다. *value*는 **sql_variant**입니다.  
  
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
  
  
