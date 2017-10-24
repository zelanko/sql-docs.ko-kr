---
title: "catalog.set_worker_agent_property (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
caps.latest.revision: 2
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: c1caf4a71e5802968d9471711b8206a26f9c28d5
ms.contentlocale: ko-kr
ms.lasthandoff: 10/20/2017

---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>catalog.set_worker_agent_property (SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

속성을 설정는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 스케일 아웃 작업자입니다.

## <a name="syntax"></a>구문

```sql
catalog.set_worker_agent_property [@WorkerAgentId =] WorkerAgentId, [@PropertyName =] PropertyName, [@PropertyValue =] PropertyValue 
```

## <a name="arguments"></a>인수
[@WorkerAgentId =] *WorkerAgentId*  
작업자 에이전트 ID의 스케일 아웃 작업자입니다. *WorkerAgentId* 은 **uniqueidentifier**합니다.

[@PropertyName =] *PropertyName*  
속성의 이름입니다. *PropertyName* 은 **nvarchar (256)**합니다.

[@PropertyValue =] *PropertyValue*  
속성 값입니다. *PropertyValue* 은 **nvarchar (max)**합니다.

## <a name="remarks"></a>주의
올바른 속성 이름은 **DisplayName**, **설명**, **태그**합니다.

## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 없음  

## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할

## <a name="errors-and-warnings"></a>오류 및 경고
  다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   사용자에게 적절한 권한이 없는 경우 

-   작업자 에이전트 ID가 잘못 되었습니다.

-   속성 이름이 올바르지 않습니다.

-   속성 값이 올바르지 않습니다.  
