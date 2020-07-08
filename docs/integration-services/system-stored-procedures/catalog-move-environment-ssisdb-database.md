---
title: catalog.move_environment(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b3fb5242-3c4c-4a87-b3e5-beb22fbab053
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7646bb7498ed18c2e0e5e28268442b4638ee16bf
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85637729"
---
# <a name="catalogmove_environment-ssisdb-database"></a>catalog.move_environment(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그 내에서 폴더 간에 환경을 이동합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.move_environment [ @source_folder = ] source_folder  
    , [ @environment_name = ] environment_name  
    , [ @destination_folder = ] destination_folder  
```  
  
## <a name="arguments"></a>인수  
 [ @source_folder = ] *source_folder*  
 이동하기 전의 환경이 있는 원본 폴더의 이름입니다. *source_folder*는 **nvarchar(128)** 입니다.  
  
 [ @environment_name = ] *environment_name*  
 이동할 환경의 이름입니다. *environment_name*은 **nvarchar(128)** 입니다.  
  
 [ @destination_folder = ] *destination_folder*  
 이동한 후의 환경이 있는 대상 폴더의 이름입니다. *destination_folder*는 **nvarchar(128)** 입니다.  
  
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
  
-   원본 폴더에 환경이 없는 경우  
  
-   대상 폴더에 이름이 같은 환경이 이미 있는 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
## <a name="remarks"></a>설명  
 프로젝트의 환경 참조는 환경과 함께 이동하지 않습니다. 따라서 수동으로 업데이트해야 합니다. 이 저장 프로시저는 환경 이동으로 인해 환경 참조가 끊어진 경우에도 성공합니다. 이 저장 프로시저가 완료된 후에 환경 참조를 업데이트해야 합니다.  
  
> [!NOTE]  
>  프로젝트에는 상대 환경 참조 또는 절대 환경 참조가 있을 수 있습니다. 상대 참조는 환경을 이름으로 참조하며 환경이 프로젝트와 같은 폴더에 있어야 합니다. 절대 참조는 환경을 이름과 폴더로 참조하며 프로젝트와 다른 폴더에 있는 환경을 참조합니다.  
  
  
