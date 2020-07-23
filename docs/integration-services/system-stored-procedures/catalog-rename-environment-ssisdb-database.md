---
title: catalog.rename_environment(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: c73d7452-31c5-4f4e-afcc-e9eca760c826
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 400b93128b19ca12550816889c732793c0e9e5d0
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912939"
---
# <a name="catalogrename_environment-ssisdb-database"></a>catalog.rename_environment(SSISDB 데이터베이스)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 환경의 이름을 변경합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.rename_environment [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @new_environment_name= ] new_environment_name  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 환경이 있는 폴더의 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [ @environment_name = ] *environment_name*  
 환경의 원래 이름입니다. *environment_name*은 **nvarchar(128)** 입니다.  
  
 [ @new_environment_name = ] *new_environment_name*  
 환경의 새 이름입니다. *new_environment_name*은 **nvarchar(128)** 입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   환경에 대한 MODIFY 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   원래 환경 이름이 잘못된 경우  
  
-   새 이름을 기존 환경에서 이미 사용하고 있는 경우  
  
## <a name="remarks"></a>설명  
 환경 이름을 바꾼 경우 프로젝트의 환경 참조는 자동으로 업데이트되지 않습니다. 따라서 수동으로 업데이트해야 합니다. 이 저장 프로시저는 환경 이름 변경으로 인해 환경 참조가 끊어진 경우에도 성공합니다. 이 저장 프로시저가 완료된 후에 환경 참조를 업데이트해야 합니다.  
  
> [!NOTE]  
>  환경 참조가 유효하지 않으면 이러한 참조를 사용하는 해당 패키지의 유효성 검사 및 실행이 실패합니다.  
  
  
