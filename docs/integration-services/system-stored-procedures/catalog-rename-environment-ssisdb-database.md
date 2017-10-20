---
title: "catalog.rename_environment (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: c73d7452-31c5-4f4e-afcc-e9eca760c826
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 504d3ca0f18c9ea11105ebb575d2f5db449f91e4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrenameenvironment-ssisdb-database"></a>catalog.rename_environment(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 환경의 이름을 변경합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
rename_environment [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @new_environment_name= ] new_environment_name  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name =] *folder_name*  
 환경이 있는 폴더의 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
 [ @environment_name =] *environment_name*  
 환경의 원래 이름입니다. *environment_name* 은 **nvarchar (128)**합니다.  
  
 [ @new_environment_name =] *new_environment_name*  
 환경의 새 이름입니다. *new_environment_name* 은 **nvarchar (128)**합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   환경에 대한 MODIFY 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   원래 환경 이름이 잘못된 경우  
  
-   새 이름을 기존 환경에서 이미 사용하고 있는 경우  
  
## <a name="remarks"></a>주의  
 환경 이름을 바꾼 경우 프로젝트의 환경 참조는 자동으로 업데이트되지 않습니다. 따라서 수동으로 업데이트해야 합니다. 이 저장 프로시저는 환경 이름 변경으로 인해 환경 참조가 끊어진 경우에도 성공합니다. 이 저장 프로시저가 완료된 후에 환경 참조를 업데이트해야 합니다.  
  
> [!NOTE]  
>  환경 참조가 유효하지 않으면 이러한 참조를 사용하는 해당 패키지의 유효성 검사 및 실행이 실패합니다.  
  
  
