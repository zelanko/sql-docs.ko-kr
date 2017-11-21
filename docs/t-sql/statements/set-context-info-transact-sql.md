---
title: SET CONTEXT_INFO (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_CONTEXT_INFO_TSQL
- SET CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- context information [SQL Server]
- CONTEXT_INFO option
- SET CONTEXT_INFO statement
ms.assetid: a0b7b9f3-dbda-4350-a274-bd9ecd5c0a74
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f74a45830a295467552c8fdc9f4781260339d9a6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="set-contextinfo-transact-sql"></a>SET CONTEXT_INFO(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  128바이트까지의 이전 정보를 현재 연결 또는 현재 세션과 연결합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SET CONTEXT_INFO { binary_str | @binary_var }  
```  
  
## <a name="arguments"></a>인수  
 *binary_str*  
 이 **이진** 상수 또는 상수를 암시적으로 변환할 수 있는 **이진**현재 세션이 나 연결에 연결 하 합니다.  
  
 **@***binary_var*  
 이 **varbinary** 또는 **이진** 변수는 현재 세션이 나 연결에 연결 하기 위해 컨텍스트 값을 보유 합니다.  
  
## <a name="remarks"></a>주의  
 현재 세션에 대한 컨텍스트 정보를 검색하는 기본 방법은 CONTEXT_INFO 함수를 사용하는 것입니다. 세션 컨텍스트 정보에 저장 되어는 **context_info** 다음 시스템 뷰에 열:  
  
-   **sys.dm_exec_requests**  
  
-   **sys.dm_exec_sessions**  
  
-   **sys.sysprocesses**  
  
 사용자 정의 함수에는 SET CONTEXT_INFO를 지정할 수 없습니다. 값을 보유하는 뷰는 Null 값을 허용하지 않으므로 SET CONTEXT_INFO에 Null 값을 지정할 수 없습니다.  
  
 SET CONTEXT_INFO는 상수나 변수 이름 이외의 식을 허용하지 않습니다. 함수 호출의 결과로 컨텍스트 정보를 설정 하려면 먼저 포함 해야에 함수 호출의 결과 **이진** 또는 **varbinary** 변수입니다.  
  
 저장 프로시저나 트리거에서 SET CONTEXT_INFO를 실행하면 다른 SET 문과 달리 저장 프로시저나 트리거가 완료된 후에도 컨텍스트 정보에 대해 설정된 새 값이 계속 유지됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-setting-context-information-by-using-a-constant"></a>1. 상수를 사용하여 컨텍스트 정보 설정  
 다음 예에서는 값을 설정하고 결과를 표시하여 `SET CONTEXT_INFO`를 보여 줍니다. `sys.dm_exec_sessions`을 쿼리하려면 SELECT 및 VIEW SERVER STATE 권한이 필요하지만 CONTEXT_INFO 함수를 사용하면 해당 권한이 필요하지 않습니다.  
  
```  
SET CONTEXT_INFO 0x01010101;  
GO  
SELECT context_info   
FROM sys.dm_exec_sessions  
WHERE session_id = @@SPID;  
GO  
```  
  
### <a name="b-setting-context-information-by-using-a-function"></a>2. 함수를 사용하여 컨텍스트 정보 설정  
 다음 예제에서는 함수의 출력을 사용 하 여 여기서 함수에서 값 처음에 배치 해야 컨텍스트 값을 설정 하는 **이진** 변수입니다.  
  
```  
DECLARE @BinVar varbinary(128);  
SET @BinVar = CAST(REPLICATE( 0x20, 128 ) AS varbinary(128) );  
SET CONTEXT_INFO @BinVar;  
  
SELECT CONTEXT_INFO() AS MyContextInfo;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [sys.dm_exec_requests &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_sessions &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [CONTEXT_INFO &#40; Transact SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)  
  
  

