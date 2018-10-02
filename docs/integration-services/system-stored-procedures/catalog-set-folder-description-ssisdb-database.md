---
title: catalog.set_folder_description(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 802416f6-5177-4db5-bca5-976dec5faf53
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 159eae51815fcb5343e81dd500dc55de90250e99
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668021"
---
# <a name="catalogsetfolderdescription-ssisdb-database"></a>catalog.set_folder_description(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 폴더에 대한 설명을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.set_folder_description [ @folder_name = ] folder_name  
    , [ @folder_description = ] folder_description  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 폴더 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [ @folder_description = ] *folder_description*  
 폴더에 대한 설명입니다. *folder_description*은 **nvarchar(MAX)** 입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 이 저장 프로시저는 새 폴더 설명에 대한 설정을 확인하는 메시지를 반환합니다.  
  
  
