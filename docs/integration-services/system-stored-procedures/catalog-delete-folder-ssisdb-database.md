---
description: catalog.delete_folder(SSISDB 데이터베이스)
title: catalog.delete_folder(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b9c08992-500c-447e-bc19-1eb13c9b0293
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1257d1751798046dc176aa8969541f92ec0a215b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456903"
---
# <a name="catalogdelete_folder-ssisdb-database"></a>catalog.delete_folder(SSISDB 데이터베이스)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에서 폴더를 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.delete_folder [ @folder_name = ] folder_name  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 삭제할 폴더의 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 폴더 삭제를 확인하는 메시지를 반환합니다.  
  
  
