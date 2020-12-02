---
description: catalog.disable_worker_agent(SSISDB 데이터베이스)
title: catalog.disable_worker_agent(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3f19dc4c-a000-4318-8fe1-e80d56720e66
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4b2642c70b5c48e6f9e1f6ad48c61ecc17f0cfc1
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129800"
---
# <a name="catalogdisable_worker_agent-ssisdb-database"></a>catalog.disable_worker_agent(SSISDB 데이터베이스)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

이 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그를 사용하여 Scale Out 마스터에 대한 Scale Out 작업자를 사용하지 않도록 설정합니다.

## <a name="syntax"></a>구문

```sql
catalog.disable_worker_agent [ @WorkerAgentId = ] WorkerAgentId
```
## <a name="arguments"></a>인수
[@WorkerAgentId =] *WorkerAgentId* Scale Out Worker의 작업자 에이전트 ID입니다. *WorkerAgentId* 는 **uniqueidentifier** 입니다.

## <a name="example"></a>예제
이 예제에서는 MachineA에서 Scale Out 작업자를 사용하지 않도록 설정합니다.

```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[disable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 None  

## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격 

## <a name="errors-and-warnings"></a>오류 및 경고
작업자 에이전트 ID가 유효하지 않은 경우 저장 프로시저가 오류를 반환합니다.
