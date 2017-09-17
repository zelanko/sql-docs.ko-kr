---
title: "catalog.enable_worker_agent (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c6e5266b-c32d-49ff-aa69-f09664009fb4
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: b348939327efbacbb612e28c4c30fbb2d7cc0a17
ms.contentlocale: ko-kr
ms.lasthandoff: 09/08/2017

---
# <a name="catalogenableworkeragent-ssisdb-database"></a>catalog.enable_worker_agent (SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

스케일 아웃 작업 마스터가에 대 한 스케일 아웃 작업자를 사용 하도록 설정 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그입니다.

## <a name="syntax"></a>구문

```tsql
enable_worker_agent [@WorkerAgentId = ] WorkerAgentId
```
## <a name="arguments"></a>인수
[ @WorkerAgentId =] *WorkerAgentId* 스케일 아웃 작업자의 작업자 에이전트 id입니다. *WorkerAgentId* 은 **uniqueidentifier**합니다.

## <a name="example"></a>예제
이 예제에서는 MachineA에서 규모 확장 작업자를 사용하도록 설정합니다.
```tsql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
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
저장된 프로시저 작업자 에이전트 ID 유효 하지 않을 경우 오류가 반환 됩니다.

