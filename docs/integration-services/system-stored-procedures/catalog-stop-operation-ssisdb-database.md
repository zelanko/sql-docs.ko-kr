---
title: "catalog.stop_operation(SSISDB 데이터베이스) | Microsoft Docs"
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
ms.assetid: 97fd9d22-03dd-4eda-8f6c-ba8b67acec68
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5be9cd2a8687a85e4d66a323d347b59a180de5d0
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="catalogstopoperation-ssisdb-database"></a>catalog.stop_operation(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 실행 인스턴스 또는 유효성 검사를 중지합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.stop_operation [ @operation_id = ] operation_id  
```  
  
## <a name="arguments"></a>인수  
 [ @operation_id = ] *operation_id*  
 실행 인스턴스 또는 유효성 검사의 고유 식별자입니다. *operation_id*는 **bigint**입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스 또는 유효성 검사에 대한 READ 및 MODIFY 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   사용자에게 적절한 권한이 없는 경우  
  
-   작업 식별자가 잘못된 경우  
  
-   작업이 이미 중지된 경우  
  
## <a name="remarks"></a>Remarks  
 한 번에 한 명의 사용자만 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 작업을 중지해야 합니다. 여러 사용자가 작업을 중지하려고 하면 첫 번째 시도에 대해서는 저장 프로시저에서 성공(값 `0`)을 반환하지만 후속 시도에는 오류가 발생합니다.  
  
  
