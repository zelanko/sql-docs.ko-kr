---
title: "catalog.delete_project (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: f3431445-8dd2-443b-813e-b99db893977e
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: abc0280a693be8e0f9fa9b3ec997c1d38d96ed54
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeleteproject-ssisdb-database"></a>catalog.delete_project(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 폴더에서 기존 프로젝트를 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.delete_project [ @folder_name = ] folder_name , [ @project_name = ] project_name  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name =] *folder_name*  
 프로젝트가 있는 폴더의 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
 [ @project_name =] *project_name*  
 삭제할 프로젝트의 이름입니다. *project_name* 은 **nvarchar (128)**합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 및 MODIFY 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 delete_project 저장 프로시저에서 오류가 발생 하는 몇 가지 조건을 설명 합니다.  
  
-   프로젝트가 없는 경우  
  
-   폴더가 없는 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
## <a name="remarks"></a>주의  
 해당 프로젝트의 모든 개체 및 환경 참조는 프로젝트와 함께 삭제됩니다. 그러나 프로젝트 버전 및 관련 작업 레코드는 다음에 작업 정리 작업을 실행할 때까지 유지됩니다.  
  
  

