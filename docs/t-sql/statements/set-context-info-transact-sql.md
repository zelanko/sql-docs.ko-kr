---
title: SET CONTEXT_INFO(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: 6c0bba2dbdae81306e7310e719f6a9cb0e66a294
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
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
 현재 세션이나 연결에 연결하는 **binary** 상수이거나 암묵적으로 **binary**로 변환할 수 있는 상수입니다.  
  
 **@** *binary_var*  
 현재 세션이나 연결에 연결할 수 있는 컨텍스트 값을 보유하는 **varbinary** 또는 **binary** 변수입니다.  
  
## <a name="remarks"></a>Remarks  
 현재 세션에 대한 컨텍스트 정보를 검색하는 기본 방법은 CONTEXT_INFO 함수를 사용하는 것입니다. 세션 컨텍스트 정보는 다음과 같은 시스템 뷰의 **context_info** 열에 저장됩니다.  
  
-   **sys.dm_exec_requests**  
  
-   **sys.dm_exec_sessions**  
  
-   **sys.sysprocesses**  
  
 사용자 정의 함수에는 SET CONTEXT_INFO를 지정할 수 없습니다. 값을 보유하는 뷰는 Null 값을 허용하지 않으므로 SET CONTEXT_INFO에 Null 값을 지정할 수 없습니다.  
  
 SET CONTEXT_INFO는 상수나 변수 이름 이외의 식을 허용하지 않습니다. 함수 호출 결과로 컨텍스트 정보를 설정하려면 먼저 **binary** 또는 **varbinary** 변수에 함수 호출 결과를 포함시켜야 합니다.  
  
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
 다음 예에서는 함수의 결과를 사용하여 컨텍스트 값을 설정합니다. 이때 함수의 값을 **binary** 변수에 먼저 넣어야 합니다.  
  
```  
DECLARE @BinVar varbinary(128);  
SET @BinVar = CAST(REPLICATE( 0x20, 128 ) AS varbinary(128) );  
SET CONTEXT_INFO @BinVar;  
  
SELECT CONTEXT_INFO() AS MyContextInfo;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [CONTEXT_INFO  &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)  
  
  
