---
title: sp_trace_setfilter (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_trace_setfilter
- sp_trace_setfilter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setfilter
ms.assetid: 11e7c7ac-a581-4a64-bb15-9272d5c1f7ac
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 64b40b4b7970db0252a873f6b3611d57672e3da0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sptracesetfilter-transact-sql"></a>sp_trace_setfilter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  추적에 필터를 적용합니다. **sp_trace_setfilter** 중지 된 기존 추적 에서만 실행할 수 있습니다 (*상태* 은 **0**). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 저장된 프로시저 않거나 존재 하지 않는 추적에서 실행 되는 경우 오류가 반환 *상태* 않습니다 **0**합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 확장 이벤트를 대신 사용하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_trace_setfilter [ @traceid = ] trace_id   
          , [ @columnid = ] column_id  
          , [ @logical_operator = ] logical_operator  
          , [ @comparison_operator = ] comparison_operator  
          , [ @value = ] value  
```  
  
## <a name="arguments"></a>인수  
 [ **@traceid=** ] *trace_id*  
 필터를 설정한 추적의 ID입니다. *trace_id* 은 **int**, 기본값은 없습니다. 사용자가이 사용 *trace_id* 식별, 수정 및 추적 제어 하는 값입니다.  
  
 [ **@columnid=** ] *column_id*  
 필터를 적용한 열의 ID입니다 *column_id* 은 **int**, 기본값은 없습니다. 경우 *column_id* 이 NULL 이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정된 된 추적에 대 한 모든 필터를 지웁니다.  
  
 [ **@logical_operator** =] *logical_operator*  
 지정 하는지 여부를 AND (**0**) 또는 OR (**1**) 연산자가 적용 됩니다. *logical_operator* 은 **int**, 기본값은 없습니다.  
  
 [ **@comparison_operator=** ] *comparison_operator*  
 비교 유형을 지정합니다. *comparison_operator* 은 **int**, 기본값은 없습니다. 비교 연산자 및 나타내는 값이 표에 나와 있습니다.  
  
|Value|비교 연산자|  
|-----------|-------------------------|  
|**0**|=(같음)|  
|**1**|<>(같지 않음)|  
|**2**|>(보다 큼)|  
|**3**|<(보다 작음)|  
|**4**|>=(크거나 같음)|  
|**5**|<=(작거나 같음)|  
|**6**|LIKE|  
|**7**|유사하지 않음|  
  
 [  **@value=** ] *값*  
 필터링할 값을 지정합니다. 데이터 형식이 *값* 필터링 할 열의 데이터 형식과 일치 해야 합니다. 예를 들어, 필터 된 개체 ID 열에 설정 된 경우는 **int** 데이터 형식을 *값* 해야 **int**합니다. 경우 *값* 은 **nvarchar** 또는 **varbinary**, 최대 길이는 8000 가질 수 있습니다.  
  
 비교 연산자가 LIKE 또는 NOT LIKE일 경우 논리 연산자는 "%" 또는 LIKE 연산에 적합한 다른 필터를 포함할 수 있습니다.  
  
 NULL을 지정할 수 있습니다 *값* 필터링 하 여 NULL 열 값이 있는 이벤트를 제외 합니다. 만 **0** (= 같음) 및 **1** (<> 같지 않음) 연산자는 NULL을 사용 하 여 유효 합니다. 이 경우 이러한 연산자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 및 IS NOT NULL 연산자와 같습니다.  
  
 열 값의 범위 필터를 적용 하려면 **sp_trace_setfilter** 는 큰 보다-같음으로 한 번 두 번 실행 되어야 합니다 ('> =') 비교 연산자와 다른 시간으로는 작음 보다-같음 ('< =') 연산자 .  
  
 데이터 열 데이터 형식에 대 한 자세한 내용은 참조는 [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md)합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 아래 표에서는 저장 프로시저가 완료된 후 사용자가 얻을 수 있는 코드 값을 설명합니다.  
  
|반환 코드|Description|  
|-----------------|-----------------|  
|0|오류가 없습니다.|  
|1.|알 수 없는 오류입니다.|  
|2|추적이 현재 실행 중입니다. 지금 추적을 변경하변 오류가 발생합니다.|  
|4|지정한 열이 유효하지 않습니다.|  
|5|지정한 열을 필터링할 수 없습니다. 이 값은 에서만 반환 **sp_trace_setfilter**합니다.|  
|6|지정한 비교 연산자가 유효하지 않습니다.|  
|7|지정한 논리 연산자가 유효하지 않습니다.|  
|9|지정한 추적 핸들이 유효하지 않습니다.|  
|13|메모리가 부족합니다. 지정한 동작을 수행할 메모리가 충분하지 않으면 반환됩니다.|  
|16|함수가 이 추적에 유효하지 않습니다.|  
  
## <a name="remarks"></a>주의  
 **sp_trace_setfilter** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 대부분의 이전 버전에서 사용할 수 있는 확장된 저장된 프로시저 실행 하 던 작업을 수행 하는 프로시저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 사용 하 여 **sp_trace_setfilter** 대신는 **xp_trace_set\*필터** 확장 저장된 프로시저를 만들려면, 적용, 제거 또는 추적에 대 한 필터를 조작 합니다. 자세한 내용은 참조 [추적 필터링](../../relational-databases/sql-trace/filter-a-trace.md)합니다.  
  
 한 번 실행에서 특정 열에 대 한 모든 필터를 함께 사용할 수 있어야 **sp_trace_setfilter**합니다. 예를 들어 필터 두 개를 응용 프로그램 이름 열에, 그리고 필터 하나를 사용자 이름 열에 적용하려면 응용 프로그램 이름에 필터를 차례로 지정해야 합니다. 한 번의 저장 프로시저 호출에서 응용 프로그램 이름에 필터 하나를 지정한 다음 사용자 이름에 필터를 지정하고 응용 프로그램 이름에 나머지 필터 하나를 지정하려고 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류를 반환합니다.  
  
 모든 SQL 추적의 매개 변수 저장 프로시저 (**sp_trace_xx**) 엄격 하 게 지정 합니다. 이러한 매개 변수를 인수 설명에 지정된 올바른 입력 매개 변수 데이터 형식으로 호출하지 않으면 저장 프로시저가 오류를 반환합니다.  
  
## <a name="permissions"></a>Permissions  
 사용자는 ALTER TRACE 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 추적 `1`에 필터 3개를 설정합니다. `N'SQLT%'` 및 `N'MS%'` 필터는 한 열(`AppName`, 값 `10`)에서 "`LIKE`" 비교 연산자를 사용하여 실행됩니다. `N'joe'` 필터는 다른 열(`UserName`, 값 `11`)에서 "`EQUAL`" 비교 연산자를 사용하여 실행됩니다.  
  
```  
sp_trace_setfilter  1, 10, 0, 6, N'SQLT%';  
sp_trace_setfilter  1, 10, 0, 6, N'MS%';  
sp_trace_setfilter  1, 11, 0, 0, N'joe';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.fn_trace_getfilterinfo&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sys.fn_trace_getinfo&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [SQL 추적](../../relational-databases/sql-trace/sql-trace.md)  
  
  
