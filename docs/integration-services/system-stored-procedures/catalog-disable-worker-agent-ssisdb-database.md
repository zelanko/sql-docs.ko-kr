---
title: "catalog.disable_worker_agent (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f19dc4c-a000-4318-8fe1-e80d56720e66
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 8f4a8cd24278742ffb13d16791ce5f1f3a95f301
ms.contentlocale: ko-kr
ms.lasthandoff: 10/20/2017

---
# <a name="catalogdisableworkeragent-ssisdb-database"></a>catalog.disable_worker_agent (SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

스케일 아웃 작업 마스터가에 대 한 스케일 아웃 작업자를 사용 하지 않도록 설정 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그입니다.

## <a name="syntax"></a>구문

```sql
catalog.disable_worker_agent [@WorkerAgentId =] WorkerAgentId
```
## <a name="arguments"></a>인수
[@WorkerAgentId =] *WorkerAgentId* 작업자 에이전트 ID의 스케일 아웃 작업자입니다. *WorkerAgentId* 은 **uniqueidentifier**합니다.

## <a name="example"></a>예제
이 예에서는 MachineA에 스케일 아웃 작업자를 해제합니다.

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
 없음  

## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할 

## <a name="errors-and-warnings"></a>오류 및 경고
작업자 에이전트 ID 유효 하지 않을 경우 저장된 프로시저가 오류를 반환 합니다.

