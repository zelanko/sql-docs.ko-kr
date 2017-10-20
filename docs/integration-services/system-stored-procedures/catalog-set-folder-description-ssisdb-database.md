---
title: "catalog.set_folder_description (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 802416f6-5177-4db5-bca5-976dec5faf53
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f707687b62be599d74bde892f86ff50754185ff8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetfolderdescription-ssisdb-database"></a>catalog.set_folder_description(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 폴더에 대한 설명을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
set_folder_description [ @folder_name = ] folder_name  
    , [ @folder_description = ] folder_description  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name =] *folder_name*  
 폴더 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
 [ @folder_description =] *folder_description*  
 폴더에 대한 설명입니다. *folder_description* 은 **nvarchar (max)**합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 이 저장 프로시저는 새 폴더 설명에 대한 설정을 확인하는 메시지를 반환합니다.  
  
  
