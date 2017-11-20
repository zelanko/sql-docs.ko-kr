---
title: "catalog.create_folder (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
ms.assetid: 06fb3549-e970-4ca2-a61f-59affb9c6dcc
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 43d128f9dcc4cea632c810a13d21eb5e1ddb61df
ms.contentlocale: ko-kr
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreatefolder-ssisdb-database"></a>catalog.create_folder(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 폴더를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.create_folder [@folder_name =] folder_name, [@folder_id =] folder_id OUTPUT  
```  
  
## <a name="arguments"></a>인수  
 [@folder_name =] *folder_name*  
 새 폴더의 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
 [@folder_name =] *folder_id*  
 폴더의 고유 식별자(ID)입니다. *folder_id* 은 **bigint**합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 폴더 식별자가 반환됩니다.  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
동일한 이름의 폴더가 이미 있는 경우 저장된 프로시저가 오류를 반환 합니다.  
  
  

