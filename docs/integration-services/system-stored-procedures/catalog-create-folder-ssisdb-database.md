---
title: "catalog.create_folder (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 06fb3549-e970-4ca2-a61f-59affb9c6dcc
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: df7b4750e813601b7e4d2a02c8f1f277f1000d9c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreatefolder-ssisdb-database"></a>catalog.create_folder(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 폴더를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```tsql  
create_folder [ @folder_name = ] folder_name, [ @folder_id = ] folder_id OUTPUT  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name =] *folder_name*  
 새 폴더의 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
 [ @folder_name =] *folder_id*  
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
 이름이 같은 폴더가 이미 있는 경우 저장 프로시저에서 오류를 반환합니다.  
  
  
