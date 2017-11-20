---
title: "catalog.get_project (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: f263c9e4-a7db-4888-a458-70ae99b1f729
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: adb3542d50db426d5908aa8786145406d7263ad6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="cataloggetproject-ssisdb-database"></a>catalog.get_project(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포된 프로젝트의 이진 스트림을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.get_project [ @folder_name = ] folder_name , [ @project_name = ] project_name   
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name =] *folder_name*  
 프로젝트가 있는 폴더의 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
 [ @project_name =] *project_name*  
 프로젝트의 이름입니다. *project_name* 은 **nvarchar (128)**합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 프로젝트의 이진 스트림으로 반환 됩니다 **varbinary (max)**합니다. 폴더 또는 프로젝트가 없으면 아무 결과도 반환되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 get_project 저장 프로시저에서 오류가 발생 하는 몇 가지 조건을 설명 합니다.  
  
-   프로젝트가 없는 경우  
  
-   폴더가 없는 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
  

