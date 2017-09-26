---
title: "catalog.set_environment_variable_value (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 1d493dad-9d9c-4f0a-87e2-20a2d4a35f99
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7f30937f6dca19f82ccb2dc8ac998dd9f9510c0f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetenvironmentvariablevalue-ssisdb-database"></a>catalog.set_environment_variable_value(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 환경 변수 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```tsql  
set_environment_variable_value [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable _name  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name =] *folder_name*  
 환경이 있는 폴더의 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
 [ @environment_name =] *environment_name*  
 환경의 이름입니다. *environment_name* 은 **nvarchar (128)**합니다.  
  
 [ @variable _name =] *변수 _name*  
 환경 변수의 이름입니다. *변수 _name* 은 **nvarchar (128)**합니다.  
  
 [ @value =] *값*  
 환경 변수의 값입니다. *값* 은 **sql_variant**합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   환경에 대한 READ 및 MODIFY 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   폴더 이름이 잘못된 경우  
  
-   환경 이름이 잘못된 경우  
  
-   환경 변수 이름이 잘못된 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
  
