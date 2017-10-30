---
title: "catalog.delete_folder (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: b9c08992-500c-447e-bc19-1eb13c9b0293
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bf4ecdd473e94c7f00c31b9f99e6cec86db93f60
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeletefolder-ssisdb-database"></a>catalog.delete_folder(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에서 폴더를 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
delete_folder [ @folder_name = ] folder_name  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name =] *folder_name*  
 삭제할 폴더의 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 폴더 삭제를 확인하는 메시지를 반환합니다.  
  
  

